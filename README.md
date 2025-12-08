# ESPHome SMSL Q5 Remote IR Control
A simple ESPHome-based IR blaster for controlling **SMSL amplifiers** from **Home Assistant**.  
Built around an ESP8266 and designed to be reliable, stateless, and easy to live with day-to-day.

Optional support for a **BME680 environmental sensor** is included for temperature, humidity, pressure and air quality monitoring. 

---

## What This Does

This project gives you:

- Full IR control of SMSL amplifiers:
  - Power
  - Volume Up / Down
  - Up / Down (alias of Volume)
  - Left / Right / OK
  - Input
  - EQ
  - Mute

- Native **ESPHome → Home Assistant** integration  
- Built-in **web interface** using ESPHome WebServer v3  
- Optional **BME680 environmental monitoring**
- Optimised for **ESP8266 with 1MB flash (OTA-safe)**

---

## Design Approach

This firmware is **intentionally stateless**.

It does **not** attempt to track:
- Volume level  
- EQ mode  
- Power state  

This avoids the common problems where things drift out of sync if the physical remote is used. Every button press always sends a real IR command. Nothing more, nothing less.

---

## Hardware

- ESP8266 (ESP-01 1MB or D1 Mini)
- IR LED with MOSFET or transistor driver
- BME680 (I²C) – optional
- 3.3 V power supply

### Recommended Hardware
These are the parts used for the reference build. Equivalent parts will also work.

| Component | Description | Buy (AliExpress) |
|----------|-------------|------------------|
| ESP8266 | ESP-01 (1MB) or D1 Mini | [AliExpress](https://s.click.aliexpress.com/e/_EGaSF1W) | [Amazon](https://amzn.to/48TDPFn) |
| IR LED | 940nm IR TX LED | [AliExpress](https://s.click.aliexpress.com/e/_EIXoR04) | [Amazon](https://amzn.to/4iGrnMq) |
| MOSFET / Transistor | Logic-level N-channel MOSFET or NPN transistor | [AliExpress](https://s.click.aliexpress.com/e/_EzvcGd6) | [Amazon](https://amzn.to/49320Aj) |
| Resistors | 100Ω (IR), 100kΩ (gate pulldown) | [AliExpress](https://s.click.aliexpress.com/e/_EJDxXIu) | [Amazon](https://amzn.to/48GBhJt) |
| BME680 (optional) | Temp, humidity, pressure & air quality | [AliExpress](https://s.click.aliexpress.com/e/_EQP2ObA) | [Amazon](https://amzn.to/3XDhqWD) |

Some of the links above may be affiliate links.  
This does **not** increase the price for you, but helps support any future development / projects.

## Repository Structure

| File | Description |
|------|------------|
| `ir-blaster.yaml` | Main ESPHome firmware |
| `ir-blaster-bme.yaml` | Main ESPHome firmware & BME680 |
| `lovelace-remote.yaml` | Home Assistant dashboard control card |
| `images/` | Photos of built device *future addition* |

---

## Installation

1. Flash either `ir-blaster.yaml` or `ir-blaster-bme.yaml` using ESPHome.
2. Add the device to Home Assistant.
3. Import `lovelace-remote.yaml` into your dashboard.
4. Aim the IR LED at your SMSL amplifier.
5. That’s it.

---

## SMSL IR Codes (NEC Extended)

**Address (Mode A): `0x3412`**

| Function      | Command  |
|---------------|----------|
| Power         | `0xF801` |
| Volume Up     | `0xF802` |
| Volume Down   | `0xF806` |
| Left          | `0xF803` |
| Right         | `0xF805` |
| OK / Centre   | `0xF804` |
| Input         | `0xF807` |
| EQ            | `0xF808` |
| Mute          | `0xF809` |
| Up            | Same as Volume Up |
| Down          | Same as Volume Down |

Tested against common models such as:
- SMSL AD18  
- SMSL AO200  
- SMSL DO100  

---

## Home Assistant Dashboard

A ready-to-use remote control layout is included in: lovelace-remote.yaml

It provides:
- Power, Mute and Input
- Directional controls
- EQ access
- Dedicated Volume + / −

---

## Licence

MIT License.  
You’re free to use, modify and redistribute this project, including for commercial use.

---
https://www.oliverbagley.com
