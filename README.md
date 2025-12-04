# Real-Time Fall Detection System (DE10-Lite FPGA)

**A synchronous sequential circuit implementation for real-time fall detection using the ADXL345 accelerometer.**

---

## 📖 Project Overview
This project implements a wearable monitoring device prototype on the Terasic DE10-Lite board (MAX 10 FPGA). It continuously monitors user movement data to detect specific kinematic signatures of a fall—specifically a period of free-fall followed immediately by a high-impact shock.

### Key Features
* **Custom I2C Master:** Written in VHDL to interface with the ADXL345 sensor.
* **DSP Logic:** Calculates Magnitude Squared ($A^2 = X^2 + Y^2 + Z^2$) for orientation-independent detection.
* **Failsafe FSM:** Monitoring $\to$ Countdown $\to$ Alarm state flow.
* **User Interface:** 30-second countdown on 7-Segment Displays and LED strobe warnings.

---

## 📂 Repository Structure
* **`src/`**: Contains all VHDL source files (`.vhd`).
  * `fall_detector_top.vhd`: Top-level entity.
  * `fall_detection_logic.vhd`: The core detection algorithm.
  * `i2c_master.vhd`: Serial protocol driver.
* **`docs/`**: Project Report (PDF) and block diagrams.
* **`quartus_project/`**: Pin assignments (`.qsf`) and bitstream (`.sof`).

---

## 📺 Demo 
A full video demonstration of the project is available here:
**[Google Drive: Demo Video](https://drive.google.com/drive/folders/1eEhtDU8e5RXOeQzP3CH7TExkWLTgeAB2?usp=sharing)**

---

## 🛠️ How to Run
1. **Software:** Intel Quartus Prime (Lite Edition).
2. **Hardware:** Terasic DE10-Lite (MAX 10 10M50DAF484C7G).
3. **Steps:**
   * Create a new Quartus project and add all files from `src/`.
   * Set `fall_detector_top.vhd` as the Top-Level Entity.
   * Import pin assignments (ensure I2C pins map to `GSENSOR_SDI`/`SDO`/`CS_N`/`SCLK`).
   * Compile and program the board using USB Blaster.

---

## 📚 References
1. Analog Devices ADXL345 Datasheet.
2. Terasic DE10-Lite User Manual.
3. Scott Larson (DigiKey) for the base I2C Master logic.

## 🌟 Support
If you found this project helpful or interesting, please consider giving this repository a **Star**! ⭐
