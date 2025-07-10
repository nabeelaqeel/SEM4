Great! Here's a **mock IoT Final Exam paper** based on your provided topics and format (4 questions, total 50 marks: 2 × 15 marks + 2 × 10 marks):

---

## **IoT Final Examination — Mock Paper**

**Duration**: 1 hour 30 minutes  
**Total Marks**: 50 marks  
**Instructions**:

- Answer **all four (4)** questions.
    
- Diagrams and code must be clearly labeled.
    
- You may use pseudocode where necessary but must show logic and structure.
    

---

### **Question 1 (15 marks)**

**Arduino LED and Sensor Control System**

You are tasked to design a simple IoT system using **Arduino Uno** to control an **LED based on a push button input** and display **analog values** from a **light-dependent resistor (LDR)**.

**a)** Write a complete **C++ Arduino code** that:

- Turns on the LED (connected to pin 13) **only when the push button (connected to pin 2)** is pressed.
    
- Reads the LDR value from **analog pin A0**, and prints it on the Serial Monitor.
    
- Includes a 500ms delay between readings.  
    _(8 marks)_
    

**b)** Draw the complete circuit diagram (label pin numbers, components, resistors).  
_(7 marks)_

---

### **Question 2 (15 marks)**

**Raspberry Pi Python GPIO Project**

You are using a **Raspberry Pi 4 Model B** to blink an LED connected to one of its **GPIO pins**.

**a)** Write a **Python script** using the `RPi.GPIO` library to:

- Blink an LED connected to GPIO17 (physical pin 11).
    
- The LED should turn on for 1 second and off for 1 second, in a loop.
    
- Include proper GPIO setup and cleanup code.  
    _(7 marks)_
    

**b)** Explain the use of **each of the following functions** in your script:

- `GPIO.setmode()`
    
- `GPIO.setup()`
    
- `GPIO.output()`
    
- `time.sleep()`
    
- `GPIO.cleanup()`  
    _(5 marks)_
    

**c)** Sketch the **circuit diagram** showing how the LED is connected to the Raspberry Pi.  
_(3 marks)_

---

### **Question 3 (10 marks)**

**Understanding Arduino I/O Functions**

Explain **what each of the following functions does**, and **give one example use case** for each in an Arduino application:

1. `pinMode()`
    
2. `digitalWrite()`
    
3. `digitalRead()`
    
4. `delay()`
    
5. `analogRead()`
    

_(2 marks each = 10 marks)_

---

### **Question 4 (10 marks)**

**IoT in BMC: Security and Implementation**

**a)** As an IoT systems engineer working on a **wireless attendance tracking system** for a smart building (BMC), list and explain **three key security measures** you would implement to protect user data and device communication.  
_(6 marks)_

**b)** Estimate the **basic cost to implement** a wireless attendance system for 100 employees using RFID or BLE. Provide cost of components (approx.), and state **what technology** you would recommend.  
_(4 marks)_

---

Let me know if you want the **answer key**, or if you'd like me to prepare a **PDF print version** or turn it into a **practice test sheet**.


Sure! Here are the **model answers** for the IoT mock exam questions:

---

## ✅ **Model Answers – IoT Final Exam**

---

### **Question 1 (15 marks)**

**Arduino LED and Sensor Control System**

**a) Arduino Code** _(8 marks)_

```cpp
const int buttonPin = 2;
const int ledPin = 13;
const int ldrPin = A0;

void setup() {
  pinMode(buttonPin, INPUT);
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int buttonState = digitalRead(buttonPin);
  int ldrValue = analogRead(ldrPin);

  if (buttonState == HIGH) {
    digitalWrite(ledPin, HIGH);
  } else {
    digitalWrite(ledPin, LOW);
  }

  Serial.print("LDR Value: ");
  Serial.println(ldrValue);
  delay(500);
}
```

**b) Circuit Diagram** _(7 marks)_  
🟩 **Describe this drawing if hand-drawn**, or recreate with simulation tools like Tinkercad.  
**Components**:

- LED: Anode → Pin 13 (via 220Ω resistor), Cathode → GND
    
- Button: One leg → Pin 2, Other leg → 5V via pull-down resistor (10kΩ), and GND
    
- LDR: One side → 5V, Other side → A0 with 10kΩ resistor to GND (voltage divider)
    

```
   5V
    |
   [LDR]
    |---------> A0
    |
  [10kΩ]
    |
   GND

Button:
 [Button]
   |   |
 Pin2 GND

LED:
 Pin13 --> [220Ω] --> Anode(LED) --> Cathode --> GND
```

---

### **Question 2 (15 marks)**

**Raspberry Pi Python GPIO Project**

**a) Python Code (RPi.GPIO)** _(7 marks)_

```python
import RPi.GPIO as GPIO
import time

LED_PIN = 17

GPIO.setmode(GPIO.BCM)
GPIO.setup(LED_PIN, GPIO.OUT)

try:
    while True:
        GPIO.output(LED_PIN, GPIO.HIGH)
        time.sleep(1)
        GPIO.output(LED_PIN, GPIO.LOW)
        time.sleep(1)
except KeyboardInterrupt:
    pass
finally:
    GPIO.cleanup()
```

**b) Function Explanations** _(5 marks)_

- `GPIO.setmode(GPIO.BCM)`: Uses Broadcom chip pin numbering (GPIO17 etc.)
    
- `GPIO.setup(pin, GPIO.OUT)`: Sets pin as output (can also be INPUT)
    
- `GPIO.output(pin, state)`: Sends HIGH or LOW to pin
    
- `time.sleep(x)`: Delays program by x seconds
    
- `GPIO.cleanup()`: Resets all GPIO pins used (good practice)
    

**c) Circuit Diagram** _(3 marks)_

- Raspberry Pi Pin 11 (GPIO17) → 220Ω resistor → LED anode
    
- LED cathode → GND (pin 6)
    

```
Raspberry Pi GPIO Pin 11 (GPIO17)
   |
 [220Ω]
   |
  Anode (LED)
   |
 Cathode
   |
  GND (Pin 6)
```

---

### **Question 3 (10 marks)**

**Understanding Arduino I/O Functions**

1. `pinMode(pin, mode)`
    
    - **Purpose**: Configures pin as INPUT or OUTPUT
        
    - **Example**: `pinMode(13, OUTPUT);` for LED
        
2. `digitalWrite(pin, value)`
    
    - **Purpose**: Sets pin HIGH or LOW
        
    - **Example**: `digitalWrite(13, HIGH);` to turn LED on
        
3. `digitalRead(pin)`
    
    - **Purpose**: Reads digital state (HIGH/LOW) from pin
        
    - **Example**: `int btn = digitalRead(2);` to check button
        
4. `delay(ms)`
    
    - **Purpose**: Pauses program for given milliseconds
        
    - **Example**: `delay(1000);` for 1-second pause
        
5. `analogRead(pin)`
    
    - **Purpose**: Reads analog voltage (0–1023) from analog pin
        
    - **Example**: `int val = analogRead(A0);` for LDR or temp sensor
        

---

### **Question 4 (10 marks)**

**IoT in BMC: Security and Implementation**

**a) Security Measures** _(6 marks)_

1. **Authentication**: Require login for attendance devices (RFID readers)
    
2. **Data Encryption**: Use TLS/SSL for wireless transmission to prevent sniffing
    
3. **Network Segmentation**: Isolate IoT devices on separate VLAN
    
4. **Firmware Updates**: Regular patching to prevent exploitation
    
5. **Logging & Alerts**: Track unusual activity for audit
    

**b) Cost and Technology** _(4 marks)_  
**Technology**: **RFID** preferred due to simplicity and lower power usage

**Estimated Cost for 100 users**:

- RFID Tags (cards): RM1 each × 100 = **RM100**
    
- RFID Readers: RM50 × 5 doors = **RM250**
    
- Microcontroller (ESP32): RM30 × 5 = **RM150**
    
- Server setup (local): RM300
    
- Misc (wiring, case, etc): RM100
    

**Total**: Around **RM900–RM1000**

---

Let me know if you want this in **PDF format**, or need help practicing using flashcards or coding challenges!

Great! Here's the **Second Set of Mock IoT Final Exam Questions** (Set 2) — still following your exam format: **4 questions = 2×15 marks + 2×10 marks = 50 marks total**.

---

## 📘 **IoT Final Examination — Mock Paper (Set 2)**

**Duration**: 1 hour 30 minutes  
**Total Marks**: 50 marks  
**Instructions**:

- Answer **all four (4)** questions.
    
- Label all diagrams and code clearly.
    
- Write neatly and show all working.
    

---

### **Question 1 (15 marks)**

**Arduino Fan Speed Monitor with Temperature Sensor**

You are designing a temperature-based fan controller using an **Arduino Uno** and **LM35 temperature sensor**. A **DC fan (simulated by an LED)** is turned on when the temperature exceeds 30°C.

**a)** Write a complete **C++ Arduino program** to:

- Read analog temperature from LM35 connected to pin A0
    
- Convert it to Celsius
    
- If temperature > 30°C, turn on fan (LED at pin 9); otherwise, turn it off
    
- Print temperature in °C on Serial Monitor  
    _(8 marks)_
    

**b)** Draw and label the full circuit diagram including LM35, LED, and resistors.  
_(7 marks)_

---

### **Question 2 (15 marks)**

**Python GPIO Project: Traffic Light Simulation**

Create a **traffic light system** using a Raspberry Pi and 3 LEDs (red, yellow, green) connected to GPIO pins.

**a)** Write a **Python program** to:

- Turn on green LED for 5 seconds
    
- Then yellow for 2 seconds
    
- Then red for 5 seconds
    
- Loop this cycle continuously  
    _(8 marks)_
    

**b)** List the **GPIO pin numbers used** and describe the **circuit connections** for each LED.  
_(4 marks)_

**c)** Suggest **one way to improve this project** using a sensor (e.g., motion or IR sensor).  
_(3 marks)_

---

### **Question 3 (10 marks)**

**Pin Functions Deep Dive (Arduino)**

Answer the following about basic Arduino functions:

1. What is the **difference** between `digitalRead()` and `analogRead()`?
    
2. When would you use `analogRead()` instead of `digitalRead()`?
    
3. What would happen if you **used `digitalWrite()` on an input pin**?
    
4. Why is `delay()` not recommended in some projects? Suggest an alternative.
    
5. What is `pinMode()` set to by default on most pins at startup?
    

_(2 marks each = 10 marks)_

---

### **Question 4 (10 marks)**

**BMC IoT System: Design Thinking**

You’ve been hired by a building management company to design a **smart energy monitoring system** using IoT.

**a)** As an IoT engineer, describe **3 data types** you would collect to monitor energy usage and how you would use them.  
_(6 marks)_

**b)** What **security risks** could this system face? Mention at least **2 risks** and how to mitigate them.  
_(4 marks)_

---

Would you like me to provide the **model answers** for this Set 2 next?

Here are the **model answers** for the **IoT Mock Final Exam – Set 2**:

---

## ✅ **Model Answers – Mock Exam Set 2**

---

### **Question 1 (15 marks)**

**Arduino Fan Speed Monitor with LM35 Sensor**

**a) Arduino Code** _(8 marks)_

```cpp
const int tempPin = A0;   // LM35 connected to A0
const int fanPin = 9;     // Fan/LED connected to pin 9

void setup() {
  pinMode(fanPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int analogValue = analogRead(tempPin);
  float voltage = analogValue * (5.0 / 1023.0);
  float temperatureC = voltage * 100.0;  // LM35 gives 10mV per °C

  Serial.print("Temperature: ");
  Serial.print(temperatureC);
  Serial.println(" C");

  if (temperatureC > 30.0) {
    digitalWrite(fanPin, HIGH);
  } else {
    digitalWrite(fanPin, LOW);
  }

  delay(1000);
}
```

**b) Circuit Diagram** _(7 marks)_  
🟢 **Components**:

- LM35:
    
    - Left pin → 5V
        
    - Middle pin → A0
        
    - Right pin → GND
        
- LED:
    
    - Anode → Pin 9 via 220Ω resistor
        
    - Cathode → GND
        

**ASCII Circuit (if drawing not available):**

```
[LM35]
 Vcc --- 5V
 OUT --- A0
 GND --- GND

[LED as Fan]
Pin 9 ---[220Ω]---|>|--- GND
```

---

### **Question 2 (15 marks)**

**Python GPIO Traffic Light Simulation**

**a) Python Code** _(8 marks)_

```python
import RPi.GPIO as GPIO
import time

red = 17
yellow = 27
green = 22

GPIO.setmode(GPIO.BCM)
GPIO.setup(red, GPIO.OUT)
GPIO.setup(yellow, GPIO.OUT)
GPIO.setup(green, GPIO.OUT)

try:
    while True:
        GPIO.output(green, True)
        time.sleep(5)
        GPIO.output(green, False)

        GPIO.output(yellow, True)
        time.sleep(2)
        GPIO.output(yellow, False)

        GPIO.output(red, True)
        time.sleep(5)
        GPIO.output(red, False)

except KeyboardInterrupt:
    pass

finally:
    GPIO.cleanup()
```

**b) GPIO Pin Numbers and Circuit Description** _(4 marks)_

- **Green LED** → GPIO22 (pin 15) via 220Ω resistor to GND
    
- **Yellow LED** → GPIO27 (pin 13)
    
- **Red LED** → GPIO17 (pin 11)
    
- Each LED’s cathode → GND
    

**c) Sensor Enhancement Suggestion** _(3 marks)_  
Use **IR sensor or ultrasonic sensor** to detect vehicles or pedestrians.  
**Example**: Extend green light duration if motion detected to reduce unnecessary delays.

---

### **Question 3 (10 marks)**

**Arduino Function Explanations**

1. **`digitalRead()` vs `analogRead()`**
    
    - `digitalRead()` reads **HIGH/LOW (0 or 1)** from digital pins.
        
    - `analogRead()` reads **voltage (0–1023)** from analog pins.
        
2. **Use Case for `analogRead()`**
    
    - When measuring **variable input** like temperature, light, or potentiometer voltage.
        
3. **`digitalWrite()` on an Input Pin**
    
    - May **not work** properly or could enable **internal pull-up**, causing unintended behavior.
        
4. **Why not use `delay()`?**
    
    - It blocks the program. Use **`millis()`** for non-blocking timing in multitask situations.
        
5. **Default `pinMode()` at Startup**
    
    - All pins are **set to INPUT** by default.
        

---

### **Question 4 (10 marks)**

**BMC IoT Smart Energy System**

**a) Three Data Types & Uses** _(6 marks)_

1. **Power Consumption (kWh)**: Monitor real-time energy usage by appliances
    
2. **Peak Usage Time**: Identify time periods with highest load for cost optimization
    
3. **Device Status**: Detect whether specific HVAC, lighting, or pumps are active
    

**b) Security Risks and Mitigation** _(4 marks)_

1. **Data Interception (Man-in-the-Middle Attack)**
    
    - _Mitigation_: Use **TLS/SSL encryption**, secure protocols like HTTPS, MQTT with TLS
        
2. **Device Compromise (Unauthorized Control)**
    
    - _Mitigation_: Implement **strong authentication**, use **firewalls**, and disable unused ports
        

---

Let me know if you want a **Set 3**, or if you'd like to practice **code tracing, MCQs**, or turn these into a **PDF practice worksheet**!