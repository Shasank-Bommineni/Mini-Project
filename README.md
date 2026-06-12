# Mini-Project
IDT project
# ESP32 Water Quality Monitoring System

A real-time water quality monitoring system built using an ESP32, TDS sensor, turbidity sensor, and ST7735 TFT display. The system continuously measures Total Dissolved Solids (TDS) and water turbidity, presenting the results through an intuitive graphical interface while providing an overall water quality assessment.

---

## Overview

Water quality is a critical factor in environmental monitoring, aquaculture, water treatment, and domestic water supply systems. This project provides a compact and cost-effective solution for monitoring key water quality parameters in real time.

The ESP32 collects analog data from a TDS sensor and a turbidity sensor, processes the readings, and displays the results on a 1.8-inch ST7735 TFT screen. Color-coded indicators allow users to quickly evaluate water quality conditions.

---

## Features

* Real-time TDS measurement (ppm)
* Real-time turbidity measurement (NTU)
* Graphical TFT display interface
* Color-coded status indicators
* Water quality classification system
* Serial Monitor debugging output
* ESP32-based architecture
* Modular and easily expandable design

---

## Hardware Requirements

| Component                      | Quantity    |
| ------------------------------ | ----------- |
| ESP32 Dev Board (38-Pin VROOM) | 1           |
| ST7735 TFT Display (1.8")      | 1           |
| TDS Sensor Module              | 1           |
| Turbidity Sensor Module        | 1           |
| Breadboard                     | 1           |
| Jumper Wires                   | As Required |
| USB Cable                      | 1           |

---

## System Architecture

```text
TDS Sensor ──────┐
                 │
                 ▼
             ESP32 MCU ──────► TFT Display
                 ▲
                 │
Turbidity Sensor ┘
```

The ESP32 acts as the central processing unit, acquiring sensor data, performing calculations, and updating the display with processed measurements.

---

## Pin Configuration

### TFT Display Connections

| TFT Pin | ESP32 Pin |
| ------- | --------- |
| VCC     | 3.3V      |
| GND     | GND       |
| SCK     | GPIO 18   |
| MOSI    | GPIO 23   |
| CS      | GPIO 5    |
| DC      | GPIO 2    |
| RST     | GPIO 4    |

### Sensor Connections

| Sensor                  | ESP32 Pin |
| ----------------------- | --------- |
| TDS Sensor Output       | GPIO 34   |
| Turbidity Sensor Output | GPIO 35   |

---

## Software Dependencies

Install the following libraries through the Arduino IDE Library Manager:

* Adafruit GFX Library
* Adafruit ST7735 and ST7789 Library
* SPI Library (included with Arduino IDE)

---

## Measurement Methodology

### TDS Calculation

The system samples the TDS sensor multiple times and computes the average voltage. Temperature compensation is applied before converting the voltage into Total Dissolved Solids (ppm).

```math
TDS = \left(133.42V^3 - 255.86V^2 + 857.39V\right)\times0.5
```

Where:

* `V` = Compensated sensor voltage
* `TDS` = Total Dissolved Solids in ppm

### Turbidity Calculation

The turbidity sensor output voltage is converted into Nephelometric Turbidity Units (NTU) using a calibrated polynomial equation.

```math
NTU = -1120.4V^2 + 5742.3V - 4353.8
```

Where:

* `V` = Sensor voltage
* `NTU` = Turbidity measurement

---

## Water Quality Classification

### TDS Classification

| Range (ppm) | Quality    |
| ----------- | ---------- |
| < 300       | Good       |
| 300 – 600   | Acceptable |
| > 600       | Poor       |

### Turbidity Classification

| Range (NTU) | Quality    |
| ----------- | ---------- |
| < 10        | Good       |
| 10 – 100    | Acceptable |
| > 100       | Poor       |

### Overall Water Status

The system determines overall water quality using both TDS and turbidity values.

| Condition                  | Status     |
| -------------------------- | ---------- |
| Low TDS and Low Turbidity  | Good Water |
| Moderate TDS and Turbidity | Acceptable |
| High TDS or High Turbidity | Poor Water |

---

## User Interface

The TFT display presents:

* Project title banner
* Current TDS reading
* Current turbidity reading
* Color-coded measurement values
* Overall water quality status

### Color Indicators

| Color  | Meaning    |
| ------ | ---------- |
| Green  | Good       |
| Yellow | Acceptable |
| Red    | Poor       |

---

## Serial Output Example

```text
TDS: 245 ppm | Turbidity: 5 NTU
TDS: 372 ppm | Turbidity: 24 NTU
TDS: 712 ppm | Turbidity: 135 NTU
```

---

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/ESP32-Water-Quality-Monitor.git
```

### 2. Install Dependencies

Install all required libraries through the Arduino IDE Library Manager.

### 3. Configure Arduino IDE

* Select the ESP32 board.
* Choose the correct COM port.
* Verify the pin assignments if using different hardware.

### 4. Upload the Code

Compile and upload the firmware to the ESP32.

### 5. Monitor Readings

* Open Serial Monitor at **115200 baud**.
* Observe live sensor values on the TFT display.

---

## Future Enhancements

Potential improvements include:

* pH sensor integration
* Temperature sensor integration (DS18B20)
* SD card data logging
* Wi-Fi dashboard
* Cloud connectivity
* Mobile application support
* Historical trend visualization
* MQTT and IoT integration

---

## Applications

* Drinking water quality assessment
* Water filtration systems
* Aquaculture monitoring
* Environmental monitoring
* Educational and research projects
* Smart water management systems

---

## License

This project is distributed under the MIT License. Feel free to use, modify, and distribute it for personal, educational, or commercial purposes.

---


