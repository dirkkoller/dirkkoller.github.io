---
layout: post
title:  "MicroPython auf dem ESP8266"
categories: MicroPython ESP8266
permalink: /micropython-esp8266
---

 Bisher war die Arduino-Plattform mit C/C++ als Sprache das Mittel der Wahl, um Sensoren auszulesen oder Servos anzusteuern. Inzwischen wird Arduino aber gleich von zwei Seiten attackiert. Die 32Bit-Mikrokontroller ESP8266 bzw. ESP32 von [Espressif](https://www.espressif.com/) werden immer beliebter und machen der etablierten Arduino-Hardware Konkurrenz.

## MicroPython
 Auf ihnen, aber auch auf anderen Mikrokontrollern wie dem Pyboard oder der STM32-Familie, lässt sich ein Python-Derivat namens [**MicroPython**](http://micropython.org/) betreiben, das die Arduino-Plattform softwareseitig herausfordert. MicroPython ist eine Python 3-Implementierung mit einem abgespeckten Umfang der Standardbibliotheken. Weiterhin  enthalten sind im ehemaligen Kickstarter-Projekt des Australiers Damien George der Compiler, eine Laufzeitumgebung und ein interaktiver Modus zur Befehlseingabe.

## Firmware und Esptool

Um MicroPython auf einem der genannten Prozessoren laufen zu lassen, muss die Firmware geflasht werden. Man erhält die MicroPython-Firmware auf der [Download-Seite](http://micropython.org/download) des Projekts. Für einen ESP8266 beispielsweise ist die aktuelle Datei esp8266-20191220-v1.12.bin. Das Programm [esptool](https://github.com/espressif/esptool) zum Flashen gibt es von *Espressif*. Es ist in Python geschrieben und lässt sich mit dem Python-Paketmanager *pip* oder *pip3* (unter Python 3) installieren:

    pip3 install esptool

## Verkabelung FTDI-Adapter und ESP-01

Hier soll eines der günstigsten ESP8266-Boards, das ESP-01 für einen Test genutzt werden. Es ist für zwei bis drei Euro erhältlich. Anders als seine teureren "großen Brüder" hat das Modul nur vier GPIOs, lediglich 1MB Flash Memory (im Fall des schwarzen Boards, sonst sogar nur 512KB) und keinen Mikro-USB-Anschluss. Für den Flashvorgang wird entweder ein Arduino, oder, wie im Folgenden gezeigt, ein USB zu TTL Konverter mit FTDI-Chip benötigt (Vorsicht, nicht alle davon funktionieren mit dem ESP). Das ESP-01-Board verträgt nur 3,3 Volt, der FTDI-Adapter ist gegebenenfalls auf diesen Wert einzustellen.

Das Pinout des Boards sieht folgendermaßen aus (Blick von oben auf die Bauteile, schlangenförmige WLAN-Antenne rechts):

    Tx(GPIO1)   GND
    CH_PD       GPIO2
    RST         GPIO0
    VCC         Rx(GPIO3)

Adapter und das ESP-01-Moduls werden wie folgt verkabelt:

Adapter  |  ESP01
--|--
VCC  |  VCC, CH_PD
GND  |  GND
Rx  |  Tx
Tx  |  Rx


Vor dem Flashen muss der ESP-01 noch in den Bootloader-Modus versetzt werden. Das geschieht über zwei weitere Verbindungen, die nach dem Flashen aber wieder entfernt werden:


Adapter  |  ESP01
--|--
GND  |  GPIO0
VCC  |  GPIO2


Der FTDI-Adapter sollte als COM-Verbindung unter Windows bzw. als Device im Verzeichnis /dev unter Linux oder MacOS auftauchen. Das Herausfinden des korrekten seriellen Ports ist betriebssystemabhängig und womöglich etwas kniffelig. Je nach Adapter-Modell und Betriebssystem kann auch die Installation eines Treibers erforderlich sein.

## Flashen des ESP8266

Wenn der Adapter als Gerät gefunden wurde, kann mit dem Flashen begonnen werden. Ein typischer Befehl (hier mit einem Port unter MacOS) sieht folgendermaßen aus:

    esptool.py --port /dev/tty.usbserial-AL0659OL  write_flash --flash_mode qio 0x00000 esp8266-20191220-v1.12.bin

Der Flashmode hängt vom verwendeten Board ab, für das verwendete ESP-01-Modul ist das *qio*. Bei Boards mit vier oder mehr Megabyte Flashspeicher muss der Mode *dio* verwendet werden.

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

Die MicroPython-Firmware ist nun auf dem ESP-Modul und harrt der Dinge die da kommen mögen. Mit dem Programmen *Screen* (unter Mac OS), *Putty* (unter Windows) oder picocom (Linux) lässt sich eine Verbindung zum interaktiven Eingabemodus *REPL* herstellen. Die Baudrate ist 115200.

    screen /dev/tty.usbserial-AL0659OL 115200

MicroPython meldet sich mit Versionsnummer und Hinweis auf die Hilfe:

    MicroPython v1.12 on 2019-12-20; ESP module with ESP8266
    Type "help()" for more information.
    >>>

Hier lassen sich nun Python-Kommandos eingeben. Der Upload von Python-Programmen in das Dateisystem (unter /pyboard) kann mit der [rshell](https://github.com/dhylands/rshell) erfolgen. Wenn die Datei dabei den Namen *main.py* bekommt, wird sie automatisch ausgeführt.

## NodeMCU zum Programmieren  

Statt dem USB zu TTL Konverter kann auch ein vorhandenes NodeMCU-Board mit Mikro-USB-Anschluss zum Programmieren genutzt werden. Der EN-Pin wird mit GND verbunden, wodurch der NodeMCU nicht startet. Ansonsten werden Tx, Rx, Gnd und VCC von ESP-01 und NodeMCU einfach durchgeschliffen (Rx und Tx also nicht gekreuzt wie oben) und CH_PD vom ESP-01 wieder mit VCC verbunden:

NodeMCU  |  NodeMCU
--|--
GND  |  EN

NodeMCU  |  ESP01
--|--
VCC  |  VCC,  CH_PD
GND  |  GND
Rx  |  Rx
Tx  |  Tx


Fürs Aufspielen neuer Firmware werden natürlich wieder die zusätzlichen Verbindungen benötigt:

NodeMCU  |  ESP01
--|--
GND  |  GPIO0
VCC  |  GPIO2