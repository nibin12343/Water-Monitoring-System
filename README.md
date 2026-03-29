# Water-Monitoring-System

A smart IoT-based water tank monitoring and control system built using ESP32.
This project measures water level, pH, TDS, and turbidity, and provides a real-time web dashboard with authentication, along with automatic pump control.

🚀 Features

🌊 Real-time Water Level Monitoring (Ultrasonic sensor)
🧪 Water Quality Analysis
pH level
TDS (Total Dissolved Solids)
Turbidity
📊 Live Dashboard UI
Animated tank visualization
Purity score (based on pH + TDS + Turbidity)
Historical level chart
🔐 Secure Login System
Session-based authentication (cookies)
⚙️ Pump Automation
Auto ON/OFF based on water level thresholds
Manual override support
🎚️ Adjustable Desired Water Level
🔔 Smart Notifications
📡 WiFi-enabled monitoring (ESP32 WebServer)
🧰 Hardware Requirements
Component	Description
ESP32	Main microcontroller
AJ-SR04M	Waterproof ultrasonic sensor
pH Sensor	Analog pH probe
TDS Sensor	Analog TDS module
Turbidity Sensor	Analog turbidity sensor
Relay Module	Pump control
Water Pump	Tank filling
🔌 Pin Configuration
#define TRIG_PIN 5
#define ECHO_PIN 18
#define PH_PIN   34
#define TDS_PIN  35
#define TURB_PIN 32
#define PUMP_PIN 23
📡 WiFi Configuration

Update your WiFi credentials in the code:

const char *ssid     = "YOUR_WIFI_NAME";
const char *password = "YOUR_WIFI_PASSWORD";
🔐 Login Credentials

Default login:

Username: user
Password: password

You can modify them here:

const char *AUTH_USER = "user";
const char *AUTH_PASS = "password";
🌐 Web Interface
Routes
Route	Description
/	Login page
/login	Authenticate
/dashboard	Main dashboard
/data	JSON sensor data
/setlevel	Set desired water level
/pump	Control pump mode/state
/logout	Logout
⚙️ System Logic
Water Level Calculation
Uses ultrasonic distance measurement
Converts distance → percentage using tank calibration
Pump Control

Auto Mode:

Pump ON when level ≤ 20%
Pump OFF when level ≥ desired level (default 75%)

Manual Mode:

Controlled via API
🧪 Sensor Processing
Median filtering (30 samples) for noise reduction
ADC-based voltage conversion
Calibration-based pH calculation
Polynomial TDS estimation
Turbidity approximated from voltage
📊 Water Purity Score

Calculated using:

pH range
TDS levels
Turbidity

Score categories:

✅ Excellent
🟢 Good
⚠️ Fair
❌ Poor
🛠️ Installation
Install Arduino IDE or PlatformIO
Install ESP32 board support
Install required libraries:
WiFi.h
WebServer.h
Preferences.h
Upload water_monitor.ino to ESP32
Open Serial Monitor to get IP address
Open browser → http://<ESP32_IP>
📷 Dashboard Highlights
Animated water tank
Circular purity indicator
Live sensor tiles
Level history chart
Notification system
🔄 API Examples
Get Data
GET /data
Set Desired Level
GET /setlevel?v=80
Pump Control
POST /pump
mode=auto
POST /pump
mode=manual&state=on
⚠️ Notes
Relay is active LOW
Ensure proper sensor calibration for accurate readings
Waterproof ultrasonic sensor recommended for tanks
Turbidity calculation is approximate
🔮 Future Improvements
Mobile app integration
Cloud data logging (Firebase / MQTT)
Temperature compensation for TDS
OTA firmware updates
Multi-tank support

