# NoEvilMaid

ESP32 IoT security system that protects server cabinets against physical tampering ("Evil Maid" attacks) and overheating. Built for **CET321 - Internet of Things**.

## Overview

Network firewalls protect servers from remote attacks, but physical access to a server rack allows an attacker to plug in malicious USB devices, tamper with network cables, or disable cooling. **NoEvilMaid** monitors a server cabinet using 4 sensors and triggers local alarms while hosting a live Wi-Fi web dashboard for monitoring and remote control.

## Hardware Components

- **Controller:** ESP32 DevKit V1 (30-Pin)
- **Sensors (4):**
  1. `PIR (HC-SR501)` – Detects motion inside the server room
  2. `SW-420 Vibration Sensor` – Detects physical tampering on the cabinet door
  3. `DHT11` – Monitors server cabinet temperature & humidity
  4. `MQ-2` – Detects smoke or electrical fire inside the rack
- **Outputs / Actuators (3):**
  1. `Active Buzzer` – Local alarm siren
  2. `5V Relay Module` – Controls emergency cooling fan / cabinet lock
  3. `Red LED` – Visual alert indicator

## Pinout (ESP32)

| Component | Module Pin | ESP32 Pin | Power |
| :--- | :--- | :--- | :--- |
| **DHT11** | `DATA` | `GPIO 4` | `3V3` & `GND` |
| **PIR Motion (HC-SR501)** | `OUT` | `GPIO 13` | `VIN (5V)` & `GND` |
| **Vibration (SW-420)** | `DO` | `GPIO 18` | `3V3` & `GND` |
| **Smoke/Gas (MQ-2)** | `AO` | `GPIO 34` | `VIN (5V)` & `GND` |
| **Active Buzzer** | `I/O` / `+` | `GPIO 25` | `GND` |
| **5V Relay Module** | `IN` | `GPIO 26` | `VIN (5V)` & `GND` |
| **Warning LED** | `Anode (+)` | `GPIO 2` | `GND` (220Ω) |

## Project Structure

```text
NoEvilMaid/
├── README.md
├── diagram.json             # Wokwi circuit simulation
├── docs/
│   └── project_report.md    # Block diagram, test results & documentation
└── NoEvilMaid/              # Arduino IDE sketch folder
    ├── NoEvilMaid.ino       # Main ESP32 sketch (sensors, actuators, HTTP routes)
    ├── config.h             # Pin definitions, Wi-Fi credentials & thresholds
    └── dashboard.h          # Embedded HTML/JS web interface
```

## Setup & Upload

1. Install **ESP32** board support in Arduino IDE.
2. Install **DHT sensor library** by Adafruit from the Arduino Library Manager.
3. Open `NoEvilMaid/NoEvilMaid.ino` in Arduino IDE (it will automatically open `config.h` and `dashboard.h` in tabs).
4. Update your hotspot credentials in `config.h` (if the hotspot is not found, the ESP32 automatically starts an access point named `NoEvilMaid-AP` with password `cyber2026`).
5. Upload to the ESP32 and open `http://192.168.4.1` (or the IP printed in the Serial Monitor).

## References

- [Superjulien/Sensor_ESP32](https://github.com/Superjulien/Sensor_ESP32)
- [anjulameegalla/SmartHome](https://github.com/anjulameegalla/SmartHome)
- [bugsNburgers/IOT-Fire-Alarm-System](https://github.com/bugsNburgers/IOT-Fire-Alarm-System)
