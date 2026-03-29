# Water-Monitoring-System

This is a comprehensive and well-structured project outline for an **IoT-based Water Management System**. To make it look professional, clean, and ready for a GitHub README or a project proposal, I have refined the formatting, improved the technical clarity, and organized the sections for better readability.

---

# 💧 Smart Water Tank Monitoring & Control System
### **IoT Solution for Real-Time Water Quality & Level Management**

An advanced ESP32-based IoT system designed to monitor water storage health and automate filling operations. This project integrates multiple chemical and physical sensors with a secure, responsive web dashboard for complete remote oversight.

---

## 🚀 Key Features

* **🌊 Dynamic Monitoring:** Real-time water level tracking using waterproof ultrasonic technology.
* **🧪 Quality Analytics:** Integrated sensing for **pH**, **Total Dissolved Solids (TDS)**, and **Turbidity**.
* **📊 Interactive UI:** Animated tank visualization, historical trend charts, and a calculated **Purity Score**.
* **🔐 Enterprise Security:** Session-based authentication (cookies) for dashboard access.
* **⚙️ Intelligent Automation:** Dual-mode pump control (Auto/Manual) with configurable thresholds.
* **🔔 Instant Alerts:** System notifications for critical levels or poor water quality.

---

## 🧰 Hardware Architecture

| Component | Description |
| :--- | :--- |
| **ESP32** | Dual-core microcontroller with integrated Wi-Fi. |
| **AJ-SR04M** | Waterproof Ultrasonic Sensor for harsh tank environments. |
| **Analog pH Probe** | Measures acidity/alkalinity ($0 - 14$ range). |
| **TDS Module** | Measures dissolved solids in ppm for purity tracking. |
| **Turbidity Sensor** | Detects suspended particles via light refraction. |
| **Relay Module** | High-voltage interface for pump switching (Active LOW). |

### **Pin Configuration**
```
cpp
#define TRIG_PIN  5    // Ultrasonic Trigger
#define ECHO_PIN  18   // Ultrasonic Echo
#define PH_PIN    34   // Analog pH Input
#define TDS_PIN   35   // Analog TDS Input
#define TURB_PIN  32   // Analog Turbidity Input
#define PUMP_PIN  23   // Relay Control
```

---

## ⚙️ System Intelligence

### **1. Pump Control Logic**
The system operates on a state-machine logic to prevent short-cycling of the pump:
* **Auto Mode:** * **ON:** Triggered when level falls below $20\%$.
    * **OFF:** Triggered when level reaches the **User-Defined Threshold** (Default: $75\%$).
* **Manual Mode:** Overrides sensor logic via API/Dashboard commands.

### **2. Signal Processing**
To ensure high accuracy in turbulent water environments, the system implements:
* **Median Filtering:** 30-sample window to eliminate ultrasonic noise.
* **Polynomial Estimation:** For TDS and Turbidity voltage-to-value conversion.
* **Temperature Compensation:** (Planned) To stabilize pH and TDS readings.

### **3. Water Purity Scoring**
The system aggregates sensor data into a simplified health index:
* **Excellent:** Optimal pH ($6.5-8.5$), Low TDS, High Clarity.
* **Good / Fair:** Minor deviations in quality parameters.
* **Poor:** Critical contamination detected; immediate attention required.

---

## 🌐 Web API & Routes

The ESP32 hosts a RESTful web server for seamless integration with the frontend:

| Endpoint | Method | Function |
| :--- | :--- | :--- |
| `/login` | `POST` | Authenticate user session. |
| `/data` | `GET` | Fetch real-time sensor JSON. |
| `/setlevel` | `GET` | Update target water level (e.g., `?v=85`). |
| `/pump` | `POST` | Toggle mode (`auto`/`manual`) and state. |
| `/logout` | `GET` | Terminate current session. |

---

## 🛠️ Installation & Deployment

1.  **Environment:** Install **VS Code + PlatformIO** or Arduino IDE.
2.  **Libraries:** Ensure `WiFi.h`, `WebServer.h`, and `Preferences.h` (for NVS storage) are installed.
3.  **Credentials:** Update the `ssid` and `password` variables in the source code.
4.  **Calibration:** * Submerge the pH probe in a $7.0$ buffer solution to calibrate the offset.
    * Measure the empty tank height to set the ultrasonic baseline.
5.  **Upload:** Flash the firmware and monitor the Serial IP to access the dashboard.

---

## 🔮 Future Roadmap

* **Cloud Sync:** MQTT integration for Home Assistant or AWS IoT.
* **OTA Updates:** Remote firmware flashing over Wi-Fi.
* **Mobile App:** Native Flutter-based application for push notifications.
* **Solar Power:** Deep-sleep optimization for battery-operated remote tanks.

---
