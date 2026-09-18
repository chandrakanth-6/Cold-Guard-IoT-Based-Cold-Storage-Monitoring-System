# ColdGuard – IoT-Based Cold Storage Monitoring System

**An IoT-based cold storage monitoring system using LPC2148, DHT11, ESP-01, EEPROM, LCD, Keypad, Buzzer and ThingSpeak**

---

## 📌 Overview

**ColdGuard** is an IoT-based cold storage monitoring system designed to continuously monitor and manage temperature and humidity conditions inside a cold storage environment.

The system uses the **LPC2148 ARM7 microcontroller** as the main controller. A **DHT11 sensor** is used to measure temperature and humidity. The measured values are displayed on a **16x2 LCD** and compared with user-configured setpoints.

When the temperature or humidity exceeds the configured limits, the system activates a **buzzer alarm** to alert the user.

The system also provides a **password-protected menu**, allowing the user to configure temperature and humidity setpoints. These settings are stored in an **AT24C256 EEPROM**, allowing the values to remain available even after power is removed.

For remote monitoring, an **ESP-01 Wi-Fi module** communicates with the LPC2148 through UART and sends monitoring data to **ThingSpeak**.

The system also includes **door monitoring** and **RTC functionality** to improve cold-storage monitoring and event handling.

---

# ✨ Highlights

| Feature | Description |
|---|---|
| 🌡️ Temperature Monitoring | Measures temperature using DHT11 |
| 💧 Humidity Monitoring | Measures humidity using DHT11 |
| 📺 LCD Display | Displays temperature, humidity, setpoints and system status |
| 🔔 Buzzer Alert | Provides an alarm when configured limits are exceeded |
| 🔐 Password Protection | Protects configuration settings |
| 🔢 Keypad Interface | Used for menu navigation and user input |
| 💾 EEPROM Storage | Stores setpoints and configuration permanently |
| 🚪 Door Monitoring | Detects door events |
| 📡 Wi-Fi Connectivity | ESP-01 provides Wi-Fi communication |
| ☁️ Cloud Monitoring | Sends data to ThingSpeak |
| ⏰ RTC | Provides real-time clock functionality |

---

# 🔧 Hardware Components

- **LPC2148 ARM7 Microcontroller**
- **DHT11 Temperature & Humidity Sensor**
- **ESP-01 Wi-Fi Module**
- **AT24C256 I2C EEPROM**
- **16x2 LCD**
- **4x4 Keypad**
- **Buzzer**
- **Door Sensor / Switch**
- **RTC**
- **12 MHz Crystal**
- Power Supply
- Embedded Development Board

---

# 🔌 Hardware Connections

The LPC2148 acts as the central controller and communicates with the different peripherals through GPIO, UART and I2C interfaces.

| Component | Interface / Connection |
|---|---|
| LPC2148 | Main Microcontroller |
| DHT11 | GPIO |
| ESP-01 | UART0 |
| AT24C256 EEPROM | I2C |
| 16x2 LCD | GPIO |
| Keypad | GPIO |
| Buzzer | GPIO |
| Door Sensor | GPIO / Door Event Detection |
| RTC | RTC Peripheral |

---

# 🧩 Hardware Block Diagram

The ColdGuard system consists of the LPC2148 microcontroller connected to the sensing, display, storage, alarm, door-monitoring and communication modules.

### Circuit Block Diagram

<img width="1536" height="1024" alt="circuit_block_diagram(1)" src="https://github.com/user-attachments/assets/a4d2ae04-473c-42ae-a7ab-7bc102b20cd1" />


---

# 🖥️ Hardware Prototype

The complete hardware prototype integrates the LPC2148 controller with the DHT11 sensor, LCD, keypad, EEPROM, buzzer, door sensor and ESP-01 Wi-Fi module.

### Complete Hardware Setup

![ColdGuard Hardware Board](Images/hardware_board.jpeg)

---

# ⚙️ System Clock Configuration

The LPC2148 system uses an external **12 MHz crystal oscillator**.

The PLL is configured to generate a **60 MHz CPU clock (CCLK)**. The peripheral clock is configured at **15 MHz**, which is used by peripherals such as UART and other timing-dependent modules.

### Clock Configuration

- Crystal Frequency (FOSC): **12 MHz**
- PLL Multiplier (M): **5**
- CPU Clock (CCLK): **60 MHz**
- Peripheral Clock (PCLK): **15 MHz**
- UART Baud Rate: **9600 bps**

### System Clock Configuration Diagram

![System Clock Configuration](Images/system_clock_configuration.png)

---

# 🔄 How the System Works

The ColdGuard system follows a continuous monitoring cycle.

### 1. System Initialization

When the system starts, the LPC2148 initializes the required peripherals such as:

- LCD
- DHT11
- Keypad
- EEPROM
- UART
- ESP-01
- Buzzer
- Door monitoring
- RTC

### 2. Configuration Loading

The system reads the stored configuration and setpoints from the EEPROM.

If valid configuration data is available, it is loaded into the system.

### 3. Sensor Reading

The DHT11 sensor provides:

- Temperature
- Relative Humidity

The LPC2148 reads and processes these values.

### 4. LCD Display

The current temperature and humidity values are displayed on the 16x2 LCD.

### 5. Threshold Monitoring

The measured values are compared with the configured setpoints.

If the monitored value exceeds the configured limit, the buzzer is activated.

### 6. Door Monitoring

The system monitors the door sensor and processes door events according to the programmed logic.

### 7. Wi-Fi Communication

The ESP-01 module communicates with the LPC2148 through UART and provides Wi-Fi connectivity.

### 8. Cloud Monitoring

The monitored data is sent to ThingSpeak for remote visualization.

---

# 🔁 Main Loop State Machine

The main program continuously executes the monitoring and control operations.

The main loop handles sensor readings, LCD updates, threshold checking, door monitoring, keypad input, configuration handling and IoT communication.

### Main Loop State Machine

![Main Loop State Machine](Images/main_loop_state_machine.png)

---

# 🔐 Menu & Password System

ColdGuard includes a password-protected menu to prevent unauthorized modification of important configuration parameters.

The keypad is used to enter the password and navigate through the menu.

The user can configure parameters such as:

- Temperature setpoint
- Humidity setpoint
- Other available system settings

### Menu and Password Flow

![Menu and Password System](Images/menu_password_system.png)

---

# 💾 EEPROM Configuration Storage

An **AT24C256 EEPROM** is used for non-volatile storage of system configuration.

The EEPROM stores important parameters such as:

- Temperature setpoint
- Humidity setpoint
- Configuration values

This allows the system to retain the configured values even after power is removed.

The LPC2148 communicates with the AT24C256 through the **I2C communication protocol**.

---

# 📺 LCD Display

A **16x2 LCD** is used to provide local information to the user.

The display can show:

- Temperature
- Humidity
- Temperature setpoint
- Humidity setpoint
- Door status
- Alarm status
- Configuration messages
- System status

### LCD Display States

![LCD Display States](Images/lcd_display_states.png)

### Actual LCD Display

![ColdGuard LCD Display](Images/display(1).png)

---

# 🚪 Door Monitoring

The ColdGuard system monitors the cold-storage door using a door sensor.

The LPC2148 detects changes in the door state and processes the corresponding door event.

The system can identify when the door remains open beyond the programmed time and can generate an appropriate alert.

### Door Event Protocol

![Door Event Protocol](Images/door_event_protocol.png)

---

# 📡 ESP-01 Wi-Fi Communication

The **ESP-01 Wi-Fi module** is used to provide wireless connectivity.

The LPC2148 communicates with the ESP-01 using **UART0**.

The ESP-01 is responsible for connecting the system to a Wi-Fi network and providing communication with the ThingSpeak cloud platform.

The communication flow is:

```text
DHT11
   ↓
LPC2148
   ↓
UART0
   ↓
ESP-01
   ↓
Wi-Fi
   ↓
ThingSpeak
☁️ ThingSpeak Cloud Monitoring

ThingSpeak is used to remotely visualize the monitoring data.

The ESP-01 sends the required sensor information to the ThingSpeak platform.

This allows temperature and humidity information to be monitored remotely through the cloud dashboard.

ThingSpeak Dashboard
📊 Data Flow

The ColdGuard data flow begins with sensor data acquisition and continues through processing, local display, alarm handling and cloud transmission.

The LPC2148 acts as the central processing unit that receives information from the connected peripherals and controls the overall system.

Data Flow Summary

🏗️ Software Architecture

The software is divided into separate modules so that each hardware component and functionality can be managed independently.

The major software modules include:

LCD Driver
DHT11 Driver
Keypad Driver
EEPROM Driver
UART Driver
ESP-01 Communication
Buzzer Control
Door Monitoring
Password Management
Menu Management
RTC
Application Configuration
Software Architecture

🧠 Software Module Structure

The project follows a modular embedded-C approach.

Application Layer
       │
       ├── Main Application
       ├── Menu
       ├── Password
       └── Application Configuration
       │
       ▼
Peripheral Drivers
       │
       ├── DHT11
       ├── LCD
       ├── Keypad
       ├── EEPROM
       ├── UART
       ├── RTC
       ├── Buzzer
       └── Door Monitoring
       │
       ▼
Communication
       │
       └── ESP-01 / Wi-Fi / ThingSpeak
       │
       ▼
Hardware
       │
       └── LPC2148 ARM7
📁 Project Structure
ColdGuard/
│
├── main.c
├── config.h
├── types.h
├── delay.h
│
├── lcd.c
├── lcd.h
│
├── dht11.c
├── dht11.h
│
├── keypad.c
├── keypad.h
│
├── buzzer.c
├── buzzer.h
│
├── door_interrupt.c
├── door_interrupt.h
│
├── password.c
├── password.h
│
├── menu.c
├── menu.h
│
├── eeprom.c
├── eeprom.h
│
├── uart0.c
├── uart0.h
│
├── esp01.c
├── esp01.h
│
├── rtc.c
├── rtc.h
│
├── app_config.h
│
├── ColdGuard.uvprojx
│
└── images/
    ├── circuit_block_diagram.png
    ├── data_flow_summary.png
    ├── display.png
    ├── door_event_protocol.png
    ├── hardware_board.jpeg
    ├── lcd_display_states.png
    ├── main_loop_state_machine.png
    ├── menu_password_system.png
    ├── software_architecture.png
    ├── system_clock_configuration.png
    └── thingspeak_dashboard.png
🧪 Testing

The system was tested by verifying individual peripherals and their integration with the LPC2148.

Test	Expected Result
DHT11 Temperature	Temperature reading obtained
DHT11 Humidity	Humidity reading obtained
LCD	Sensor and system information displayed
Keypad	User input detected
Password	Configuration access controlled
EEPROM	Configuration retained after restart
Buzzer	Alarm activated according to threshold
Door Sensor	Door event detected
UART	Communication with ESP-01 established
ESP-01	Wi-Fi communication established
ThingSpeak	Monitoring data displayed on dashboard
🛠️ Challenges Faced
DHT11 Sensor Integration

The DHT11 requires proper timing and initialization for reliable temperature and humidity readings.

ESP-01 Communication

UART communication and ESP-01 initialization required careful handling to establish reliable communication between the LPC2148 and Wi-Fi module.

EEPROM Storage

The AT24C256 required correct I2C communication and memory addressing to store and retrieve configuration values.

Threshold-Based Alarm

The buzzer logic needed to correctly compare sensor readings with the configured temperature and humidity setpoints.

Door Monitoring

Door event detection required proper monitoring of the door sensor state and timing logic.

Peripheral Integration

Integrating multiple peripherals with the LPC2148 required proper initialization order and coordination between the different software modules.

🔨 Build & Flash
🔨 Build & Flash

The project was developed using Keil µVision for LPC2148 ARM7.

Software Requirements
Keil µVision
ARM7 LPC2148 development environment
Flash Magic
Embedded C
ThingSpeak account
Build Steps
Open the .uvprojx project in Keil µVision.
Verify that all source and header files are included.
Build the project.
Resolve any compilation errors.
Generate the HEX file.
Connect the LPC2148 development board.
Use Flash Magic to program the HEX file.
Reset the board and start testing.
🌐 Applications

ColdGuard can be used in environments where temperature and humidity monitoring are important.

Possible applications include:

Cold storage facilities
Pharmaceutical storage
Medical storage
Food storage
Refrigerated warehouses
Laboratories
Temperature-sensitive material storage
🔮 Future Enhancements

Possible future improvements include:

📱 Mobile application for remote monitoring
📧 Email notifications
📩 SMS alerts
📊 Advanced cloud analytics
🗃️ Long-term data logging
🌡️ Multiple temperature and humidity sensors
❄️ Automatic cooling control
🚪 Advanced door-open alerts
🔔 Real-time mobile notifications
📈 Improved web dashboard
