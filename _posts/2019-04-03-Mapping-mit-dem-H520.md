---
layout: post
title:  "Mapping mit dem H520"
date:   2019-02-04 09:53:28 +0200
categories: mapping
permalink: /mapping-mit-dem-h520
---


![Data Pilot]({{site.url}}/images/data-pilot.jpg)

Drohnen sind zu einem wichtigen Werkzeug in der Vermessung geworden. Noch kommen die Ergebnisse in Form georeferenzierter Karten oder 3D-Modelle nicht ganz an die Genauigkeit heran, die mit herkömmlichen Instrumenten wie Tachymeter oder Theodolit erreicht wird. Für viele Anwendungszwecke genügt aber die erreichbare Auflösung. Die Geschwindigkeit, mit der auch größere Flächen erfasst werden können ist auf jeden Fall ein gewichtiges Argument für die Drohnenvermessung.

<!--more-->

Der typische Workflow der Bilderfassung soll hier am Beispiel des YUNEEC H520 vorgestellt werden. Der Hexakopter des chinesischen Unternehmens wurde unter anderem für Bau-, Vermessungs- und Kartierungsanwendungen konzipiert. Er lässt sich mit verschiedenen Kameras ausstatten, unter anderem auch mit einer hochauflösenden Wärmebild- und Restlichtkamera. Für 3D Mapping/Modelling kommt hier die Weitwinkelkamera E90, ebenfalls von YUNEEC zum Einsatz.

### Ground Control Points
Um georeferenzierte Karten zu erhalten, werden Geokoordinaten benötigt. Die E90 speichert diese in den Exif-Informationen des Bildes ab. Allerdings handelt es sich dabei um herkömmliche GPS-Koordinaten mit der üblichen Ungenauigkeit von ca. 5 Metern. Für Vermessungsaufgaben ist das nicht brauchbar, sodass vor der Befliegung Passpunkte, (engl. Ground Control Points, GCP) ausgelegt werden müssen. Dabei handelt es sich um eingemessene Markierungen, die aus der Luft mit fotografiert werden und später in der Software mit den zugehörigen Koordinaten versehen werden.

<figure style="float: right;" hspace="20">
	<img  vspace="5" width="200" caption ="GCP" src="/images/ground-control-point.jpg" alt="Ground Control Point">
	<figcaption>      Ground Control Point</figcaption>
</figure>


 Das Einmessen der Kontrollpunkte muss möglichst exakt, also zum Beispiel mit RTK GPS (Genauigkeit etwa 1 cm) erfolgen. Für eine gute Georeferenzierung werden zwischen fünf und acht gleichmäßig verteilte GCPs benötigt. Weitere eingemessene Punkte verbessern das Ergebnis nicht, können aber zur abschließenden Qualitätskontrolle als Checkpoints verwendet werden. Steht ein spezieller Ort wie zum Beispiel ein Gebäude im Fokus der Vermessung, ist ein Kontrollpunkt in der Nähe dieses Orts von Vorteil.

Die Kontrollpunkte sollten aus der Luft gut erkennbar und am Boden fixiert sein. Je nach Flughöhe ist ein flaches Objekt etwa in der Größe eines Bierdeckels gut geeignet. Nicht optimal sind die oft vorhandenen rot lackierten Absteckpfähle auf Baustellen. Die vertikale Ausdehnung (die 3-Dimensionalität) des Pflocks erschwert erfahrungsgemäß das Erkennen und genaue Markieren in der Software.


### Einstellungen für den automatischen Flug
Der Flugcontroller des H520 ermöglich autonome Fotoflüge mit automatischem Start und Landung. Die Arbeit des Piloten liegt eher bei der Vorbereitung des Flugs. Die Planung wird mit der Software *[DataPilot][datapilot]*, entweder auf dem Display der Fernbedienung oder komfortabler auf dem Desktop mit der Mac- oder Windows-Version von DataPilot durchgeführt. Das Markieren des Fluggebietes erfolgt im Survey-Modus, bei dem ein Raster mit dem zu befliegenden Areal auf eine Karte gezogen wird (siehe Abbildung oben).

Im rechts eingeblendeten Fenster sind die Flugparameter einzugeben. Neben der Überlappung - mindestens 75% frontal und 60% seitlich für gute Ergebnisse – ist die Flughöhe ein wichtiger Parameter. Sie hat direkte Auswirkungen auf die Genauigkeit des Ergebnisses. Umso tiefer geflogen wird, umso detaillierter sind die Fotos und später das resultierende Artefakt. Umso länger dauert allerdings auch der Flug, was zu Problemen mit dem Akku führen könnte. Beim H520 hält der Akku fast 30 Minuten und kann sogar während einer Befliegung gewechselt werden. Die erwartete Genauigkeit bei der eingestellten Höhe wird in Form der Ground resolution (auch *Ground Sampling Distance*, GSD) berechnet. Ein Wert von 1 cm/px bedeutet, dass ein realer Zentimeter als 1 Pixel im Modell abgebildet wird. Wer Wert auf hohe Genauigkeit legt, sollte noch die Kreuzbefliegung aktivieren (Refly at 90 degree offset), bei der das Areal zusätzlich im 90°-Winkel beflogen wird. Auch dieser Punkt wirkt sich auf die Flugzeit aus, die ebenfalls im Vorhinein berechnet wird. Darüber hinaus sollte die Anzahl der resultierenden Fotos bedacht werden. 500 Bilder einer Befliegung mögen ein tolles Modell liefern, könnten aber bei der Auswertung den Rechner überfordern.

Entsprechen alle Einstellungen den Wünschen müssen die Flugdaten noch auf die Fernbedienung bzw. das Fluggerät übertragen werden. Dort harrt die Mission dann bis zum Tag der Befliegung, die möglichst an einem etwas bewölkten Tag durchgeführt wird um harte Schatten auf den Fotos zu vermeiden.

 Im nächsten Beitrag wird dann die Verarbeitung des Bildmaterials mit der Photogrammetriesoftware [Pix4D][pix4d] vorgestellt.

[pix4d]: https://www.pix4d.com
[datapilot]: http://de.commercial.yuneec.com/comm-de-datapilot

<img src="https://vg08.met.vgwort.de/na/5c6489c3a0784a958ef37ff539da5df9" width="1" height="1" alt="">
