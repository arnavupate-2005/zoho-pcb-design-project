<img width="940" height="663" alt="image" src="https://github.com/user-attachments/assets/9e88224a-6caa-4867-97c5-bdacc840a7a2" />
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/c79c76cd-1767-4adc-824d-a992f8878434" />
# ESP32 6-Channel PWM Fan Controller

An industrial-grade, IoT-enabled 6-channel PWM fan controller built around the ESP32-WROOM-32E and MAX31790 fan driver IC. Designed as a 4-layer PCB in KiCad, this board provides precise acoustic and thermal management for 12V PC or industrial fans, featuring high-side power gating, closed-loop RPM monitoring, and daisy-chainable I2C temperature sensing.

## System Architecture

* **Microcontroller:** ESP32-WROOM-32E handling Wi-Fi/Bluetooth telemetry, I2C communication, and core logic. Includes a CP2102N USB-to-UART bridge with a dual-NPN auto-program circuit for seamless flashing via USB-C without manual boot-button toggling.
* **Fan Control (MAX31790):** Offloads high-frequency PWM generation and tachometer pulse counting from the ESP32. Controls up to 6 independent 4-pin fans with closed-loop RPM feedback via 10kΩ open-drain pull-ups on the 3.3V logic rail.
* **Power Delivery:**
* **Input:** 12V DC barrel jack protected by a polyfuse and reverse-polarity diode.
* **Load Switching:** NCP45560 high-current load switch tied to GPIO 23, acting as a master power gate for the 12V fan headers, enabling zero-RPM emergency shutdown and low-power standby modes.
* **Voltage Regulation:** Dual-stage conversion utilizing a TPS5430 switching buck converter (12V to 5V) to minimize heat dissipation, followed by a TLV1117-33 LDO linear regulator (5V to 3.3V) for a clean, low-noise supply to the sensitive microcontroller logic.


* **Expansion:** Two dedicated I2C headers (J9, J10) support external environmental temperature sensors to enable dynamic, automated thermal curves.

## Hardware Specifications

| Feature | Specification |
| --- | --- |
| **MCU** | ESP32-WROOM-32E |
| **Fan Driver** | MAX31790 (I2C interface) |
| **Channels** | 6x Standard 4-Pin PWM (12V, GND, Tach, PWM) |
| **Input Voltage** | 12V DC |
| **Logic Voltage** | 3.3V DC |
| **PCB Construction** | 4-Layer |
| **EDA Software** | KiCad |

## Repository Structure

* `/Hardware`: KiCad project files, schematics, PCB layout files, and production-ready Gerbers.
* `/Firmware`: C/C++ source code for the ESP32, including the MAX31790 I2C driver integration and wireless telemetry logic.
* `/Docs`: Reference datasheets for the core ICs (TPS5430, NCP45560, MAX31790, ESP32).

## Getting Started

1. **Fabrication:** Use the provided Gerber files in the `/Hardware` directory to manufacture the 4-layer PCB.
2. **Assembly:** Solder the SMD components, ensuring solid connections on the ground thermal pads for the TPS5430 and ESP32 to maintain proper heat dissipation under load.
3. **Firmware Flashing:** Connect the board to your development environment via USB-C. The integrated CP2102N will handle the DTR/RTS boot logic automatically. Compile and flash your C++ firmware using VS Code (PlatformIO) or the Arduino IDE.

## Author

**Arnav Upate**
