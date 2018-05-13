[Home](../..)

# Basisinstallation Software

Für die meisten Nutzer sind nur die Punkte *SD Karte initial beschreiben* und *SD Karte aktualisieren* relevant.

## SD Karte initial beschreiben

TODO

## SD Karte aktualisieren

TODO

## SD Kartenabbild erstellen

1. NOOBS von https://www.raspberrypi.org/downloads/noobs/ herunterladen, z.B. *NOOBS_v2_8_1.zip*.
1. SHA-256 kontrollieren
1. Zip Datei entpacken
1. Parameter ` silentinstall` an die Parameterliste in *recovery.cmdline* anhängen. Dieser Parameter wird für die initiale headless Installation und bei Updates benötigt. Ist bereits ein Betriebssystem installiert, wird NOOBS kein *silentinstall* durchführen. Damit kann der Parameter immer in der Datei bleiben.
1. Eine leere Datei *[ssh](files/ssh)* erstellen. Die Datei liegt auf der gleichen Ebene wie *recovery.cmdline*. Die Datei wird beim Partitionsetup in die boot Partition kopiert und sorgt beim Boot Vorgang dafür, dass der ssh Server gestartet wird und man sich somit remote anmelden kann.
1. In Verzeichnis *os/* alle Betriebssysteme ausser *Raspbian* löschen (z.B. LibreELEC_RPi, LibreELEC_RPi2).
1. Eine große Datei *.placeholder* in das Verzeichnis *os/* legen (Datei in [zip](files/placeholder1.5gb.zip)). Die Datei dient dazu, Platz in der ersten Partition zu reservieren. Dadurch können auch größere Updates installiert werden.


## Referenzen

* https://github.com/raspberrypi/noobs
