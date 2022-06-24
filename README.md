# Description
A problem with the TP4056 breakout circuit is that the load must be disconnected when the battery is being charged. This is because the charging circuitry detects when the charge current falls below C/10 (constant current charge mode near the end of the charge cycle).
C is the battery capacity in mAh. When a load is connected to the battery, this changes the detected current, allowing the TP4056 to stop charging may never end!

A "bypass" consisting of an additional current path with a diode and a p-channel mosfet can help here. It is a controlled switch that disconnects the battery when an external power supply (e.g. solar cell) is connected.
![TCP4056 circuit diagram](https://github.com/DoImant/Stuff/blob/main/TP4056-Bypass/circuit_diagram.png?raw=true)

The idea is that the P-channel FET will disconnect the battery from the load when a power source is connected to the charging chip. The TP4056 still charges the battery, but with no load. The load is directly from the power source powered. With a solar cell, the battery is disconnected when sufficient solar energy is available. If it generates more electricity than the load needs, the battery is also charged.

When the power source is removed, the P-channel FET conducts, connecting the load to the battery.

With this configuration, the TP4056 can safely charge the battery when the load is connected because the battery is charged during application external power supply is disconnected from the load.

The circuit presented here implements the load distribution. The board can be glued to the back of the TP4056-breakout and be connected to the existing soldering pads.
![TCP4056 R3](https://github.com/DoImant/Stuff/blob/main/TP4056-Bypass/TP4056-pcb-glued.jpg?raw=true)

## Connection example
![TCP4056 Connection](https://github.com/DoImant/Stuff/blob/main/TP4056-Bypass/TC4056-power-path.png?raw=true)

A detailed explanation can be found here:  [detailed explanation](https://www.best-microcontroller-projects.com/tp4056.html)

Have PCBs made: [Aisler](https://aisler.net/p/JAYYOSGH)

## Operation with solar cell
If the TP4056 breakout is operated with a solar cell, the maximum possible charging current must probably be reduced because, for example, 5V solar cells usually cannot deliver 1A charging current. A 2.5W solar cell with 5V generates a maximum charging current of 500mA. The adjustment is made on the TP4056 breakouts by swapping the resistor R3 (1.2kΩ).

<div align="center">
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
</div>

A value between 2kΩ and 3kΩ would be appropriate for a solar cell such as that listed above.
![TCP4056 R3](https://github.com/DoImant/Stuff/blob/main/TP4056-Bypass/tp4056-resistor.jpg?raw=true)
