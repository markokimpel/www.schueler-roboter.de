[Home](../..)

# Basisinstallation Software

Der Roboter nutzt einen Raspberry Pi als Herzstück. Das Standard-Betriebssystem für den Raspberry Pi ist [Raspbian](https://de.wikipedia.org/wiki/Raspberry_Pi#Raspbian). Es gibt aber auch Alternativen. Beispielsweise bietet Dexter Industries für den GoPiGo3 [DexterOS](https://www.dexterindustries.com/dexteros/get-dexteros-operating-system-for-raspberry-pi-robotics/), [Raspbian for Robots](https://www.dexterindustries.com/raspberry-pi-robot-software/) und [Cinch](https://www.dexterindustries.com/howto/use-cinch-operating-system/) an. DexterOS ist leicht zu benutzen und zu updaten, beinhaltet eine Scratch-ähnliche Umgebung namens Bloxter ([Onlineversion](http://www.bloxter.com/)) und eine Entwicklungsumgebung für Python. DexterOS ist Closed Source und nicht erweiterbar - kein freier Zugriff auf das Dateisystem, keine Installation eigener Software. Raspbian for Robots basiert auf Raspbian, mit zusätzlicher Software von Dexter Industries. Cinch soll das Erstellen eines Wi-Fi Access Points ermöglichen.

Für die Experimente mit dem Schüler-Roboter wird eine eigene Softwareinstallation benutzt:
* Basis ist ein reines Raspbian.
* Mit Bibliotheken um den GoPiGo3 anzusteuern.
* Sie enthält weitere Software für die Workshops, z.B. Integration mit Scratch 2 Offline Editor und ScratchX.
* Der im GoPiGo3 verbaute Raspberry Pi muss nicht mit Tastatur, Maus oder Bildschirm verbunden werden - er wird *headless* betrieben.
* Funktionen zum Aktualisieren und Zurücksetzen der Installation.
* Die SD Karte muss für Aktualisierungen und zum Zurücksetzen der Installation nicht entfernt werden.
* Automatische Erstellung eines Wi-Fi Access Points zum leichten kabellosen Verbinden mit dem Roboter.
* Zusätzlich kann sich der Roboter über einen USB WLAN Adapter mit dem lokalen WLAN verbinden.

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

*NOOBS* (nicht *NOOBS Lite*) von https://www.raspberrypi.org/downloads/noobs/ herunterladen, z.B. *NOOBS_v2_8_1.zip*.

SHA-256 kontrollieren.

Zip Datei entpacken. Der Inhalt wird in den nächsten Schritten modifiziert und dann auf eine SD Karte geschrieben.

Parameter ` silentinstall` an die Parameterliste in *recovery.cmdline* anhängen. Dieser Parameter wird für die initiale headless Installation und bei Updates benötigt. Ist bereits ein Betriebssystem installiert, wird NOOBS kein silentinstall durchführen. Damit kann der Parameter immer in der Datei bleiben.

Eine leere Datei *[ssh](files/ssh)* erstellen. Die Datei liegt im gleichen Verzeichnis wie *recovery.cmdline*. Die Datei wird beim Partitionsetup in die boot Partition kopiert und sorgt beim Boot Vorgang dafür, dass der ssh Server gestartet wird und man sich somit remote anmelden kann.

In Verzeichnis *os/* alle Betriebssysteme ausser *Raspbian* löschen (z.B. *LibreELEC_RPi*, *LibreELEC_RPi2*).

Eine große Datei *.placeholder* (Datei in [zip](files/placeholder1.5gb.zip)) in das Verzeichnis *os/* legen. Die Datei dient dazu, Platz in der ersten Partition zu reservieren. Dadurch können auch größere Updates installiert werden.

microSD Karte mit mindestens 8GB mit einer Partition und FAT32 formatieren.

Dateien auf die Karte kopieren.

Die lokalen Dateien behalten. Wir brauchen sie später bei der Erstellung des Images.

### Raspbian konfigurieren

SD Karte in den Raspberry stecken.

Netzwerkkabel in den Raspberry stecken.

Raspberry anschalten. Es muss keine Tastatur oder Monitor mit dem Raspberry verbunden sein. Der Raspberry installiert und bootet selbständig Raspbian. Die Zeitdauer für die Installation hängt von der Geschwindigkeit der SD Karte ab. Bei einer 32GB Sandisk dauert die Installation etwa 20 Minuten. Der Vorgang ist abgeschlossen, wenn die Schreib LED (grün) aus bleibt.

Netzwerkadresse ermitteln

Mit Raspberry über ssh verbinden. Nutzername/Passwort sind *pi*/*raspberry*.

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

Samba installieren. Damit kann auf Verzeichnisse zugegriffen werden, und Windows Clients finden den Raspberry mit dem Namen.

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

Bei den *ls aliases* hinzufügen

```
alias ll='ls -laF'
```

Feste Namen den Wi-Fi Adaptern zuweisen.

Nach dem Einstecken des USB WLAN Adapters hat der Raspberry Pi zwei WLAN Schnittstellen. Diese heissen *wlan0* und *wlan1*. Welche Schnittstelle welchen Namen bekommt ist zufällig und kann sich zwischen Neustarts ändern. Damit lässt sich kein Access Point aufsetzen oder Firewall Regeln definieren. Die *Predictable Network Interface Names* sind nur bedingt hilfreich. Beim Raspberry bekommt der USB WLAN Adapter damit eine ID, die seine MAC Adresse beinhaltet. Das macht die Konfiguration aufwendiger, wenn das gleiche SD Kartenimage für mehrere Raspberries benutzt werden soll. Schlimmer noch: das interne WLAN ist manchmal wlan0, manchmal wlan1. Folgende Änderungen erzwingen den namen wlan0 für das interne WLAN und wlan1 für einen USB Adapter. Nur ein WLAN USB Adapter darf gleichzeitig benutzt werden.

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


TODO

1. Root Partition sichern
    ```
    sudo apt install bsdtar
    sudo mkdir /mnt/transfer
    sudo mount -t cifs -o user=username //fileserver/folder /mnt/transfer
    cd /
    sudo bsdtar --numeric-owner --format gnutar --one-file-system -cpf /mnt/transfer/myroot.tar .
    ```

## Referenzen

* https://github.com/raspberrypi/noobs
* https://www.raspberrypi.org/forums/viewtopic.php?t=198946
* https://www.raspberrypi.org/documentation/configuration/wireless/access-point.md
