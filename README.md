# 10Base-T1S-USB-ETH

This repository provides drivers, tools, and configuration scripts for the **10Base-T1S USB Ethernet** adapter, specifically optimized for Raspberry Pi 4 and Raspberry Pi 5. 10Base-T1S is an automotive Ethernet standard that supports multidrop networking over a single twisted pair.

---

## Features

*   **10Base-T1S Support**: Enables automotive Ethernet connectivity via USB.
*   **PLCA Configuration**: Includes tools to configure Physical Layer Collision Avoidance (PLCA) parameters.
*   **Raspberry Pi Optimized**: Dedicated scripts for Raspberry Pi 4 and Raspberry Pi 5.
*   **Automatic MAC Configuration**: Python scripts to read MAC addresses from on-board I2C EEPROM and apply them to the interface.

---

## Repository Contents

*   `microchip_t1s.ko`, `lan865x_t1s.ko`: Kernel modules for the 10Base-T1S controller.
*   `lan865x.dtbo`: Device tree overlay for hardware integration.
*   `ethtool`: Custom version of ethtool with PLCA support.
*   `eth1_up_pi4.py` / `eth1_up_pi5.py`: Initialization scripts for Raspberry Pi 4 and 5.
*   `lan865x-linux-driver-0v4.zip`: Source code for the Linux drivers.

---

## Installation & Usage

### 1. Prerequisites
Ensure you have the necessary dependencies installed on your Raspberry Pi:
```bash
sudo apt update
sudo apt install python3-gpiod python3-smbus i2c-tools
```

### 2. Setup for Raspberry Pi 5
To initialize the 10Base-T1S interface on a Raspberry Pi 5, run:
```bash
sudo python3 eth1_up_pi5.py
```
This script will:
1. Load the required kernel modules (`microchip_t1s.ko`, `lan865x_t1s.ko`).
2. Assign a default IP address (`192.168.5.100/24`).
3. Read the unique MAC address from the I2C EEPROM and apply it to `eth1`.
4. Enable PLCA with default parameters (Node ID: 0, Node Count: 8).

### 3. Setup for Raspberry Pi 4
For Raspberry Pi 4, use the corresponding script:
```bash
sudo python3 eth1_up_pi4.py
```

### 4. Manual PLCA Configuration
You can manually adjust PLCA settings using the provided `ethtool`:
```bash
sudo ./ethtool --set-plca-cfg eth1 enable on node-id [ID] node-cnt [COUNT]
```

---

## Hardware Information
The adapter uses the **Microchip LAN865x** series controller. It includes an I2C EEPROM at address `0x50` for MAC address storage and utilizes GPIOs for status LEDs (e.g., GPIO 19 on Raspberry Pi).

---

## Support
For technical support and hardware inquiries, please contact:
*   **Company**: [buelectech](https://github.com/buelectech)
*   **Email**: [buelectech@gmail.com](mailto:buelectech@gmail.com)
