---
layout: post
title:  "Preiswerter GPS-Dualband-Empfänger ZED-F9P"
date:   2019-01-21
categories: rtk
permalink: /preiswerter-gps-dual-band-empfaenger-zed-f9p
---

Das Schweizer Unternehmen [ublox](http://www.u-blox.com), ein renommierter Hersteller von GPS-Empfängern hat Anfang 2018 mit dem **ZED-F9P** einen sehr günstigen Dualband-Receiver angekündigt. Primäre Zielgruppe für den ZED-F9P ist vermutlich der Milliardenmarkt *Autonomes Fahren*, aber auch für Vermessungsaufgaben dürfte das Bauteil sehr gut geeignet sein. Inzwischen ist der Empfänger in verschiedenen Variationen erhältlich und soll hier kurz vorgestellt werden.

## ZED-F9P on Board
Dem Beitrag liegt das Board aus dem [CGS-Shop](https://www.csgshop.com/product.php?id_product=263) für 260 Dollar zugrunde. Eine interessante Alternative ist das [simpleRTK2B-Projekt](https://www.ardusimple.com), das den ZED-F9P in verschiedenen Starter-Kits anbietet. In beiden Fällen ist das noch kein benutzerfreundliches Endgerät in robustem Gehäuse mit Bedienungsanleitung usw. Vielmehr handelt es sich eher um ein Bauteil, das in Endgeräten verbaut werden kann, mit dem sich aber die ganze Receiver-Funktionalität nutzen lässt. Womöglich werden wir in nächster Zeit GPS-Geräte mit dem dem ZED-F9P "inside" zu sehen bekommen.

![GPS-Stab mit ZED-F9P und TW 3870](/images/teaser-ZED-F9P.JPG)


## Hardware: ZED-F9P + TW 3870
Das CGS-Board verfügt über eine ganze Reihe von Anschlussmöglichkeiten (USB, I2C, UART und SPI). Für einen ersten Test bietet sich der USB-Port an, mit dem das Board einfach an ein Notebook angeschlossen werden kann. Der ZED-F9P wird auf diese Weise mit Strom versorgt und kann mit einer auf dem Rechner laufenden GPS-Software wie zum Beispiel [u-center](https://www.u-blox.com/de/product/u-center) oder [rtklib](http://www.rtklib.com) kommunizieren.
Das Board verfügt außerdem über eine SMA-Buchse, über die sich eine Antenne anschließen lässt. Hier wird die Dualband-fähige TW 3870 von Tallysman verwendet, die GPS L1/L2, GLONASS G1/G2, BeiDou B1 und Galileo E1 empfängt. Man erhält die Antenne bei [Digikey](https://www.digikey.de) für etwas über 250 Euro. Um Störungen durch reflektierte Signale vom Boden zu unterdrücken wurde noch eine metallische Grundplatte unter die Antenne montiert. Außerdem wird ein Adapter oder ein Pigtailkabel benötigt (die TW 3870 hat einen TNC-Anschluss). Insgesamt kosten die Bauteile also knapp 500 Euro, dafür bekommt man allerdings auch ein GPS-System mit Empfangseigenschaften eines Geräts der Profiklasse.

![GPS-Stab mit ZED-F9P und TW 3870](/images/GPS-Stab-mit-ZED-F9P.JPG)


## u-center
Der Test erfolgt mit der Windows-Software u-center von ublox. Nach der Auswahl des entsprechenden COM-Ports (z.B. Receiver > Connection > COM4) tauchen sofort die ersten Satelliten auf. Mit GPS, GLONASS und Galileo stehen in Deutschland inzwischen drei leistungsfähige GNSS zur Verfügung. Bei der Anzeige der Empfangsstärke (View *satellite level*) zeigt sich ein erster Unterschied zu einem Singleband-Empfänger: Im Empfangsbalken werden am unteren Rand gegebenenfalls beide Empfangsstärken aufgeführt (siehe Abbildung). E steht hier übrigens für Galileo, R für GLONASS und G für GPS.

![Dualband-Anzeige der Empfangsstärke](/images/satellite-view.JPG)

## Korrektur mit SAPOS
Zur Bestimmung von zentimetergenauen Positionen mittels RTK GPS wird eine RTK-Engine und ein Korrekturdienst benötigt. Die RTK-Berechnung erfolgt beim ZED-F9P direkt auf dem Chip, die Receiver der P-Reihe enthalten ein internes RTK-Modul. Die RTCM-Korrekturdaten kann man in Deutschland zum Beispiel von SAPOS bekommen, das ist ein Angebot der Landesämter für Bodenmanagement und Geoinformation. Seit Anfang 2019 stellt SAPOS erfreulicherweise auch Korrektursignale für Galileo bereit. Außerdem ist der Dienst nun zumindest in Hessen kostenfrei. Im u-center werden die SAPOS-Daten unter Receiver > NTRIP-Client eingegeben. Bei vorliegender Internetverbindung (bei NTRIP werden RTCM-Daten über das Internet versendet) erhält u-center Korrekturen für die empfangenen Satelliten und zeigt dies durch eine Meldung in der Statusleiste am unteren Bildschirmrand an (NTRIP-Client:IP-Adresse). Im View *data* wechselt der Fix Mode nach Eingang der Korrektursignale zunächst auf *3D/GNSS/FLOAT* und bei sehr genauer Bestimmung der Position schließlich auf *3D/GNSS/FIXED*. Im Test war das ohne Probleme drei Meter von einer Hauswand entfernt möglich.


![Fix mit dem ZED-F9P](/images/data-view.JPG)


Low-Cost RTK GPS war zumindest in Deutschland schon länger möglich. Mit Galileo, kostenlosen Korrekturdaten und dem preisgünstigen Dualband-Receiver ZED-F9P macht es nun auch wirklich Spaß. Wer sich genauer für technische Daten und Messwerte zum ZED-F9P interessiert, findet im Blog [rtklibexplorer](https://rtklibexplorer.wordpress.com) detaillierte Informationen.

<img src="https://vg08.met.vgwort.de/na/a1252b559d264faf91a3d572a6e4b073" width="1" height="1" alt=">
