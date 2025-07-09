# L1- Things and Connections

### The Internet of Things
- The Presence of IoT in Today's World
	• The IoT is all around us.
	• The IoT helps individuals to improve quality of life.
	• The IoT also helps industries to become more efficient.
- Cisco IoT Solutions
	• The rapid IoT growth has introduced new challenges.
	• Cisco IoT System reduces the complexities of digitization.
	• Six Pillars of the Cisco IoT System are:
		• Network Connectivity
		• Fog Computing
		• Cybersecurity and Physical Security		
		• Data Analytics
		• Management and Automation
		• Application Enablement Platform

### Building Blocks of an IoT System
 - Overview of a Controlled System

	• Feedback loops are used to provide real-time information to its controller based on current behavior.
	• In a closed loop, feedback is continuously being received by the controller from its sensors.
	• The controller continuously analyzes and processes information, and use actuators to modify conditions.

 - Sensors
	• A sensor is a device that can be used to measure a physical property bydetecting some type of information from the physical world.
	• A sensor may be connected to a controller either directly or remotely.
- ![](../images/Pasted%20image%2020250709101214.png)

- Actuators
	• An actuator is a basic motor that can be used to control a system.
	• Can be hydraulic, electric or pneumatic.
	• can be responsible for transforming an electrical signal into physical output.

- Controllers
	• Responsible for collecting data from sensors and providing network connectivity.
	• Controllers may have the ability to make immediate decisions.
	• May also send data to remote and more powerful computer for analysis.

- IoT Process Flow
	• A simple IoT system include sensors connecting, through a wireless or wired connection, to actuators or controllers.
	• Some devices can have more than one function.

### Processes in Controlled Systems
- Processes
	• A process is a series of steps or actions taken to  achieve a desired result by the consumer of the process.

- Feedback
	• Feedback is when the output of a process affects the input.
	• Feedback is often referred to as a feedback loop.
	• Feedback loops can be positive or negative.

- Control Systems

	• Includes a controller that uses inputs and outputs to manage and regulate the behavior Of the system in an attempt to achieve a desired state.
	• The controlled portion of the system is often called the plant.
	• Choosing the adjustments to apply to a plant to achieve a desired output is called control theory.
	• Control theory is applied to many systems, including driving a car.

- Open-Loop Control Systems
	• Open-loop control systems do not use feedback.
	• The plant performs a predetermined action without any verification of the desired results.
	• Open-loop control systems are often used for simple processes.
	
-  Closed-Loop Control Systems
	• A closed-loop control system uses feedback to determine whether the collected output is the desired output.
	• The result is then fed back into a controller to adjust the plant for the next iteration of output, and the process repeats.
- ![](../images/Pasted%20image%2020250709101524.png)
- Closed-Loop Controllers

	• There are many types of closed-loop controllers:
		• Proportional controllers (P): based on the difference between the measured output and the desired output.
		• Integral controllers (PI): use historical data to measure how long the system has deviated from the desired output.
		• Proportional, Integral and Derivative controllers (PID): include data about how quickly the system is approaching the desired output.
		• PID controller is an efficient way to implement feedback control.
		• The Arduino and Raspberry Pi devices can be used to
		implement PID controllers.

- Interdependent Systems

	• Most systems have many interdependent pieces contributing to and affecting the output.

# L2 - What are Connections?
-  Models of Communication
	• Layered networking models are used to illustrate how a network operates. Benefits include:
		• Assists in protocol design.
		• Fosters competition.
		• Promotes technology or capability independence.
		• Provides a common language to describe networking
		functions and capabilities.
	- ![](../images/Pasted%20image%2020250709102157.png)
	- Standardization

		• The challenge for the IoT is to ensure these emerging IoT devices can connect securely and reliably to the Internet and to each other.
		• Consistent, secure, and commonly recognized technologies and standards is needed.
		• Organizations such as the Industrial Internet Consortium, OpenFog Consortium, and the Open Connectivity Foundation, are helping to develop standard architectures and frameworks.
	- TCP and OSI Models
		• Both OSI and TCP/IP models are used to describe network connections and often used interchangeably.
		• The TCP/IP model is commonly referred to as the Internet model.
		• The OSI model provides an extensive list of functions and services that can occur at each layer.

	 - IoT World Forum Reference Model
		• Developed as a common framework to guide and to help accelerate IoT deployments.
		• It’s intent is to provide common terminology and help
		 clarify how information flows and is processed for a unified IoT industry.
		 
	- Simplified IoT Architecture
		• Several architectures exist to help facilitate the design and creation of IoT systems.
		
		• The OSI model, TCP/IP model, and the IoT World
		 Forum Reference model have been presented as examples.
		
		• A simpler approach is based on connection levels
		The levels are:
			• Device-to-Device
			• Device-to-Cloud
			• Device-to-Gateway-to-Cloud
			• Device-to-Gateway-to-Cloud-to-Application
		- ![](../images/Pasted%20image%2020250709102550.png)

### Layers of Connections
- Connections Within Networks
		• Connections can have different contexts.
		• Power connections, circuit connections or network connections.

- Physical Connections
		• Relate to the media and cable type.		
		• Common media types include copper,
		fiber optics and wireless.

- Data Link and Network Connections

	• Network communication requires protocols to establish the rules of communications. Data Link protocols:
		• Allow the upper layers to access the media
		• Prepare network data for the physical network
		• Control how data is placed and received on the media
		• Exchange frames between nodes over a physical network media,such as copper or fiber-optic
		• Receive and directing packets to an upper layer protocol
		• Perform error detection
	• The most popular data link layer connection used in wired networks is Ethernet.
	• Other data link protocols include wireless standards such as IEEE 802.11 (Wi-Fi), IEEE 802.15 (Bluetooth), and cellular 3G or 4G networks.
	• LoRaWAN and NB-IoT are examples of emerging IoT supporting	technologies.

	- Application Connections

		• The IoT supports many types of connections.
		
		• Devices must use the same application layer protocols to connect.
		
		• The application will vary depending on the devices and type of connection involved.
		
		• MQTT and REST are newer application protocols, created to support IoT devices that
		
		connect in the myriad of different types of remote configurations.
		
		• MQTT is a lightweight messaging protocol with minimal overhead that provides high
		
		data integrity and security for remote environments.
		
		• REST or RESTful web services is a type of API designed to make it easier for
		
		programs to interact over the Internet.
		- ![](../images/Pasted%20image%2020250709102900.png)
### Impact of Connections on Pri