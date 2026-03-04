# 🤖 WiFi Controlled Robot Car
### NodeMCU ESP8266 + L298N + 4x 12V DC Gear Motor

<div align="center">

![Robot Car](https://img.shields.io/badge/Project-WiFi%20Robot%20Car-blue?style=for-the-badge&logo=arduino)
![ESP8266](https://img.shields.io/badge/MCU-NodeMCU%20ESP8266-red?style=for-the-badge&logo=espressif)
![L298N](https://img.shields.io/badge/Driver-L298N-orange?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Language](https://img.shields.io/badge/Language-C%20%2F%20Arduino-blue?style=for-the-badge&logo=c)

</div>

---

## 🏆 Achievement — 1st Prize Winner!

<div align="center">

> ### 🥇 RoboRace Competition — 1st Prize
> **Buddha Institute of Technology, Gorakhpur**
>
> 🎖️ Certificate of Excellence &nbsp;|&nbsp; 💰 Cash Prize ₹1000

</div>

<div align="center">

![Certificate](Achievement/cirtificate.jpg)

</div>

<div align="center">

![Car Image](Achievement/car_image.png)

</div>

---

## 📌 Project Overview

A **WiFi-controlled 4-wheel robot car** built using NodeMCU ESP8266 that hosts its own web server. Control the car from **any mobile or PC browser** — no app needed!

- 🎮 Mobile-responsive web controller (touch + keyboard)
- ⚡ PWM speed control 0–100%
- 📡 WiFi HTTP REST API
- ⌨️ WASD / Arrow key support on PC
- 🔄 Auto-stop on button release

---

## 📁 Project Structure

```
Robo_race_car/
├── 📂 Achievement/
│   ├── cirtificate.jpg              ← Competition certificate
│   └── car_image.png                ← Robot car photo
├── 📂 Car_Deshboard/
│   └── dashboard.html               ← Web controller UI
├── 📂 circuit_and_block_daigram/
│   ├── circuit-diagram.jpg          ← Full circuit diagram
│   ├── block diagram.png            ← System block diagram
│   ├── block diagram (2).png        ← WiFi flow diagram
│   └── final_car_image.png          ← Final assembled car
├── 📂 robot_car_wifi_code/
│   └── robot_car_wifi_code.ino      ← Main Arduino source code
├── 📂 WiFi_Robot_Car_Report/
│   └── WiFi_Robot_Car_Report.pdf    ← Full project report (PDF)
├── 📄 LICENSE
└── 📄 README.md
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
NodeMCU              L298N Motor Driver
──────────────────────────────────────────
D1  (GPIO5)  ──►    IN1   (Left Motor A)
D2  (GPIO4)  ──►    IN2   (Left Motor B)
D3  (GPIO0)  ──►    IN3   (Right Motor A)
D4  (GPIO2)  ──►    IN4   (Right Motor B)
D5  (GPIO14) ──►    ENA   (Left PWM Speed)
D6  (GPIO12) ──►    ENB   (Right PWM Speed)
GND          ──►    GND   (Common Ground ⚠️)

12V Battery  ──►    L298N 12V Input
NodeMCU      ──►    USB  or  L298N 5V OUT
```

> ⚠️ **Common GND — Battery + L298N + NodeMCU — zaroor connect karo!**

---

## 🔧 Circuit Diagram

![Circuit Diagram](circuit_and_block_daigram/circuit-diagram.jpg)

---

## 📊 Block Diagrams

### System Block Diagram
![Block Diagram](circuit_and_block_daigram/block%20diagram.png)

### WiFi Communication Flow
![Block Diagram 2](circuit_and_block_daigram/block%20diagram%20(2).png)

---

## 🚗 Final Assembled Car

![Final Car](circuit_and_block_daigram/final_car_image.png)

---

## 💻 Software Setup

### Step 1 — Arduino IDE Install Karo
[arduino.cc/en/software](https://www.arduino.cc/en/software) se download karo

### Step 2 — ESP8266 Board Add Karo
`File > Preferences` mein yeh URL daalo:
```
http://arduino.esp8266.com/stable/package_esp8266com_index.json
```
Phir: `Tools > Board > Board Manager` → **esp8266** search → Install

### Step 3 — CH340G Driver Install Karo
[wch-ic.com](https://www.wch-ic.com/downloads/CH341SER_EXE.html) se download → install → PC restart

### Step 4 — Board & Port Select Karo
```
Tools > Board  →  NodeMCU 1.0 (ESP-12E Module)
Tools > Port   →  COMxx
```

### Step 5 — WiFi Credentials Set Karo
`robot_car_wifi_code.ino` mein yeh lines update karo:
```c
const char* WIFI_SSID     = "rsmaurya";
const char* WIFI_PASSWORD = "123456788";
```

### Step 6 — Upload & Control!
1. **Upload** button click karo ⬆️
2. **Serial Monitor** kholo (115200 baud)
3. **IP address** note karo (e.g. `192.168.1.105`)
4. Same WiFi pe phone/PC browser mein IP daalo
5. **Robot Car control karo! 🚗**

---

## 🎮 Web Controller Features

| Button | Action |
|--------|--------|
| ▲ Forward | Aage badhna |
| ▼ Backward | Peeche jaana |
| ◄ Left | Left spin turn |
| ► Right | Right spin turn |
| ↖ Soft Left | Gentle curve left |
| ↗ Soft Right | Gentle curve right |
| ⏹ Stop | Ruk jaana |
| 🐢 Slow | 30% speed preset |
| 🐈 Medium | 60% speed preset |
| 🐇 Fast | 100% speed preset |

**PC Keyboard:** `W` `A` `S` `D` ya Arrow Keys &nbsp;|&nbsp; `Space` = Stop

---

## 🌐 HTTP API Endpoints

```
GET /                       → Controller webpage load
GET /cmd?action=forward     → Aage chalao
GET /cmd?action=backward    → Peeche chalao
GET /cmd?action=left        → Left turn
GET /cmd?action=right       → Right turn
GET /cmd?action=softleft    → Soft left curve
GET /cmd?action=softright   → Soft right curve
GET /cmd?action=stop        → Sab motors band
GET /speed?val=80           → Speed 80% set karo
```

---

## ⚙️ Motor Direction Logic

| Movement | IN1 | IN2 | IN3 | IN4 |
|----------|-----|-----|-----|-----|
| Forward | HIGH | LOW | HIGH | LOW |
| Backward | LOW | HIGH | LOW | HIGH |
| Turn Left | LOW | HIGH | HIGH | LOW |
| Turn Right | HIGH | LOW | LOW | HIGH |
| Stop | LOW | LOW | LOW | LOW |

---

## 📐 Speed Calculation

```
Wheel diameter  = 65mm
Circumference   = π × 65mm = 204mm = 0.204m

100% speed → 200 RPM → 0.68 m/sec
 50% speed → 100 RPM → 0.34 m/sec
 25% speed →  50 RPM → 0.17 m/sec
```

---

## 🔮 Future Enhancements

- [ ] HC-SR04 Ultrasonic — Obstacle avoidance
- [ ] ESP32-CAM — Live video streaming
- [ ] HC-05 Bluetooth — Backup control
- [ ] Virtual joystick on web interface
- [ ] Battery level indicator (A0 pin)
- [ ] BTS7960 MOSFET driver upgrade
- [ ] IR sensor — Line following mode

---

## 🐛 Troubleshooting

| Problem | Solution |
|---------|----------|
| `PermissionError(13)` upload pe | Data USB cable use karo + CH340G driver install karo |
| WiFi connect nahi ho raha | SSID/password check karo, NodeMCU restart karo |
| Motors nahi chal rahe | Common GND check karo, 12V supply verify karo |
| Web page nahi khul raha | Same WiFi pe ho, Serial Monitor se IP check karo |
| Speed change nahi ho raha | L298N se ENA/ENB jumper caps hata do |
| Sirf 2 motors chal rahe | Parallel wiring check karo same channel pe |

---

## 👨‍💻 Developer

**RS Maurya (Ramsudarshanmaurya)**
📍 Buddha Institute of Technology, Gorakhpur
🏆 **RoboRace Competition — 1st Prize Winner** 🥇
🔧 Embedded Systems | IoT | Robotics | PCB Design | Web

---

## 📄 License

MIT License — freely use, modify and distribute with attribution.

---

<div align="center">

**⭐ Agar project helpful laga toh Star zaroor do! ⭐**

Made with ❤️ by RS Maurya | Buddha Institute of Technology, Gorakhpur

</div>
