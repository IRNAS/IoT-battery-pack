# IoT battery pack requirements
IoT battery pack is designed to provide power in various sensing applications, being able to deliver sufficient power for a wide range of sensors for short periods of time and have a long standby operation time between them. BLE interface allows users to configure it as well as provide a communication channel to talk to other sensors in the vicinity.

 * Capacity: 1P-6P Li-Po 18650 (3600mAh - 20000mAh)
  * Batteries connected in 3 branches of two, each branch fuse protected
  * User can connect 1-6 cells in parallel. For safety, no more then two can be directly connected in parallel, thus the 6 cells in parallel are split in 3 pairs of 2 cells in parallel, the sets connected together each via its own fuse.
  * Connector for cells: 2.54 JST (not mounted)
 * Input: 2A at 5V, input range 3-6V
  * DC jack input for solar cell, no diode used
  * Micro USB input for wall-socket (Additionally 2 pads for connections)
  * USB input must disconnect the solar cell and prevent discharge into it, can be done with a relay. Relay powered from USB socket via diode in a way, that NC is solar cell and NO is external 5 V input.
  * Current shall be adjustable from MCU (PWM?) and via trimmer in a way, that voltage is defined, where current is lowered (i.e. at 4V5 system goes to CV mode on input). Dynamic adjustment of charge current, such that the input voltage does not drop below 4.5V or other configurable level if possible. This prevents overloading of the supply, for example when solar cell is connected holds it reasonably close to maximum power output voltage. If possible the voltage level should be software controlled via BLE.

 * Output: 2A at 5V, 1A at 3.3V, direct battery voltage output
  * 5V - High-side switch or DC-DC module disable + fuse
  * 3.3V - High-side switch or DC-DC module disable + fuse
  * battery voltage - High-side switch and a fuse
  * Out connectors 2.54mm header/JST terminal
 * BLE processor (preferred Nordic nRF51822) on board implementing the following features in software:
  * battery voltage and current measurement. All voltages (inputs, outputs), current is measured through Fuel gauge chip via I2C
  * configurable thermal protection/shutdown via fuel gauge I2C
  * configurable battery charge voltage (over-voltage protection) via fuel gauge I2C
  * configurable battery discharge voltage (under-voltage protection) via fuel gauge I2C
  * I2C interface (nRF51822 SDA 10, SCL 8)
  * Enable/disable outputs as defined above
  * Expose remaining GPIO, about 8-10 are sufficient (to 10 pin header vcc/+3v3+8gpios)
  * RG(B) LED from MCU, software controlled and can be disabled fully
  * Standard Cortex programming connector
  * [Grove I2C connector](http://wiki.seeed.cc/Grove-I2C_Hub/)
 * Simultaneous charging and discharging
 * Low quiescent current - standby mode with 3.3V branch active no more then 100uA battery discharge current
 * Input DC-DC with current limiter
  * Dynamic adjustment of charge current, such that the input voltage does not drop below 4.5V or other configurable level if possible. This prevents overloading of the supply, for example when solar cell is connected holds it reasonably close to maximum power output voltage. If possible the voltage level should be software controlled via BLE.


 * Target production cost ~15EUR@1k
  * Batteries excluded
 * Prototyping process: 10 units for testing in first batch, 30 units in second batch

## Diagram
Diagram is made in http://draw.io

![diagram](IoT-battery-pack.png)
