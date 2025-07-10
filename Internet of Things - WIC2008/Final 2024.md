# Q1
![](../images/Pasted%20image%2020250707104734.png)
## Question 1

Part a) Difference between open-loop and closed-loop control systems

**Open-loop control system:**

- Operates without feedback from the output    
- The control action is independent of the system output
- Simpler design and less expensive
- Less accurate as it cannot correct for disturbances
- Examples: Toaster, washing machine timer, traffic light controller
    
**Closed-loop control system:**
- Uses feedback from sensors to compare actual output with desired output
- Can automatically correct errors in the system
- More complex design and more expensive
- More accurate and stable performance
- Examples: Thermostat-controlled heating system, cruise control in cars
    

Key differences:
1. Feedback: Open-loop has none, closed-loop uses feedback
2. Accuracy: Closed-loop is more accurate
3. Cost: Open-loop is generally cheaper
4. Complexity: Closed-loop is more complex
5. Disturbance handling: Closed-loop can compensate for disturbances
    

 Part b) Cloud Computing vs Fog Computing comparison table

|Feature|Cloud Computing|Fog Computing|
|---|---|---|
|Definition|Centralized computing resources delivered over the internet|Decentralized computing infrastructure between IoT devices and cloud|
|Location|Remote data centers|Near the edge of the network (closer to devices)|
|Latency|Higher latency due to distance|Lower latency as processing is closer|
|Bandwidth Usage|High bandwidth requirements|Reduced bandwidth needs|
|Security|Centralized security model|Distributed security model|
|Scalability|Highly scalable|Limited by edge devices|
|Cost|Operational expenses (pay-as-you-go)|Higher initial infrastructure cost|
|Real-time Processing|Not ideal for real-time applications|Better suited for real-time processing|

**IoT Applications Examples:**

1. **Cloud Computing Examples:**
    
    - _Smart Home Automation_: Cloud stores user preferences, usage patterns, and allows remote access from anywhere. Data from multiple homes can be aggregated for analytics.
        
        - Advantages: Centralized management, accessible from anywhere, scalable storage
            
        - Disadvantages: Latency in commands, requires constant internet connection
            
    - _Industrial IoT Predictive Maintenance_: Cloud analyzes data from factory equipment to predict failures and schedule maintenance.
        
        - Advantages: Powerful analytics, long-term data storage, global access
            
        - Disadvantages: Bandwidth intensive, potential data privacy concerns
            
2. **Fog Computing Examples:**
    
    - _Smart Traffic Lights_: Fog nodes process data from vehicle sensors and cameras locally to optimize traffic flow in real-time.
        
        - Advantages: Immediate response to changing conditions, works even if cloud connection is lost
            
        - Disadvantages: Limited processing power compared to cloud
            
    - _Healthcare Wearables_: Fog nodes process vital signs data locally and only send alerts to cloud when abnormalities are detected.
        
        - Advantages: Reduced data transmission, faster response to critical events
            
        - Disadvantages: More complex deployment, requires edge devices
# Q2
![](../images/Pasted%20image%2020250707104747.png)
![](../images/Pasted%20image%2020250707104801.png)
## Question 2

 Part a) Function of digital, analog and PWM pins on Arduino Uno

**Digital Pins:**
- Can be configured as either input or output
- Read or write binary values (HIGH/LOW, 1/0, 5V/0V)
- Typically used for buttons, LEDs, and digital sensors
- Pins 0-13 on Arduino Uno are digital pins
- Some digital pins (2,3) support external interrupts
    

**Analog Pins:**
- Can only be used as inputs by default (except some boards)
- Read analog voltage values (0-5V) with 10-bit resolution (0-1023)
- Used with analog sensors (potentiometers, light sensors, etc.)
- Pins A0-A5 on Arduino Uno are analog input pins
- Can be configured as digital pins if needed
    

**PWM Pins (Pulse Width Modulation):**
- Digital pins that can simulate analog output
- Work by rapidly switching between HIGH and LOW states
- Duty cycle determines the effective voltage
- Marked with ~ on Arduino Uno (pins 3,5,6,9,10,11)
- Used for dimming LEDs, controlling motor speed, etc.
    
Part b) Arduino code for button-controlled LED with connections

**Circuit Connections:**

- LED anode to digital pin 13 through a 220Ω resistor    
- LED cathode to GND
- Push button one leg to digital pin 2
- Push button other leg to 5V through a 10kΩ pull-down resistor
    
**Arduino Code:**

```cpp
const int buttonPin = 2;     // Push button connected to digital pin 2
const int ledPin =  13;      // LED connected to digital pin 13

int buttonState = 0;         // Variable for reading push button status

void setup() {
  pinMode(ledPin, OUTPUT);   // Initialize LED pin as output
  pinMode(buttonPin, INPUT); // Initialize push button pin as input
}

void loop() {
  buttonState = digitalRead(buttonPin); // Read the state of push button
  
  if (buttonState == HIGH) { // If button is pressed
    digitalWrite(ledPin, HIGH); // Turn LED on
  } else {
    digitalWrite(ledPin, LOW);  // Turn LED off
  }
}
```

```
5V O--->| |<----O GND
           | BUTTON  |
           |         |
           |         |
           +---------O Digital Pin 2
           |
          | |
          | | 10kΩ (Pull-down Resistor)
          |_|
           |
          ---
           |
          GND

      GND O--->| |<----O Digital Pin 13
           | LED     |
           |         |
           +---------O
           |
          | |
          | | 220Ω (Current-limiting Resistor)
          |_|
           |
        (To LED Anode)
```

```
Arduino
+-------------------------------------------------+
|                                                 |
|  5V  >----(One leg of PUSH BUTTON)              |
|                                                 |
|  GND >----(Cathode[-] of LED)                   |
|        |                                        |
|        +----(One end of 10kΩ RESISTOR)          |
|                                                 |
| Pin 2 >----(Other leg of PUSH BUTTON)           |
|        |                                        |
|        +----(Other end of 10kΩ RESISTOR)        |
|                                                 |
| Pin 13 >---(One end of 220Ω RESISTOR)----(Anode[+] of LED)
|                                                 |
+-------------------------------------------------+
```
Part c) Arduino code for potentiometer-controlled LED dimming with connections

**Circuit Connections:**

- LED anode to PWM pin 9 through a 220Ω resistor    
- LED cathode to GND
- Potentiometer outer pins to 5V and GND
- Potentiometer middle pin to analog input A0
    
**Arduino Code:**

```cpp
const int potPin = A0;    // Potentiometer connected to analog pin A0
const int ledPin = 9;     // LED connected to PWM pin 9

int potValue = 0;         // Variable to store potentiometer value
int ledValue = 0;         // Variable to store LED brightness value

void setup() {
  pinMode(ledPin, OUTPUT);  // Initialize LED pin as output
}

void loop() {
  potValue = analogRead(potPin); // Read potentiometer value (0-1023)
  ledValue = map(potValue, 0, 1023, 0, 255); // Map to PWM range (0-255)
  analogWrite(ledPin, ledValue); // Set LED brightness
  delay(10); // Small delay for stability
  
}
```
# Q3
![](../images/Pasted%20image%2020250707104822.png)
![](../images/Pasted%20image%2020250707104833.png)
![](../images/Pasted%20image%2020250707104850.png)

Question 3: Raspberry Pi Traffic Light Control

**Python Code for Traffic Light Control:**

```python
import RPi.GPIO as GPIO
import time

# Set up GPIO pins
GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)

# Define pin numbers
button_pin = 18
main_red = 6
main_yellow = 13
main_green = 19
ped_red = 16
ped_green = 20

# Setup pins
GPIO.setup(button_pin, GPIO.IN, pull_up_down=GPIO.PUD_UP)
GPIO.setup(main_red, GPIO.OUT)
GPIO.setup(main_yellow, GPIO.OUT)
GPIO.setup(main_green, GPIO.OUT)
GPIO.setup(ped_red, GPIO.OUT)
GPIO.setup(ped_green, GPIO.OUT)

# Initial state - main green, pedestrian red
GPIO.output(main_red, False)
GPIO.output(main_yellow, False)
GPIO.output(main_green, True)
GPIO.output(ped_red, True)
GPIO.output(ped_green, False)

try:
    while True:
        # Check if button is pressed
        if GPIO.input(button_pin) == False:
            # Only respond if main light is green
            if GPIO.output(main_green):
                # Change main light to yellow
                GPIO.output(main_green, False)
                GPIO.output(main_yellow, True)
                time.sleep(2)  # Yellow light duration
                
                # Change main light to red and pedestrian to green
                GPIO.output(main_yellow, False)
                GPIO.output(main_red, True)
                GPIO.output(ped_red, False)
                GPIO.output(ped_green, True)
                
                # Wait for pedestrian crossing time
                time.sleep(10)
                
                # Blink pedestrian green before changing
                for _ in range(5):
                    GPIO.output(ped_green, False)
                    time.sleep(0.5)
                    GPIO.output(ped_green, True)
                    time.sleep(0.5)
                
                # Return to initial state
                GPIO.output(ped_green, False)
                GPIO.output(ped_red, True)
                GPIO.output(main_red, False)
                GPIO.output(main_yellow, True)
                time.sleep(2)
                GPIO.output(main_yellow, False)
                GPIO.output(main_green, True)
                
        time.sleep(0.1)  # Small delay to debounce button

except KeyboardInterrupt:
    GPIO.cleanup()
```

**Explanation:**

1. The code initializes all the required GPIO pins - 3 for main traffic light, 2 for pedestrian light, and 1 for the button.    
2. The initial state sets main light to green and pedestrian light to red.
3. When the button is pressed (GPIO goes LOW due to pull-up resistor):
    - Main light changes from green to yellow for 2 seconds
    - Then changes to red while pedestrian light changes to green
    - After 10 seconds, pedestrian light blinks before switching back to red
    - Main light briefly shows yellow before returning to green
4. The system only responds when main light is green to prevent interruption during transition.
5. Includes debouncing and cleanup for proper operation.
# Q4
![](../images/Pasted%20image%2020250707104919.png)
## Question 4: IoT-based Security System

 a) Two important components

1. **Sensor: PIR Motion Sensor**    
    - Passive Infrared sensor detects movement by measuring infrared radiation
    - Detects when a human (or animal) moves within its range (typically 5-7 meters)
    - Low power consumption, suitable for continuous operation
    - Provides digital output (HIGH when motion detected)
    - Commonly used in security systems due to reliability and low cost
        
2. **Actuator: Siren/Alarm**
    - Audible alarm that activates when intrusion is detected
    - Can be paired with strobe lights for visual alert
    - Acts as both deterrent and notification mechanism
    - Can be programmed for different patterns (continuous, pulsed, etc.)
    - Should have backup power for reliability
        

b) System Design and Python Code

**System Components:**

1. PIR Sensor connected to SBC-PT (e.g., GPIO pin 4)    
2. Siren connected to SBC-PT (e.g., GPIO pin 17)
3. SBC-PT connected to network via DSL-Modem-PT
4. Notification service (email/SMS) through internet
    

**Python Code:**

python

```python
import RPi.GPIO as GPIO
import time
import smtplib
from email.mime.text import MIMEText

# GPIO Setup
GPIO.setmode(GPIO.BCM)
PIR_PIN = 4
SIREN_PIN = 17
GPIO.setup(PIR_PIN, GPIO.IN)
GPIO.setup(SIREN_PIN, GPIO.OUT)

# Email configuration

SMTP_SERVER = 'smtp.gmail.com'
SMTP_PORT = 587
EMAIL_ADDRESS = 'security@company.com'
EMAIL_PASSWORD = 'password'
RECIPIENT_EMAIL = 'security_team@company.com'

def send_alert():
    msg = MIMEText("Intruder detected at facility! Time: " + time.strftime("%Y-%m-%d %H:%M:%S"))
    msg['Subject'] = "SECURITY ALERT: Intruder Detected"
    msg['From'] = EMAIL_ADDRESS
    msg['To'] = RECIPIENT_EMAIL
    
    try:
        server = smtplib.SMTP(SMTP_SERVER, SMTP_PORT)
        server.starttls()
        server.login(EMAIL_ADDRESS, EMAIL_PASSWORD)
        server.send_message(msg)
        server.quit()
        print("Alert email sent")
    except Exception as e:
        print("Failed to send email:", str(e))

try:
    print("Security system activated")
    while True:
        if GPIO.input(PIR_PIN):
            print("Intruder detected!")
            # Activate siren
            GPIO.output(SIREN_PIN, True)
            
            # Send notification
            send_alert()
            
            # Keep siren on for 30 seconds
            time.sleep(30)
            GPIO.output(SIREN_PIN, False)
            
            # Add delay to prevent multiple detections
            time.sleep(10)
        
        time.sleep(0.1)

except KeyboardInterrupt:
    GPIO.cleanup()`
```

**System Operation:**

1. PIR sensor continuously monitors for motion
2. When motion is detected:
    - Siren is activated for 30 seconds
    - Email alert is sent to security team with timestamp
    - System enters brief cooldown period to prevent repeated alerts
3. Security team can check facility through connected cameras or dispatch personnel
4. System can be expanded with additional sensors (door/window contacts, glass break detectors)

# Q5
![](../images/Pasted%20image%2020250707104948.png)

## Question 5: Smart Farming System

### Part a) Block Diagram and Explanation

**Block Diagram Components:**

1. Soil Moisture Sensor → Arduino (Analog Input)
    
2. Temperature Sensor → Arduino (Analog Input)
    
3. Arduino Uno ↔ Raspberry Pi (Serial Communication/USB)
    
4. Raspberry Pi ↔ Wi-Fi Router (Ethernet/Wi-Fi)
    
5. Water Sprinkler → Relay Module → Arduino (Digital Output)
    

**Connections:**

- Sensors connect to Arduino for real-time data collection
    
- Arduino handles immediate control tasks
    
- Raspberry Pi provides network connectivity and remote access
    
- Data flows from sensors → Arduino → Raspberry Pi → Cloud/Remote Device
    

**Roles:**

- **Arduino Uno:**
    
    - Direct interface with sensors and actuators
        
    - Real-time data collection from analog sensors
        
    - Immediate control of water sprinklers based on thresholds
        
    - Low-power operation suitable for field deployment
        
- **Raspberry Pi:**
    
    - Network gateway for remote monitoring/control
        
    - Data logging and analysis
        
    - Web server for farmer's dashboard
        
    - Handles communication with cloud services
        
    - Can send SMS/email alerts
        

**Can we remove Raspberry Pi?**  
Yes, but with limitations:

- Arduino alone could handle basic functionality with Ethernet/Wi-Fi shield
    
- Would lose advanced features like remote access, data logging
    
- Limited user interface options
    
- More difficult to implement over-the-air updates
    
- No data backup if local storage fails
    

### Part b) Water Flow Control Component

**Component: Solenoid Valve with Flow Control**

- Electrically controlled valve that can regulate water flow
    
- Can be pulse-width modulated for precise flow control
    
- Available in various sizes for different pipe diameters
    
- Can be normally open or normally closed
    

**Integration into Block Diagram:**

1. Add between water supply and sprinklers
    
2. Connect to Arduino via digital output (or PWM for variable control)
    
3. Add relay module if valve requires higher voltage than Arduino can provide
    
4. Modify control logic to include flow rate adjustment
    

**Enhanced System Operation:**

- Farmer can set desired flow rate through mobile app
    
- Raspberry Pi sends flow rate setting to Arduino
    
- Arduino modulates valve opening to achieve desired flow
    
- Flow sensor (optional) can provide feedback for closed-loop control
    
- System can log water usage for conservation monitoring
    

**Example Arduino Code Addition:**

```CPP
// Add to existing smart farming code
const int flowValvePin = 6; // PWM pin connected to valve

void setWaterFlow(int percent) {
  int pwmValue = map(percent, 0, 100, 0, 255);
  analogWrite(flowValvePin, pwmValue);
}
```
This detailed answer covers all aspects of the exam questions with technical depth, practical implementations, and considerations for real-world IoT applications.