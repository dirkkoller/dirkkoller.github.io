---
layout: post
title:  "Jetson Nano Headless betreiben"
date:   2020-05-18
categories: jetson-nano
permalink: /jetson-nano-headless
---

Die graphische Oberfläche des Jetson Nano ist hinreichend schnell und ganz gut benutzbar. Trotzdem werden viele Nutzer wahrscheinlich gerne auf eine weitere Maus, Tastatur, Monitor oder entsprechende Umschaltmöglichkeiten auf dem Schreibtisch verzichten. Kein Problem, der Nano lässt sich *headless* betreiben, der Zugang erfolgt also von einem anderen Rechner via *ssh* oder *putty*.

Der kleine Rechner muss dazu über ein 5V-Netzteil mit Strom versorgt werden (dazu ist ein Jumper erforderlich, der die beiden Pins zwischen Kamera- und Netzteil-Anschluss überbrückt) und über Micro-USB mit dem Host-Rechner verbunden sein. Außerdem ist ein Netzwerkanschluss zum Beispiel über Ethernetkabel notwendig. Ein Monitor darf dagegen nicht angeschlossen sein, sonst startet der normale graphische Installer. Die Anleitung geht außerdem von einer frisch geflashten SD-Karte aus. Das Jetson Nano Developer Kit SD Card Image erhält man im Jetson Download Center unter https://developer.nvidia.com/embedded/downloads. Momentan ist die Version JP 4.4 vom 21.4.2020 aktuell.

Nach dem Einschalten des Nano sucht man auf dem Linux- oder MacOS-Host in /dev nach dem USB-Gerät. Hier im Beispiel ist das tty.usbmodemFD133. Mit diesem Device wird sich dann mit Hilfe des Terminal Emulators *screen* verbunden:

    screen /dev/tty.usbmodemFD133 115200

Unter Windows funktioniert das ähnlich, die USB-Verbindung wird als COM-Port angelegt und kann mit [Putty](https://putty.org/) über eine serielle Verbindung angesprochen werden.

![Jetson Nano im Headless-Mode](/images/jetson-nano-headless/jetson-nano-headless.jpg)

Bei erfolgreicher Verbindung fragt der Installationsassistent *oem-config* dann über diesen Weg die erforderlichen Daten (Sprache, Location, Keyboard, Zeitzone, Username und -passwort, Partitionsgröße, Netzwerk, Hostname) ab. Ist das geschehen, kann man sich über ssh oder putty mit dem Nano verbinden:

ssh dirk@jetson-nano

Der Vorgang ist ausführlicher im [NVIDIA Jetson Linux Developer Guide](https://docs.nvidia.com/jetson/l4t/index.html#page/Tegra%2520Linux%2520Driver%2520Package%2520Development%2520Guide%2Fflashing.html%23wwpID0E0KD0HA) beschrieben.
