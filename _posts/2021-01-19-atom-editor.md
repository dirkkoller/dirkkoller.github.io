---
layout: post
title:  "Atom, der Editor für das 21. Jahrhundert"
categories: Schreiben Atom
permalink: /atom-editor
---
## Vom Schreiben und Coden

Schreibprogramme lassen sich grob in Editoren und Textverarbeitungen unterteilen. Ein Editor hat dabei nur eingeschränkte Layout- und Formatierungsfunktionen und ein einfaches Textformat, ASCII oder UTF-8.

In der Vergangenheit nutzte man Editoren bevorzugt, um Computerprogramme zu schreiben oder Config-Files zu bearbeiten. Bekannte Editoren wie Emacs wurden dabei mit Funktionen wie Kalender, News- und Mailreader, einer eingebauten Shell, und gar Webbrowser und Spielen zum alternativen Betriebssystem für Entwickler. Größere Texte mit Überschriften, Tabellen und formatiertem Text waren dagegen eher Textverarbeitungen wie MS Word, Pages oder Libre Writer vorbehalten.

Seit dem Aufkommen von Auszeichnungssprachen wie Markdown verschwimmt die Grenze zwischen Editor und Textverarbeitung, zumindest in eine Richtung: Auch mit einem Editor lassen sich Blogbeiträge, Zeitschriftenartikel, Universitätsarbeiten oder ganze Bücher schreiben. Grade wenn das Ergebnis in verschiedenen Formaten wie html, pdf, epub benötigt wird, ist das einfache Textformat dem Output einer Textverarbeitung mit den enthaltenen Formatanweisungen überlegen.

Der Editor wird also nicht etwa zwischen Entwicklungsumgebung auf der einen und Textverarbeitung auf der anderen Seite erdrückt, gute Editoren schicken sich vielmehr an, die Arbeit dieser beiden etablierten Anwendungen zu übernehmen. Und um einen solchen guten Editor soll es hier gehen, um *Atom*, den "hackable text editor for the 21st Century".

## Made by Github
Atom ist ein kostenloser Editor, der von GitHub, der bekannten Hosting-Plattform für Softwareprojekte, entwickelt wird. Das Programm ist in JavaScript mit dem plattformübergreifenden Framework _Electron_ geschrieben und deshalb für zahlreiche Betriebssysteme wie Windows, macOS, Linux und ChromeOS verfügbar. Auf der [Homepage des Projekts](https://atom.io) kann man derzeit Atom in der Version 1.50.0 laden. Die Philosophie des Projekts ist, Erweiterbarkeit wie man sie von Emacs oder Vim kennt, mit Benutzbarkeit zu verknüpfen. Atom soll einfach sein für den Anfänger und mitwachsen mit zunehmender Erfahrung und Ansprüchen. Und das ist ganz hervorragend gelungen!

## Einfach einfach
Das User Interface von Atom ist übersichtlich und aufgeräumt. Kein Ribbon Interface, das versucht die wichtigsten Funktionen zu verstecken und kein Wizard, der helfen soll ein neues Dokument in eine ungewollte Form zu zwängen. Der Editor ist grundsätzlich untergliedert in drei Bereiche: Dem Editor-Bereich (in der Mitte), der Tree-View (links) und dem Git Tab (rechts).

![Aufbau von Atom](/images/atom-editor/atom.png)

Geöffnete Dateien werden in Form von Reitern im mittleren Bereich, den Editor Pane, angezeigt. Das ist der Hauptarbeitsbereich, die Reiter können bei Bedarf horizontal oder vertikal aufgesplittet werden.

Links daneben findet sich die Tree View. Hier werden geöffnete Dateien oder Ordner in Form einer Baumansicht dargestellt. Entwickler werden diese Art der Darstellung aus Ihrer IDE kennen. Die Tree View ist mit einem kleinen Button ein- und ausfahrbar, bei der Arbeit mit einem Text blendet man sie am besten aus, um den vollen Platz zur Verfügung zu haben.

Ebenfalls ausblendbar sind die beiden Git-Reiter, die im rechten Bereich angezeigt werden. Hier lässt sich die Arbeit schnell und unkompliziert in einer Versionsverwaltung sichern. Die Git-Integration in den Editor ist hervorragend gelöst und eines der großen Highlights von Atom.

Mit Strg + Shift + P lässt sich die Command Palette einblenden, die Zugriff auf alle Aktionen bietet, die sich in Atom ausführen lassen. Nach Eingabe von _find_ und Auswahl von _Find And Replace: Show_ aus der Liste der angebotenen Optionen lässt sich beispielsweise die leistungsfähige Suchoption am unteren Fensterrand einblenden.

![Command Palette](/images/atom-editor/command.png)

## Erweiterbar - Packages und Themes
Atom funktioniert Plugin-basiert. Es gibt Pakete, die Features und Funktionen nachrüsten und Themes, mit denen sich das UI und das Syntax-Highlighting komplett umgestalten lässt. Für beides existieren Core-Pakete, die mit der Installation mitgeliefert werden und zahlreiche Community-Projeke. Durch das Installieren der benötigten Pakete wird Atom immer mehr zum persönlichen Editor. Zum Installieren neuer Pakete File > Preferences und dann Install lässt sich nach Paketen suchen. Unter https://atom.io/themes bzw. https://atom.io/packages findet man auch eine Auflistung im Netz. Die zahlreichen Pakete lassen sich ohne Sorgen um einen verunstalteten Editor ausprobieren. Durch Löschen des Ordners _.atom_ im Benutzerverzeichnis wird Atom wieder in den Ursprungszustand zurückversetzt.

## Zen des Schreibens
Atom eignet sich bestens für Autoren und Blogger. Bereits zum Start, also als Core-Paket enthalten, ist die Rechtschreibprüfung _spell-check_. In den Settings können gewünschte Sprache und Wörterbuch angegeben werden. Wie man das aus anderen Editoren kennt, werden erkannte Fehler unterstrichen und lassen sich durch das Kontextmenü korrigieren.
Ebenfalls als Core-Paket  ist eine Markdown-Preview enthalten, die Ansicht kann mit _Packages > Markdown Preview > Toggle Preview_ als Reiter im Editor Pane eingeblendet werden:

![Markdown Preview](/images/atom-editor/markdown-preview.png)

Sehr praktisch für die Arbeit mit Markdown sind auch die Snippets, die es ermöglichen, kompliziertere Markdown-Elemente in den Text einzufügen, ohne die genaue Syntax dafür zu kennen. Um beispielsweise eine Tabelle einzufügen, gibt man einfach _table_, gefolgt von der Tab-Taste ein. Dabei wird das folgende Snippet eingefügt:

```
| Header One     | Header Two     |
| :------------- | :------------- |
| Item One       | Item Two       |
```

Das funktioniert genauso für viele andere Elemente wie zum Beispiel Codeblöcke (code), Bilder (img) oder Links (l).

Im wissenschaftlichen Umfeld wird gerne Latex oder AsciiDoc genutzt. Auch dafür gibt es mit atom-latex bzw. asciidoc-preview entsprechende Community-Pakete, die sich nachrüsten lassen. Die Integration von Literaturverwaltungen wie Zotero oder Citavi ist durch verschiedene Bibtex-Pakete ebenso gegeben.

Für Schreiber ganz hilfreich ist das Community-Paket _wordcount_, mit dem sich die Anzahl der Wörter und Anschläge in die Statusleiste am unteren Bildschirmrand einblenden lässt.

![wordcount](/images/atom-editor/wordcount.png)

Beim Schreiben gibt es oft Stellen die noch recherchiert werden müssen, an denen noch ein Bild eingefügt werden muss oder Ähnliches. Diese lassen sich mit einer Reihe von Schlüsselworten markieren: TODO, FIXME, CHANGED, XXX, IDEA, HACK, NOTE, REVIEW, NB, BUG, QUESTION, COMBAK, TEMP, DEBUG, OPTIMIZE, und WARNING: Mit Hilfe des Paktes _todo-show_ werden diese in einer Listenansicht aufgeführt und sind sogar durch einen Klick auf einen Eintrag direkt anspringbar. Das Feature kommt eigentlich aus der Entwicklung, leistet aber auch bei der Arbeit an einem Text großartige Dienste.

Wer sich von den wenigen UI-Elementen wie Statusbar oder Tab noch gestört fühlt und deshalb unter Schreibblockade leidet, installiert das Paket _zen_. Es präsentiert den Text im ablenkungsfreien puristischen Look. Jetzt gibt es keine Ausreden mehr.

![zen](/images/atom-editor/zen.png)


## Atom für Entwickler
Atom ist keine ausgewachsene IDE. Wer eine solche sucht wird enttäuscht sein. Atom ist ein leichtgewichtiger, schneller Editor, der aber gut mit Code umgehen kann. Aus dem Stand verfügbar sind beispielsweise Syntax-Highlighting und Snippets für JavaScript:

```javascript
function ShowMessage() {
    alert("Hello World!");
}

ShowMessage();
```

Weitere Features für alle möglichen Programmiersprachen lassen sich in Form von Paketen nachrüsten. Dazu gehören zum Beispiel Pakete, die die Arbeit mit den großen JavaScript-Frameworks wie Angular, React oder Vue erleichtern, aber auch Spring Boot-Support für Java-Entwickler oder Tools für Python. Auch hier lässt sich also Atom toll an die eigenen Anforderungen anpassen und erschlägt den Nutzer nicht mit einer Vielzahl an Features, die gar nicht gebraucht werden.

Trotz tausender Pakete ist Atom aber doch nicht der beste Editor für Entwickler. Nicht weil Atom schlecht wäre, Nein, das ganz und gar nicht. Sondern einfach weil das ganz ähnlich aufgebaute Visual Studio Code ziemlich perfekt ist.


## Fazit

Für mich ist Atom derzeit der perfekte Editor, zumindest zum Schreiben. Atom ist schlicht und lenkt nicht ab. Der komplette Platz lässt sich für die Arbeit nutzen und alle wichtigen Kommandos sind, hat man sicher erst mal das Arbeiten mit der Command Palette angewöhnt, über die Tastatur erreichbar.

Dennoch ist Atom mächtig, wenn etwas fehlt, findet es man mit einiger Wahrscheinlichkeit in den Tausenden von Community-Paketen. Und im extremen Notfall kann man es sogar selber schreiben (oder zumindest schreiben lassen).

Die Git-Integration ermöglicht einen tollen Workflow, der nicht nur Entwickler begeistern dürfte. Mit _Teletype_ ist dabei sogar das gleichzeitige Arbeiten an einem Dokument mit anderen möglich.

<img src="https://vg08.met.vgwort.de/na/2f397182ae9e4bfeb9055cb8611f53a0" width="1" height="1" alt=">
