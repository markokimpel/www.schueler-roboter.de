[Hardware](..)

# Version 0

Version 0 ist unser erster Wurf. Er basiert auf dem [RasPiRobot Rover Kit](https://www.monkmakes.com/pi-rover/) von [Monk Makes](https://www.monkmakes.com/). Dieses Kit hatte eine gute sehr gute [Kritik](https://www.raspberrypi.org/magpi/raspirobot-rover-kit-review/) vom MagPi Magazine bekommen.

## Komponenten

Wir wählten folgende Komponenten:

Komponente | Bezug / Preis
-----------|------------
[Raspberry Pi 3 Model B](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/) | [Amazon](https://www.amazon.de/gp/product/B01CD5VC92/) (ca. 35 €)
[Raspberry Pi Netzteil](https://www.raspberrypi.org/products/raspberry-pi-universal-power-supply/) | [Amazon](https://www.amazon.de/Raspberry-Offizielles-Pi-Netzteil-schwarz/dp/B01DP8O5A4/) (ca. 13 €)
32 GB microSD Karte mit Adapter | [Amazon](https://www.amazon.de/gp/product/B073JWXGNT/) (ca. 17 €)
[RasPiRobot Rover Kit](https://www.monkmakes.com/pi-rover/) | [Amazon](https://www.amazon.de/gp/product/B018Y8IMUE/) (ca. 51 €)
6 AA Ni-MH Akkus mit hoher Kapazität | [Amazon](https://www.amazon.de/gp/product/B00JVV8HRW/) (2x ca. 12 €)
Ladegerät für AA Ni-MH Akkus | bereits vorhanden
**Gesamt** | **ca. 140 €**

PS: Die Auswahl der Komponenten basiert auf persönlichen Erfahrungen und Präferenzen. Die Produkte können von einem beliebigen Händler bezogen werden - Bezugsquellen und Preise werden nur beispielhaft angegeben. Sollten wir von einem Hersteller oder Händler Vergünstigungen - jeglicher Art - für die Auswahl oder das Verlinken erhalten haben, wird das explizit erwähnt.

## Kritik

### Gut

* Alles funktioniert!
* Das RasPiRobot Rover Kit ist recht umfangreich. Alle benötigten Teile - inkl. Schraubendreher in verschiedenen Größen - liegen bei. Der Zusammenbau per Anleitung ist gut möglich, wenn auch manchmal ein bisschen friemelig. Hilfe von Erwachsenen ist zwingend erforderlich.
* Das Driver Board [RasPiRobot Board V3](https://www.monkmakes.com/rrb3/) liegt dem RasPiRobot Rover Kit bei.
  * Die Stromversorgung des Raspberries erfolgt bei Batteriebetrieb über das Driver Board. Die gleiche Stromquelle (6x AA Batterien oder Akkus) kann für Raspberry (5V) und die Motoren (6V) genutzt werden.
  * Das Driver Board hat zusätzlich Anschlüsse für einen Ultraschall-Sensor (liegt bei), zwei Schalter (einer liegt bei) und zwei Open Collector Ausgänge. Zwei LEDs sind verbaut und können über GPIO PINs angesprochen werden.
  * Das Glimmen der verbauten LEDs zeigt an, dass Raspi und Driver Board mit Batterie-Strom versorgt werden. (Da die rote LED des Raspis nur bei USB Strom leuchtet wüsste man sonst nicht, ob der Raspi mit Strom versorgt wird.)
  * Beispielcode zum Ansteuern des verwendeten Driver Boards [RasPiRobot Board V3](https://www.monkmakes.com/rrb3/) mit Python liegt vor. Integration mit Scratch2 mit selbstgeschriebenem Code war möglich.
* Laufzeit mit Batterie/Akku ausreichend (mehrere Stunden).

### Verbessern

Bitte diese Kritikpunkte nicht als direkte Kritik am RasPiRobot Rover Kit misverstehen. Das Kit ist für verschiedene Nutzergruppen gedacht und die haben unterschiedliche Anforderungen. Hier geht es um Verbesserungen für den Schüler-Roboter.

* Ist der Raspi mit dem Chassis verschraubt, kommt man an viele Raspi Anschlüsse nur noch schwer ran: USB Stromversorgung - nur mit großer Vorsicht und kurzem Stecker, HDMI - nicht möglich, microSD Karte - schwierig und nur mit Hilfsmittel.
* Das Board hat keinen Netzschalter. Der Raspi wird durch das Entfernen einer Batterie stromlos geschaltet. Funktioniert, ist aber nicht elegant. (Wohin legt man die verbleibende Batterie?)
* Häufig kam es zu Wackelkontakten im Batteriehalter. Die Suche nach der Ursache war dann schwierig


* Akku
board wackelig
