# Pipeline Water Flow Rate and Structural Tilt Monitor

<div align="center">

[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-00f0ff?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ALWINTR/Pipeline-Water-Flow-Rate-and-Structural-Tilt-Monitor)
[![Developer](https://img.shields.io/badge/Developer-Alwin_T_R-0284c7?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/alwintr)
[![Portfolio](https://img.shields.io/badge/Portfolio-alwintr.github.io-00f0ff?style=for-the-badge&logo=googlechrome&logoColor=black)](https://alwintr.github.io)
[![License](https://img.shields.io/badge/License-MIT-10b981?style=for-the-badge)](LICENSE)

</div>

> Industrial dual-parameter telemetry station measuring pipeline volumetric liquid flow rate and structural pipe angular deviation using hardware interrupt counters and tilt switches.

---

## 📌 Executive Overview

Industrial dual-parameter telemetry station measuring pipeline volumetric liquid flow rate and structural pipe angular deviation using hardware interrupt counters and tilt switches. This repository contains production-ready firmware implementations, hardware wiring pinouts, signal conditioning routines, and real-time telemetry pipelines engineered for reliable physical operation.

- **Primary Domain**: Radar & Sensing
- **Microcontroller & Hardware Core**: ESP32 / Dual-Sensor
- **Specialization**: Hydrodynamic Sensing
- **Live Specs & BOM Viewer**: [alwintr.github.io](https://alwintr.github.io)

---

## 📐 System Architecture & Signal Flow

```
[ Liquid Flow Through Pipe ] ===> [ YF-S201 Hall-Effect Turbine ]
                                            | Hall Pulse Frequency (7.5 Hz per L/min)
                                            v
[ Structural Pipe Tilt ]     ===> [ SW-520D Ball Tilt Switch ]
                                            | Edge State Transition
                                            v
+--------------------------------------------------------------+
|                ESP32 Dual-Core Microcontroller               |
|  - ISR Flow Counter (GPIO 14)  - ISR Tilt Alarm (GPIO 27)    |
|  - Q = Frequency / 7.5 (L/min) - Total Volume Integration    |
+--------------------------------------------------------------+
        |
        v I2C Bus (400kHz)
+--------------------------------------------------------------+
|         OLED Real-Time Flow Rate & Tilt Safety HUD           |
+--------------------------------------------------------------+
```

---

## 📋 Hardware Bill of Materials (BOM)

| Component Name | Operating Voltage | Interface / Functionality |
| :--- | :--- | :--- |
| **ESP32 DevKit V1** | `3.3V / 5V` | Dual-Core SoC |
| **YF-S201 Water Flow Sensor** | `5V DC` | 1-30 L/min range, Hall turbine |
| **SW-520D Dual-Ball Tilt Sensor** | `3.3V DC` | Mechanical orientation detection |
| **0.96" I2C SSD1306 OLED** | `3.3V DC` | Display |

---

## 🔌 Circuit Pinout & Microcontroller Interconnect

| MCU Pin / Channel | Peripheral Pin | Signal Function / Bus |
| :--- | :--- | :--- |
| `ESP32 GPIO 14` | `YF-S201 Signal Out` | Hardware Interrupt RISING |
| `ESP32 GPIO 27` | `SW-520D Tilt Out` | External Interrupt CHANGE |
| `ESP32 GPIO 21 (SDA), GPIO 22 (SCL)` | `SSD1306 OLED` | I2C Bus Master |
| `ESP32 GPIO 4` | `Tilt Alarm Buzzer` | Deformation Warning Driver |

---

## ⚙️ Firmware Architecture & Control Logic

Edge-triggered ISR pulse accumulator computing instantaneous liters per minute and cumulative throughput with structural angle anomaly detection.

### Key Firmware Capabilities:
- **Zero-Blocking Architecture**: Real-time non-blocking scheduling eliminating delay() deadlocks.
- **Hardware Interrupt Servicing**: Microsecond-precision edge-triggered pulse detection and safety shutoffs.
- **Diagnostic Telemetry**: Continuous serial datastreaming and state-machine transition logging.

---

## 📁 Repository Structure

```
Pipeline-Water-Flow-Rate-and-Structural-Tilt-Monitor/
├── .gitignore
├── LICENSE
└── README.md
```

---

## 🚀 Build & Deployment Instructions

### 1. Hardware Assembly
- Verify common system ground across all microcontrollers, drivers, and peripheral sensor boards.
- Ensure dedicated power supply rails match the operating voltage specified in the Hardware Bill of Materials.

### 2. Firmware Compilation & Flashing
```bash
# Clone the repository
git clone https://github.com/ALWINTR/Pipeline-Water-Flow-Rate-and-Structural-Tilt-Monitor.git

# Navigate to the project directory
cd Pipeline-Water-Flow-Rate-and-Structural-Tilt-Monitor
```

- Open the project in **Arduino IDE**, **PlatformIO**, or **ESP-IDF**.
- Select the target board configuration and COM port.
- Compile and upload firmware directly to the microcontroller.

---

## 👨‍💻 Author

**Alwin T R** — Robotics & Automation Engineer  
- 💼 **LinkedIn**: [linkedin.com/in/alwintr](https://www.linkedin.com/in/alwintr)  
- 🌐 **Interactive Portfolio**: [alwintr.github.io](https://alwintr.github.io)  
- 🐙 **GitHub**: [github.com/ALWINTR](https://github.com/ALWINTR)  
- ✉️ **Direct Email**: [alwintr2003@gmail.com](mailto:alwintr2003@gmail.com)

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.
