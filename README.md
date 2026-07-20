**The project is divided into 8 major parts**  
lets understand each component's function one by one in a block to see what function they have in the circuit.   
1. Block 1 – USB Input & Protection  

| Ref | Component        | Role in the Circuit                                                                     |
| --- | ---------------- | --------------------------------------------------------------------------------------- |
| J1  | USB-C Receptacle | Receives 5 V power and USB data from the host PC.                                       |
| D1  | TVS Diode        | Protects the board from ESD and voltage spikes coming through the USB connector.        |
| F1  | Polyfuse         | Limits current during short circuits and protects the USB port from overcurrent damage. |
| R1  | 5.1 kΩ           | USB-C CC1 pull-down resistor to advertise the board as a power sink.                    |
| R2  | 5.1 kΩ           | USB-C CC2 pull-down resistor to advertise the board as a power sink.                    |


2. Block 2 – 3.3 V Power Supply

| Ref | Component       | Role in the Circuit                                                                 |
| --- | --------------- | ----------------------------------------------------------------------------------- |
| U1  | TPS62162        | Converts the USB 5 V input into a stable 3.3 V supply with high efficiency.         |
| L1  | 2.2 µH Inductor | Stores energy during switching and smooths the regulator output current.            |
| C1  | 10 µF           | Input bulk capacitor that stabilizes the 5 V input to the regulator.                |
| C2  | 100 nF          | High-frequency input bypass capacitor that filters switching noise.                 |
| C4  | 4.7 µF          | Main output capacitor that stabilizes the 3.3 V output voltage.                     |
| C9  | 100 µF          | Bulk output capacitor that supplies transient current to the ESP32 and peripherals. |
| R3  | 100 kΩ          | Feedback resistor used by the regulator to maintain the correct output voltage.     |


3. Block 3 – USB to UART Interface  

| Ref | Component | Role in the Circuit                                                                           |
| --- | --------- | --------------------------------------------------------------------------------------------- |
| U2  | CP2102N   | Converts USB communication into UART for programming and serial communication with the ESP32. |
| C3  | 100 nF    | Decouples the CP2102N supply to reduce high-frequency noise.                                  |
| C5  | 1 µF      | Stabilizes the USB VBUS supply for the CP2102N.                                               |
| C6  | 1 µF      | Stabilizes the internal regulator output of the CP2102N.                                      |

4. Block 4 – ESP32 Auto-Programming Circuit  

| Ref | Component   | Role in the Circuit                                                        |
| --- | ----------- | -------------------------------------------------------------------------- |
| Q1  | MMBT3904    | Uses the RTS signal to automatically reset the ESP32.                      |
| Q2  | MMBT3904    | Uses the DTR signal to place the ESP32 into bootloader mode automatically. |
| R11 | 10 kΩ       | Pull-up resistor for the ESP32 EN pin.                                     |
| R12 | 10 kΩ       | Pull-up resistor for the ESP32 GPIO0 (BOOT) pin.                           |
| SW1 | Push Button | Manual reset button for the ESP32.                                         |
| SW2 | Push Button | Manual bootloader button for programming mode.                             |

5. Block 5 – ESP32 Module  

| Ref | Component       | Role in the Circuit                                                                                          |
| --- | --------------- | ------------------------------------------------------------------------------------------------------------ |
| U3  | ESP32-WROOM-32E | Main microcontroller that reads sensors, stores data, communicates over USB, and controls the entire system. |
| C10 | 100 nF          | Local decoupling capacitor placed close to the ESP32 power pin.                                              |
| C11 | 100 nF          | Additional high-frequency decoupling capacitor for stable ESP32 operation.                                   |
| C16 | 10 µF           | Bulk capacitor that supports sudden current demands from the ESP32's Wi-Fi and Bluetooth radio.              |


6.  Block 6 – Environmental Sensors

(a) BME280  

| Ref | Component | Role in the Circuit                                       |
| --- | --------- | --------------------------------------------------------- |
| U4  | BME280    | Measures temperature, humidity, and atmospheric pressure. |
| C12 | 100 nF    | Filters supply noise to improve sensor accuracy.          |

(b)  BH1750  

| Ref | Component | Role in the Circuit                                       |
| --- | --------- | --------------------------------------------------------- |
| U4  | BME280    | Measures temperature, humidity, and atmospheric pressure. |
| C12 | 100 nF    | Filters supply noise to improve sensor accuracy.          |

(c) RTC  

| Ref | Component      | Role in the Circuit                                               |
| --- | -------------- | ----------------------------------------------------------------- |
| U6  | DS3231M        | Maintains accurate date and time, even when USB power is removed. |
| BT1 | CR2032 Battery | Keeps the RTC running during power loss.                          |
| C15 | 100 nF         | Decouples the RTC power supply.                                   |

7. Block 7 – microSD Storage  

| Ref | Component        | Role in the Circuit                                                           |
| --- | ---------------- | ----------------------------------------------------------------------------- |
| J3  | MicroSD Socket   | Stores logged environmental data on a removable SD card.                      |
| R9  | Pull-up resistor | Pulls the Card Detect line to a defined logic level when no card is inserted. |


8. Block 8 – User Interface

| Ref | Component   | Role in the Circuit                                                         |
| --- | ----------- | --------------------------------------------------------------------------- |
| J2  | OLED Header | Connects the external OLED display over the I²C bus.                        |
| D2  | Status LED  | Indicates board status such as power or firmware activity.                  |
| R10 | 1 kΩ        | Limits current through the status LED to protect it from excessive current. |






