---
layout: post
title:  "Python mit Jupyter Notebook"
date:   2020-05-13
categories: python
permalink: /python-jupyter-notebook
---

Es gibt eine ganze Reihe ausgezeichneter IDEs für Python. Zum Publizieren, Teilen, Visualisieren und Dokumentieren von eigenen Projekten ist allerdings das **[Jupyter Notebook](https://jupyter.org/)** der Standard. Das gilt insbesondere für den wissenschaftlichen Bereich.

Notebook ist eine web-basierte Anwendung. Die Oberfläche wird also im Browser bedient. Im Hintergrund, womöglich in der Cloud, läuft ein Server, der die Webseiten ausliefert und den Python-Code ausführt. Abgelegt werden die Daten in einem offenen Format, das auf JSON basiert.

## Installation von Jupyter Notebook
Die Installation erfolgt am einfachsten mit Anaconda. Hier lässt sich Notebook einfach über den Navigator per Knopfdruck starten.

Wer Anaconda nicht nutzt, kann *pip* bemühen:

    pip3 install --upgrade pip
    pip3 install jupyter

Der Server muss danach noch gestartet werden:

    jupyter notebook

Der Server ist vom Browser aus unter dem Defaultport 8888 zu erreichen:

    http://127.0.0.1:8888


Auf der Hauptseite wird zunächst das serverseitige Dateisystem angezeigt:

![image](images/python-jupyter-notebook/jupyter-tree.jpg)

Falls bereits existierende Notizbücher mit der Endung *ipynb* vorliegen, lassen sie sich durch Anklicken öffnen.

## Notizbuch bearbeiten
Wenn noch keine erstellt wurden, ist der New-Button rechts oben sicher eine gute Wahl. Nach der Auswahl der Programmiersprache wird ein leeres Notizbuch mit einer einzigen Zelle geöffnet. In diese Zelle lässt sich jetzt wahlweise Text im Markdown-Format oder Programmcode schreiben. Der Typ der Zelle wird in der Auswahlbox am rechten Rand des Menüs definiert. Codezellen erkennt man auf den ersten Blick an den eckigen Klammern auf der linken Seite. Die Klammern sind leer, wenn der Code noch nicht ausgeführt wurde. Nach der Ausführung findet sich ein Index in den Klammern, der angibt, in welcher Reihenfolge die Zellen ausgeführt wurden.

Neue Zellen fügt man mit dem Plus-Button zu, gelöscht werden sie mit der Schaltfläche mit dem Scheren-Icon.

Im Beispiel wurde zunächst ein Text und dann eine Zeile Code eingegeben:

![image](images/python-jupyter-notebook/jupyter-cells.jpg)

## Ausführen des Kernels
Das Ausführen des Programms erfolgt erwartungsgemäß mit *Run*. Die grade ausgewählte Zelle, erkennbar am grünen Rahmen, wird dabei in einem sogenanntem *Kernel* ausgeführt. Ein Kernel ist ein programmiersprachenabhängiger Interpreter, der die Anfragen bearbeitet, Code ausführt und die Antworten zurückliefert. Der mitgelieferte Standardkernel für Python ist *iPython*. Weitere Kernel lassen sich bei Bedarf installieren. Jupyter unterstützt durch diese Technik 40 verschiedene Programmiersprachen. Die weiteste Verbreitung hat Jupyter Notebook aber nach wie vor im Umfeld der Sprachen **Ju**lia, **Py**thon und **R**, die auch Namensgeber für das Projekt sind.

![image](images/python-jupyter-notebook/jupyter-run.jpg)