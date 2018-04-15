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
  * Der Roboter bietet ein WLAN Netzwerk an. Der Netzwerkname (SSID) ist `student-robot`, bei Arbeitsgruppen `student-robot[zahl]`. Das voreingestellte Passwort ist `changeitnow`. Bei Arbeitsgruppen erfrage das Passwort von deinem Gruppenleiter.
  * Verbinde dich mit deinem Arbeitsrechner zum WLAN des Roboters. Wennn du dich mit dem Roboter WLAN verbindest, verlierst du eine evtl. vorher bestehende WLAN Verbindung zum lokalen WLAN Router und damit zum Internet.
* Mit VNC Viewer verbinden
  * Mit dem VNC Viewer verbindest du dich zum Roboter und kannst den Desktop des Roboters sehen.
  * Bei Raspbian ist der VNC Viewer bereits installiert. Für Windows kann er von https://www.realvnc.com/de/connect/download/viewer/ (Standalone EXE ist ausreichend) heruntergeladen werden.
  * Server-Adresse ist `student-robot`, bei Arbeitsgruppen `student-robot[zahl]`, Benutzname ist `pi`, Passwort ist `myrobot`. Beim ersten Aufruf mit der Fingerprint des Servers bestätigt werden.
  * Nun kannst du mit dem Raspbian Betriebssystem auf dem Roboter so arbeiten, als säßest du direkt davor.

## Roboter ausschalten

* Das geht einfach: Offene Dokumente speichern, dann die Power Taste (rechts hinten am GoPiGo3 Board) drücken. Die LED daneben beginnt rot zu blinken. Offene Programme werden beendet und das Betriebssystem wird heruntergefahren. Die LED geht aus, wenn der Roboter vollständig heruntergefahren wurde. Du kannst nun die Akkus entfernen.

