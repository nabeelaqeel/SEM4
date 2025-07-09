# W10

> [!NOTE]- Blink the LED - python
> ```python
> # Import the GPIO modules to control the GPIO pins of the Raspberry Pi
> import RPi.GPIO as GPIO
> # Set the desired pin numbering scheme:
> GPIO.setmode(GPIO.BCM)
> 
> 
> # GPIO PIN where the LED is connected 
> #  pin numbering based on the BCM scheme
> LEDPin = 17
> 
> # Setup the direction of the GPIO pin - either INput or OUTput 
> GPIO.setup(LEDPin, GPIO.OUT)
> 
> import time
> 
> for i in range(5):
>     print("ON")
>     GPIO.output(LEDPin, True)
>     time.sleep(1)
>     print("OFF")
>     GPIO.output(LEDPin, False)
>     time.sleep(1)
> ```

> [!NOTE]- Connecting to Webex -python
> ```python
> #Step 1: Get Webex Teams API Token Key
> 
> # Define a local variable in Python that will hold our Authentication API KEY:
> 
> APIAuthorizationKey = 'Bearer YjcxZDkxMTItMWFhMy00NjQ1LTxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';
> 
> #Step 2: Import the needed Python modules
> 
> import requests
> import json
> import time
> 
> # Step 3: Access the API Endpoints - rooms
> 
> 
> # Using the requests library, create a new HTTP GET Request against the Webex Teams API Endpoint for Webex Teams Rooms:
> #  the local object "r" will hold the returned data:
> r = requests.get(   "https://api.ciscospark.com/v1/rooms",
>                     headers={'Authorization':APIAuthorizationKey}
>                 )
> 
> # Check if the response from the API call was OK (resp. code 200)
> if(r.status_code != 200):
>     print("Something wrong has happened:")
>     print("ERROR CODE: {} \nRESPONSE: {}".format(r.status_code, r.text))
>     assert()
>     
> # See what is in the JSON data:
> 
> jsonData = r.json()
> 
> print(
>     json.dumps(
>         jsonData,
>         indent=4
>     )
> )
> 
> rooms = r.json()['items']
> for room in rooms:
>     print ("Room name: '" + room['title'] + "' ID: " + room['id'])
>     
> # Replace contents of this varialble with a real room name from your Webex Teams account
> roomNameToSearch = 'Jozef'
> 
> # Define a variable that will hold the roomId 
> roomIdToMessage = None
> 
> rooms = r.json()['items']
> for room in rooms:
>     #print "Room name: '" + room['title'] + "' ID: " + room['id']
>     if(room['title'].find(roomNameToSearch) != -1):
>         print ("Found rooms with the word " + roomNameToSearch)
>         print ("Room name: '" + room['title'] + "' ID: " + room['id'])
>         roomIdToMessage = room['id']
>         roomTitleToMessage = room['title']
>         break
> 
> if(roomIdToMessage == None):
>     print("Did not found any room with " + roomNameToSearch + " name in it.")
> else:
>     print("A valid room has been found and this is the room id: " + roomIdToMessage)
>     
> print(roomIdToMessage)
> 
> # Step 4 : Access the API Endpoints - messages
> 
> # define the mandatory or optional GET parameters for the `messages` API endpoint:
> getMessagesUrlParameters = {
>             # mandatory parameter - the room ID
>             "roomId": roomIdToMessage,
>             # optional parameter - number of the last messages to return
>             "max": 8
> }
> 
> # Using the requests library, create a new HTTP GET Request against the Webex Teams API Endpoint for Webex Teams Messages:
> #  the local object "r" will hold the returned data:
> r = requests.get(   "https://api.ciscospark.com/v1/messages",
>                     params=getMessagesUrlParameters,
>                     headers={'Authorization':APIAuthorizationKey}
>                 )
> 
> if(r.status_code != 200):
>     print("Something wrong has happened:")
>     print("ERROR CODE: {} \nRESPONSE: {}".format(r.status_code, r.text))
>     assert()
> 
> # See what is in the JSON data:
> 
> jsonData = r.json()
> 
> print(
>     json.dumps(
>         jsonData,
>         indent=4
>     )
> )
> 
> messages = jsonData['items']
> for message in messages:
>     print("Message: " + message['text'])
>     if(message['text'] == '/Turn On'):
>         messageId = message['id']
>         print("Found a command message to TURN ON the LED!")
>         break
>     if(message['text'] == '/Turn Off'):
>         messageId = message['id']
>         print("Found a command message to TURN OFF the LED!")
>         break
> 
> #Step 5: Continuos loop for new messages
> 
> lastMessageId = None
> 
> while True:
>     # the code should not hammer the API service with too many reqeuests in a short time
>     #  to limit the number of requests in the while loop, begin with a short 1 second delay:
>     time.sleep(1)
>     print("Next iteration is starting ...")
>     
>     # define the mandatory or optional GET parametrs for the `messages` API endpoint:
>     getMessagesUrlParameters = {
>                 # mandatory parameter - the room ID
>                 "roomId": roomIdToMessage,
>                 # optional parameter - number of the last messages to return
>                 #  only interested in the very last message in the room
>                 #   thefore max = 1
>                 "max": 1
>     }
> 
>     # Using the requests library, creare a new HTTP GET Request against the Webex Teams API Endpoint for Webex Teams Messages:
>     #  the local object "r" will hold the returned data:
>     r = requests.get(   "https://api.ciscospark.com/v1/messages",
>                         params=getMessagesUrlParameters,
>                         headers={'Authorization':APIAuthorizationKey}
>                     )
>     if(r.status_code != 200):
>         print("Something wrong has happened:")
>         print("ERROR CODE: {} \nRESPONSE: {}".format(r.status_code, r.text))
>         assert()
>     
>     
>     # Store the json data from the reply
>     jsonData = r.json()
>     
>     # Get the items (array of messages) from the jsonData.
>     messages = jsonData['items']
>     # since the request specified max=1, only one message should be returned:
>     message  = messages[0]
>     
>     # Verify if this is a new message:
>     if(lastMessageId == message['id']):
>         #this is the same message as before, no new messages
>         print("No New Messages.")
>     else:
>         # this is a new message, its ID is different from the one in the previous iteration
>         print("New Message: " + message['text'])
>         # save the message id for the next iteration:
>         lastMessageId = message['id']
>         if(message['text'] == '/Turn On'):
>             messageId = message['id']
>             print("Found a command message to TURN ON the LED!")
>             # Turn on the LED:
>             GPIO.output(LEDPin, True)
>             #break
>         if(message['text'] == '/Turn Off'):
>             messageId = message['id']
>             print("Found a command message to TURN OFF the LED!")
>             # Turn off the LED:
>             GPIO.output(LEDPin, False)
>             #break
> ```

# W11

> [!NOTE]- Task 1: Set up an MongoDB User Account for a Cloud MongoDB Database
> ```python
> # Install pymongo
> !pip install pymongo dnspython
> 
> # Import the MongoClient acts as a client from Python to MongoDB
> from pymongo import MongoClient
> 
> # Import the pprint library
> from pprint import pprint
> 
> #Ignore warnings
> import warnings
> warnings.filterwarnings('ignore')
> 
> #Paste the URI connection string and replace Password with new user password
> mongoURI="!!! Paste your URI connection string here !!!"
> 
> # CONNECT TO THE ONLINE MONGO DATABASE
> client = MongoClient(MongoURI)
> 
> # LOAD THE COLLECTION OF "DOCUMENTS" (AKA. JSON FORMAT)
> # Replace database with your database name 
> # Replace collection with your collection name
> 
> db_collection = client.database.collection
> 
> print("\n\n ------ THE CURRENT STATUS -------")
> # FIND THE FIRST MATCH
> found=db_collection.find_one({"alarm": 'True'})
> if found is None:
>     alarm_status='False'
> else:
>     alarm_status=found['alarm']
> print('Current State = ', alarm_status)
> 
> # UPDATE THE DB HERE
> # SET NEW SEARCH VARIABLE
> if alarm_status == 'True':
>     db_collection.replace_one({'alarm':'True'},{'alarm':'False'})
>     new_find='False'
> else:
>     db_collection.replace_one({'alarm':'False'},{'alarm':'True'})
>     new_find='True'
> 
> print('\n\n New Status')
> pprint(db_collection.find_one())
> print('\n\n ------ SET THE VARIABLE -------')
> 
> # RE-FIND THE FIRST MATCH USING THE new_find VARIABLE SET ABOVE
> found=db_collection.find_one({"alarm": new_find})
> alarm_status=found['alarm']
> print('Sound the Alarm = ', alarm_status)
> ```

> [!NOTE]- Task 3: Software to Connect the Dots
> ```python
> # Import the GPIO modules to control the GPIO pins of the Raspberry Pi
> import RPi.GPIO as GPIO
> 
> # Import the json module to work with JSON encoded objects
> import json
> 
> # Import the time module to control the timing of your application (e.g. add delay, etc.)
> import time
> 
> # LED LIGHTS PIN NUMBERS (GPIO PIN using BCM scheme)
> GPIO.setmode(GPIO.BCM)
> GreenLEDPin = 20
> RedLEDPin = 21
> # SET PIN MODE TO SEND POWER OUT
> GPIO.setup(GreenLEDPin, GPIO.OUT)
> GPIO.setup(RedLEDPin, GPIO.OUT)
> 
> for i in range(2):
>     print("ON")
>     GPIO.output(GreenLEDPin, True) # True = set 3.3V on the pin
>     GPIO.output(RedLEDPin, True) # True = set 3.3V on the pin
>     time.sleep(1)
>     print("OFF")
>     GPIO.output(GreenLEDPin, False) # False = set 0V on the pin
>     GPIO.output(RedLEDPin, False) # False = set 0V on the pin
>     time.sleep(1)
>     
> print("Started the factory Emergency Shutdown system ...")
> 
> # LOOP FOREVER
> while True:
> # FIND THE FIRST MATCH
>     found = db_collection.find_one({"alarm": 'True'})
>     if found is None:
>         alarm_status = 'False'
>     else:
>         alarm_status = found['alarm']
>     if alarm_status == 'True':
>         print("RUN!!! RUN!! RUN!!")
>         GPIO.output(GreenLEDPin, False)
>         GPIO.output(RedLEDPin, True)
>     else:
>         print("All Clear")
>         GPIO.output(GreenLEDPin, True)
>         GPIO.output(RedLEDPin, False)
>     # wait one second before the next iteration
>     time.sleep(1)
>     
> # IF YOU ARE THE EMERGENCY SIGNAL SENDER
> # AKA THE BUTTON PUSHER !!
> 
> print("\n\n ------ THE CURRENT DB STATUS -------")
> # FIND THE FIRST MATCH
> found = db_collection.find_one({"alarm": 'True'})
> if found is None:
>     alarm_status = 'False'
> else:
>     alarm_status = found['alarm']
> print('STORED DB STATUS = ', alarm_status)
> # END MONGO DB CONNECTION TEST
> 
> ########################################################################
> # RED PANIC EMERGENCY button PIN NUMBER (GPIO PIN using BCM scheme)
> GPIO.setmode(GPIO.BCM)
> buttonPin = 21
> 
> # SET PIN MODE TO READ INPUT
> GPIO.setup(buttonPin, GPIO.IN)
> 
> # READ THE VOLTAGE ON THE PIN
> # POSITIVE VOLTAGE = TRUE BUTTON STATE = BUTTON IS CURRENTLY PRESSED
> buttonState = previousItterationButtonState = GPIO.input(buttonPin)
> 
> print("Button state is: " + str(buttonState))
> print("Try to press the button...")
> 
> push_count = 0
> while True:
>     buttonState = GPIO.input(buttonPin)
>     # CHECK IF THE CURRENT STATE = THE PREVIOUS STATE
>     if(buttonState != previousItterationButtonState):
>         push_count = push_count + 1
>         print("Button change. New state is: " + str(buttonState))
>     # UPDATE CURRENT STATE
>     previousItterationButtonState = buttonState
>     if push_count >= 2:
>         break
> print("Exiting Loop, and ...")
> 
> print("Press and hold the button to simulate an emergency alarm ...")
> print("Started the factory Control system ...")
> 
> buttonState = previousItterationButtonState = GPIO.input(buttonPin)
> while True:
>     buttonState = GPIO.input(buttonPin)
>     if(buttonState != previousItterationButtonState):
>     # CONVERT BUTTON STATE TO BOOLEN VALUE (1=True, 0=False)
>         alarmValue = True if buttonState == 1 else False
>         print("Button change. New state is: " + str(buttonState) + " and alarm is: " + str(alarmValue))
>         # UPDATE THE DB HERE
>         if alarmValue == True:
>             db_collection.replace_one({'alarm':'False'},{'alarm':'True'})
>             print('Updating DB Status to True')
>         else:
>             db_collection.replace_one({'alarm':'True'},{'alarm':'False'})
>             print('Updating DB Status to False')
>         # UPDATE CURRENT STATE
>         previousItterationButtonState = buttonState
> ```

# W13
## Lab: Record sunrise and sunset in Google Calendar using IFTTT

> [!NOTE]- Task 3: Software to connect to dots : bash
> ```bash
> 
> %%bash
> # ^^^ The commands below are to be executed as Linux Bash commands. 
> # You can get the same output by opening a terminal connection to the device and executing these commands manually.
> 
> dmesg | grep -v disconnect | grep -Eo "tty(ACM|USB)." | tail -1
> ```

> [!NOTE]- Task 3: Advance Bash
> ```bash
> %%bash
> # ^^^ The commands below are to be executed as Linux Bash commands. 
> # You can get the same output by opening a terminal connection to the device and executing these commands manually.
> 
> for sysdevpath in $(find /sys/bus/usb/devices/usb*/ -name dev); do
>     (
>         syspath="${sysdevpath%/dev}"
>         devname="$(udevadm info -q name -p $syspath)"
>         [[ "$devname" == "bus/"* ]] && continue
>         eval "$(udevadm info -q property --export -p $syspath)" 2>/dev/null
>         [[ -z "$ID_SERIAL" ]] && continue
>         echo "/dev/$devname - $ID_SERIAL"
>     )
> done
`

> [!NOTE]- Task 3 : python
> ```python
> import pyfirmata  # RPi to Arduino over the Firmata serial communication library
> import time       # time.sleep(int seconds)
> import requests   # web http requests library
> 
> # copy here your personal Maker Secret Key from https://ifttt.com/maker
> #  e.g.: iFTTTMakerSecretKey = "lBX_vJGs2xa******************P7bakzuQq"
> iFTTTMakerSecretKey = "lBX_vJGs2xa******************P7bakzuQq"
> # The IFTTT Maker Channel URLs as configured in your IFTTT recipes for SunRise and SunSet
> iFTTTSunRiseURL = "https://maker.ifttt.com/trigger/SunRise/with/key/" + iFTTTMakerSecretKey
> iFTTTSunSetURL  = "https://maker.ifttt.com/trigger/SunSet/with/key/"  + iFTTTMakerSecretKey
> 
> # set the initial value of the lightSensorValue variable which holds the value read from the sensor
> lightSensorValue = 0
> # threshold number differenciating light from dark - e.g. sunrise from sunset 
> 
> lightSensorValueThreshold = 500
> 
> # define an Arduino board connected as a /dev/ttyXXXX device:
> arduinoBoard = pyfirmata.Arduino('/dev/ttyUSB0')
> #                               ^^^^^^ set this with the ttyACM0 or ttyUSB0 name of your Arduino device
> 
> # start the communication between the RPi and Arduino using the Firmata serial protocol
> arduinoReader = pyfirmata.util.Iterator(arduinoBoard) 
> arduinoReader.start()
> 
> # map the lightSensorInputAnalogPin variable to a physical Analog (a) Pin Number 0 (0) as an Input (i)
> lightSensorInputAnalogPin = arduinoBoard.get_pin("a:0:i")
> 
> # before reading the very first input values from the Arduino, wait at least one second
> #  this is needed to initialize the communication, for once we read the input, the values are valid 
> time.sleep(1)
> 
> # this variable holds the value of previous state
> previousStateOfLight = None
> # loop forever
> while True:
>     # once we read the analog input pin value, normalize it from the returned values <0.0,1.0> to <0,1023>
>     lightSensorValue = round((lightSensorInputAnalogPin.read() or 0) * 1023)
>     print ("The current light value = " + str(lightSensorValue))
>     # the ineresting logic starts here:
>     #  once a threshold value is reached with the current measurement, check what was the previous state
>     #  based on a previous state, if needed, trigger an action - update a calendar
>     if(lightSensorValue > lightSensorValueThreshold):
>         if(previousStateOfLight == False):
>             print ("SunRise is here!")
>             # using the requests library, execute an HTTP GET request for the specified URL 
>             r = requests.get(iFTTTSunRiseURL)
>             # if the status_code is different from 200, something went wrong:
>             print ("The resulting HTTP GET status code was " + str(r.status_code))
>             # update the state of the previousStateOfLight variable with the current state 
>         previousStateOfLight = True
>     else:
>         if(previousStateOfLight == True):
>             print ("SunSet is here!")
>             # using the requests library, execute an HTTP GET request for the specified URL 
>             r = requests.get(iFTTTSunSetURL)
>             # if the status_code is different from 200, something went wrong:
>             print ("The resulting HTTP GET status code was " + str(r.status_code))
>         # update the state of the previousStateOfLight variable with the current state 
>         previousStateOfLight = False
>     # be nice - it is not worth to use the whole CPU just to have precisions at miliseconds level
>     #  by running the loop itterations as fast as possible 
>     # pause this loop for at least one second
>     time.sleep(1)
> ```

