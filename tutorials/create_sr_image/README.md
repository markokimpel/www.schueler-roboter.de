[Home](../..)

# Basisinstallation Software

Der Roboter nutzt einen Raspberry Pi als Herzstück. Das Standard-Betriebssystem für den Raspberry Pi ist [Raspbian](https://de.wikipedia.org/wiki/Raspberry_Pi#Raspbian). Es gibt aber auch Alternativen. Beispielsweise bietet Dexter Industries für den GoPiGo3 [DexterOS](https://www.dexterindustries.com/dexteros/get-dexteros-operating-system-for-raspberry-pi-robotics/), [Raspbian for Robots](https://www.dexterindustries.com/raspberry-pi-robot-software/) und [Cinch](https://www.dexterindustries.com/howto/use-cinch-operating-system/) an. DexterOS ist leicht zu benutzen und zu updaten, beinhaltet eine Scratch-ähnliche Umgebung namens Bloxter ([Onlineversion](http://www.bloxter.com/)) und eine Entwicklungsumgebung für Python. DexterOS ist Closed Source und nicht erweiterbar - kein freier Zugriff auf das Dateisystem, keine Installation eigener Software. Raspbian for Robots basiert auf Raspbian, mit zusätzlicher Software von Dexter Industries. Cinch soll das Erstellen eines Wi-Fi Access Points ermöglichen.

Für die Experimente mit dem Schüler-Roboter wird eine eigene Softwareinstallation benutzt:
* Basis ist ein aktuelles Raspbian.
* Mit Bibliotheken um den GoPiGo3 anzusteuern.
* Sie enthält weitere Software für die Workshops, z.B. Integration mit Scratch 2 Offline Editor und ScratchX.
* Der im GoPiGo3 verbaute Raspberry Pi muss nicht mit Tastatur, Maus oder Bildschirm verbunden werden - er wird *headless* betrieben.
* Funktionen zum Aktualisieren und Zurücksetzen der Installation.
* Die SD Karte muss für Aktualisierungen und zum Zurücksetzen der Installation nicht entfernt werden.
* Automatische Erstellung eines Wi-Fi Access Points zum leichten kabellosen Verbinden mit dem Roboter.
* Zusätzlich kann sich der Roboter über einen USB WLAN Adapter mit dem lokalen WLAN verbinden. Damit sind die Nutzung des Access Points und Internet gleichzeitig möglich.

Wer es einfach mag, nutzt ein vorhandenes Kartenimage und muss sich um die Details der Installation und Konfiguration nicht kümmern. Siehe Kapitel *SD Karte initial beschreiben*, *Mit Roboter verbinden* und *SD Karte aktualisieren*. Gruppenleiter sollten ausserdem *Installation anpassen* und *Installation zurücksetzen* lesen. *SD Kartenimage erstellen* ist für die Maintainer des Kartenimages und technisch Interessierte gedacht.

## SD Karte initial beschreiben

TODO

## Mit Roboter verbinden

TODO

## SD Karte aktualisieren

TODO

## Installation anpassen

TODO

## Installation zurücksetzen

TODO

```
sudo rm /media/pi/SETTINGS/installed_os.json
sudo shutdown -r now
```

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

microSD Karte mit mindestens 8GB mit einer Partition und FAT32 formatieren.

Dateien auf die Karte kopieren.

Die lokalen Dateien behalten. Wir brauchen sie später bei der Erstellung des Images.

### Raspbian konfigurieren

SD Karte in den Raspberry Pi des GoPiGo3 stecken.

Ethernet Netzwerkkabel in den Raspberry Pi stecken.

Der Raspberry Pi/GoPiGo3 wird während der Softwareinstallation vorzugsweise über den USB Anschluss mit Strom versorgt. Die Akkus können entfernt werden.

Raspberry Pi anschalten (durch Einstecken des USB Kabels). Die Power LED des GoPiGo3 wird erst dann korrekt über An/Aus und Batteriezustand informieren, wenn die entsprechende Software installiert wurde.

Der Raspberry Pi installiert und bootet selbständig Raspbian. Die Zeitdauer für die Installation hängt von der Geschwindigkeit der SD Karte ab. Bei einer 32GB Sandisk dauert die Installation etwa 20 Minuten. Der Vorgang ist abgeschlossen, wenn die Schreib LED (grün) aus bleibt.

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
no-hosts
address=/student-robot/192.168.42.1

interface=wlan0
    dhcp-range=192.168.42.100,192.168.42.200,255.255.255.0,24h
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
channel=1
wmm_enabled=0
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
* Mit *VNC Viewer* zu *student-robot* verbinden, Nutzer *pi*/*myr0bot*.
* Konfigurationstool mit Cancel abbrechen. Das Standardimage soll nicht auf eine spezielle Sprache oder Zeitzone eingestellt sein. Das kann bei *Installation anpassen* gemacht werden.
* Bildschirmauflösung auf 1280x1024 ändern: Menü > *Preferences* > *Raspberry Pi Configuration*, *Set Resolution*, Neustart notwendig, evtl. erneut mit Access Point verbinden
* GoPiGo3 Verknüpfungen auf dem Desktop löschen. Die sind für die Integration mit Scratch 1 und verwirren deshalb eher.
* Bluetooth abschalten
* Adapter wlan1 mit lokalem WLAN verbinden.
* Öffentliche Webseite, z.B. https://www.schueler-roboter.de/, auf Laptop öffnen (bedeutet, dass IP Forwarding funktioniert).
* In Terminal: `cd ~/student-robot.org/gopigoscratchextension/gpg3server/`, `./run.sh`
* Scratch 2 starten: Menü *Programming* > *Scratch 2*
* Beispielprogramm *~/student-robot.org/gopigoscratchextension/scratch_examples/Simple Manual Rover.sb2* öffnen
* Experimentelle Erweiterung laden: *http://student-robot:8080/scratch_extension.js* (mit Umschalt + linke Maustaste auf *File* Menü)
* Bewegungen testen
* Abstandssensor testen (Doppelklick auf *distance* Block)
* In weiterem Terminal: `cd ~/student-robot.org/gopigoscratchextension/streamingserver/`, `./run.sh`
* Video in Browser testen: http://student-robot:8081/
* Beide Server stoppen
* Zugriff auf Samba Shares. Nutzer *pi*/*myr0bot*. Share *\\\\student-robot\\root* sollte nur lesbar sein, *\\\\student-robot\\pi* sollte auch schreibbar sein.
* Zugangsdaten zum lokalen Netzwerk löschen damit sie nicht im image auftauchen: `sudo nano /etc/wpa_supplicant/wpa_supplicant-wlan1.conf`, die beiden ersten Zeilen bleiben stehen.
* GoPiGo3 über Power Taste herunterfahren. Während des Herunterfahrens blinkt sie rot, dann geht sie aus.

### Partition sichern

Ethernetkabel mit Raspberry Pi verbinden.

Stromversorgung vorzugsweise über USB Port. Die Akkus können entfernt werden.

Nicht benötigte Pakete entfernen, ggf. Reboot.

```
sudo apt autoremove
[ -f /var/run/reboot-required ] && sudo shutdown -r now
```

Sichern der Root Partition mit bsdtar. Das Archiv muss ausserhalb der zu sichernden Partition gespeichert werden, z.B. auf einem SMB Share.

```
sudo apt install bsdtar
sudo mkdir /mnt/transfer
sudo mount -t cifs -o user=<username> //<fileserver>/<folder> /mnt/transfer
cd /
sudo bsdtar --numeric-owner --format gnutar --one-file-system -cpvf /mnt/transfer/root.tar .
```

TODO: Dateien/Verzeichnisse ausschliessen

Während der Ausführung von bsdtar in der Root Partition werden die folgenden Fehlermeldungen auf stderr ausgegeben. Sie können ignoriert werden.
* Viele Male *: tar format cannot archive socket*: diese Fehlermeldung bezieht sich auf Sockets im Verzeichnis /var/lib/samba/private/msg.sock/
* *bsdtar: Couldn't list extended attributes: No data available*: diese Fehlermeldung bezieht sich auf das Verzeichnis /media/pi/

Das Komprimieren geht am schnellsten, wenn eine schnelle CPU mit mehreren Kernen und viel Speicher zur Verfügung stehen. Das geht ausserhalb des Raspberry Pis am besten. Neuere Versionen von *xz* unterstützen die Option `-T 0`. Damit werden mehrere Ausführungs-Threads genutzt.

```
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
    "release_date": "2018-05-27",
    "supported_models": [
        "Pi 3"
    ],
    "url": "https://www.student-robot.org/",
    "username": "pi",
    "version": "stretch"
}
```

In Datei *partitions.json* for partition *root* folgende Werte anpassen:

* *uncompressed_tarball_size*: Größe in MB, z.B. `4173`
* *partition_size_nominal*: mindestens `5000`

Datei *Raspbian.png* in *RaspbianForStudentRobot.png* umbenennen.

Datei *[README.txt](files/README.txt)* dem Verzeichnis hinzufügen.

TODO: Datei boot.tar.gz ändern (in config.txt dtparam=i2c_arm=on und dtparam=spi=on unkommentieren, weitere Änderungen).

Datei *root.tar.xz* durch die oben erzeugte Version ersetzen.

Das gesamte NOOBS Verzeichnis in ein zip, z.B. *RaspbianForStudentRobot_2018-05-27.zip*, einpacken. Dateien wie *recovery.cmdline* liegen direkt im Wurzelverzeichnis.

Glückwunsch, du hast ein neues SD Kartenimage erzeugt. Dieses kann nun wie in *SD Karte initial beschreiben* und *SD Karte aktualisieren* beschrieben genutzt werden.

## Referenzen

* https://github.com/raspberrypi/noobs
* https://www.raspberrypi.org/forums/viewtopic.php?t=198946
* https://www.raspberrypi.org/documentation/configuration/wireless/access-point.md
* https://w1.fi/cgit/hostap/plain/hostapd/hostapd.conf
* https://github.com/DexterInd/GoPiGo3
* https://github.com/DexterInd/DI_Sensors
