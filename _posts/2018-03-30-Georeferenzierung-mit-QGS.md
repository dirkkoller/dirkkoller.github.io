---
layout: post
title:  "Georeferenzierung mit QGIS"
date:   2018-03-30 09:53:28 +0200
categories: gis
permalink: /georeferenzierung-mit-qgis
---

![Georeferenzierung mit QGIS]({{site.url}}/images/georeferenzierung-mit-qgis/Georeferenzierung mit QGIS.png)


Bei einem Luftbild handelt es sich um eine Zentralprojektion, und diese lässt sich nicht ohne weiteres exakt auf einer echten oder virtuellen Karte wie *Google Earth* oder *Google Maps* platzieren. Selbst wenn die Kamera beim Einfangen des Bildes vermeintlich exakt nach unten ausgerichtet war, entstehen Verzerrungen durch Bildneigung und Höhenunterschiede des Geländes (*radiale Punktverschiebung*). Strecken werden verkürzt bzw. verlängert dargestellt und höher liegende Objekte werden in größerem Maßstab als tiefer liegende abgebildet.

<!--more-->

Diese Verzerrungen lassen sich durch eine Transformation softwaremäßig beseitigen. Das Foto wird korrigiert indem es gedehnt, gestaucht, gedreht und durch weitere Operationen an die Wirklichkeit angenähert (*rektifiziert*) wird. Grundlage dafür ist, dass das Bild georeferenziert ist, also Positionen mit bekannten Koordinaten (*Passpunkte*, *Referenzpunkte* oder *Ground Control Points* genannt) Punkten auf dem Foto zugeordnet werden können.

## Georeferencer-Plugin
In *QGIS* lassen sich beide Operationen (das Zuweisen von Passpunkten und die anschließende Transformation) mit dem *Georeferencer GDAL* durchführen. Da es sich um ein Plugin handelt, muss es gegebenenfalls noch installiert werden. Man findet das Werkzeug anschließend unter *Raster > Georeferencer > Georeferencer...*

Als Beispielfoto für diesen Beitrag dient eine Luftaufnahme einer gepflasterten Weggabelung, die bei einer Ausgrabung freigelegt wurde (hessen Archäologie 2016, S. 246). Das Foto wurde mit Hilfe einer an einem UAV befestigten Systemkamera (Sony Alpha 6000, 19mm Festbrennweite) angefertigt.

![Gepflasterte Wegekreuzung]({{site.url}}/images/georeferenzierung-mit-qgis/Weggabelung.jpg)

Auf dem Foto sind nach Vergrößern rot lackierte Holzpfähle zu erkennen. Die Positionen einige dieser Holzpfähle wurden mit einem RTK GPS (Genauigkeit 1-2 cm) sehr exakt eingemessen und können nun auf dem Foto identifiziert werden.

## Auswahl des CRS in QGIS
Dazu wird das Foto im Georeferencer geladen (*File > Open Raster*). Im sich öffnenden Dialog ist das Koordinatenreferenzsystem für das Bild einzugeben. Da die Koordinaten mit GPS erfasst wurden, ist *WGS 84* hier die richtige Wahl.

![Auswahl des CRS in QGIS]({{site.url}}/images/georeferenzierung-mit-qgis/CRS Selector.png)

 Anschließend wird durch File > Add Point... ein bekannter Punkt (also ein Holzpfahl) auf dem Foto markiert und die zugehörigen Koordinaten im folgenden Dialog eingetragen:

![Zufügen eines Kontrollpunktes]({{site.url}}/images/georeferenzierung-mit-qgis/AddPoint.png)

Um gute Ergebnisse zu erhalten sollten mindestens fünf Referenzpunkte, gleichmäßig verteilt über das zu korrigierende Bild vorliegen und markiert werden. Im Beispiel hier ist die Verteilung der Punkte nicht optimal (aber ausreichend, um das Vorgehen zu demonstrieren)

![Alle GCPs gesetzt]({{site.url}}/images/georeferenzierung-mit-qgis/Punkte gesetzt.png)


Sind die bekannten Punkte erfasst, wird die Georeferenzierung mit *File > Start Georeferencing* in die Wege geleitet. Im sich öffnenden Settings-Dialog müssen das Output-Raster und der Transformations-Typ bestimmt werden. Transformationen höheren Grades benötigen mehr Punkte, können aber durch mehr Freiheitsgrade zu besseren Ergebnissen führen. Mit den hier gesetzten fünf Punkten lässt sich maximal eine Transformation vom Typ *Polynomial 1* durchführen. Außerdem ist es empfehlenswert, die beiden Reports generieren zu lassen.
Nach der Georeferenzierung lässt sich das Ergebnis in QGIS visualisieren. Wie dem folgenden Screenshot zu entnehmen ist, wurde die Luftaufnahme nach der Transformation ganz passabel in die Hintergrundkarte (die ja auch nicht exakt ist) eingefügt. Die Schienen passen nicht ganz genau aneinander, der Fehler liegt in der Größenordnung einer Schienenbreite.
Besser verteilte Passpunkte hätten hier zu einem deutlich besseren Ergebnis geführt.

![QGIS]({{site.url}}/images/georeferenzierung-mit-qgis/ergebnis.png)

Mehr zu QGIS in [Learn QGis](https://amzn.to/3cPoCXC) von Andrew Cutts und Anita Graser.

<img src="https://vg08.met.vgwort.de/na/9210e49cdd83406aa2d3a5dca1555c7a" width="1" height="1" alt=">
