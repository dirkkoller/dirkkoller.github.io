---
layout: post
title:  "OpenStreetMap-Daten in QGIS nutzen"
date:   2018-02-11 09:53:28 +0200
categories: gis
permalink: /openstreetmap-daten-in-qgis-nutzen
---

![OpenstreetMap in QGIS]({{site.url}}/images/openstreetmap_qgis_header.png)

Das Projekt [**OpenStreetMap**][osm] (kurz OSM) ist vermutlich die umfangreichste Geodatensammlung unserer Erde. Ein Heer von Freiwilligen erfasst unentwegt Straßen, Eisenbahnen, Flüsse, Wälder, Häuser und alles andere, was auf Karten zu sehen ist. Diesen Datenschatz darf jeder lizenzkostenfrei einsetzen und beliebig weiterverarbeiten. Der gesamte Datensatz des Planeten ist inzwischen 250 GB groß und damit etwas unhandlich. Um die Daten in einem GIS wie **QGIS** vernünftig nutzen zu können, gilt es zunächst die enorme Datenmenge zu reduzieren.

<!--more-->

# Datenextrakte der Geofabrik
Ein sinnvoller erster Schritt auf diesem Weg ist es lediglich die Daten der Region auf die Platte zu laden, die auch wirklich interessieren. Das Unternehmen [GEOFABRIK][geofabrik] bietet unter [download.geofabrik.de][download-geofabrik] täglich aktualisierte Teilmengen der OSM-Daten, die auf einen Kontinent, ein Land oder ein Bundesland beschränkt sind.
Die Daten können in den Formaten osm.pbf, shp.zip oder osm.bz2 heruntergeladen werden. QGIS und auch das im Folgenden vorgestellte Werkzeug zum Extrahieren von Teildaten kann mit der Binärvariante (osm.pbf) der Daten umgehen. Es empfiehlt sich also, zum Nachvollziehen eine Datei dieses Formats zu laden. Die gepackte XML-Variante osm.bz2 ist etwas größer und für Anwendungen gedacht, die das Binärformat nicht direkt unterstützen. Darüber hinaus steht für ArcGis-Anwender noch eine Shapefile-Variante (shp.zip) zur Verfügung.

# Osmosis installieren
Der Datensatz Germany.osm.pbf ist immer noch stolze 3,1 GB groß und kann in QGIS nicht sinnvoll verarbeitet werden. Im nächsten Schritte werden deshalb die interessierenden Bestandteile (Straßen, Flüsse, Häuser oder was auch immer) extrahiert. Dazu existieren verschiedene Tools, hier wird die Java-Anwendung [Osmosis][osmosis] verwendet.
Die Installation von Osmosis für die verschiedenen Betriebssysteme ist auf der genannten Wiki-Seite beschrieben. Unter Windows beispielsweise entpackt man das zip-File zum Beispiel in C:\Programme (x86) und trägt den Pfad zum Ordner *bin* in die Umgebungsvariable *PATH* ein, so dass das die dort liegende Batch-Datei osmosis.bat gefunden wird. Eine funktionierende Installation erkennt man daran, dass die Eingabe von "osmosis" in der Kommandozeile zu einer Ausführung der Osmosis-Pipeline mit entsprechenden Ausgaben (und nicht etwa zu "Der Befehl osmosis ist entweder falsch geschrieben oder konnte nicht gefunden werden") führt.

# Extrahieren
Wenn Osmosis startbereit ist, geht's ans Extrahieren. Der folgende Befehl liest das pbf-File germany-latest.osm.pbf ein und schreibt alle OSM-Daten raus, die mit highway=motorway getaggt wurden. Das Ergebnis in highway.osm.pbf enthält also die deutschen Autobahnen:   

    osmosis --read-pbf "C:\Users\Dirk\Documents\germany-latest.osm.pbf" --tf accept-ways highway=motorway --used-node --write-pbf highway.osm

# Laden in QGIS
QGIS erlaubt das Zufügen von osm.pbf-Dateien als Vector-Layer. Via Layer > Add Layer > Add Vector Layer... lassen sich die Autobahndaten als Layer laden.

![QGIS]({{site.url}}/images/openstreetmap_qgis.png)


[osm]: https://www.openstreetmap.de
[geofabrik]: http://www.geofabrik.de
[download-geofabrik]: http://download.geofabrik.de
[osmosis]: http://wiki.openstreetmap.org/wiki/Osmosis

<img src="https://vg08.met.vgwort.de/na/9d671b651a3c4672b9113af7fb585c5f" width="1" height="1" alt="">
