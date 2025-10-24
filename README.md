# 🕊️ Ornithopter – Flapping Wing Mechanism

### Machine Design (ME205) Laboratory Project  
**IIT Ropar | Second Semester (2023–2024)**  
**Group C/11 (Friday)**  

**Submitted by:**  
- Sumit Yadav (2022MEB1352)  
- Sunny Bharti (2022MEB1353)  
- Tanish Goyal (2022MEB1356)  
- Tarini Magotra (2022MEB1358)  
- Tejasva Jindal (2022MEB1359)  

---

## 📘 Project Overview

An **ornithopter** is an aircraft that achieves flight by **flapping its wings**, mimicking the flight mechanism of birds and insects.  
Unlike fixed-wing aircraft that rely on continuous forward motion, an ornithopter generates **both lift and propulsion** through the oscillatory motion of its wings.

This project aimed to **design and construct a functional ornithopter mechanism** using **multiple four-bar linkages**, and to perform **velocity analysis** of its moving components.  

The entire model was designed and analyzed using **SolidWorks**, with a focus on mechanical design optimization and basic aerodynamic analysis.

---

## 🎯 Objectives

- Design and model an **ornithopter mechanism** using SolidWorks.  
- Perform **velocity analysis** of multiple links.  
- Study and analyze **airfoil performance** to optimize lift and thrust.  
- Develop a **gear train** for motion transmission.  
- Implement a **motor-driven flapping mechanism**.  
- Create a **lightweight and robust prototype** with 3D-printed components.

---

## 🧠 Work Breakdown (Weekly Progress)

**Week 1:**  
- Studied ornithopter mechanisms.  
- Designed individual links in SolidWorks for the flapping mechanism.  

**Week 2:**  
- Analyzed different airfoils (NACA series) to understand lift characteristics.  
- Designed gears based on module, addendum, and dedendum values.  

**Week 3:**  
- Rescaled the prototype.  
- Performed velocity analysis of linkage motion.  

**Week 4:**  
- Assembled the full system and tested mechanical motion.  

---

## ⚙️ Mechanical Design

### Gear Design
- **Type:** Spur gears (low friction and high efficiency).  
- **Number of Teeth:** 25  
- **Module:** 2 mm  
- **Pressure Angle:** 20°  
- **Pitch Circle Radius:** 50 mm  
- **Gear Reduction Ratio:** 8/25 (Driver/Driven)  

The reduction slows down the motor’s high RPM to match realistic wing-beat frequencies for efficient flapping.

---

### Linkage Design
- Multiple **four-bar linkages** were used to convert rotary motion into oscillatory flapping.  
- Iterative testing was performed to optimize link lengths and pivot distances for smooth, synchronized motion.

---

## 🪶 Airfoil Analysis

**Airfoil Chosen:** NACA 4404  

- Chosen for high lift-to-drag ratio and delay in stall onset.  
- Designed and simulated in **SolidWorks Flow Simulation**.  
- Low Reynolds number regime considered (based on low-speed flight assumption).  
- Roughness length factor: 0.1 m (agricultural terrain equivalent).  

**Key Finding:**  
At low-speed flight conditions, NACA 4404 provides stable lift with minimal flow separation — ideal for small-scale flapping mechanisms.

---

## ⚡ Electronics and Control

### Motor Selection
- **Type:** DC Motor  
- **Speed:** 48 RPM  
- **Torque:** ~5 N·m  
- Chosen to match mechanical load and flapping frequency.

### Arduino Code (Snippet)

```cpp
const int button1 = 9;
const int button2 = 8;
const int button3 = 7;
int en = 10;
int i1 = 11;
int i2 = 12;
int a = 100;

void setup() {
  pinMode(button1, INPUT_PULLUP);
  pinMode(button2, INPUT_PULLUP);
  pinMode(button3, INPUT_PULLUP);
  pinMode(en, OUTPUT);
  pinMode(i1, OUTPUT);
  pinMode(i2, OUTPUT);
  Serial.begin(9600);
  analogWrite(en, a);
  digitalWrite(i1, HIGH);
  digitalWrite(i2, LOW);
}

void loop() {
  int b1 = digitalRead(button1);
  int b2 = digitalRead(button2);
  int b3 = digitalRead(button3);
  if (b1 == LOW) { a = min(255, a + 50); }
  else if (b2 == LOW) { a = max(0, a - 50); }
  else if (b3 == LOW) { digitalWrite(i1, !digitalRead(i1)); digitalWrite(i2, !digitalRead(i2)); }
  analogWrite(en, a);
  delay(500);
}
