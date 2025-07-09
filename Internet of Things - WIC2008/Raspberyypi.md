Great! Let’s begin learning **Python for Raspberry Pi**, focusing on **IoT and hardware control** — especially useful for your exam and real-world projects.

---

## 🧠 What You'll Learn in Python for Raspberry Pi (Beginner IoT Focus)

### Core Areas:

1. **GPIO Pin Control** (input/output)
    
2. **Sensor Reading** (e.g., button, LDR)
    
3. **Actuator Control** (e.g., LED, buzzer, relay)
    
4. **PWM** (for dimming LED, controlling servo)
    
5. **Timers and loops**
    
6. **Libraries** (like `RPi.GPIO` and `gpiozero`)
    
7. **Basic communication (e.g., serial, I2C)**
    
8. **Project examples** (e.g., blink LED, button press counter, motion sensor alert)
    

---

## 🟢 1. **Basic Setup**

Install dependencies (only once):

```bash
sudo apt update
sudo apt install python3-gpiozero python3-rpi.gpio
```

---

## 🟡 2. **GPIO with `RPi.GPIO` (Low-Level Control)**

### ✅ Example: Blink an LED on pin 18

```python
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BCM)        # use GPIO numbering
GPIO.setup(18, GPIO.OUT)      # set pin 18 as output

while True:
    GPIO.output(18, GPIO.HIGH)  # LED ON
    time.sleep(1)
    GPIO.output(18, GPIO.LOW)   # LED OFF
    time.sleep(1)
```

🔚 Don’t forget:

```python
GPIO.cleanup()
```

> Call at the end of program or in `try/finally` to reset pins.

---

## 🔵 3. **Reading Input (e.g., Button)**

```python
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BCM)
GPIO.setup(17, GPIO.IN, pull_up_down=GPIO.PUD_UP)  # button with pull-up resistor

while True:
    if GPIO.input(17) == GPIO.LOW:  # button pressed
        print("Button Pressed")
    time.sleep(0.1)
```

---

## 🔴 4. **PWM (e.g., Dim LED)**

```python
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BCM)
GPIO.setup(18, GPIO.OUT)

pwm = GPIO.PWM(18, 1000)  # set PWM on pin 18 at 1kHz
pwm.start(0)

try:
    while True:
        for dc in range(0, 101, 5):
            pwm.ChangeDutyCycle(dc)  # increase brightness
            time.sleep(0.05)
except KeyboardInterrupt:
    pwm.stop()
    GPIO.cleanup()
```

---

## 🟣 5. **Using `gpiozero` Library (Simpler)**

```python
from gpiozero import LED, Button
from time import sleep

led = LED(18)
button = Button(17)

while True:
    button.wait_for_press()
    led.on()
    sleep(1)
    led.off()
```

> `gpiozero` handles setup/cleanup automatically. Great for beginners!

---

## 🧪 6. **Mini Project: Motion Sensor Alert (PIR)**

```python
from gpiozero import MotionSensor
import time

pir = MotionSensor(4)  # PIR sensor connected to GPIO 4

while True:
    pir.wait_for_motion()
    print("Motion Detected!")
    time.sleep(2)
```

---

## 🧰 7. **Useful Functions (Quick Reference)**

|Function/Module|Description|
|---|---|
|`GPIO.setmode()`|Set pin numbering mode (`BCM` or `BOARD`)|
|`GPIO.setup()`|Set pin as input/output|
|`GPIO.output()`|Write HIGH or LOW|
|`GPIO.input()`|Read pin state|
|`GPIO.PWM()`|Create PWM object|
|`gpiozero.LED(pin)`|Simplified LED control|
|`gpiozero.Button(pin)`|Simplified button input|
|`MotionSensor(pin)`|Used with PIR sensor|
|`pwm.ChangeDutyCycle(val)`|Change PWM duty (0–100)|
|`GPIO.cleanup()`|Reset GPIO settings|

---

## 🧠 Tips for Exam and Projects:

- Use **`gpiozero` for simple** programs, **`RPi.GPIO` for more control**.
    
- Know the **pin numbers**: BCM vs BOARD.
    
- Always clean up GPIO to avoid errors.
    
- Add **delays (sleep)** to debounce button presses or limit output speed.
    
- Practice writing your own mini-scripts for **LED + button**, **sensor + alert**, etc.
    

---

Would you like:

- **Code + wiring diagram** (e.g., Fritzing image)?
    
- A **practice quiz or mock coding question set**?
    
- More **project examples** like buzzer alerts, LCD display, or IoT dashboard integration?
    

Let’s build your confidence step-by-step!