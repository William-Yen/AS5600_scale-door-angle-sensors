# AS5600_scale-door-angle-sensors
 Door angle sensor boards and I2C multiplexer board. Created for use in the 1/20th scale "IoT Sandbox" of the New Futures project squad at Industrial Design at TU/e.

 This repository contains the .step files, and KiCAD PCB design files, and Arduino code for replicating the project. Each multiplexer board allows interfacing with up to 24 sensors, and up to 2 multiplexer boards can be used on one I2C bus. 

 ### Note- Silkscreen Mistake
 The A0 and A2 headers corresponding to both U2 and U3 of the multiplexer boards are switched, meaning that the silkscreen markings are wrong. Keep this in mind when setting I2C addresses for U2 and U3.

 ## Electronics Hardware and Assembly
 Two types of custom basic 2-layer PCBs will need to be manufactured. Populating them requires generic breakout boards for the AS5600 magnetic encoder and TCA9548A I2C multiplexer. As donor boards, these are used for the passive components and ICs, as well as the included diametric magnet and headers included with the encoder. 
 
 M2 screws, header jumpers, JST-PH female and male connectors will need to be separately sourced, with the amount depending on how many sensors are used. The reset button on the multiplexer board is optional. The following is a list of hardware used for the final setup; total hardware cost was around 100 Euro for 24 sensors and 1 multiplexer board (populated), with several spare, unpopulated PCBs.

|     Hardware                | Quantity |  Link                                                                                                                                                       |  Notes  |
|:---------------------------:|:--------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------|
|  Sensor board PCBs          |  24      |                                   NA                                                                    |  custom fabricated PCB                                      |
|  Multiplexer board PCBs     |  1       |                                   NA                                                                    |  custom fabricated PCB                                      |
|  AS5600 donor boards        |  24      |  [Aliexpress](https://www.aliexpress.com/item/1005006246654932.html)                                    |  white breakout PCBs, with headers and diametric magnet     |
|  TCA9548A donor boards      |  3       |  [Aliexpress](https://www.aliexpress.com/item/1005006263235377.html)                                    |  purple breakout PCBs, with headers                         |
|  JST-PH male, 5-pin         |  48      |  [LCSC](https://www.lcsc.com/product-detail/Wire-To-Board-Wire-To-Wire-Connector_JST-B5B-PH-K-S-LF-SN_C157993.html)                                         |         |
|  JST-PH female, 5-pin       |  48      |  [LCSC](https://www.lcsc.com/product-detail/Rectangular-Connectors-Housings_JST-PHR-5_C157953.html)                                                         |         |
|  JST-PH female, 4-pin       |  1       |  [LCSC](https://www.lcsc.com/product-detail/Wire-To-Board-Wire-To-Wire-Connector_span-style-background-color-ff0-JST-span-B4B-PH-K-S-LF-SN_C131334.html)    |         |
|  JST-PH female terminal     |  48      |  [LCSC](https://www.lcsc.com/product-detail/Line-Pressing-Terminals_JST-SPA-001T-P0-5_C264002.html)                                                         |         |
|  2.54mm header jumpers      |  26      |  [LCSC](https://www.lcsc.com/product-detail/Shunts-Jumpers_HanElectricity-HY-2540-A0NIB_C18185737.html) | 1 for each sensor and 2 for setting multiplexer addresses   |
|  6.00mm x 3.60mm SMD switch |  1       |  [LCSC](https://www.lcsc.com/product-detail/Tactile-Switches_HYP-Hongyuan-Precision-1TS002C-2400-4300-CT_C319341.html)                                      |         |
|  Assorted wires             |  N/A     |                                   NA                                                                    |  wires to crimp and connect sensors to multiplexer board    |
|  M2x5mm Philips-head screws |  48      |                                   NA                                                                    |  screws to attach sensor boards to the door frame mount     |
|  M2x10mm hex screws         |  24      |                                   NA                                                                    |  screw to attach the door and hinge to the door frame       |
### Assembling the Angle Sensor Boards
Soldering the JST-PH connector to the board first is recommended. Either a horizontal connector can be used (with pins trimmed post-soldering), or vertical connectors with the pins bent 90 degrees. A hotplate or hot air gun from below the PCB is recommmended due to the low melting temperatures of the plastic connector housing.

All SMD components from the generic AS5600 breakout boards can be transferred via hot air or hand soldering; component numbering is the same on the donor boards and custom PCB. Footprints were chosen for 0402 size resistors and capacitors, but 0603 (as was noticed on some purchased boards) will also fit; ensure R2, R3, and R4 are not bridged if passives are 0603. The headers can also be soldered after.

A jumper is required to select either clockwise or counter-clockwise as the positive direction for the rotational values. The programming pin for burning rotation range is also broken out via a header, but it is not used nor necessary for this project.

### Assembling the I2C Multiplexer Board
All resistors used in the TCA9548A breakout boards are the same; therefore only capacitor positions have been marked on the silkscreen. It is recommended to solder the SMD components before the through-hole connectors and headers. Jumpers 

## 3D Printing and Mounting
_____.step, _____.step, and _____.step are the doorframe, door, and door hinge files respectively. One M2x__mm hex screw is used for assembly. This is the original main door structure in the IoT Sandbox, designed by Joep Frens. _____.step is the adapter from M2x10mm hex screw to the magnet, and _____.step is the sensor mount which press fits into frame. Two M2x5mm philips screws secure the sensor board to the mount.

3 M4 screws can be used to secure the multiplexer board if desired.

## Software
_____.ino is the program that runs on an ESP32 Dev Module and interfaces via I2C to the multiplexer board. The code requires the following libraries:

https://github.com/RobTillaart/TCA9548

https://github.com/RobTillaart/AS5600

The ESP32 uses the default I2C pins to connect to the multiplexer board, with SDA on GPIO21 and SCL on GPIO22. The addresses of the multiplexer ICs are set via the jumpers to U1: 0x70; U2: 0x71, and U3, 0x72.







 
