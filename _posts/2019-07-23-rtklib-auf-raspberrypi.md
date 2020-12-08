---
layout: post
title:  "RTKLIB auf dem Raspberry Pi"
date:   2019-07-23
categories: rtklib, rtk, raspberrypi
permalink: /rtklib-auf-raspberrypi
---


Im Beitrag [DGPS mit RTKLIB]({% post_url 2016-08-07-DGPS mit RTKLIB %}) wurde gezeigt, wie man mit der offenen Software [RTKLIB](http://www.rtklib.com) und einem ublox M8T-Empfänger mit geeigneter Antenne GPS-Koordinaten exakt, also im Zentimeterbereich bestimmen kann. Da man nun unterwegs nicht immer das Windows-Notebook mitnehmen möchte (oder womöglich gar keins besitzt) ist die Installation der Software auf einem Raspberry Pi eine portable und günstige Alternative. Der Beitrag erläutert die Schritte von der Installation des Betriebssystems auf dem Pi Zero W bis hin zum ersten Fix.

## Benötigte Komponenten
Zum Nachvollziehen ist folgendes Equipment erforderlich:

- Rasperry Pi Zero W (oder ein anderer Pi der WLAN beherrscht )
- SD-Karte für den Pi (am besten mind. 8 GB)
- u-blox LEA M8T-Empfänger auf einem Board mit USB-Anschluss
- eine leistungsfähige GPS-Antenne (z.B. TW3710 von Tallysman)

## Installieren von Raspbian Lite
Das gängige Betriebssystem für den Pi ist *Raspian*. Da keine Desktopumgebung benötigt wird (es gibt keine grafischen RTKLIB-User Interfaces für Linux) genügt hier die [Lite-Variante von Raspian](https://www.raspberrypi.org/downloads/raspbian/). Nach dem Download wird das Image auf die Speicherkarte geschrieben, zum Beispiel mit *Etcher*. Genaue Anweisungen dazu finden sich unter [https://www.raspberrypi.org/documentation/installation/installing-images](https://www.raspberrypi.org/documentation/installation/installing-images).


## SSH-Zugang einrichten
Vor dem ersten Start muss das Image noch konfiguriert werden, damit man sich mit SSH mit dem Pi verbinden kann.
Dazu legt man eine leere Datei mit Namen `ssh` (ohne Endung) im Verzeichnis /boot der Karte an.
Im gleichen Verzeichnis wird außerdem die Datei wpa_supplicant.conf mit folgendem Inhalt angelegt:

    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1

    network={
    ssid="WLAN-Name"
    psk="WLAN-Passwort"
    }

Der Pi ist damit in der Lage sich in das heimische Netzwerk einzuklinken und über SSH erreichbar. Das probiert man am besten aus indem man den Pi startet (SD-Karte einschieben, Stromversorgung an den äußeren Micro-USB-Port anschließen) und anpingt: 

    ping raspberrypi.local

Erscheint hier eine passende Antwort (Reply from ...) sollte man sich auch mit SSH anmelden können:

    ssh pi@raspberrypi.local

Das Standard-Passwort für den SSH-Zugriff ist *raspberry* und kann mit sudo raspi-config geändert werden.

## RTKLIB installieren

Der Quellcode für RTKLIB liegt bei Github (https://github.com/tomojitakasu/RTKLIB). Der Pi muss also erst mal um Git-Kung Fu erweitert werden:

    sudo apt install git

Danach kann dann RTKLIB in der stabilen Version 2.4.2 ausgecheckt werden:

    git clone https://github.com/tomojitakasu/RTKLIB.git

Und das benötige Programm rtkrcv gebaut werden:

    cd RTKLIB/app/rtkrcv/gcc

    make

Die auftretenden Warnungen können ignoriert werden. Zeit für Kaffee, das dauert auf dem Pi ein paar Minuten ...

## Device herausfinden

Der ublox-Empfänger wird mit der (inneren) Micro-USB-Buche des Pi mit Hilfe eines USB OTG-Kabel verbunden.
Nun muss das Device rausgefunden werden, unter dem der Empfänger erreichbar ist (ttyUSB0, ttyUSB1, ttyACM0 usw). 

Am besten probiert man das vermutete Device mit cat /dev/ttyACM0 aus. Im Erfolgsfall sollten Daten des GPS-Empfängers ähnlich den folgenden geliefert werden:

$GNTXT,01,01,02,u-blox AG - www.u-blox.com*4E
$GNTXT,01,01,02,HW UBX-M80xx 00080000 *43cd 
...


## Anpassen der Config

Als Nächstes wird eine config-Datei benötigt, mit der rtkrcv gestartet wird. Ein Beispiel liegt unter /RTKLIB/app/rtkrcv/rtkrcv.conf

Am besten fertigt man sich eine Kopie davon an, die man dann mit dem Editor der Wahl (z.B. pico) anpassen kann:

    cp rtkrcv.conf my.conf

Die Konfiguration von RTKLIB ist recht komplex, hier werden nur die erforderlichen Änderungen aufgeführt:

    inpstr1-type       =serial 	# Inputstream 1 ist der Empfänger am seriellen Port  

    inpstr1-path       =ttyACM0:115200:8:n:1:off	  # hier gegebenenfalls das herausgefundene Device anpassen

    inpstr1-format     =ubx  # Der Empfänger liefert ubx Raw-Daten

    file-cmdfile1      =../../../data/ubx_m8t_glo_raw_5hz.cmd	# hier das passende cmd file einsetzen, in dem der Receiver konfiguriert wird (in RTKLIB enthalten)

    pos1-navsys        =5  # GNSS auswählen, 5=GPS+GLONASS 

    pos1-posmode       =static	# Der Empfänger steht still und wird nicht etwa herumgefahren



Den Eintrag pos1-snrmask im Conf-File ist anscheinend veraltet (siehe auch Conf-Beispiel in der RTKLIB-Doku), er wird ersetzt durch:

    pos1-snrmask_r     =off        # (0:off,1:on)

    pos1-snrmask_b     =off        # (0:off,1:on)

    pos1-snrmask_L1    =35,35,35,35,35,35,35,35,35

Die anderen Streams und Logs am besten auf *off* setzen, um unnötige Fehlermeldungen zu vermeiden.

Dann fehlen noch zwei Rechte zum Ausführen von Dateien:

    chmod +x rtkstart.sh
    chmod +x rtkshut.sh

## Start ohne Korrektur

Nun kann rtkrcv mit der Konfigurationsdatei gestartet werden (am einfachsten aus dem Verzeichnis, in dem sich auch die conf-Datei befindet). Die Antenne sollte vorher mit dem Empfänger verbunden werden und sich außerhalb von Gebäuden befinden.

    rtkrcv -o my.conf

Dann wird der Server gestartet:

    start

Und der Status angezeigt und automatisch aktualisiert (deshalb die 2):

    status 2

In der Statusanzeige sollten valide Satelliten auftauchen und die Position (pos) berechnet werden.

## RTKLIB Fix mit Korrekturdaten 
Nun zur Königsdisziplin der RTK-Vermessung, dem Fix, der zentimetergenauen Position.

Die Antenne sollte dafür von einer Metallscheibe gegen Reflexionen von unten abgeschirmt sein und tolle Rundumsicht haben. In einer Häuserschlucht wird man zumindest mit diesem Einphasen-Empfänger keine fixe Position erhalten.

Wie im [Beitrag DGPS mit RTKLIB]({% post_url 2016-08-07-DGPS mit RTKLIB %}) ausführlicher erläutert werden Korrekturdaten zur Bestimmung der fixen Position benötigt. Diese kann man mit einem zweiten Empfänger selber generieren oder von einem Anbieter (z.B. *SAPOS* in Hessen) via *NTRIP* über das Internet beziehen. Hier wird letzterer Weg beschritten. Zur Einbindung der Korrekturdaten sind die folgenden Änderungen an der Config erforderlich:

    inpstr2-type       =ntripcli	 # Inpustream 2 ist ein NTRIP-Client

    inpstr2-path       =username:password@160.44.207.225:2101/VRS_3_2G_HE	# Die Zugagnsdaten für SAPOS Hessen

    inpstr2-format     =rtcm3 # Das Format, in dem die Daten verschickt werden

    inpstr2-nmeareq    =single # Die eigene Position wird an den Korrekturdienst verschickt

    ant2-postype 		=rtcm	 # Die Antennenposition der Basis kommt mit den Korrekturdaten

    pos2-armode 		=fix-and-hold # Die gewählte Strategie zur Lösung der Phasen-Mehrdeutigkeiten

Ein erneuter Start von *rtkrcv* zeigt in der Statusanzeige zunächst die eingehenden Korrekturdaten an und führt nach ein paar Minuten zum Fix. 

![Positions](/images/rtklib_pi_fix.jpg)










 











 