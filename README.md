# Color Checker Sorting System
### BS Electrical Engineering – Spring 2022

This project is an embedded systems color-sorting mechanism built using an **Arduino Uno**, a **TCS3200 RGB color sensor**, a **servo motor**, and an **I2C LCD display**. The system detects the color of plastic checkers (red or black) and automatically sorts them using a servo-driven gate.

---

## ✨ Features

- **Real-time RGB color detection** using a TCS3200 sensor  
- **Calibration mode** to tune minimum/maximum pulse-width values  
- **Mapped RGB intensity values (0–255)** for reliable color thresholds  
- **Automated sorting mechanism** controlled by a servo motor  
- **LCD display feedback** for live color detection  
- **Serial monitor debugging** for fine-tuning thresholds and sensor behavior  
- **Failsafe "None detected" state** for uncertain readings

---

## 📡 Hardware Used

- Arduino Uno  
- TCS3200 / TCS230 RGB Color Sensor  
- SG90 / TowerPro Micro Servo  
- I2C 16×2 LCD Display  
- Assorted jumper wires  
- 5V power supply  
- Custom checker sorting chute / mechanical assembly

---

## 🔧 How It Works

### **1. Color Sensing**
The TCS3200 outputs frequency pulses based on detected color intensity.  
The Arduino reads:

- **Red pulse width**  
- **Green pulse width**  
- **Blue pulse width**

Each is measured using `pulseIn()` and mapped to 0–255 values using `map()` with calibration minima/maxima.

---

### **2. Classification Logic**

Checkers are classified based on measured RGB thresholds:

- **Red Checker:**  
  - High red value  
  - Lower green/blue values  
- **Black Checker:**  
  - Low red, green, and blue values

If neither range is met, the system outputs **"None"** and resets the servo.

---

### **3. Sorting Mechanism**

The servo rotates to one of three positions:

- `60°` → Release red checker  
- `150°` → Release black checker  
- `100°` → Default middle position

Servo angles differ depending on mechanical alignment and were tuned experimentally.

---

## 📟 Display Outputs

The I2C LCD shows:

- **"RED!"** when a red checker is detected  
- **"BLACK!"** when a black checker is detected  
- **"None"** when detection fails  

The serial monitor simultaneously prints exact RGB values for calibration and debugging.

---

## 🔬 Calibration Mode

The code contains a dedicated calibration block derived from DroneBot Workshop’s RGB sensor demo.

You can toggle behaviors by uncommenting either:

- **Calibration block**  
- **Normal sorting block**

This allowed fine-tuning of red/green/blue minimum and maximum values.

---

## 📁 Code Structure

- RGB reading functions  
  - `getRedPW()`  
  - `getGreenPW()`  
  - `getBluePW()`
- Value mapping and thresholding  
- Servo control  
- LCD output  
- Main loop handling detection + sorting

---

## 🚀 Future Improvements

- Add support for more colors  
- Use machine learning for color classification  
- Add conveyor-belt automation  
- Improve mechanical precision of sorting gate  
- Add 3D-printed enclosure

---

## 🙌 Acknowledgments

Calibration reference from **DroneBot Workshop (2020)**.  
LCD library from **Arduino-LiquidCrystal-I2C**.

---

