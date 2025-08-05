
# IoT Challenge – Parking Occupancy Node & Energy Analysis

This repository contains the implementation and analysis for **IoT Challenge #1** of the *Internet of Things* course.  
The project focuses on developing a low-power parking occupancy sensor node using **ESP32**, **HC-SR04 ultrasonic sensor**, and **ESP-NOW protocol**, simulated in Wokwi.  
It includes detailed **power and energy consumption estimation** and **lifetime prediction**.

---

## 🚗 Project Overview
- **Objective:**  
  Detect parking slot occupancy and send the status ("FREE" / "OCCUPIED") to a central ESP32 sink node with minimal energy consumption.

- **Platform:**  
  - **ESP32 microcontroller**  
  - **HC-SR04 ultrasonic sensor** for distance measurement  
  - **ESP-NOW** for wireless communication  
  - **Wokwi** simulation environment

- **Energy-Saving Strategy:**  
  The node operates on a **duty cycle**:  
  1. Wake up from deep sleep every *X seconds*.  
  2. Measure distance.  
  3. Transmit status to sink node.  
  4. Return to deep sleep.

---

## ⚙ Implementation Details
1. **Sensor Readings:**  
   - Distance < 50 cm → **OCCUPIED**  
   - Distance ≥ 50 cm → **FREE**

2. **Communication:**  
   - Send status via ESP-NOW to a pre-defined MAC address of the sink node.

3. **Duty Cycle Calculation:**  
   - Based on leader person code `10904847`:  
     `X = (47 % 50) + 5 = 52 seconds`

4. **Energy Consumption Estimation:**  
   - Calculated average power for:
     - Deep Sleep
     - Idle
     - Transmission
     - Sensor Reading  
   - Estimated battery life with **Y = 4852 Joules**:
     - **1 cycle energy:** ~3.78 J  
     - **Battery lifetime:** ~1284 cycles (~0.77 days with 52s duty cycle)


**Proposed Improvements:**
1. Enter deep sleep mode as soon as possible after transmission.
2. Fine-tune delay times instead of fixed delays.
3. Reduce transmission power to save energy.

