Die großen Frameworks in der JavaScript-Entwicklung sind derzeit Angular, Vue.js und React. Vue ist zuletzt hinzugekommen (im Jahr 2013), wird aber zunehmend beliebter. Im Vergleich zu den anderen genannten Frameworks gilt es als leichtgewichtig und leicht zu lernen.

Die Installation erfolgt mit npm, dem Node Package Manager. Node wird auf dem Entwicklungsrechner also vorausgesetzt und muss gegebenfalls zuerst installiert werden. Ist das der Fall wird vue mit folgendem Aufruf installiert:

npm install vue


Wie Angular arbeitet Vue mit einem CLI (Command Line Interface), das zum Generieren von Projekt und Starten des Servers verwendet wird. Unter vue heißt das CLI sinnigerweise vue. Die Eingabe von vue --help listet die verfügbaren Kommandos auf.

## Ein Vue-Projekt anlegen

Zum Anlegen des Projekts wird das create-Kommando verwendet:

vue create hello-world

Vue fragt anschließend nach den Presets für XXX. Die Vorgabe kann zunächst einfach mit Return bestätigt werden. Anschließend wird das Projekt erstellt. Dabei werden Pakete geladen und installiert, das dauert also einen Moment.

Wenn der Vorgang beendet ist lohnt ein Blick in den Aufbau des angelegten Projekts im Ordner hello-world:

├── README.md
├── babel.config.js
├── node_modules
├── package-lock.json
├── package.json
├── public
|    └── index.html
└── src
     ├── App.vue
     ├── assets
     ├── main.js
     └── components
            └── HelloWorld.vue

Die grundlegenden Eigenschaften des Projekts wie zum Beispiel Name, Version und Abhängigkeiten zu anderen Projekten werden in package.json (und der dazugehörigen package-lock.json) beschrieben. Die Datei wird vom Node Package Manager (npm) ausgewertet. Das führt dazu dass bei Bedarf zum Beispiel erforderliche Pakete nachgeladen werden.

index.HTML

main.js



Wenn man sich innerhalb des Projektverzeichnisses befindet kann die neue App auch gleich auf dem Entwicklungsserver gestartet werden:

npm run serve

Die Anwendung findet sich unter http://localhost:8080/.


## Komponenten
Eine Vue -Anwendung ist aus Komponenten aufgebaut. Eine Komponente ist Teil einer Webseite, also zum Beispiel der Footer, das Menü, ein Eingabeformular und so weiter. Eine Webseite besteht aus vielen solcher Komponenten die verschachtelt werden. Im zuvor angelegten Projekt findet such die Komponente App.vue und HelloWorld.vue. App.vue ist die in jedem Projekt vorhandene Root-Komponente. Das ist der Einstiegspunkt in die Anwendung. Wie jede Komponente besteht der Inhalt der Datei aus drei Teilen:

Im Template-Tag ist der HTML-Code für diese Komponente enthalten, also der strukturelle Aufbau der Komponente. Man beachte das <HelloWorld>-Tag, das eine weitere Komponente einbindet.
Im script-Bereich findet sich der JavaScript-Code.
Der Style-Abschnitt (im Code unten etwas gekürzt) enthält das CSS, das auf den HTML-Code dieser Komponente angewendet wird.

<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>

import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  [..]
}
</style>


Die Komponente HelloWorld, die ebenfalls automatisch generiert wurde ist analog aufgebaut.

## Data Binding

Erwähnenswert ist folgender Ausdruck  im Template der HelloWorld-Komponente:

<h1>{{ msg }}</h1>

 Mit einer Technik namens Text Interpolation  wird hier die Variable  msg aus dem JavaScript-Bereich eingebunden, deren Wert wird also angezeigt:

 <script>
 export default {
   name: 'HelloWorld',
   props: {
     msg: String
   }
 }
 </script>


## Event Handling

Die Hauptaufgabe des Codes ist es auf Aktionen die mit den Elemetenm im Templazte ausgeführt werden zu reagieren. Ein Klick auf einen Button wird zum Beispiel folgendermaßen abgehandelt:

<template>
  <button v-on:click="doSomething">Event!</button>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    doSomething: function () {
      console.log("doSomething called")
    }
  }
}
</script>

Mit Hilfe der Direktive v-on:click bekommt Vue mitgeteilt, welche Funktionen aufgerufen werden soll, wenn der Button betätigt wird. Die Methode selber wird als Objekt unter methods auspropgrammiert.
