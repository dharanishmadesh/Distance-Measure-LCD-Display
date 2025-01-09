
# **Distance Meter Using Ultrasonic Sensor and LCD Display**

**Project Overview:**
This project utilizes an **HC-SR04 Ultrasonic Sensor** to measure distances in both **centimeters** and **inches**, displaying the results on a **16x2 LCD screen**. It continuously updates the distance, providing real-time measurements for any object in its range.

---

### **Components Used:**
- **HC-SR04 Ultrasonic Sensor** (for distance measurement)
- **16x2 LCD Display** (for visual output)
- **Arduino Uno/Nano/Compatible Board** (to control the components)

---

### **Key Features:**
- **Real-time Distance Measurement**: Displays the distance in **centimeters** and **inches**.
- **Continuous Updates**: The LCD updates the distance at regular intervals for live tracking.
- **Simple & Efficient**: Easily set up and works out of the box with minimal wiring and configuration.

---

### **Wiring Diagram:**

1. **HC-SR04 Ultrasonic Sensor:**
   - **VCC** → **5V**
   - **GND** → **GND**
   - **Trig Pin** → **Pin 10**
   - **Echo Pin** → **Pin 11**

2. **16x2 LCD:**
   - **VSS** → **GND**
   - **VDD** → **5V**
   - **V0** → **Adjustable Potentiometer** (for contrast)
   - **RS** → **Pin 6**
   - **EN** → **Pin 7**
   - **D4** → **Pin 5**
   - **D5** → **Pin 4**
   - **D6** → **Pin 3**
   - **D7** → **Pin 2**

---

### **Code Explanation:**
```cpp
#include <LiquidCrystal.h>

LiquidCrystal lcd(6, 7, 5, 4, 3, 2); // LCD setup
const int trigPin = 10;
const int echoPin = 11;
long duration;
int distanceCm, distanceInch;

void setup() {
  lcd.begin(16, 2); // LCD initialization
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
}

void loop() {
  // Trigger ultrasonic pulse
  digitalWrite(trigPin, LOW);
  delayMicroseconds(10);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH); // Measure pulse duration
  distanceCm = duration * 0.034 / 2; // Calculate distance in cm
  distanceInch = duration * 0.0133 / 2; // Calculate distance in inches

  // Display distance in cm and inches on the LCD
  lcd.setCursor(0, 0);
  lcd.print("Distance: ");
  lcd.print(distanceCm);
  lcd.print(" cm");
  delay(10);

  lcd.setCursor(0, 1);
  lcd.print("Distance: ");
  lcd.print(distanceInch);
  lcd.print(" inch");
  delay(10);
}
```

---

### **How It Works:**

1. **Ultrasonic Sensor**: 
   - The **Trig Pin** sends out a pulse, and the **Echo Pin** listens for the reflected pulse.
   - The time taken for the pulse to return is measured and used to calculate the distance.

2. **LCD Display**: 
   - The LCD screen shows the distance in both **centimeters** and **inches**, updating every 10ms for continuous feedback.

---

### **Example Output on the LCD:**
```
Distance: 50 cm
Distance: 19.7 inch
```

As the object moves, the distance updates accordingly on the LCD.

---

### **Improvements & Customizations:**
- **Buzzer/LED Indicator**: Add a buzzer or LED to alert when an object is within a certain range.
- **Switch Units**: Implement a button to toggle between metric (cm) and imperial (inches) units.
- **Enhanced Display**: Use larger fonts or add more information such as time of measurement.
- **Range Limitation**: Set a specific range for measuring or trigger actions based on the distance.

---

### **Applications:**
- **Proximity Sensing**: Detect nearby objects for automation or security systems.
- **Obstacle Avoidance**: Use for robots or vehicles that need to avoid obstacles.
- **Distance Measurement**: Can be used in measuring tools for various projects or DIY gadgets.

---


