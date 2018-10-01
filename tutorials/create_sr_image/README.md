---
title: Basisinstallation Software
permalink: /tutorials/create_sr_image/
---

[Home](../..)

# Basisinstallation Software

Der Roboter nutzt einen Raspberry Pi 3 Model B als Herzstück. Das Standard-Betriebssystem für den Raspberry Pi ist [Raspbian](https://de.wikipedia.org/wiki/Raspberry_Pi#Raspbian). Es gibt aber auch Alternativen. Beispielsweise bietet Dexter Industries für den GoPiGo3 [DexterOS](https://www.dexterindustries.com/dexteros/get-dexteros-operating-system-for-raspberry-pi-robotics/), [Raspbian for Robots](https://www.dexterindustries.com/raspberry-pi-robot-software/) und [Cinch](https://www.dexterindustries.com/howto/use-cinch-operating-system/) an. DexterOS ist leicht zu benutzen und zu updaten, beinhaltet eine Scratch-ähnliche Umgebung namens Bloxter ([Onlineversion](http://www.bloxter.com/)) und eine Entwicklungsumgebung für Python. DexterOS ist Closed Source und nicht erweiterbar - kein freier Zugriff auf das Dateisystem, keine Installation eigener Software. Raspbian for Robots basiert auf Raspbian, mit zusätzlicher Software von Dexter Industries. Cinch soll das Erstellen eines Wi-Fi Access Points ermöglichen.

Für die Experimente mit dem Schüler-Roboter wird eine eigene Softwareinstallation benutzt:
* Basis ist ein aktuelles Raspbian.
* Mit Bibliotheken um den GoPiGo3 anzusteuern.
* Sie enthält weitere Software für die Workshops, z.B. Integration mit Scratch 2 Offline Editor und ScratchX.
* Der im GoPiGo3 verbaute Raspberry Pi muss nicht mit Tastatur, Maus oder Bildschirm verbunden werden - er wird *headless* betrieben.
* Funktionen zum Aktualisieren und Zurücksetzen der Installation.
* Die SD Karte muss für Aktualisierungen und zum Zurücksetzen der Installation nicht entfernt werden.
* Automatische Erstellung eines Wi-Fi Access Points zum leichten kabellosen Verbinden mit dem Roboter. Ein WLAN wird nicht benötigt.
* Zusätzlich kann sich der Roboter über einen USB WLAN Adapter mit dem lokalen WLAN verbinden. Damit sind die Nutzung des Access Points und Internet gleichzeitig möglich.

Wer es einfach mag, nutzt ein vorhandenes Kartenimage und muss sich um die Details der Installation und Konfiguration nicht kümmern. Siehe Kapitel *SD Karte initial beschreiben* und *Mit Roboter verbinden*. Gruppenleiter sollten ausserdem *Installation anpassen* und *Installation zurücksetzen* lesen. In *SD Karte aktualisieren* ist beschrieben, wie die Installation ohne das Entfernen der SD Karte aktualisiert werden kann. *SD Kartenimage erstellen* ist für die Maintainer des Kartenimages und technisch Interessierte gedacht.

## SD Karte initial beschreiben

Um die SD Karte im GoPiGo3 zu wechseln, müssen mehrere Kabel entfernt werden. Das ist mühsam und tut den Steckverbindern auch nicht gut. Deshalb versuchen wir die Karte so selten wie möglich zu wechseln. Am Besten du beschreibst die Karte vor dem Bau des Roboters und steckst sie in den Raspberry Pi. Spätere Aktualisierungen von RaspbianForStudentRobot sind in der Regel ohne das Entfernen der Karte möglich.

Zum initialen Beschreiben der SD Karte brauchst du einen weiteren Computer mit SD Kartenleser, z.B. einen Windows Laptop. Die physische Kartengröße muss microSD sein, denn nur diese akzeptiert der Raspberry Pi 3 Model B. Wir empfehlen eine Kapazität von 32 GB. Häufig werden microSD Karten mit einem Adapter verkauft. Mit diesem können sie in einem Computer genutzt werden, der nur die SD Größe unterstützt.

Die SD Karte muss eine Partition haben und diese muss mit FAT32 formatiert sein. Das ist bei neue gekauften Karten in der Regel bereits der Fall. Ansonsten kann das mit Betriebssystem Boardmitteln erreicht werden, oder du nutzt den [SD Memory Card Formatter](https://www.sdcard.org/downloads/formatter_4/index.html) der [SD Association](https://www.sdcard.org/).

RaspbianForStudentRobot liegt als zip Datei vor. Den Inhalt der Datei musst du auf die SD Karte kopieren.

Dann stecke die Karte in den Raspberry Pi und baue den Roboter fertig zusammen.

Ist der Roboter fertig zusammengebaut, die Kamera, der Servo, der Abstandssensor und der Wi-Fi Adapter installiert, kannst du den Roboter erstmalig starten. Das machst du, indem du die Power Taste (rechts hinten am GoPiGo3 Board) drückst. Beim ersten Start wird das Betriebssystem automatisch installiert und dann gestartet. Während dieses Vorgangs blinkt die grüne LED neben der Power Taste. Die kleine grüne LED neben dem mini-USB Anschluss blinkt bei Lese- und Schreiboperationen auf der SD Karte. Die Zeitdauer für die Installation hängt von der Geschwindigkeit der SD Karte ab. Bei einer 32 GB Samsung EVO Plus dauert die Installation etwa 12 Minuten. Die Installation ist abgeschlossen und das Betriebssystem gestartet, wenn die LED neben der Power Taste ständig grün leuchtet. Jetzt kannst du dich mit dem Roboter verbinden - siehe unten.

## Mit Roboter verbinden

* Arbeitsrechner mit WLAN
  * Du brauchst einen weiteren Computer um auf den Roboter zuzugreifen. An diesem Arbeitsrechner sitzt du und programmierst den Roboter. Der Arbeitsrechner kann ein Raspberry Pi mit Monitor, Tastatur und Maus sein, oder ein Windows Laptop. Da der Roboter über WLAN kommuniziert, muss auch der Arbeitsrechner über WLAN kommunizieren können.
* Roboter anschalten
  * Starte den Roboter indem du die Power Taste (rechts hinten am GoPiGo3 Board) drückst. Die grüne LED daneben beginnt zu blinken. Das bedeutet, das Betriebssystem wird geladen. Wenn die LED ständig grün leuchtet ist der Roboter betriebsbereit.
  * Übrigens: Wenn die LED neben der Power Taste beginnt gelb oder gar violett zu leuchten, dann bedeutet das die Akkus sind fast leer. Dann den Roboter ausschalten und Akkus wechseln.
* Arbeitsrechner mit Roboter WLAN verbinden
  * Der Roboter bietet ein WLAN Netzwerk an. Der Netzwerkname (SSID) ist *student-robot*, bei Arbeitsgruppen *student-robot[zahl]*. Das voreingestellte Passwort ist *changeitnow*. Bei Arbeitsgruppen erfrage das Passwort von deinem Gruppenleiter.
  * Verbinde dich mit deinem Arbeitsrechner zum WLAN des Roboters. Wennn du dich mit dem Roboter WLAN verbindest, verlierst du eine evtl. vorher bestehende WLAN Verbindung zum lokalen WLAN Router und damit zum Internet. Hierfür gibt es eine Lösung - siehe unten.
* Mit VNC Viewer am Roboter arbeiten
  * Mit dem VNC Viewer verbindest du dich zum Roboter und kannst den Desktop des Roboters sehen.
  * Bei Raspbian wird der VNC Viewer nicht mehr vorinstalliert. Er muss mit `sudo apt install realvnc-vnc-viewer` installiert werden. Die Verknüpfung befindet sich dann unter dem Menüpunkt *Internet*.
  * Für Windows kann der Viewer von https://www.realvnc.com/de/connect/download/viewer/ (Standalone EXE ist ausreichend) heruntergeladen werden.
  * Server-Adresse ist *student-robot.home*, bei Arbeitsgruppen *student-robot[zahl].home*. Beim ersten Aufruf muss die Identität des Servers bestätigt werden. Benutzname ist *pi*, das Passwort ist *myr0bot*.
  * Nun kannst du mit dem Raspbian Betriebssystem auf dem Roboter so arbeiten, als säßest du direkt davor.
* Roboter WLAN Passwort und Nutzerpasswort ändern
  * TODO
* Roboter mit dem lokalem WLAN verbinden
  * Wahrscheinlich war dein Arbeitsrechner über ein lokales WLAN mit dem Internet verbunden. Seitdem du dich mit dem Roboter WLAN verbunden hast, hat dein Arbeitsrechner keinen Internetzugriff mehr. Aber es gibt eine Lösung: Der Roboter hat zwei WLAN Schnittstellen. Die eine stellt das Roboter WLAN Netzwerk zur Verfügung und die andere kannst du mit dem lokalen WLAN verbinden. Dann haben dein Roboter, und über den Roboter auch dein Arbeitsrechner wieder Internetgriff.
  * Achtung: Ist der Roboter mit dem lokalem WLAN verbunden, können auch andere Nutzer des WLANs auf Dienste des Roboters zugreifen. Du solltest dich deshalb nur mit vertrauenswürdigen WLANs verbinden.
  * Am einfachsten richtest du die WLAN Verbindung vom Raspbian Desktop aus ein. Rechts oben in der Leiste ist das Symbol für WLAN. Dort wählst du das lokale WLAN Netzwerk aus und kannst dann das Passwort eingeben.
* Mit ssh auf Roboter zugreifen
  * Du kannst dich mit einem Terminal wie ssh oder PuTTY zur Kommandozeile des Roboters verbinden.
  * Die Adresse ist *student-robot.home*, Nutzername *pi* und Passwort *myr0bot*. Beim ersten Verbinden muss die Signatur des Servers bestätigt werden.

## Roboter ausschalten

* Das geht einfach: Offene Dokumente speichern, dann die Power Taste (rechts hinten am GoPiGo3 Board) drücken. Die LED daneben beginnt rot zu blinken. Offene Programme werden beendet und das Betriebssystem wird heruntergefahren. Die LED geht aus, wenn der Roboter vollständig heruntergefahren wurde. Du kannst nun die Akkus entfernen.

## SD Karte aktualisieren

Eine neue Version von RaspbianForStudentRobot kann ohne das Entfernen der SD Karte aus dem Raspberry Pi installiert werden. Die notwendigen Schritte werden hier beschrieben. Wen das Entfernen der SD Karte nicht stört kann alternativ den Schritten in *SD Karte initial beschreiben* folgen.

In der NOOBS Partition liegen die Installationsdateien für RaspbianForStudentRobot. Diese soll aktualisiert werden. Die Installation selber wird bei diesem Prozess nicht verändert. Erst beim nächsten Zurücksetzen der Installation werden die neuen Installationsdateien benutzt. NOOBS wird bei diesem Prozess nicht aktualisiert.

Als Quelle für das Image wird ein SMB Share angenommen.

```
sudo mkdir /mnt/transfer
sudo mount -r -t cifs -o user=<username> //<fileserver>/<folder> /mnt/transfer

sudo mkdir /mnt/noobs
sudo mount /dev/mmcblk0p1 /mnt/noobs

sudo rm -r /mnt/noobs/os/*

sudo unzip /mnt/transfer/<image>.zip os/* -x os/.placeholder -d /mnt/noobs/

sudo umount /mnt/transfer
sudo rmdir /mnt/transfer

sudo umount /mnt/noobs
sudo rmdir /mnt/noobs
```

Siehe Kapitel *Installation zurücksetzen* zum Installieren des neuen Images.

## Installation zurücksetzen

Die vorhandene Installation wird gelöscht und neu aufgesetzt. Alle gespeicherten Daten gehen dabei vorloren. Das ist hilfreich, wenn der Roboter von mehreren Personen genutzt wird und Änderungen des Vorgängers entfernt werden sollen, oder wenn eine neue Version installiert werden soll. Wichtige Dateien bitte vorher sichern.

Wird die u.g. Datei gelöscht, wird der NOOBS Installer beim Neustart automatisch das Image neu installieren und dann die Installation booten.

```
sudo rm /media/pi/SETTINGS/installed_os.json
sudo shutdown -r now
```

Die Zeitdauer für die Installation hängt von der Geschwindigkeit der SD Karte ab. Bei einer 32 GB Sandisk dauert die Installation etwa 15 Minuten. Der Vorgang ist abgeschlossen, wenn die Schreib LED (grün) aus bleibt.

Achtung beim ersten Verbinden: Hostname und Passwort wurden bei der Installation auch zurückgesetzt. Siehe Kapitel *Mit Roboter verbinden* für Voreinstellungen.

## Installation anpassen

TODO

```
sudo nano /etc/hostapd/hostapd.conf
```

Zeile *ssid* ändern.

```
ssid=student-robot1
```

```
sudo nano /etc/dnsmasq.conf
```

Zeile *address* ändern.

```
address=/student-robot1.home/192.168.42.1
```

```
sudo raspi-config
```

- Network Options > Hostname: *student-robot1*
- Finish, reboot

## SD Kartenimage erstellen

Wer sich nicht mit den Details der Installation herumschlagen möchte nimmt ein vorhandenes Kartenimage (siehe *SD Karte initial beschreiben*) und kann diesen Abschnitt ignorieren. :-)

### Kopieren von NOOBS und Raspbian auf die SD Karte

Die folgenden Schritte auf einem anderen Rechner als dem Raspberry Pi ausführen (z.B. einem Windows Laptop). Der Rechner muss auf die SD Karte schreiben können.

*NOOBS* (nicht *NOOBS Lite*) von https://www.raspberrypi.org/downloads/noobs/ herunterladen, z.B. *NOOBS_v2_8_2.zip*.

SHA-256 kontrollieren.

Zip Datei entpacken. Der Inhalt wird in den nächsten Schritten modifiziert und dann auf eine SD Karte geschrieben.

Parameter ` silentinstall` an die Parameterliste in *recovery.cmdline* anhängen. Dieser Parameter wird für die initiale headless Installation und bei Updates benötigt. Ist bereits ein Betriebssystem installiert, wird NOOBS kein silentinstall durchführen. Damit kann der Parameter immer in der Datei bleiben.

Eine leere Datei *[ssh](files/ssh)* erstellen. Die Datei liegt im gleichen Verzeichnis wie *recovery.cmdline*. Die Datei wird beim Partitionsetup in die boot Partition kopiert und sorgt beim Boot Vorgang dafür, dass der ssh Server gestartet wird und man sich somit remote anmelden kann.

In Verzeichnis *os/* alle Betriebssysteme ausser *Raspbian* löschen (z.B. *LibreELEC_RPi*, *LibreELEC_RPi2*).

Eine große Datei *.placeholder* (Datei in [zip](files/placeholder1.5gb.zip)) in das Verzeichnis *os/* legen. Die Datei dient dazu, Platz in der ersten Partition zu reservieren. Dadurch können später auch größere Updates installiert werden.

microSD Karte mit mindestens 8 GB mit einer Partition und FAT32 formatieren.

Dateien auf die Karte kopieren.

Die lokalen Dateien behalten. Wir brauchen sie später bei der Erstellung des Images.

### Raspbian konfigurieren

SD Karte in den Raspberry Pi des GoPiGo3 stecken.

Ethernet Netzwerkkabel in den Raspberry Pi stecken.

Der Raspberry Pi/GoPiGo3 wird während der Softwareinstallation vorzugsweise über den USB Anschluss mit Strom versorgt. Die Akkus können entfernt werden.

Raspberry Pi anschalten (durch Einstecken des USB Kabels). Die Power LED des GoPiGo3 wird erst dann korrekt über An/Aus und Batteriezustand informieren, wenn die entsprechende Software installiert wurde.

Der Raspberry Pi installiert und bootet selbständig Raspbian. Die Zeitdauer für die Installation hängt von der Geschwindigkeit der SD Karte ab. Bei einer 32GB Sandisk dauert die Installation etwa 15 Minuten. Der Vorgang ist abgeschlossen, wenn die Schreib LED (grün) aus bleibt.

Netzwerkadresse ermitteln

Mit Raspberry Pi über ssh verbinden. Nutzername/Passwort sind *pi*/*raspberry*.

Passwort ändern.

```
passwd
```

*raspberry*, 2x *myr0bot*

Raspbian aktualisieren, reboot wenn notwendig.

```
sudo apt update
sudo apt upgrade
[ -f /var/run/reboot-required ] && sudo shutdown -r now
```

Konfiguration mit raspi-config

```
sudo raspi-config
```

- Network Options > Hostname: *student-robot*
- Boot Options > Desktop / CLI: Desktop Autologin
- Interfacing Options: enable Camera, VNC, SPI, I2C
- Finish, reboot

Samba installieren. Damit kann auf Verzeichnisse zugegriffen werden, und Windows Clients finden den Raspberry Pi mit dem Namen.

```
sudo apt install samba
```

Nutzer *pi* hinzufügen

```
sudo smbpasswd -a pi
```

2x *myr0bot*

Samba Konfiguration anpassen

```
sudo nano /etc/samba/smb.conf
```

Im Bereich *[homes]* *read only = yes* ändern in

```
   read only = no
```

Am Ende der Datei folgendes Share hinzufügen

```
[root]
   comment = root
   path = /
   read only = yes
   valid users = pi
```

Parameter überprüfen

```
testparm
```

Samba neu starten

```
sudo systemctl restart smbd
sudo systemctl restart nmbd
```

*ll* in der bash erlauben

```
nano .bashrc
```

Bei den *ls aliases* hinzufügen. Änderung gilt erst für die nächste bash session.

```
alias ll='ls -laF'
```

Midnight Commander (ein textbasierter Dateimanager) installieren.

```
sudo apt install mc
```

Feste Namen den Wi-Fi Adaptern zuweisen.

Nach dem Einstecken des USB WLAN Adapters hat der Raspberry Pi zwei WLAN Schnittstellen. Diese heissen *wlan0* und *wlan1*. Welche Schnittstelle welchen Namen bekommt ist zufällig und kann sich zwischen Neustarts ändern. Damit lässt sich kein Access Point aufsetzen oder Firewall Regeln definieren. Die *Predictable Network Interface Names* sind nur bedingt hilfreich. Beim Raspberry Pi bekommt der USB WLAN Adapter damit eine ID, die seine MAC Adresse beinhaltet. Das macht die Konfiguration aufwendiger, wenn das gleiche SD Kartenimage für mehrere Raspberries benutzt werden soll. Schlimmer noch: das interne WLAN ist manchmal wlan0, manchmal wlan1. Folgende Änderungen erzwingen den namen wlan0 für das interne WLAN und wlan1 für einen USB Adapter. Nur ein WLAN USB Adapter darf gleichzeitig benutzt werden.

Neue Datei anlegen

```
sudo nano /etc/udev/rules.d/72-wlan-geo-dependent.rules
```

Als Inhalt einfügen

```
#
# +---------------+
# | wlan1 | wlan1 |
# +-------+-------+
# | wlan1 | wlan1 |
# +---------------+ (RPI USB ports with position independent device names for a maximum of 1 optional wifi dongle)
# 
# | wlan0 | (onboard wifi)
#
ACTION=="add", SUBSYSTEM=="net", SUBSYSTEMS=="sdio", KERNELS=="mmc1:0001:1", NAME="wlan0"
ACTION=="add", SUBSYSTEM=="net", SUBSYSTEMS=="usb",  KERNELS=="1-1.2",       NAME="wlan1"
ACTION=="add", SUBSYSTEM=="net", SUBSYSTEMS=="usb",  KERNELS=="1-1.4",       NAME="wlan1"
ACTION=="add", SUBSYSTEM=="net", SUBSYSTEMS=="usb",  KERNELS=="1-1.3",       NAME="wlan1"
ACTION=="add", SUBSYSTEM=="net", SUBSYSTEMS=="usb",  KERNELS=="1-1.5",       NAME="wlan1"
```

Neu starten

```
sudo shutdown -r now
```

Zuweisung der Gerätenamen kontrollieren

```
ifconfig
```

*wlan0* sollte jetzt der interne WLAN Adapter sein, *wlan1* der USB Adapter, *eth0* das Ethernet Kabel und *lo* das Loopback Device.

### Access Point, DHCP und DNS Server installieren

Dnsmasq (DHCP und DNS Server) und hostapd (Access Point Software) installieren.

```
sudo apt-get install dnsmasq hostapd
```

Services stoppen, bis wir mit der Konfiguration fertig sind.

```
sudo systemctl stop dnsmasq
sudo systemctl stop hostapd
```

Der interne WLAN Adapter (*wlan0*) wird als Access Point genutzt. Ihm wird eine statische IP Adresse zugewiesen.

```
sudo nano /etc/dhcpcd.conf
```

Am Ende der Datei einfügen

```
interface wlan0
    static ip_address=192.168.42.1/24
```

Dhcpcd neu starten.

```
sudo systemctl restart dhcpcd
```

Dnsmasq konfigurieren

```
sudo nano /etc/dnsmasq.conf
```

Am Ende der Datei einfügen

```
interface=wlan0

dhcp-range=192.168.42.100,192.168.42.200,1h

no-hosts
address=/student-robot.home/192.168.42.1
```

Neue Konfigurationsdatei für hostapd erstellen

```
sudo nano /etc/hostapd/hostapd.conf
```

Als Inhalt einfügen

```
interface=wlan0
driver=nl80211
ssid=student-robot
hw_mode=g
#country_code=DE
# non-overlapping channels: 1, 6, 11
channel=1
ieee80211n=1
wmm_enabled=1
ht_capab=[HT40][SHORT-GI-20][DSSS_CCK-40]
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=changeitnow
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
```

Position der Konfigurationsdatei festlegen

```
sudo nano /etc/default/hostapd
```

Zeile *#DAEMON_CONF=""* ändern in

```
DAEMON_CONF="/etc/hostapd/hostapd.conf"
```

Services starten

```
sudo systemctl start hostapd
sudo systemctl start dnsmasq
```

IP-Forwarding aktivieren

```
sudo nano /etc/sysctl.conf
```

Ändere Zeile *#net.ipv4.ip_forward=1* in

```
net.ipv4.ip_forward=1
```

Masquerate für ausgehende Verbindungen auf eth0 und wlan1.

```
sudo nano /etc/rc.local
```

Vor *exit 0* einfügen

```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
iptables -t nat -A POSTROUTING -o wlan1 -j MASQUERADE
```

Wpa_supplicant soll nur wlan1 steuern (nicht aber den Access Point wlan0).

```
sudo mv /etc/wpa_supplicant/wpa_supplicant.conf /etc/wpa_supplicant/wpa_supplicant-wlan1.conf
```

Reboot

```
sudo shutdown -r now
```

### GoPiGo3 Software installieren

GoPiGo3 Software installieren und Reboot. Die Software beinhaltet u.a. einen Service für die GoPiGo3 Power LED und den Power Schalter, sowie Python Bibliotheken für GoPiGo3 Hardware.

```
curl -L https://dexterindustries.com/update_gopigo3 | bash
sudo shutdown -r now
```

DI_Sensors installieren - wird für den Abstandssensor benötigt.

```
curl -L https://dexterindustries.com/update_sensors | bash
```

### GoPiGo Scratch Erweiterung installieren

Die Erweiterung installieren.

```
git clone https://github.com/markokimpel/gopigoscratchextension.git ~/student-robot.org/gopigoscratchextension/
```

Zur Vorbereitung des Tests Raspberry Pi runterfahren. 

```
sudo shutdown -h now
```

Warten bis grüne LED nicht mehr leuchtet. Dann USB Stromversorgung entfernen.

Ethernetkabel entfernen.

### Installation testen

* Akku mit GoPiGo3 verbinden.
* GoPiGo3 über Power Taste starten. LED daneben sollte während des Ladens des Betriebssystems grün blinken. Dann sollte sie ständig grün leuchten.
* Laptop mit Access Point *student-robot*, passwort *changeitnow* verbinden.
* Der Laptop sollte eine IP Adresse im Bereich 192.168.42.100-200 erhalten haben.
* Mit *VNC Viewer* zu *student-robot.home* verbinden, Nutzer *pi*/*myr0bot*.
* Konfigurationstool mit Cancel abbrechen. Das Standardimage soll nicht auf eine spezielle Sprache oder Zeitzone eingestellt sein. Das kann bei *Installation anpassen* gemacht werden.
* Bildschirmauflösung auf 1280x1024 ändern: Menü > *Preferences* > *Raspberry Pi Configuration*, *Set Resolution*, Neustart notwendig, evtl. erneut mit Access Point verbinden
* GoPiGo3 Verknüpfungen auf dem Desktop löschen. Die sind für die Integration mit Scratch 1 und verwirren deshalb eher.
* Bluetooth abschalten
* Adapter wlan1 mit lokalem WLAN verbinden.
* Öffentliche Webseite, z.B. https://www.schueler-roboter.de/, auf Laptop öffnen (bedeutet, dass IP Forwarding funktioniert).
* In Terminal: `cd ~/student-robot.org/gopigoscratchextension/gpg3server/`, `./run.sh`
* Scratch 2 starten: Menü *Programming* > *Scratch 2*
* Beispielprogramm *~/student-robot.org/gopigoscratchextension/scratch_examples/Simple Manual Rover.sb2* öffnen
* Experimentelle Erweiterung laden: *http://student-robot.home:8080/scratch_extension.js* (mit Umschalt + linke Maustaste auf *File* Menü)
* Bewegungen testen
* Abstandssensor testen (Doppelklick auf *distance* Block)
* In weiterem Terminal: `cd ~/student-robot.org/gopigoscratchextension/streamingserver/`, `./run.sh`
* Video in Browser testen: http://student-robot.home:8081/
* Beide Server stoppen
* Zugriff auf Samba Shares. Nutzer *pi*/*myr0bot*. Share *\\\\student-robot.home\\root* sollte nur lesbar sein, *\\\\student-robot.home\\pi* sollte auch schreibbar sein.
* Zugangsdaten zum lokalen Netzwerk löschen damit sie nicht im image auftauchen: `sudo nano /etc/wpa_supplicant/wpa_supplicant-wlan1.conf`, die beiden ersten Zeilen bleiben stehen.
* GoPiGo3 über Power Taste herunterfahren. Während des Herunterfahrens blinkt sie rot, dann geht sie aus.

### Partitionen sichern

Ethernetkabel mit Raspberry Pi verbinden.

Stromversorgung vorzugsweise über USB Port. Die Akkus können entfernt werden.

Nicht benötigte Pakete entfernen, ggf. Reboot.

```
sudo apt autoremove
[ -f /var/run/reboot-required ] && sudo shutdown -r now
```

Die Partitionen werden mit *bsdtar* gesichert.

```
sudo apt install bsdtar
```

Die Archive müssen ausserhalb der zu sichernden Partition gespeichert werden, z.B. auf einem SMB Share.

```
sudo mkdir /mnt/transfer
sudo mount -t cifs -o user=<username> //<fileserver>/<folder> /mnt/transfer
```

Boot Partition mit bsdtar sichern.

Die Datei *cmdline.txt* beziehen wir vom Originalarchiv in der NOOBS Partition. Sie wurde während der Installation verändert. Die Datei *os_config.json* wird während der Installation erzeugt und muss deshalb nicht gesichert werden. Die Datei *config.txt* enthält Informationen zur Aktivierung der Kamera, der Schnittstellen SPI und I2C, sowie die voreingestellt Bildschirmauflösung.

```
sudo bsdtar --numeric-owner --format gnutar -cpvf /mnt/transfer/boot.tar -C /boot --exclude ./cmdline.txt --exclude ./os_config.json .

sudo mkdir /mnt/noobs
sudo mount -r /dev/mmcblk0p1 /mnt/noobs

cd ~
cp /mnt/noobs/os/Raspbian/boot.tar.xz boot.tar.xz
unxz boot.tar.xz
sudo bsdtar --numeric-owner --format gnutar -rpvf /mnt/transfer/boot.tar --include ./cmdline.txt @boot.tar
rm boot.tar

sudo umount /mnt/noobs
sudo rmdir /mnt/noobs
```

Root Partition mit bsdtar sichern.

```
sudo bsdtar --numeric-owner --format gnutar --one-file-system -cpvf /mnt/transfer/root.tar -C / .
```

TODO: Dateien/Verzeichnisse ausschliessen

Während der Ausführung von bsdtar in der Root Partition werden die folgenden Fehlermeldungen auf stderr ausgegeben. Sie können ignoriert werden.
* Viele Male *: tar format cannot archive socket*: diese Fehlermeldung bezieht sich auf Sockets im Verzeichnis /var/lib/samba/private/msg.sock/
* *bsdtar: Couldn't list extended attributes: No data available*: diese Fehlermeldung bezieht sich auf das Verzeichnis /media/pi/

Das SMB Share wieder entfernen.

```
sudo umount /mnt/transfer
sudo rmdir /mnt/transfer
```

Das Komprimieren geht am schnellsten, wenn eine schnelle CPU mit mehreren Kernen und viel Speicher zur Verfügung stehen. Das geht ausserhalb des Raspberry Pis am besten. Neuere Versionen von *xz* unterstützen die Option `-T 0`. Damit werden mehrere Ausführungs-Threads genutzt.

```
xz -k -9 -e -T 0 boot.tar
xz -k -9 -e -T 0 root.tar
```

### Partitionen in NOOBS integrieren

Jetzt wird das ausgepackte NOOBS Image aus dem ersten Schritt weiter modifiziert.

Verzeichnis *os/Raspbian/* in *os/RaspbianForStudentRobot/* umbenennen.

Die folgenden Änderungen erfolgen im Verzeichnis *os/RaspbianForStudentRobot/*.

Beim Editieren von Textdateien auf Unix Zeilenendungen achten.

Datei *os.json* anpassen. Neuer Inhalt:

```
{
    "description": "Raspbian with modifications for the Student-Robot",
    "kernel": "4.14",
    "name": "RaspbianForStudentRobot",
    "password": "myr0bot",
    "release_date": "2018-08-15",
    "supported_models": [
        "Pi 3"
    ],
    "url": "https://www.student-robot.org/",
    "username": "pi",
    "version": "stretch"
}
```

In Datei *partitions.json* for partition *root* folgende Werte anpassen:

* *uncompressed_tarball_size*: Größe in MB (1 MB = 1.000.000 Byte), z.B. `4354`
* *partition_size_nominal*: mindestens 400 MB mehr, z.B. `5000`

Datei *Raspbian.png* in *RaspbianForStudentRobot.png* umbenennen.

Datei *[README.txt](files/README.txt)* dem Verzeichnis hinzufügen.

Datei *boot.tar.xz* durch die oben erzeugte Version ersetzen.
Datei *root.tar.xz* durch die oben erzeugte Version ersetzen.

Das gesamte NOOBS Verzeichnis in ein zip, z.B. *RaspbianForStudentRobot_2018-08-15.zip*, einpacken. Dateien wie *recovery.cmdline* liegen direkt im Wurzelverzeichnis.

Glückwunsch, du hast ein neues SD Kartenimage erzeugt. Dieses kann nun wie in *SD Karte initial beschreiben* und *SD Karte aktualisieren* beschrieben genutzt werden.

## Referenzen

* https://github.com/raspberrypi/noobs
* https://www.raspberrypi.org/forums/viewtopic.php?t=198946
* https://www.raspberrypi.org/documentation/configuration/wireless/access-point.md
* https://w1.fi/cgit/hostap/plain/hostapd/hostapd.conf
* https://github.com/DexterInd/GoPiGo3
* https://github.com/DexterInd/DI_Sensors

*Copyright 2018 Marko Kimpel*

*Licensed under the GNU General Public License version 3, or (at your option) any later version.*
