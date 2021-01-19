---
layout: post
title:  "Atom, der Editor für das 21. Jahrhundert - Teil 2"
categories: Schreiben Atom
permalink: /atom-editor/2
---

## Einfach einfach
Das User Interface von Atom ist übersichtlich und aufgeräumt. Kein Ribbon Interface, das versucht die wichtigsten Funktionen zu verstecken und kein Wizard, der helfen soll ein neues Dokument in eine ungewollte Form zu zwängen. Der Editor ist grundsätzlich untergliedert in drei Bereiche: Dem Editor-Bereich (in der Mitte), dem Tree-View (links) und dem Git Tab (rechts).

![Aufbau von Atom](/atom-editor/atom.png)

Geöffnete Dateien werden in Form von Reitern im mittleren Bereich, den Editor Pane, angezeigt. Das ist der Hauptarbeitsbereich, die Reiter können bei Bedarf horizontal oder vertikal aufgesplittet werden.

Links daneben findet sich der Tree View. Hier werden geöffnete Dateien oder Ordner in Form einer Baumansicht dargestellt. Entwickler werden diese Art der Darstellung aus Ihrer IDE kennen. Der Tree View mit einem kleinen Button ein- und ausfahrbar, bei der Arbeit mit einem Text blendet man ihm am besten aus um den vollen Platz zur Verfügung zu haben.

Ebenfalls ausblendbar sind die beiden Git-Reiter, die im rechten Bereich angezeigt werden. Hier lässt sich die Arbeit schnell und unkompliziert in einer Versionsverwaltung sichern. Die Git-Integration in den Editor ist hervorragend gelöst und eines der großen Highlights von Atom.

Mit Cmd + Shift * P lässt sich die Command Palette einblenden, die Zugriff auf alle Aktionen bietet, die sich in Atom ausführen lassen. Nach Eingabe von _find_ und Auswahl von _Find And Replace: Show_ aus der Liste der angebotenen Optionen lässt sich beispielsweise die leistungsfähige Suchoption am unteren Fensterrand einblenden.

![Command Palette](atom-editor/command.png)


## Erweiterbar - Packages und Themes
Atom funktioniert Plugin-basiert. Es gibt Pakete, die Features und Funktionen nachrüsten und Themes, mit denen sich das UI und das Syntax-Highlighting komplett umgestalten lässt. Für beides existieren Core-Pakete, die mit der Installation mitgeliefert werden und zahlreiche Community-Projeke. Durch das Installieren der benötigten Pakete wird Atom immer mehr zum persönlichen Editor. Zum Installieren neuer Pakete File > Preferences und dann Install lässt sich nach Paketen suchen. Unter https://atom.io/themes bzw. https://atom.io/packages findet man auch eine Auflistung im Netz. Die zahlreichen Pakete lassen sich ohne Sorgen um einen verunstalteten Editor ausprobieren. Durch Löschen des Ordners .atom im Benutzerverzeichnis wird Atom wieder in den Ursprungszustand zurückversetzt.
