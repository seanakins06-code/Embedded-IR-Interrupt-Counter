# PIC16F690 IR Event Counter

A digital counter designed to detect and count the amount of physical objects that break an Infra Red (IR) beam. This project demonstrates low-level embedded C programming, interrupt handling, and 7-segment display multiplexing.

---

##  Overview
When fully built, this project functions as a **automatic counting station**. An Infrared (IR) LED and photodiode connected in reverse bias pair create an invisible beam; every time an object passes through and breaks this beam, the system increments a count from **00 to 99**.

### Key Functionality:
* **Interrupt-Driven Logic:** Uses the `RA2/INT` external interrupt pin to detect signal changes instantly without using a CPU.
* **Low-Power Optimization:** Specifically tuned to run consistently on a **5V supply**, overcoming standard logic threshold challenges.
* **Dual-Digit Display:** Real-time rendering of counts across two 7-segment displays using efficient port mapping and modulo math.
* **Signal Stability:** Features integrated **software debouncing** within the ISR to prevent "ghost counts" from noisy sensor signals.

---

##  Technical Specifications
| Feature | Details |
| :--- | :--- |
| **Microcontroller** | Microchip PIC16F690 |
| **Compiler** | XC8 (MPLAB X IDE) |
| **Sensors** | IR LED & Photodiode Pair |
| **Output** | Dual 7-Segment Displays (Common Cathode) |
| **Input Voltage** | 5.0V |

---

##  How it Works
1. **The Trigger:** The photodiode signal is monitored via the `OPTION_REGbits.INTEDG` bit.
2. **The ISR:** When the beam is broken, the `isr()` function pauses the main loop, increments the `eventCount`, and applies a 50ms safety delay.
3. **The Math:** The system splits the count (e.g., 25) into **Tens** (2) and **Units** (5) using:
   - `units = number % 10;`
   - `tens = number / 10;`
4. **The Update:** The `while(1)` loop constantly refreshes the ports to ensure the display stays bright and accurate.

---

## Physical Circuit 
*(Optional: Drag and drop a photo of your breadboard here to impress recruiters!)*
