# 🌱 SMART IoT Irrigation System

An **IoT-based smart irrigation system** developed using the **LPC2148 ARM7 microcontroller** to monitor environmental conditions and automatically control irrigation. The system measures **temperature, humidity, and soil moisture**, displays the information on an LCD, and uploads selected data to the **ThingSpeak Cloud** through an **ESP-01 Wi-Fi module**.

The system can automatically control a water motor based on soil moisture and user-defined irrigation settings, helping reduce water wastage and improve irrigation efficiency.

---

## 📖 Project Overview

The **Smart IoT Irrigation System** is an embedded IoT automation project designed for smart agriculture.

The system continuously monitors:

* 🌡️ Temperature
* 💧 Relative Humidity
* 🌱 Soil Moisture
* 🔄 Motor ON/OFF Status

The collected sensor data is displayed locally on an **LCD** and uploaded to the **ThingSpeak Cloud** using an **ESP-01 Wi-Fi module**.

The LPC2148 microcontroller controls the irrigation motor through a **relay** based on soil moisture conditions and user-configured irrigation settings.

---

## 🎯 Aim of the Project

The main aim of this project is to develop an **IoT-based automatic irrigation system** capable of monitoring environmental parameters and controlling irrigation according to field requirements.

The system is designed to:

* Monitor temperature and humidity.
* Detect soil moisture conditions.
* Automatically control the irrigation motor.
* Allow users to configure irrigation duration.
* Upload sensor information to the cloud.
* Enable remote monitoring through ThingSpeak.

---

## ✨ Features

* 🌡️ Real-time temperature monitoring
* 💧 Real-time humidity monitoring
* 🌱 Soil moisture detection
* 🚰 Automatic water motor control
* 📟 LCD-based local monitoring
* ☁️ ThingSpeak cloud monitoring
* 📡 ESP-01 Wi-Fi communication
* ⚡ UART interrupt-based communication
* ⏰ RTC-based timed data transmission
* 🔢 Menu-driven user interface
* ⌨️ Keypad-based configuration
* 🔘 External interrupt-based menu access
* ⚙️ User-configurable irrigation settings
* ⏱️ Custom irrigation duration selection
* 🌾 Different irrigation modes for different crop/field requirements

---

# 🔧 Hardware Requirements

| Component                          | Purpose                              |
| ---------------------------------- | ------------------------------------ |
| **LPC2148**                        | Main ARM7 microcontroller            |
| **DHT11**                          | Temperature and humidity measurement |
| **LCD 16×2**                       | Display sensor values and menus      |
| **ESP-01**                         | Wi-Fi and cloud communication        |
| **Soil Moisture Sensor**           | Detects soil moisture condition      |
| **Keypad**                         | User input and menu selection        |
| **Push Button**                    | External interrupt / menu access     |
| **Relay**                          | Controls the water motor             |
| **12V Power Supply**               | Power supply for motor/system        |
| **Water Motor**                    | Irrigation system                    |
| **DB9 Cable / USB-UART Converter** | Serial communication/programming     |

---

# 💻 Software Requirements

* **Embedded C**
* **Keil C Compiler**
* **Flash Magic**
* **ThingSpeak Cloud**

---

# 🏗️ System Architecture

The overall system consists of the following major modules:

<img width="1663" height="946" alt="projectn Archi" src="https://github.com/user-attachments/assets/adc068c5-7e3c-46da-a100-30f463a2b2e5" />

---

# ⚙️ Working Principle

## 1. System Initialization

When the system is powered ON, the LPC2148 initializes all required peripherals:

* LCD
* DHT11
* Soil Moisture Sensor
* ESP-01
* RTC
* Keypad
* External Interrupt
* UART

---

## 2. Sensor Monitoring

The system continuously reads:

### DHT11

The DHT11 provides:

* Temperature
* Relative Humidity

### Soil Moisture Sensor

The soil moisture sensor determines whether the soil is sufficiently wet or dry.

The measured values are displayed on the LCD.

---

# ⚡ 3. Interrupt-Based User Configuration

When the user presses the **external interrupt switch**, the system enters the configuration/menu mode.

The user can navigate through the menu using the keypad.

### LCD Menu

```text
1. Set Irrigation Time
2. Temp & Humidity
3. Exit
Select Option:
```

---

## Menu Option 1: Motor Timing Selection

The user can configure the irrigation motor ON duration.

Example:

```text
1 Minute
2 Minutes
3 Minutes
```

This allows different irrigation durations depending on crop or field requirements.

---

## Menu Option 2: Temperature & Humidity Settings

The user can configure irrigation timing according to environmental conditions.

Example:

| Condition                                | Motor Duration |
| ---------------------------------------- | -------------: |
| High Temperature + Low Humidity          |      3 Minutes |
| Moderate Temperature + Moderate Humidity |      2 Minutes |
| Low Temperature + High Humidity          |       1 Minute |

These settings allow the user to customize irrigation according to field requirements.

---

# 🚰 4. Automatic Irrigation Control

The **soil moisture condition is the primary parameter** used for automatic irrigation.

### Dry Soil

```text
Soil Moisture = LOW
        ↓
Check User Settings
        ↓
Motor ON
        ↓
Run for Configured Duration
```

### Wet Soil

```text
Soil Moisture = HIGH
        ↓
Motor OFF
```

The motor is controlled through a relay.

During testing, an LED can be used to represent the motor ON/OFF condition.

---

# 📡 5. UART Communication with ESP-01

The LPC2148 communicates with the ESP-01 Wi-Fi module using **UART**.

The LPC2148 sends AT commands to configure the ESP-01 and establish communication with the ThingSpeak cloud.

### Example AT Commands

```text
AT
AT+CWMODE
AT+CWJAP
AT+CIPSTART
AT+CIPSEND
```

The system then sends an HTTP request containing the required sensor information to ThingSpeak.

---

# ⚡ UART Reception Using Interrupts

The ESP-01 sends responses such as:

```text
OK
ERROR
SEND OK
Wi-Fi connection status
```

The LPC2148 uses a **UART receive interrupt** to handle incoming data.

### UART Interrupt Process

```text
ESP-01 sends response
        ↓
UART Receive Interrupt
        ↓
Receive Character
        ↓
Store in Buffer
        ↓
Process Response
        ↓
Display Status / Continue Operation
```

### Benefits

* Efficient communication
* Faster response handling
* Reduced continuous polling
* Real-time response processing
* Easier debugging
* Reliable UART communication

---

# ☁️ 6. ThingSpeak Cloud Monitoring

After establishing communication with the ESP-01, the system uploads data to **ThingSpeak Cloud**.

The cloud can be used to monitor:

* 🌡️ Temperature
* 💧 Humidity
* 🔄 Motor ON/OFF Status

### Motor Status

```text
1 → Motor ON
0 → Motor OFF
```

The motor status changes according to the soil moisture condition and configured irrigation settings.

---

# 🖼️ Project Images

## 📊 1. System Block Diagram

The block diagram shows the interconnection between:

* LPC2148
* DHT11
* Soil Moisture Sensor
* RTC
* LCD
* Keypad
* ESP-01
* Relay
* Motor

<img width="608" height="346" alt="594010965-5b0164cf-9dc1-40ea-9cea-2340c369b3e4" src="https://github.com/user-attachments/assets/b8653680-8364-4b3f-9d1e-3c26297b37a6" />

---

## 🔌 2. Hardware Setup

The hardware implementation consists of the LPC2148 development board and connected peripherals.

<img width="1280" height="960" alt="598679629-2f26a454-bf60-4503-8c78-696bbf2c0dba" src="https://github.com/user-attachments/assets/e6618b4d-5240-4dae-9d3f-1ac3c21b9e09" />

---

## 📟 3. LCD Output

This image shows the LCD displaying real-time humidity, temperature, and checksum values read from the DHT11 sensor.

<img width="908" height="608" alt="project LCD output" src="https://github.com/user-attachments/assets/104b1f13-15fd-470e-be4d-d37e9049950e" />

---

## 📟 4. LCD Menu Navigation

The external interrupt button allows the user to enter the menu without restarting the system.

Example menu:

```text
1. Set Irrigation Time
2. Temp & Humidity
3. Exit
Select Option:
```
<img width="1600" height="600" alt="650687062-68da31e8-4a82-4ae6-b8b4-6473be6f2cea" src="https://github.com/user-attachments/assets/b8bdf9e9-6a74-4eb7-9935-1e4dd558ba34" />

---

# ☁️ ThingSpeak Cloud Output

## 🌡️ Temperature Monitoring

The temperature measured by the DHT11 is uploaded to ThingSpeak and displayed as a real-time graph.

<img width="1064" height="736" alt="WhatsApp Image 2026-10-01 at 3 05 07 PM" src="https://github.com/user-attachments/assets/1076e642-802b-4150-a5cc-acce36912409" />

---

## 💧 Humidity Monitoring

The humidity measured by the DHT11 is uploaded to ThingSpeak.

<img width="1080" height="724" alt="WhatsApp Image 2026-10-01 at 3 05 07 PM (1)" src="https://github.com/user-attachments/assets/482005f7-b0ac-4c17-a521-fd906cffa010" />


---

## 🔄 Motor ON/OFF Status

The motor operating status is uploaded to ThingSpeak.

```text
1 → Motor ON
0 → Motor OFF
```

<img width="602" height="415" alt="594015164-47a6979e-9fe1-4c6d-8a9a-1f56a425012a" src="https://github.com/user-attachments/assets/a047de90-1d2f-4573-b21b-0573632fad71" />


---

# 🚀 How to Run the Project

## Step 1: Create Project Folder

Create a project folder and place all Embedded C source files and header files inside it.

---

## Step 2: Verify LCD Module

Test the LCD for:

* Character display
* String display
* Integer display
* Cursor positioning

---

## Step 3: Verify UART Communication

Connect the UART interface and transmit a test string through a serial terminal.

---

## Step 4: Connect DHT11

Develop and test the DHT11 driver for:

* Temperature reading
* Humidity reading
* Data validation
* LCD display

---

## Step 5: Configure ESP-01

Test the ESP-01 using a serial terminal and AT commands.

Example:

```text
AT
AT+CWMODE
AT+CWJAP
```

Verify that the ESP-01 successfully connects to the Wi-Fi network.

---

## Step 6: Connect ESP-01 to LPC2148

Develop the UART driver and communicate with the ESP-01.

Test sending sample data to ThingSpeak.

---

## Step 7: Connect Soil Moisture Sensor

Connect the soil moisture sensor and verify:

* Dry soil detection
* Wet soil detection
* Motor/LED control

---

## Step 8: Implement Main Logic

Combine all modules:

```text
Sensor Reading
      ↓
LCD Display
      ↓
Soil Moisture Decision
      ↓
Motor Control
      ↓
ESP-01 Communication
      ↓
ThingSpeak Cloud
```

---

## Step 9: Build and Flash

1. Compile the project using **Keil C Compiler**.
2. Generate the HEX file.
3. Connect the LPC2148 to the computer.
4. Use **Flash Magic** to program the microcontroller.
5. Power ON the complete system.
6. Verify sensor readings, motor control, LCD menu, and ThingSpeak data.

---

# 🧩 Major Modules

The project is divided into the following software/hardware modules:

| Module             | Function                        |
| ------------------ | ------------------------------- |
| DHT11 Driver       | Reads temperature and humidity  |
| Soil Moisture      | Detects soil condition          |
| LCD Driver         | Displays system information     |
| Keypad Driver      | User input                      |
| UART Driver        | Communication with ESP-01       |
| UART Interrupt     | Handles ESP-01 responses        |
| ESP-01             | Wi-Fi connectivity              |
| RTC                | Timing and scheduled operations |
| External Interrupt | Menu access                     |
| Relay Control      | Controls motor                  |
| ThingSpeak         | Cloud monitoring                |
| Main Application   | Integrates all modules          |

---

# 🌍 Applications

* 🌾 Smart Agriculture
* 💧 Automated Irrigation
* 🌱 Crop Irrigation Management
* ☁️ Remote Environmental Monitoring
* 🚜 IoT-Based Farming Systems
* 💦 Water Conservation
* 🌐 Remote Irrigation Monitoring

---

# 🔮 Future Improvements

The project can be further enhanced with:

* 📱 Mobile application control
* 📊 Accurate soil moisture percentage using ADC
* 🚰 Automatic pump hardware integration
* 📈 Advanced cloud analytics dashboard
* 📩 SMS/Email alerts
* ☀️ Solar-powered operation
* 🌐 Web-based irrigation control
* 🤖 AI-based irrigation prediction
* 🌦️ Weather API integration
* 📍 Multiple-field monitoring

---

# 🛠️ Technologies Used

```text
Microcontroller : LPC2148 ARM7
Programming     : Embedded C
Compiler        : Keil C
Programming Tool: Flash Magic
Sensors         : DHT11, Soil Moisture Sensor
Communication   : UART
Wi-Fi           : ESP-01
Display         : 20x4 LCD
Input           : Keypad / Push Button
Timing          : RTC
Cloud           : ThingSpeak
Motor Control   : Relay
```

---

# 📚 Key Embedded Concepts Used

This project demonstrates practical knowledge of:

* ARM7 LPC2148
* GPIO
* UART
* UART Interrupts
* External Interrupts
* RTC
* Sensor Interfacing
* LCD Interfacing
* Keypad Interfacing
* DHT11 Communication
* ESP-01 Communication
* AT Commands
* Relay Control
* IoT Communication
* Cloud Data Monitoring
* Embedded C

---

# 👨‍💻 Author

**Shaik Hazari Tajuddin**

**Project:** Smart IoT Irrigation System

---

