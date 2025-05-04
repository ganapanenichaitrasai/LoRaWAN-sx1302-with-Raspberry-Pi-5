# LoRaWAN-sx1302-with-Raspberry-Pi-5

This repository provides a complete guide to interfacing the **SX1302 LoRaWAN concentrator** with the **Raspberry Pi 5**. It includes hardware setup, software configuration, and a working example to establish communication between LoRa nodes and a ChirpStack Network Server or The Things Network (TTN).

---

## 🚀 Features

- Raspberry Pi 5 as LoRa Gateway Host
- Semtech SX1302 Gateway Concentrator Setup
- Packet Forwarder Configuration
- Integration with ChirpStack and The Things Network (TTN)
- Example Code for Gateway Setup

---

## 📦 Hardware Requirements

- Raspberry Pi 5
- SX1302 Gateway (Waveshare, RAK2287, Seeed Studio, etc.)
- LoRa Node (e.g., Wio-E5, STM32WLE5JC)
- Power Supply (for Pi and concentrator)
- Antenna and SD Card

---

## ⚙️ Software Stack

- Raspberry Pi OS (64-bit recommended)
- Semtech Packet Forwarder (`sx1302_hal`)
- ChirpStack Gateway Bridge / TTN Gateway Registration
- Git, SPI Tools, `systemd` for autostart

---

## 📁 Folder Structure

- `code/` – Code examples for configuration and communication
- `images/` – Diagrams and visual aids

---

## 🧠 How It Works

The Raspberry Pi communicates with the SX1302 concentrator over the SPI interface. Once the packet forwarder is configured, the gateway will capture packets from LoRa nodes and forward them to a network server like ChirpStack or TTN.

### Enable SPI on the Raspberry Pi:

from the command in raspberry pi sudo raspi-config

---

## 📸 Hardware Setup

Make sure your SX1302 HAT is properly connected to the Raspberry Pi GPIO header.

### 🛠️ Installation Instructions (sx1302_hal)

#### 1. Update and Install Git

sudo apt update
sudo apt install git

#### 2. Clone and Build the Semtech HAL

cd ~/Documents/
git clone https://github.com/Lora-net/sx1302_hal.git
cd sx1302_hal
make clean all
make all

#### 3. Reset and Get Gateway EUI

cp tools/reset_lgw.sh util_chip_id/
cd util_chip_id/
./reset_lgw.sh
./chip_id

#### 4. Prepare Packet Forwarder

cd ~/Documents/sx1302_hal/
cp tools/reset_lgw.sh packet_forwarder/
cd packet_forwarder/

#### 5. Create/Edit Configuration

Create a test_conf.json file (you can download this from the TTN console after registering your gateway with the EUI). It typically includes:

• Gateway EUI
• Server address (eu1.cloud.thethings.network, etc.)
• Radio settings

Place the test_conf.json inside the packet_forwarder/ directory.

#### 6. Start the Packet Forwarder

./lora_pkt_fwd -c test_conf.json

This command will:

• Initialize the SX1302 concentrator
• Start listening to uplinks from nodes
• Forward them to TTN or your own network server

---

### 👨‍💻 Example Code

See the `code/` folder for:

• Packet forwarder examples
• SPI configuration test code
• Sample scripts to test connectivity


## 📄 License

This project is licensed under the MIT License.
