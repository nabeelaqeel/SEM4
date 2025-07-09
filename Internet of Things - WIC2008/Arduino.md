Great! Let’s get you started on **C++ for Arduino** – focusing on **important functions that might come out in exams**, with **examples and explanations**. This will be beginner-friendly, exam-focused, and Arduino-specific.

---

## 🧠 Key Concepts in Arduino C++

### 1. **Arduino Sketch Structure**

Every Arduino program (called a _sketch_) has two main functions:

```cpp
void setup() {
  // runs once when the board is powered on or reset
}

void loop() {
  // runs continuously after setup()
}
```

---

## 🔧 Essential Arduino C++ Functions (Exam-Relevant)

|Function|Purpose|
|---|---|
|`pinMode(pin, mode)`|Set a pin as input or output|
|`digitalWrite(pin, HIGH/LOW)`|Turn an output pin ON or OFF|
|`digitalRead(pin)`|Read HIGH or LOW from a digital input pin|
|`analogRead(pin)`|Read an analog value (0-1023) from an analog pin (A0–A5)|
|`analogWrite(pin, value)`|Write a PWM value (0-255) to simulate analog output|
|`delay(ms)`|Pause the program for a given time in milliseconds|
|`Serial.begin(baud)`|Start serial communication|
|`Serial.print()` / `Serial.println()`|Print text/values to Serial Monitor|
|`millis()`|Returns time since Arduino started (in ms) – used for timers|
|`attachInterrupt()`|Set an external interrupt on a digital pin|
|`noInterrupts()` / `interrupts()`|Disable/enable global interrupts|

---

## 🧪 Code Examples for Each Function

### 🟢 `pinMode()` + `digitalWrite()`

```cpp
void setup() {
  pinMode(13, OUTPUT);    // set pin 13 as output
}

void loop() {
  digitalWrite(13, HIGH); // turn LED ON
  delay(1000);            // wait 1 second
  digitalWrite(13, LOW);  // turn LED OFF
  delay(1000);
}
```

---

### 🟡 `digitalRead()`

```cpp
void setup() {
  pinMode(2, INPUT);       // button input
  pinMode(13, OUTPUT);     // LED
}

void loop() {
  int state = digitalRead(2);    // read button state
  digitalWrite(13, state);       // mirror state to LED
}
```

---

### 🔵 `analogRead()` (e.g., LDR sensor)

```cpp
void setup() {
  Serial.begin(9600);
}

void loop() {
  int light = analogRead(A0);   // read analog from A0
  Serial.println(light);        // print light value
  delay(500);
}
```

---

### 🔴 `analogWrite()` (PWM to dim LED)

```cpp
void setup() {
  pinMode(9, OUTPUT);
}

void loop() {
  for (int brightness = 0; brightness <= 255; brightness++) {
    analogWrite(9, brightness);  // increase brightness
    delay(10);
  }
}
```

---

### 🕒 `millis()` – better than `delay()`

```cpp
unsigned long previousTime = 0;

void setup() {
  pinMode(13, OUTPUT);
}

void loop() {
  if (millis() - previousTime >= 1000) {
    digitalWrite(13, !digitalRead(13)); // toggle LED
    previousTime = millis();
  }
}
```

---

### 🔌 `Serial.begin()`, `Serial.print()`

```cpp
void setup() {
  Serial.begin(9600);        // start serial at 9600 baud
}

void loop() {
  Serial.print("Temp: ");
  Serial.println(analogRead(A0));
  delay(1000);
}
```

---

### ⚡ `attachInterrupt()`

```cpp
volatile int counter = 0;

void setup() {
  pinMode(2, INPUT_PULLUP);
  attachInterrupt(digitalPinToInterrupt(2), count, FALLING);
  Serial.begin(9600);
}

void loop() {
  Serial.println(counter);
  delay(1000);
}

void count() {
  counter++;   // runs when pin 2 goes LOW
}
```

---

## 📊 Summary Table of Functions

|Function|Description|
|---|---|
|`pinMode(pin, mode)`|Configure a pin as INPUT, OUTPUT, or INPUT_PULLUP|
|`digitalWrite(pin, val)`|Write HIGH or LOW to a digital output pin|
|`digitalRead(pin)`|Read a digital pin (returns HIGH/LOW)|
|`analogRead(pin)`|Read analog input (0–1023)|
|`analogWrite(pin, val)`|Output PWM (0–255) on PWM-capable pins (e.g., 3, 5, 6, 9, 10, 11)|
|`delay(ms)`|Pause program for milliseconds|
|`millis()`|Time elapsed since board started (useful for non-blocking delays)|
|`Serial.begin(baud)`|Start Serial comm (use 9600, 115200, etc.)|
|`Serial.print()`|Print data without newline|
|`Serial.println()`|Print data with newline|
|`attachInterrupt()`|Set up external interrupts (digital pins 2 and 3 on Uno)|
|`noInterrupts()`|Temporarily disable interrupts|
|`interrupts()`|Re-enable interrupts|

---

## ✅ Tips for Exams:

- Always write `setup()` and `loop()` — they are mandatory.
    
- Know which pins support **PWM** (`analogWrite`).
    
- Be able to **read sensor input and control an output (LED, buzzer)**.
    
- Understand **non-blocking code** using `millis()` vs `delay()`.
    
- Know how to **print values to Serial Monitor** for debugging.
    

---

Would you like:

- A **mock Arduino exam with C++ coding questions**?
    
- **Circuit diagrams** for these codes?
    
- Notes in PDF format?
    

Let me know how you'd like to continue!

Here’s a comprehensive list of **commonly used C++ Arduino functions** (including both **basic** and **advanced** ones) that may come out in exams — grouped by category for easier understanding.

---

## 🧩 1. **Pin and IO Control**

|Function|Description|
|---|---|
|`pinMode(pin, mode)`|Set pin as `INPUT`, `OUTPUT`, or `INPUT_PULLUP`|
|`digitalWrite(pin, val)`|Write `HIGH` or `LOW` to digital output|
|`digitalRead(pin)`|Read `HIGH` or `LOW` from digital input|
|`analogRead(pin)`|Read analog voltage (0–1023) from analog input|
|`analogWrite(pin, val)`|Output PWM (0–255) to simulate analog voltage on PWM pin|

---

## 🕓 2. **Time Functions**

|Function|Description|
|---|---|
|`delay(ms)`|Pause for `ms` milliseconds (blocking delay)|
|`delayMicroseconds(us)`|Pause for `us` microseconds|
|`millis()`|Returns milliseconds since program started|
|`micros()`|Returns microseconds since program started|

---

## 🧠 3. **Interrupts**

|Function|Description|
|---|---|
|`attachInterrupt(pin, ISR, mode)`|Call ISR when condition met on pin (e.g., `RISING`, `FALLING`)|
|`detachInterrupt(pin)`|Disable the interrupt on the pin|
|`noInterrupts()`|Temporarily disable all interrupts|
|`interrupts()`|Re-enable interrupts|

---

## 🛠️ 4. **Serial Communication (Serial Monitor)**

|Function|Description|
|---|---|
|`Serial.begin(baud)`|Begin serial communication at given baud rate (e.g., 9600)|
|`Serial.print(val)`|Print data without newline|
|`Serial.println(val)`|Print data with newline|
|`Serial.read()`|Read next byte from serial buffer|
|`Serial.available()`|Returns number of bytes in buffer|
|`Serial.flush()`|Waits until all outgoing data is sent|

---

## 📟 5. **Communication Protocols (I2C, SPI)**

|Function|Description|
|---|---|
|`Wire.begin()`|Start I2C (for sensors like MPU6050, OLED displays)|
|`Wire.beginTransmission(address)`|Start transmission to I2C slave device|
|`Wire.write(data)`|Send data over I2C|
|`Wire.endTransmission()`|End I2C transmission|
|`Wire.requestFrom(address, count)`|Request data from I2C slave device|
|`SPI.begin()`|Start SPI (for SD cards, some displays)|
|`SPI.transfer(data)`|Send data via SPI|

---

## 📡 6. **PWM and Tone (Sound)**

|Function|Description|
|---|---|
|`analogWrite(pin, val)`|Write PWM signal (0–255)|
|`tone(pin, freq)`|Generate sound wave on pin at given frequency|
|`noTone(pin)`|Stop tone generation on the pin|

---

## 🧰 7. **Math & Utility**

|Function|Description|
|---|---|
|`map(x, in_min, in_max, out_min, out_max)`|Re-map value `x` from one range to another|
|`constrain(x, a, b)`|Limit value `x` between `a` and `b`|
|`abs(x)`|Absolute value|
|`pow(base, exp)`|Raise to power|
|`sqrt(x)`|Square root|
|`random(min, max)`|Generate random number in range|
|`randomSeed(seed)`|Seed the random number generator|

---

## 🔁 8. **Control Structures (Same as C++)**

|Structure|Purpose|
|---|---|
|`if`, `else`|Conditional branching|
|`switch`, `case`|Multi-condition branching|
|`for`|Counted loop|
|`while`|Loop while condition is true|
|`do...while`|Loop executes at least once|
|`break` / `continue`|Control loop flow|

---

## 🧩 9. **Other Useful Functions / Concepts**

|Function / Concept|Description|
|---|---|
|`setup()`|Runs once when the board starts|
|`loop()`|Runs continuously after `setup()`|
|`F("string")`|Store string in Flash memory (saves RAM)|
|`sizeof(var)`|Get number of bytes used by a variable|
|`PROGMEM`|Store large data (like text, images) in flash|

---

## 📝 Summary Table Format (Quick Exam Revision)

|Function|Category|Description|
|---|---|---|
|`pinMode()`|I/O Control|Set pin as input/output/input_pullup|
|`digitalWrite()`|I/O Control|Write HIGH or LOW to a pin|
|`analogRead()`|Analog Input|Read value (0–1023) from analog pin|
|`analogWrite()`|PWM Output|Output simulated analog using PWM|
|`delay()` / `millis()`|Timing|Blocking and non-blocking time control|
|`Serial.begin()`|Serial|Start communication with Serial Monitor|
|`attachInterrupt()`|Interrupts|React to changes on a digital input|
|`map()` / `constrain()`|Math|Rescale values / keep inside range|
|`tone()` / `noTone()`|Sound Output|Generate and stop tone on speaker|
|`Wire.begin()`|I2C|Begin I2C communication|
|`SPI.begin()`|SPI|Begin SPI communication|

---

Would you like me to generate:

- A **PDF printable cheatsheet**?
    
- **Flashcards** to test yourself?
    
- Code + **circuit diagrams** to go with these functions?
    

Let me know how you want to revise!