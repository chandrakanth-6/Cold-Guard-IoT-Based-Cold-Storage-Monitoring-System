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

<img width="1536" height="1024" alt="circuit_block_diagram(1)" src="https://github.com/user-attachments/assets/ddf898bd-e92f-48ca-bc81-a76e4bcaa53e" />


---

# 🖥️ Hardware Prototype

The complete hardware prototype integrates the LPC2148 controller with the DHT11 sensor, LCD, keypad, EEPROM, buzzer, door sensor and ESP-01 Wi-Fi module.

### Complete Hardware Setup

<img width="984" height="898" alt="hardware_board" src="https://github.com/user-attachments/assets/67c89a2e-51c7-4ef8-be1d-e601a4f29d94" />


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

