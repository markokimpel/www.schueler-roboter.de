---
title: Über das Projekt
permalink: /project/
breadcrumb_path: home
---

## Vision

Schaffung einer offenen und leistungsstarken Plattform auf der Schüler jeden Alters mit Freunde Computerkenntnisse erwerben können.

## Werte

1. Nutzung weit verbreiteter Technologien und offener Standards
1. Genaue und leicht zu folgende Anweisungen um definierte Ziele zu erreichen
1. Leichte Erweiterbarkeit durch den Schüler
1. Teilen der Ergebnisse mit der Community
1. Freude am Lernen

## Ziele

### 1. Definition eines fahrbaren Roboters auf Basis des Raspberry Pis

[Physical Computing](https://de.wikipedia.org/wiki/Physical_Computing) macht einfach mehr Spaß als das trockene Programmieren am Computer. Wir Menschen können leichter eine Verbindnung zu physischen Objekten aufbauen als zu abstrakten Aufgabenstellungen. Zielstellungen wie *Ding beweg dich* oder *mach' dies und das* ergeben sich bei physischen Objekten natürlich, ohne dass es einer zusätzlichen Motivation bedarf. Ein **selbstfahrender Roboter** erscheint hier als ideale Hardwarebasis.

Mit dem [Raspberry Pi 3 Model B](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/) der Raspberry Pi Foundation steht ein leistungsstarker und kostengünstiger Einplatinenrechner zur Verfügung. Seine offene Architektur erlaubt es verschiedene Betriebssysteme und Softwarepakete auf ihm laufen zu lassen und ihn mit eigener Hardware zu integrieren. Seine große Beliebtheit im akademischen und Hobbybereich hat zu einer sehr aktiven Community und einem umfangreichen Angebot an Erweiterungen und Anleitungen geführt. Wir wählen den Raspberry Pi 3 Model B als Steuereinheit für den Roboter, da er ein **sehr breites Spektrum von Anwendungen** ermöglicht - von der Ansteuerung einzelner Komponenten (Motor an/aus), über die Programmierung mit Standardprogrammiersprachen wie Python, JavaScript und Java, die Nutzung von Roboterbetriebssystemen, bis zur Bilderkennung und künstlichen Intelligenz.

Das umfangreiche und teilweise unübersichtliche Angebot an Erweiterungen für den Raspberry Pi und an Roboterkomponenten macht es dem Einsteiger bisweilen schwer geeignete und zueinander passende Komponenten auszuwählen und in ersten eigenen Projekten zu nutzen. Diese Hürde soll durch die **genaue Vorgabe von Komponenten** und **detailierten Aufbauanweisungen** genommen werden. Mit diesen erreicht der Schüler - mit Hilfe eines Kursleiters, Lehrers oder der Eltern - sicher das Ziel einen programmierbaren Roboters zu erschaffen. Die Programmierkurse sind auf diese Hardwarekomponenten abgestimmt. Von dem vorgegebenen Modell ausgehend können eigene Umbauten und Erweiterungen vorgenommen werden. Die Vielzahl der Projekte in der Community laden geradezu dazu ein.

Relativ geringe Anschaffungskosten sollen es möglichst vielen Interessenten ermöglichen den Schüler-Roboter selber zu besitzen. Die ständige Verfügbarkeit *zu Hause* schafft zusätzliche Möglichkeiten zur selbständigen Nutzung.

### 2. Erstellung Unterlagen Programmierkurs

Programmierkurse in verschiedensten Umgebungen und unterschiedlichen Anforderungen an Vorkenntnissen sind mit dem Schüler-Roboter denkbar. Ziel ist es, über die Zeit mehrere Kurse zu entwickeln, die jeweils in unterschiedlichen Settings genutzt werden können - z.B geleiteter Kurs über zwei Tage, oder wöchentlich 90 Minuten, oder selbständiges Erarbeiten.

Es erscheint naheliegend mit einem Kurs, der wenige Vorkenntisse erfordert, zu beginnen. Die Wahl fällt auf die visuelle Programmiersprache **[Scratch](https://de.wikipedia.org/wiki/Scratch_(Programmiersprache))** des MIT Media Labs, mit der der Roboter gesteuert werden soll. Scratch unterstützt die Grundelemente der [imperativen Programmierung](https://de.wikipedia.org/wiki/Imperative_Programmierung) (Sequenz, Verzweigung, Schleifen) ohne den Schüler mit dem Komplexität von Syntax von Computerprogrammen zu belästigen. Konzepte wie Variablen, Unterprogramme, Ereignisorientierung und Parallelausführung können erlernt werden. Die Scratch Programmiersprache kann über eine Schnittstelle erweitert werden. Eine Anbindung an die Hardware des Schüler-Roboters ist zu erstellen.

### 3. Angebot und Durchführung von ersten Kursen zum Bau und der Programmierung des Schüler-Roboters

Hier geht es darum die Projektidee in der Realität zu überprüfen.
* Wie groß ist das Interesse an einem Schüler-Roboter?
* Wie werden Schüler und Eltern am sinnvollsten über das Angebot informiert?
* Ist die Zahlungsbereitschaft für den Kauf der Komponenten ausreichend?
* Wie kommt der Kurs an?
* Können geleitete Kurse kostendeckend angeboten werden?

### 4. Wachstum und Nachhaltigkeit

Hochwertige Kursunterlagen zu erstellen und zu pflegen ist aufwendig. Ohne eine große Zahl von Freiwilligen oder eine Finanzierungsquelle wird das langfristig nicht gelingen. Ziel ist es ein Betriebsmodell und Partner zu finden, die das Angebot des Schüler-Roboters langfristig ermöglichen.

## Hindernisse

* Derzeit nur eine Person involviert - ehrenamtlich.
* Interesse der Schüler und Eltern ungetestet
* Zahlungsbereitschaft der Eltern ungetestet

## Messbare Ergebnisse

### 1. Hardwarebasis definiert

* Nachbaubar durch Schüler mit Hilfe Erwachsener
* Nur haushaltsübliche Werkzeuge werden benötigt, oder liegen bei (ok: Schere, Schraubendreher; nicht ok: Lötkolben, Spannungsmessgerät)
* DONE: Der [GoPiGo3](https://www.dexterindustries.com/gopigo3/) wurde als Hardwarebasis ausgewählt. Vielen Dank an die [Lichtwerkstatt](http://www.acp.uni-jena.de/lichtwerkstatt) des Abbe Center of Photonics für die Unterstützung.
* TODO: [Anleitung](../tutorials/build_a_robot/)
* IN_PROGRESS: [Basisinstallation Software](../tutorials/create_sr_image/)

### 2. Integration mit Scratch implementiert

* Abhängigkeit zu #1
* Veröffentlichung als Open Source
* DONE: [GoPiGo Scratch Extension](https://github.com/markokimpel/gopigoscratchextension) veröffentlicht

### 3. Kurs Scratch Programmierung vorbereitet

* Abhängigkeiten zu #1 und #2
* Beschreibungen können stichpunktartig sein
* DONE: [Programmieren mit Scratch](../tutorials/programming_with_scratch/)

### 4. Ersten Kurs gehalten

* Abhängigkeit zu #3
* TODO

Referenz: Die Gliederung orientiert sich an Salesforces [V2MOM](https://trailhead.salesforce.com/de/modules/manage_the_sfdc_organizational_alignment_v2mom/units/msfw_oav2m_creating_org_alignment_v2mom). (Es wurde eine andere deutsche Übersetzung gewählt.)
