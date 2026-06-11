# GPU Temperature Monitor to LCD Display

This project reads the real-time temperature and name of your NVIDIA GPU using Python and transmits that data via serial communication to an Arduino Uno. The Arduino then processes the incoming string and displays the GPU details on a 16x2 character LCD screen.

---

## Features
* **Real-time Monitoring:** Fetches GPU diagnostics every 2 seconds.
* **Hardware Display:** Offloads system stats to an external 16x2 LCD display, freeing up monitor workspace.
* **String Parsing:** Automatically sanitizes the GPU name (e.g., removing "NVIDIA GeForce" prefixes and structural dashes) to fit the display limits elegantly.

---

## Hardware Requirements
* **Arduino Uno** (or compatible microcontroller)
* **16x2 LCD Display** (HD44780 compatible)
* **10k Ohm Potentiometer** (for display contrast adjustment)
* **220 Ohm Resistor** (for the LCD backlight LED protection)
* **Breadboard & Jumper Wires**
* **USB Cable** (to connect Arduino to PC)

---

## Circuit Schematic & Wiring

### Wiring Diagram
![Arduino LCD Wiring Diagram](<schematics/DisplayConfig.png>)

### Pin Mapping Table
Connect your LCD to the Arduino using the standard 4-bit initialization configuration shown below:

| LCD Pin | Label | Connection / Arduino Pin |
| :--- | :--- | :--- |
| 1 | **GND** | Ground Rail (GND) |
| 2 | **VCC** | 5V Power Rail (5V) |
| 3 | **VO** | Potentiometer Center Wiper Pin (Contrast Control) |
| 4 | **RS** | **Arduino Pin 12** |
| 5 | **R/W** | Ground Rail (GND) |
| 6 | **E** | **Arduino Pin 11** |
| 11 | **D4** | **Arduino Pin 5** |
| 12 | **D5** | **Arduino Pin 4** |
| 13 | **D6** | **Arduino Pin 3** |
| 14 | **D7** | **Arduino Pin 2** |
| 15 | **LED+ (A)** | Connected via **220Ω Resistor** to 5V Rail |
| 16 | **LED- (K)** | Ground Rail (GND) |

---

