---
layout: post
title:  "DGPS mit RTKLIB"
date:   2016-08-07
categories: rtk rtklib gps
permalink: /dgps-mit-rtklib
---

Mit Differential Global Positioning System-Verfahren (DGPS) wie RTK GPS lassen sich zentimetergenaue GPS-Messungen durchführen. Professionelle Geräte von Anbietern wie Topcon, Novatel, Javad oder Trimble erhält man ab etwa 5.000 €. Wer sich für die Technik interessiert und keinen Wert auf eine komfortable Plug & Play-Lösung mit hoher Ausfallsicherheit legt, kann aber auch günstiger zu Top-Ergebnissen kommen. Der Beitrag zeigt, wie man mit der kostenlosen Open-Source-Software RTKLIB, geeignetem Empfänger und Antenne sowie den Korrekturdaten von [SAPOS](http://www.sapos.de/)  DGPS-Messungen mit hoher Genauigkeit durchführt.

## GPS-Empfänger und Antenne
Als Empfänger wird hier der u-blox LEA M8T auf einem Board mit USB-Anschluss (etwa 150 €) verwendet, bei der Antenne handelt es sich um die TW3710 von Tallysman (ca. 100 €). Beide Komponenten kommen sowohl mit dem amerikanischen *(Navstar) GPS* als auch mit dem russischen *GLONASS* klar. Der u-blox-Empfänger mit der Endung *T* (für *Timing*) liefert richtig konfiguriert Raw-Daten, ohne die RTKLIB nicht funktioniert.

Die Antenne sollte zur Minimierung von reflektierten Signalen auf einer metallischen Grundplatte (z.B. Alu) und optimalerweise mit freier Rundumsicht montiert sein.  Diese Bedingungen kann man mit einer Messung auf einem Hügel mit der Antenne auf dem Autodach zu Testzwecken schnell schaffen.

## u-blox Center
Für einen ersten Test von Sender und Empfänger bietet sich die GNSS‑Evaluierungssoftware u-Center von u-blox an. Nach dem Start muss lediglich der USB-Anschluss (zum Beispiel COM3) mittels Receiver>Port ausgewählt werden und schon zeigt die Software die gefundenen Satelliten an (siehe Abbildung). Die Bezeichnung der Glonass-Satelliten beginnen mit einem "R", die der GPS-Satelliten mit einem "G". Die Deviation-Map links zeigt die ermittelten Positionen mit der typischen Ungenauigkeit von etwa 5 m ohne Optimierung an.

![u-Center](/images/u-blox-center.png)

## RTKLIB
Wer im Internet nach Differential GPS sucht, landet recht bald auf der Seite [rtklib.com](http://www.rtklib.com/)  des Japaners Tomoji Takasu. Die Seite bietet eine ganze Suite von Anwendungen zur Arbeit mit GPS/GNSS. Auf der Support-Seite (http://www.rtklib.com/rtklib_support.htm) findet sich ein Link zum Download des letzten Patches (rtklib_2.4.2_p11.zip). Darin enthalten ist im Ordner *bin* das Programm rtknavi.exe, das hier verwendet wird. Benutzer von Mac oder Linux müssen sich mit der Kommandozeilenversion begnügen oder eine Virtualiserungslösung wie Parallels einsetzen.

Nach dem Start von *rtknavi* wird zunächst mit Hilfe eines mit einem mit *I* beschriftetem Button in der rechten oberen Ecke der Inputstream eingestellt:

- Häkchen bei *Rover*
- Type *Serial*
- Opt: Port Com3 (zum Beispiel)
- Format: *u-blox*
- cmd

Dann werden folgende "Commands at Startup" benötigt:

!UBX CFG-GNSS 0 32 32 1 0 10 32 0 1

!UBX CFG-GNSS 0 32 32 1 6 8 16 0 1

!UBX CFG-MSG 3 15 0 1 0 1 0 0

!UBX CFG-MSG 3 16 0 1 0 1 0 0

!UBX CFG-MSG 1 32 0 1 0 1 0 0

Die beiden CFG-GNSS-Kommandos regeln die Kanalvergabe an GPS und GLONASS. Die darauf folgenden-CFG-MSG Kommandos aktivieren die Ausgabe der Nachrichten TRK-MEAS, TRK-SFRBX und NAV-CLOCK+NAV-TIMEGPS auf USB und UART1.

Hinweis: Die Kommandos wurden einem Script zur Konfiguration eines M8N entnommen, den M8T kann man alternativ und bequemer in u-Blox Center konfigurieren. Dabei wird allerdings die Konfiguration des Receiver dauerhaft verändert (was für Einstieg vielleicht erst mal keine gute Idee ist).

Nach einem Klick auf *Start* sollte nun auch rtknavi die ersten Satelliten anzeigen. Unter Option... Setting1 lassen sich durch ein Häkchen bei *Glo* die GLONASS-Satelliten zuschalten. Das führt zu deutlich mehr Satelliten, die aber derzeit bei Typ-verschiedenen Receivern (u-blox LEA M8T und Receiver von SAPOS) noch nicht zur Integer Ambiguity Resolution verwendet werden können.  Unter Setting2 sollte deshalb bei *Integer Ambiguity Res* der Wert für Glo auf *OFF* stehen.

![Setting2](/images/Setting2.png)

 rtknavi zeigt GPS-Satelliten mit grüner und Glonass mit beiger ID an.

Nach ein paar Minuten warten erhält man eine *Single Solution*, also eine unkorrigierte Position wie sie jedes Handy-GPS auch liefert.

![Single Solution](/images/Single.png)

## SAPOS

Richtig genau wird die Position erst durch Korrektur mit Hilfe der Daten einer eingemessenen Referenzstation. Die Referenzdaten kann man über Funk oder wie hier gezeigt als NTRIP-Daten über das Internet beziehen. Ein flächendeckendes Netz von permanent betriebenen GNSS-Referenzstationen wird in Deutschland von den Landesämtern für Bodenmanagement und Geoinformation unter dem Namen SAPOS zur Verfügung gestellt. Um SAPOS nutzen zu können, muss man sich dort zunächst anmelden. Die Kosten für die Nutzung betragen je nach Dienst 10 oder 20 Cent pro Minute, mindestens jedoch 10 Euro pro Monat. UPDATE: SAPOS ist zumindest in Hessen seit Januar 2019 kostenlos!

Zur Verwendung der Daten wird ein weiterer InputStream (Button *I* rechts oben) konfiguriert:

- Häkchen bei *Base Station*
- Type *Ntrip-Client*
- Opt:
	-NTRIP Caster Host:	62.225.76.202
	-Port: 2101
	-Mountpoint: MAC_3_2G_HE
	-User-ID: erhält man von SAPOS
	-Password erhält man von SAPOS
- Format: *RTCM 3*

Außerdem muss bei *Transmit NMEA GPGGA to Base Station* die Option  *Single Solution* eingestellt werden (SAPOS berechnet virtuelle Referenzstationen und benötigt dafür eine Position).

![Input Streams](/images/InputStreams.png)

Schließlich geht's noch mal in die Optionen. Unter Setting1 wird als Positioning Mode nun *Static* (rtk-korrigierte Daten für einen unbeweglichen Empfänger) ausgewählt. Der M8T ist ein Einfrequenzempfänger, so dass lediglich die Daten des L1-Frequenzbands ausgewertet werden können (inzwischen gibt es auch preisgünstige Dualbandempfänger, mehr dazu im [Beitrag über den ZED-F9P]({% post_url 2019-01-21-preiswerter-gps-dual-band-empfaenger-zed-f9p %})).

![Setting1](/images/Setting1.png)

Unter *Positions* wird für die Base Station-Position *RTCM Antenna Position* ausgewählt, die Koordinaten kommen mit den Korrekturdaten.

![Positions](/images/Positions.png)


Nach dem Start der Messung werden nach einiger Zeit zusätzlich zu den Satelliten des Empfängers auch die Satelliten der SAPOS-Referenzstation angezeigt und der Status der Solution wechselt auf Float:

![Float Solution](/images/Float.png)

Wenn es die Bedingungen (Ionosphärenwetter, Satellitenkonstellation, freie Rundumsicht) hergeben ist die Position dann nach einigen Minuten *Fix* und sehr, sehr genau.

![Float Solution](/images/Fix.png)

Wenn's nicht klappt, lässt sich durch einen Klick auf das kleine Quadrat über dem Start-Button der RTK-Monitor öffnen, der wertvolle Tipps (zum Beispiel im Bereich Error/Warning gibt).

<img src="https://vg08.met.vgwort.de/na/0fa4c785f7b8445fb3978392e3200fb6" width="1" height="1" alt="">
