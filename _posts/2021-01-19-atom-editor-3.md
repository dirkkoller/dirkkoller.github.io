---
layout: post
title:  "Atom, der Editor für das 21. Jahrhundert - Teil 3"
categories: Schreiben Atom
permalink: /atom-editor/3
---

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

[Weiter zu Teil 4]({% post_url 2021-01-19-atom-editor-4 %})
