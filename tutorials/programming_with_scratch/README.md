[Home](../..)

# Programmierung mit Scratch

## Voraussetzungen

* Roboter mit aktuellen Software (siehe [Bau des Roboters](../build_a_robot))
* Einen weiteren Computer um auf den Roboter zuzugreifen. An diesem Computer sitzt du und programmierst den Roboter. Der Computer kann ein Raspberry Pi mit Monitor, Tastatur und Maus sein, oder ein Windows Laptop. Da der Roboter über WLAN kommuniziert, muss auch der weitere Computer über WLAN kommunizieren können.

## Mit dem Roboter verbinden

* Anschalten
  * Starte den Roboter indem du die Power Taste (rechts hinten am GoPiGo3 Board) drückst. Die grüne LED daneben beginnt zu blinken. Das bedeutet, das Betriebssystem wird geladen. Wenn die LED ständig grün leuchtet ist der Roboter betriebsbereit.
  * Übrigens: Wenn die LED neben der Power Taste beginnt gelb oder gar violett zu leuchten, dann bedeutet das die Akkus sind fast leer. Dann den Roboter ausschalten und Akkus wechseln.
* Mit WLAN verbinden
  * Der Roboter bietet ein WLAN Netzwerk an. Der Netzwerkname (SSID) ist *student-robot*, bei Arbeitsgruppen *student-robot[zahl]*. Das voreingestellte Passwort ist *changeitnow*. Bei Arbeitsgruppen erfrage das Passwort von deinem Gruppenleiter.
  * Verbinde dich mit deinem Arbeitsrechner zum WLAN des Roboters. Wennn du dich mit dem Roboter WLAN verbindest, verlierst du eine evtl. vorher bestehende WLAN Verbindung zum lokalen WLAN Router und damit zum Internet.
* Mit VNC Viewer verbinden
  * Mit dem VNC Viewer verbindest du dich zum Roboter und kannst den Desktop des Roboters sehen.
  * Bei Raspbian ist der VNC Viewer bereits installiert (Menüpunkt *Internet*). Für Windows kann er von https://www.realvnc.com/de/connect/download/viewer/ (Standalone EXE ist ausreichend) heruntergeladen werden.
  * Server-Adresse ist *student-robot*, bei Arbeitsgruppen *student-robot[zahl]*, Benutzname ist *pi*, Passwort ist *myrobot*. Beim ersten Aufruf mit der Fingerprint des Servers bestätigt werden.
  * Nun kannst du mit dem Raspbian Betriebssystem auf dem Roboter so arbeiten, als säßest du direkt davor.

## Roboter ausschalten

* Das geht einfach: Offene Dokumente speichern, dann die Power Taste (rechts hinten am GoPiGo3 Board) drücken. Die LED daneben beginnt rot zu blinken. Offene Programme werden beendet und das Betriebssystem wird heruntergefahren. Die LED geht aus, wenn der Roboter vollständig heruntergefahren wurde. Du kannst nun die Akkus entfernen.

## GoPiGo3 Server starten

* Scratch benötigt eine Erweiterung um den Roboter steuern zu können. Teil der Erweiterung ist der GoPiGo3 Server. Dieser muss zuerst gestartet werden.
* Terminal öffnen und ausführen
```
pi@student-robot:~ $ cd gopigoscratchextension/
pi@student-robot:~/gopigoscratchextension $ cd gpg3server/
pi@student-robot:~/gopigoscratchextension/gpg3server $ ./run.sh 
Server listening at 0.0.0.0:8080

GPG3 Server homepage : http://127.0.0.1:8080/
Scratch extension URL: http://127.0.0.1:8080/scratch_extension.js

Press Ctrl-C to stop server
```
* Bitte die angezeigten URLs für *GPG3 Server homepage* und *Scratch extension URL* beachten. Diese werden später gebraucht.
* Bitte das Terminal offen lassen, während man mit Scratch arbeitet. Das Schliessen des Terminals würde den Server stoppen.

## Roboterfunktionen kennen lernen

* Im Browser die GPG3 Server homepage (im Beispiel *http://127.0.0.1:8080/*) öffnen. Dann zu *Controller UI* gehen.

## Scratch starten

* Menüpunkt *Entwicklung*, *Scratch 2* starten
* Die Sprache kann bei Bedarf geändert werden. Hierzu den Erdball links oben anklicken und die gewünschte Sprache wählen. Viele Texte, aber nicht alle, erscheinen dann in der gewählten Sprache.
* Das Laden von Erweiterungen funktioniert in Scratch 2 so:
  * Umschalttaste (Shift-Taste) gedrückt halten und Menü *Datei* anklicken.
  * Durch das Drücken der Umschalttaste werden weitere Menüpunkte angezeigt. Wir wählen *Import experimental extension*.
  * Die *Scratch extension URL* (im Beispiel *http://127.0.0.1:8080/scratch_extension.js*) eingeben.
  * Im Bereich *Skripte* werden in der Gruppe *Weitere Blöcke* Funktionen angeboten, die du zum Steuern des Roboters benutzen kannst.
  
# Projekte laden und speichern in Scratch

* Das Laden und Speichern von Projekten mit Erweiterungen ist etwas hakelig in Scratch 2. Wird in einem Projekt eine Erweiterung verwendet, so verwendet Scratch beim Speichern des Projekts immer den Dateiendung *.sbx* (auch wenn man eine andere angibt). Beim Laden besteht Scratch jedoch auf die Dateiendung *.sb2*.
* Ein Workaround ist, die Projekte mit *.sbx* Dateinamen zu speichern und einen Link vom *.sb2* Dateinamen auf den *.sbx* Dateinamen zu erstellen. Damit steht der Inhalt der Datei unter zwei verschiedenen Dateinamen zur Verfügung. Bei Laden des Projektes wählt man dann einfach den *.sb2* Dateinamen und läd somit den Inhalt der *.sbx* Datei.
* Im Terminal:
```
pi@student-robot:~/Scratch $ ls -l
insgesamt 60
-rw------- 1 pi pi 58064 Apr 15 13:53 Project.sbx
pi@student-robot:~/Scratch $ ln -s Project.sbx Project.sb2
pi@student-robot:~/Scratch $ ls -l
insgesamt 60
lrwxrwxrwx 1 pi pi    11 Apr 15 13:58 Project.sb2 -> Project.sbx
-rw------- 1 pi pi 58064 Apr 15 13:53 Project.sbx
pi@student-robot:~/Scratch $ 
```
