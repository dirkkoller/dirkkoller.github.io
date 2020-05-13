---
layout: post
title:  "Python mit Anaconda"
date:   2020-05-13
categories: python
permalink: /anaconda
---

Python ist die Sprache der Wahl für Projekte im Umfeld von Machine Learning und Data Science. Verschiedene Versionen der Sprache selbst, aber vor allen Dingen tausende in diesem Kontext benötigten Pakete und Bibliotheken sind schwer zu kontrollieren. Zum Glück steht mit **Anaconda** ein Werkzeug zur Verfügung, das hilft den Überblick zu behalten und das Projekt zu verwalten.

Anaconda bezeichnet sich selbst als Data Science-Plattform, ist also eine Python-Distribution mit Fokus auf vorhersagende Analyse und wissenschaftliche Berechnungen.

Enthalten sind unter anderem:

- der Conda Package Manager mit dem zugehörigen Repository
- die Programmiersprachen Python und R
- ein Cloud Repository zum Teilen von eigenen Projekten
- ein Manager für virtuelle Umgebungen
- Jupyter Notebooks und andere Entwicklungsumgebungen
- der Anaconda Navigator

Die *Individual Edition* der aktuellen Version Anaconda 3 ist kostenlos erhältlich und richtet sich an Solo-Entwickler. Für Teams oder Unternehmen stehen umfangreichere, aber kostenpflichtige Editionen bereit.

## Installation
Anaconda ist für Windows, Mac OS und Linux jeweils für Python 2.7 und Python 3.7 verfügbar. Die ARM-Architektur wird leider noch nicht unterstützt, es gibt also keine offizielle Version für den Raspberry Pi. Mit Miniconda (Link) steht aber eine abgespeckte Variante zur Verfügung. Der graphische Installer ist 460 MB groß, die Installation beinhaltet keine großen Hürden.

## Anwendungen
Nach der Installation lässt sich der Anaconda Navigator starten, der den Überblick über alle Anwendungen, Pakete und Umgebungen bietet. Auf der linken Seite findet sich ein Menü, dessen erster Punkt "home" lautet. Hier hier lassen sich weitere Anwendungen wie das bekannte Jupyter Notebook oder die IDE Spyder leiht installieren oder bereits installierte Anwendungen starten.

![Anaconda Navigator](/images/anaconda/anaconda-navigator.jpg)

## Conda
Der Paketmanager *conda* ist von der Kommandozeile aus erreichbar. Um beispielsweise TensorFlow in der CPU-Variante zu installieren sind die folgenden Eingaben erforderlich:

    conda create -n tf tensorflow
    conda activate tf

## Virtuelle Umgebungen
In Python-Projekten arbeitet man gerne in isolierten virtuellen Umgebungen, um die Abhängigkeiten in Form von Paketen und Module verschiedener Projekte auseinanderzuhalten. Im Prinzip ist das eine Verzeichnisstruktur wo genau die passende Python-Version und erforderliche Pakete für das jeweilige Projekt enthalten sind. Die zuvor aktivierte Umgebung ist nun im Navigator unter Environments zu finden. Nach der Auswahl des Umgebungsnamens werden auf der rechten Seite die enthaltenen Pakete mit ihren jeweiligen Versionen aufgelistet.

Abb
