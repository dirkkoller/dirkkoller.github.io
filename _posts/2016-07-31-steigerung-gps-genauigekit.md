---
layout: post
title:  "Steigerung der GPS-Genauigkeit"
date:   2016-07-31
categories: rtk rtklib gps
permalink: /steigerung-gps-genauigkeit
---


Mit einem einfachen GPS/GNSS-Empfänger wie er beispielsweise in aktuellen Handys oder Autonavis verbaut wird, lässt sich die Position auf ca. 5-10 m Genauigkeit bestimmen. Die Unschärfe entsteht durch Naturphänomene in Iono- und Tropospähre (Sonnenaktivität, Wolken) und die Gegebenheiten am Boden (Bäume, Häuser, nasser Boden), die das Signal auf dem Weg vom Satelliten zum Empfänger verlangsamen, reflektieren oder abschirmen. Dazu kommen ungünstige Satellitenanordnungen zu einer gegebenen Zeit, Rundungsfehler und Ungenauigkeit der Uhren im Empfänger.

Für viele Anwendungsfälle genügt allerdings diese Genauigkeit. Ein Autonavi geht zum Beispiel immer davon aus, dass sich die Position auf der Straße befunden muss, wodurch die Position eingeschränkt wird.
In anderen Bereichen wird eine höhere Genauigkeit benötigt. Beispiele sind autonome Maschinen in der Landwirtschaft (Precision Farming) oder das Einmessen von Funden in der Archäologie.

Zur Verbesserung der Genauigkeit stehen verschiedene Verfahren zur Verfügung. Allen gemein ist die Verwendung einer leistungsstarken Antenne und einer metallischen Grundplatte, die vom Boden reflektierte Signale abschirmt. Mit Werkzeugen wie zum Beispiel dem [Trimble GNSS Planning Online](https://www.trimble.com/gnssplanningonline/) kann man sich schon vor der Messung einen Überblick über die verfügbaren Satelliten zu einer bestimmten Uhrzeit verschaffen:

![Trimble GNSS Planning Online](/images/trimble-planning.jpg)

## Langzeitmessung
Die günstigste Variante besteht in der Langzeitmessung der Position (> 12 h). Wetterphänomene mitteln sich so raus und es wird eine genaue Position erhalten. Das ist natürlich oft nicht praktikabel. Ein Anwendungszweck ist zum Beispiel die Einmessung einer Referenzstation (siehe unten).

## Mehrfrequenzempfäner
Neuere Satelliten strahlen ihr Signal in mehreren Frequenzen aus (L1, L2, L5). Empfänger die mehrere Frequenzen empfangen können sind deutlich genauer, kosten aber auch noch deutlich mehr und sollen hier nicht weiter betrachtet werden.

## PPP
Einige GPS-Chips (zum Beispiel die P-Serie von u-blox) beherrschen ein Verfahren namens Precise Point Positioning. Dabei werden die Koordinaten durch Korrektursignale weiterer Satelliten verbessert. Ein solches Satellitensystem nennt sich SBAS (Satellite Based Augmentation System), die europäische Ausprägung ist EGNOS. Die Korrekturdaten enthalten zum Beispiel Informationen über die aktuellen Gegebenheiten in der Ionosphäre. Als Faustregel lässt sich sagen, dass hier eine Genauigkeit von etwa 1 m erreicht werden kann. Das Einbeziehen der Korrekturdaten dauert allerdings ein paar Minuten.

## RTK GPS
Noch genauere Positionen erhält man durch Korrektur der Daten mit denen einer Referenzstation. Die Station ist eingemessen, die korrekte Position ist also bekannt. Ein Empfänger in der Referenzstation ermittelt die Position unter den aktuellen Bedingungen (z.B. Ionosphärenwetter) und erhält dadurch eine Differenz zur wahren Position. Diese Differenz kann benutzt werden, um die Position eines Empfängers (Rover) in bis zu etwa 10 km Entfernung zu korrigieren. Bei einer Abwandlung des Verfahrens wird die (herkömmlich genaue) Position des Rover zum Beispiel über Internet (Ntrip) an einen Dienst gesendet, der aus den Daten mehrerer Referenzstationen eine virtuelle Referenzstation für den gegebenen Ort berechnet. Die Verhältnisse an dieser Referenzstation werden dann benutzt, um die Koordinaten zu korrigieren. Mit RTK-Verfahren werden Genauigkeiten von 1-2 cm erreicht.

## Postprocessing
Das zuvor beschriebene Verfahren kann auch nachträglich angewendet werden, das heißt, die erfassten Daten werden erst später mit den herunter geladenen Daten einer echten oder virtuellen Referenzstation korrigiert. Man spricht dann von *Postprocessing* oder genauer *Post-Processed Kinematic (PPK)*.

<img src="https://vg08.met.vgwort.de/na/cc745219c28d427d8049ee497c3391b2" width="1" height="1" alt=">
