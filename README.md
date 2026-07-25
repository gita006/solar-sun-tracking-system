# ☀️ Solar Tracking System using Arduino

## 📌 Project Overview

The **Solar Tracking System** is an Arduino-based IoT project designed to automatically rotate a solar panel towards the direction of maximum sunlight. The system uses **four Light Dependent Resistors (LDRs)** to detect the intensity of sunlight from different directions and a **servo motor** to align the panel accordingly. This helps improve the efficiency of solar energy collection compared to a fixed solar panel.

---

## 🚀 Features

* 🌞 Automatic sun tracking using four LDR sensors
* 🔄 Smooth servo motor movement for accurate positioning
* 💡 LED indication showing the darkest LDR direction
* 📊 Real-time LDR readings and servo angle displayed on the Serial Monitor
* ⚙️ Adjustable sensitivity using an error threshold
* 🔋 Low-cost and energy-efficient design

---

## 🛠️ Components Required

| Component                                |    Quantity |
| ---------------------------------------- | ----------: |
| Arduino Uno                              |           1 |
| Servo Motor (SG90/MG90S)                 |           1 |
| LDR (Light Dependent Resistor)           |           4 |
| 10kΩ Resistors                           |           4 |
| LEDs                                     |           4 |
| Breadboard                               |           1 |
| Jumper Wires                             | As required |
| Solar Panel (Optional for demonstration) |           1 |

---

## 🔌 Circuit Connections

### LDR Connections

| LDR          | Arduino Pin |
| ------------ | ----------- |
| Top Left     | A0          |
| Top Right    | A1          |
| Bottom Left  | A2          |
| Bottom Right | A3          |

### Servo Connection

| Servo Wire | Arduino Pin |
| ---------- | ----------- |
| Signal     | D9          |
| VCC        | 5V          |
| GND        | GND         |

### LED Connections

| LED          | Arduino Pin |
| ------------ | ----------- |
| Bottom Right | D11         |
| Bottom Left  | D10         |
| Top Right    | D6          |
| Top Left     | D3          |

---

⚙️ Working Principle

1. The four LDR sensors continuously measure the intensity of sunlight.
2. The Arduino reads the analog values from each LDR.
3. Average light values are calculated for:

   * Top
   * Bottom
   * Left
   * Right
4. The controller compares the left and right light intensities.
5. If the difference exceeds the predefined threshold, the servo motor rotates one step toward the brighter side.
6. The servo continues adjusting until both sides receive nearly equal light.
7. The LED corresponding to the darkest LDR turns ON, indicating the least illuminated sensor.
8. Every five seconds, the Arduino prints all LDR values and the current servo angle to the Serial Monitor.

---

📈 Algorithm

1. Initialize servo motor and LEDs.
2. Read analog values from all four LDRs.
3. Calculate:

   * Top Average
   * Bottom Average
   * Left Average
   * Right Average
4. Compute horizontal light difference.
5. If difference > threshold:

   * Rotate servo left or right.
6. Find the LDR with the lowest light value.
7. Turn ON the corresponding LED.
8. Display sensor readings on the Serial Monitor.
9. Repeat continuously.

---
 📋 Sample Serial Output

```text
LDR1=825 LDR2=810 LDR3=640 LDR4=620 Servo=94

LDR1=840 LDR2=835 LDR3=650 LDR4=630 Servo=95

LDR1=860 LDR2=855 LDR3=670 LDR4=655 Servo=96



▶️ How to Run

1. Clone this repository.
2. Open the `.ino` file in the Arduino IDE.
3. Install the **Servo** library (already included with the Arduino IDE).
4. Connect the Arduino according to the circuit diagram.
5. Select the correct board and COM port.
6. Upload the code.
7. Open the Serial Monitor at **9600 baud**.
8. Shine light on the LDRs and observe the servo tracking the brightest direction.
📸 Project Images

Hardware Setup

<img width="900" height="1600" alt="image" src="https://github.com/user-attachments/assets/2718d6d3-efb8-4c4b-bb5e-08d9d707992e" />

Circuit Diagram
<img width="1536" height="1024" alt="ChatGPT Image Jul 25, 2026, 08_03_07 PM" src="https://github.com/user-attachments/assets/c854cd6e-8e91-4706-b621-726b2ab8b440" />

🔮 Future Improvements

* Dual-axis solar tracking using two servo motors
* Real-time monitoring using NodeMCU (ESP8266/ESP32)
* IoT dashboard for remote monitoring
* Solar panel voltage and current measurement
* Battery charging status monitoring
* Weather data integration
* Mobile application for live monitoring

---

🎯 Applications

* Solar power plants
* Smart solar charging systems
* Renewable energy projects
* IoT and embedded system learning
* Engineering academic projects
* Research and prototype development

