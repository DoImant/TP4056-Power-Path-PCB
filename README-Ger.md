# Beschreibung
Ein Problem der TP4056-Breakoutschaltung besteht darin, dass die Last getrennt werden muss, wenn der Akku geladen wird. Der Grund dafür ist, dass die Ladeschaltung erkennt, wenn der Ladestrom unter C/10 fällt (Konstantstrom-Lademodus gegen Ende des Ladezyklus). 
C ist die Akkukapazität in mAh. Wenn eine Last an dem Akku angeschlossen ist, ändert dies den erkannten Strom, sodass das TP4056 den Ladevorgang möglicherweise niemals beendet!

Ein "Beipass" aus einem zusätzlichen Strompfad mit einer Diode und einem P-Kanal-Mosfet kann hier Abhilfe schaffen. Es handelt sich um einen gesteuerterten Schalter, der den Akku trennt, wenn eine externe Stromversorgung (z.B. Solarzelle) angeschlossen wird.
![TCP4056 circuit diagram](https://github.com/DoImant/Stuff/blob/main/TP4056-Bypass/circuit_diagram.png?raw=true)

Die Idee ist, dass der P-Kanal-Fet die Batterie vom Verbraucher trennt wenn eine Stromquelle an den Ladechip angeschlossen ist. Der TP4056 lädt den Akku immer noch, aber ohne Last. Der Verbraucher wird direkt von der Stromquelle mit Strom versorgt. Bei einer Solarzelle erfolgt die Trennung vom Akku, wenn genügens Solarenergie verfügbar ist. Erzeugt sie mehr Strom als er Verbraucher benötigt, wird der Akku ebenfalls geladen.

Wenn die Stromquelle getrennt wird, wird der P-Kanal-FET leitend und verbindet die Last mit der Batterie.

Mit dieser Konfiguration kann das TP4056 die Batterie bei angeschlossener Last sicher laden, da der Akku während des Anlegens einer externer Stromversorgung von der Last getrennt ist.

Die hier vorgestellte Schaltung setzt die Lastverteilung um. Die Platine kann auf die Rückseite des TP4056 Breakouts geklebt werden und mit den vorhandnen Lötpads verbunden werden. 
![TCP4056 R3](https://github.com/DoImant/Stuff/blob/main/TP4056-Bypass/TP4056-pcb-glued.jpg?raw=true)

## Anschlussbeispiel
![TCP4056 Connection](https://github.com/DoImant/Stuff/blob/main/TP4056-Bypass/TC4056-power-path.png?raw=true)

Eine ausführliche Erklärung ist hier zu finden: [detailierte Beschreibung](https://www.best-microcontroller-projects.com/tp4056.html)

Platine fertigen lassen: [Aisler](https://aisler.net/p/JAYYOSGH)

## Betrieb mit einer Solarzelle
Wird das TP4056-Breakout mit einer Solarzelle betrieben, so muss der max. mögl. Ladestrom reduziert werden, weil 5V Solarzellen üblicherweise nicht 1A Ladestrom liefern können. Bei einer 2,5W Solarzelle mit 5V werden maximal 500mA Ladestrom erzeugt. Die Anpassung erfolgt auf den TP4056-Breakouts, indem der Widerstand R3 (1,2kΩ) ausgetauscht wird.
 
|  R3 (kΩ)   | I-Bat (mA) |
| ----------:|-----------:|
|    10      |        130 |
|     5      |        250 |
|     4      |        300 |
|     3      |        400 |
|     2      |        580 |
|     1.66   |        690 |
|     1.50   |        780 |
|     1.33   |        900 |
|     1.20   |       1000 | 
 
Zu einer Solarzelle wie oben beispielsweise aufgeführt wurde, passt ein Wert zwischen 2kΩ und 3kΩ.
![TCP4056 R3](https://github.com/DoImant/Stuff/blob/main/TP4056-Bypass/tp4056-resistor.jpg?raw=true)