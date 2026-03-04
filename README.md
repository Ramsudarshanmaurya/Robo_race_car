# 🤖 WiFi Controlled Robot Car
### NodeMCU ESP8266 + L298N + 4x 12V DC Gear Motor



## 🏆 Achievement

<div align="center">

> ### 🥇 1st Prize — RoboRace Competition
> **Buddha Institute of Technology, Gorakhpur**
> 
> 🎖️ Certificate of Excellence &nbsp;|&nbsp; 💰 Cash Prize ₹1000
> 
> *"Best WiFi Controlled Robot Car — IoT & Embedded Systems Category"*

</div>

---

## 📌 Project Overview

A **WiFi-controlled 4-wheel robot car** built using NodeMCU ESP8266 that hosts its own web server. Control the car from **any mobile or PC browser** connected to the same WiFi network — no app installation needed!

- 🎮 Control via beautiful mobile-responsive web interface  
- ⚡ Real-time PWM speed control (0–100%)  
- 📡 WiFi communication over HTTP REST API  
- ⌨️ Keyboard support (WASD / Arrow Keys) on PC  
- 🔄 Auto-stop when button is released  

---

## 📁 Project Structure

```
Robo Race Car/
├── 📂 Car_Dashboard/          # Web dashboard UI files
├── 📂 circuit_and_block_diagram/   # Circuit & block diagrams (PNG)
│   ├── NodeMCU_L298N_Circuit.png
│   ├── block_diagram_1_system.png
│   ├── block_diagram_2_wifi.png
│   └── block_diagram_3_complete.png
├── 📂 robot_car_wifi/         # Main Arduino source code
│   └── robot_car_wifi.ino
├── 📂 WiFi_Robot_Car_Report/  # Project report (DOCX)
│   └── WiFi_Robot_Car_Report.docx
└── 📄 README.md               # This file
```

---

## 🛠️ Hardware Required

| Component | Specification | Qty |
|-----------|--------------|-----|
| NodeMCU ESP8266 | 80MHz, 3.3V, WiFi 2.4GHz | 1 |
| L298N Motor Driver | 12V, 2A/channel, Dual H-Bridge | 1 |
| DC Gear Motor | 12V, 200RPM, High Torque | 4 |
| 12V Li-ion Battery | 3S, 2200mAh | 1 |
| Buck Converter | LM2596, 12V → 5V | 1 |
| 4WD Robot Chassis | Acrylic/Aluminium frame | 1 |
| Rubber Wheels | 65mm diameter | 4 |
| Jumper Wires | Male-Female, various | 20+ |
| Data USB Cable | Micro USB (data type) | 1 |

---

## 🔌 Pin Connections

```
NodeMCU          L298N Motor Driver
─────────────────────────────────────
D1 (GPIO5)  ──►  IN1   (Left Motor A)
D2 (GPIO4)  ──►  IN2   (Left Motor B)
D3 (GPIO0)  ──►  IN3   (Right Motor A)
D4 (GPIO2)  ──►  IN4   (Right Motor B)
D5 (GPIO14) ──►  ENA   (Left PWM Speed)
D6 (GPIO12) ──►  ENB   (Right PWM Speed)
GND         ──►  GND   (Common Ground ⚠️)

12V Battery ──►  L298N 12V Input
NodeMCU     ──►  USB or L298N 5V OUT
```

> ⚠️ **Important:** Always connect Common GND between Battery, L298N, and NodeMCU!

---

## 🔧 Circuit Diagram

![Circuit Diagram](circuit_and_block_diagram/NodeMCU_L298N_Circuit.png)

---

## 📊 Block Diagrams

### System Overview
![System Block Diagram](circuit_and_block_diagram/block_diagram_1_system.png)

### WiFi Communication Flow
![WiFi Flow](circuit_and_block_diagram/block_diagram_2_wifi.png)

### Complete Project
![Complete Block Diagram](circuit_and_block_diagram/block_diagram_3_complete.png)

---

## 💻 Software Setup

### Step 1 — Install Arduino IDE
Download from [arduino.cc/en/software](https://www.arduino.cc/en/software)

### Step 2 — Add ESP8266 Board Support
Go to `File > Preferences` and add this URL:
```
http://arduino.esp8266.com/stable/package_esp8266com_index.json
```
Then: `Tools > Board > Board Manager` → search **esp8266** → Install

### Step 3 — Install CH340G USB Driver
Download from [wch-ic.com](https://www.wch-ic.com/downloads/CH341SER_EXE.html) and install, then restart PC.

### Step 4 — Board & Port Settings
```
Tools > Board  →  NodeMCU 1.0 (ESP-12E Module)
Tools > Port   →  COMxx  (shown in Device Manager)
Upload Speed   →  115200
```

### Step 5 — Configure WiFi Credentials
Open `robot_car_wifi.ino` and update:
```c
const char* WIFI_SSID     = "rsmaurya";     // Your WiFi name
const char* WIFI_PASSWORD = "123456788";    // Your WiFi password
```

### Step 6 — Upload & Run
1. Click **Upload** button in Arduino IDE
2. Open **Serial Monitor** at `115200 baud`
3. Note the **IP address** shown (e.g. `192.168.1.105`)
4. Open browser on phone/PC connected to same WiFi
5. Type the IP address → **Start controlling! 🚗**

---

## 🎮 Controls

| Button | Action |
|--------|--------|
| ▲ Forward | All 4 motors forward |
| ▼ Backward | All 4 motors backward |
| ◄ Left | Tank turn left |
| ► Right | Tank turn right |
| ↖ Soft Left | Gentle curve left |
| ↗ Soft Right | Gentle curve right |
| ⏹ Stop | All motors stop |
| 🐢 Slow | Speed preset 30% |
| 🐈 Medium | Speed preset 60% |
| 🐇 Fast | Speed preset 100% |

**Keyboard (PC):** `W` `A` `S` `D` or Arrow Keys | `Space` = Stop

---

## 🌐 HTTP API Endpoints

```
GET /                      → Controller web page
GET /cmd?action=forward    → Move forward
GET /cmd?action=backward   → Move backward
GET /cmd?action=left       → Turn left
GET /cmd?action=right      → Turn right
GET /cmd?action=softleft   → Soft left curve
GET /cmd?action=softright  → Soft right curve
GET /cmd?action=stop       → Stop all motors
GET /speed?val=80          → Set speed to 80%
```

---

## ⚙️ Motor Direction Logic

| Movement | IN1 | IN2 | IN3 | IN4 |
|----------|-----|-----|-----|-----|
| Forward  | HIGH | LOW | HIGH | LOW |
| Backward | LOW | HIGH | LOW | HIGH |
| Turn Left | LOW | HIGH | HIGH | LOW |
| Turn Right | HIGH | LOW | LOW | HIGH |
| Stop | LOW | LOW | LOW | LOW |

---

## 📐 Speed Calculation

With 65mm diameter wheels and 200RPM motors:

```
Circumference = π × 65mm = 204mm = 0.204m

At 200 RPM (100% speed):
Speed = 200 × 0.204 = 40.8 m/min = 0.68 m/sec

At 100 RPM (50% speed):
Speed = 100 × 0.204 = 20.4 m/min = 0.34 m/sec
```

> Perfect indoor speed for a robot car! ✅

---

## 🔮 Future Enhancements

- [ ] Ultrasonic sensor (HC-SR04) for obstacle avoidance
- [ ] ESP32-CAM for live video streaming
- [ ] HC-05 Bluetooth backup control
- [ ] Virtual joystick on web interface
- [ ] Battery level indicator (A0 pin)
- [ ] MOSFET driver (BTS7960) upgrade
- [ ] IR line following mode
- [ ] GPS tracking integration

---

## 📋 Troubleshooting

| Problem | Solution |
|---------|----------|
| `PermissionError(13)` on upload | Use data USB cable, install CH340G driver |
| WiFi not connecting | Check SSID/password spelling, restart NodeMCU |
| Motors not moving | Check Common GND connection, verify L298N 12V supply |
| Web page not loading | Ensure phone/PC on same WiFi, check Serial Monitor for IP |
| Slow/no speed change | Remove ENA/ENB jumpers from L298N module |
| Only 2 motors work | Check parallel wiring of motors on same channel |

---

## 👨‍💻 Developer

**RS Maurya**  
📍 Buddha Institute of Technology, Gorakhpur  
🏆 RoboRace Competition — **1st Prize Winner** 🥇  
🔧 Embedded Systems | IoT | Robotics | PCB Design

---

## 📄 License

This project is licensed under the **MIT License** — feel free to use, modify and distribute with attribution.

---

<div align="center">

**⭐ If this project helped you, please give it a Star! ⭐**

Made with ❤️ by RS Maurya | Buddha Institute of Technology, Gorakhpur

</div>
