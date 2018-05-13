[Home](../..)

# Basisinstallation Software

Für die meisten Nutzer sind nur die Punkte *SD Karte initial beschreiben* und *SD Karte aktualisieren* relevant. Gruppenleiter sollten auch *Installation zurücksetzen* lesen. *SD Kartenimage erstellen* ist für die Maintainer des Kartenimages gedacht.

## SD Karte initial beschreiben

TODO

## SD Karte aktualisieren

TODO

## Installation zurücksetzen

TODO

```
sudo rm /media/pi/SETTINGS/installed_os.json
sudo shutdown -r now
```

## SD Kartenimage erstellen

1. NOOBS von https://www.raspberrypi.org/downloads/noobs/ herunterladen, z.B. *NOOBS_v2_8_1.zip*.
1. SHA-256 kontrollieren
1. Zip Datei entpacken. Der Inhalt wird in den nächsten Schritten modifiziert und dann auf eine SD Karte geschrieben.
1. Parameter ` silentinstall` an die Parameterliste in *recovery.cmdline* anhängen. Dieser Parameter wird für die initiale headless Installation und bei Updates benötigt. Ist bereits ein Betriebssystem installiert, wird NOOBS kein silentinstall durchführen. Damit kann der Parameter immer in der Datei bleiben.
1. Eine leere Datei *[ssh](files/ssh)* erstellen. Die Datei liegt auf der gleichen Ebene wie *recovery.cmdline*. Die Datei wird beim Partitionsetup in die boot Partition kopiert und sorgt beim Boot Vorgang dafür, dass der ssh Server gestartet wird und man sich somit remote anmelden kann.
1. In Verzeichnis *os/* alle Betriebssysteme ausser *Raspbian* löschen (z.B. LibreELEC_RPi, LibreELEC_RPi2).
1. Eine große Datei *.placeholder* (Datei in [zip](files/placeholder1.5gb.zip)) in das Verzeichnis *os/* legen. Die Datei dient dazu, Platz in der ersten Partition zu reservieren. Dadurch können auch größere Updates installiert werden.
1. microSD Karte mit mindestens 8GB mit einer Partition und FAT32 formatieren.
1. Dateien auf die Karte kopieren.
1. Karte in den Raspberry stecken.
1. Netzwerkkabel in den Raspberry stecken.
1. Raspberry anschalten. Es muss keine Tastatur oder Monitor mit dem Raspberry verbunden sein. Der Raspberry installiert und bootet selbständig Raspbian. Die Zeitdauer für die Installation hängt von der Geschwindigkeit der SD Karte ab. Bei einer 32GB Sandisk dauert die Installation etwa 20 Minuten. Der Vorgang ist abgeschlossen, wenn die Schreib LED (grün) aus bleibt.
1. Netzwerkadresse ermitteln
1. Mit Raspberry über ssh verbinden. Nutzername/Passwort sind *pi*/*raspberry*.
1. Passwort ändern. `passwd`, *raspberry*, 2x *myr0bot*
1. Raspbian aktualisieren

    ```
    sudo apt update
    sudo apt upgrade
    ```

    - reboot if needed
1. `sudo raspi-config`
    - Network Options > Hostname: *student-robot*
    - Boot Options > Desktop / CLI: Desktop Autologin
    - Interface Options: enable Camera, VNC, SPI, I2C
    - Reboot
1. *.bashrc* hinzufügen `alias ll='ls -laF'`

## Referenzen

* https://github.com/raspberrypi/noobs
