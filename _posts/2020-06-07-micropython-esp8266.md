---
layout: post
title:  "MicroPython auf dem ESP8266"
categories: MicroPython ESP8266
permalink: /micropython-esp8266
---

 Bisher war die Arduino-Plattform mit C/C++ als Sprache das Mittel der Wahl, um Sensoren auszulesen oder Servos anzusteuern. Inzwischen wird Arduino aber gleich von zwei Seiten attackiert. Die 32Bit-Mikrokontroller  ESP8266 bzw. ESP32 von [Espressif](https://www.espressif.com/) werden immer beliebter und machen der Arduino-Hardware Konkurrenz.

## MicroPython
 Auf ihnen, aber auch auf anderen Mikrokontrollern wie dem Pyboard oder der STM32-Familie, lässt sich ein Python-Derivat namens [**MicroPython**](http://micropython.org/) betreiben, das die Arduino-Plattform softwareseitig herausfordert. MicroPython ist eine Python 3-Implementierung mit einem abgespeckten Umfang der Standardbibliotheken. Weiterhin  enthalten sind im ehemaligen Kickstarter-Projekt des Australiers Damien George der Compiler, eine Laufzeitumgebung und ein interaktiver Modus zur Befehlseingabe.

## Firmware und Esptool

Um MicroPython auf einem der genannten Prozessoren laufen zu lassen, muss die Firmware geflasht werden. Man erhält die MicroPython-Firmware auf der [Download-Seite](http://micropython.org/download) des Projekts. Für einen ESP8266 beispielsweise ist die aktuelle Datei esp8266-20191220-v1.12.bin. Das Programm [esptool](https://github.com/espressif/esptool) zum Flashen gibt es von *Espressif*. Es ist in Python geschrieben und lässt sich mit dem Python-Paketmanager *pip* oder *pip3* (unter Python 3) installieren:

    pip3 install esptool

## Verkabelung FTDI-Adapter und ESP-01

Hier soll einer der günstigsten ESP8266-Chips, der ESP-01 für einen Test genutzt werden. Er ist für etwa drei Euro erhältlich. Anders als seine teureren "großen Brüder" hat das Modul keinen Mikro-USB-Anschluss. Für den Flashvorgang wird also entweder ein Arduino, oder, wie im Folgenden gezeigt, ein USB zu TTL Adapter mit FTDI-Chip benötigt. Der ESP-01 verträgt nur 3,3 Volt, der FTDI-Adapter ist gegebenenfalls auf diesen Wert einzustellen.

Das Pinout des ESP-01 sieht folgendermaßen aus (Blick von oben auf die Bauteile, schlangenförmige WLAN-Antenne rechts):

    Tx    GND
    CH_PD GPIO2
    RST   GPIO0
    VCC   Rx

Adapater und das ESP-01-Modul werden wie folgt verkabelt:

Adapater  |  ESP01
--|--
VCC  |  VCC, CH_PD
GND  |  GND
Rx  |  Tx
Tx  |  Rx


Vor dem Flashen muss der ESP-01 noch in den Bootloader-Modus versetzt werden. Das geschieht über zwei weitere Verbindungen, die nach dem Flashen aber wieder entfernt werden:


Adapater  |  ESP01
--|--
GND  |  GPIO0
VCC  |  GPIO2


Der FTDI-Adapter sollte als COM-Verbindung unter Windows bzw. als Device im Verzeichnis /dev unter Linux oder MacOS auftauchen. Das Herausfinden des korrekten seriellen Ports ist betriebssystemabhängig und womöglich etwas kniffelig. Je nach Adapater-Modell und Betriebssystem kann auch die Installation eines Treibers erforderlich sein.

## Flashen des ESP8266

Wenn der Adapter als Gerät gefunden wurde, kann mit dem Flashen begonnen werden. Ein typischer Befehl (hier mit einem Port unter MacOS) sieht folgendermaßen aus:

    esptool.py --port /dev/tty.usbserial-AL0659OL  write_flash --flash_mode qio 0x00000 esp8266-20191220-v1.12.bin

Der Flashmode hängt vom verwendeten Board ab, für das verwendete ESP-01-Modul ist das *qio*.

Der erfolgreiche Flash-Vorgang liest sich etwa so:

```
esptool.py v2.7
Serial port /dev/tty.usbserial-AL0659OL
Connecting....
Detecting chip type... ESP8266
Chip is ESP8266EX
Features: WiFi
Crystal is 26MHz
MAC: 50:02:91:fe:5b:f2
Uploading stub...
Running stub...
Stub running...
Configuring flash size...
Auto-detected Flash size: 1MB
Flash params set to 0x0020
Compressed 619828 bytes to 404070...
Wrote 619828 bytes (404070 compressed) at 0x00000000 in 35.9 seconds (effective 138.1 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...
```

## REPL

Die MicroPython-Firmware ist nun auf dem ESP-Modul und harrt der Dinge die da kommen mögen. Mit dem Programm *Screen* (unter Mac OS) oder *Putty* (unter Windows) lässt sich eine Verbindung zum interaktiven Eingabemodus REPL herstellen.

    screen /dev/tty.usbserial-AL0659OL 115200

MicroPython meldet sich mit Versionnummer und Hinweis auf die Hilfe:

    MicroPython v1.12 on 2019-12-20; ESP module with ESP8266
    Type "help()" for more information.
    >>>

Hier lassen sich nun Python-Kommandos eingeben.
