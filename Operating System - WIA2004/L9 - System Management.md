# System Management

### Learning Objectives 
- After completing this chapter, you should be able to describe: 
- System performance measurement
- Positive and negative feedback loops 

### System Management
- Evaluating an Operating System
	- Need to understand its design goals
	- How it communicates with users
	- How resources are managed
	- What trade offs were made to achieve its goals
- Cooperation among components
	- The performance of any resource depends on the performance of the other resources in the system.
	- Role of memory management
	- Role of processor management
	- Role of device management
	- Role of file management
	- Role of network management

### Measuring System Performance
- Total system performance can be defined as the efficiency with which a computer system meets its goals – how well it serves its users.
- System efficiency is affected by three major components:
	- User programs
	- Operating system programs
	- Hardware

### Measurement Tools 
- Most designers and analysts rely on certain measures of system performance: 
	- Throughput & capacity, 
		- Throughput
			- A composite measure that indicates the productivity of the system as a whole. 
			- Usually measured under steady-state conditions and reflects quantities such as 
				- the number of jobs processed per day or 
				- the number of online transactions handled per hour. 
			- The volume of work handled by one unit of the computer system.
		- Capacity
			- Capacity = maximum throughput

	- response time & turnaround time, 
		- Response Time 
			- The interval required to process a user’s request in real time: from when the user presses the key to send the message until the system indicates receipt of the message. 
			- It is an important measure of system performance especially to online interactive users.
		- Turnaround Time
			- The time taken (batch jobs) from the submission of a job to the return of the output to the user.


	- resource utilization, 
		- A measure of how much each unit is contributing to the overall operation. 
		- It’s usually given as a percentage of time that a resource is actually in use. For example: Is the CPU busy 60 percent of the time? Is the line printer busy 90 percent of the time? 

	- availability, 
		- Availability indicates the likelihood that a resource will be ready when a user needs it. 
		- Availability is influenced by two factors: mean time between failures (MTBF) and mean time to repair (MTTR). 
		- MTBF is the average time that a unit is operational before it breaks down, and MTTR is the average time needed to fix a failed unit and put it back in service. These values are calculated with simple arithmetic equations. 
		- Example:
		- You buy a device with an MTBF of 4000 hours (the number is given by the manufacturer), and you plan to use it for 4 hours a day for 20 days a month (= 80 hours per month). What is the failure rate?
		- Failure rate = MTBF/usage = 4000/80 = 50
		- The MTTR is the average time it would take to have a piece of hardware repaired, and would depend on several factors: the seriousness of the damage, the location of the repair shop, how quickly you need it back, how much you are willing to pay etc.
		- ![](../images/Pasted%20image%2020250212111247.png)
		- From the previous example:
			- MTBF = 4000 hours
			- MTTR = 2 hours
			- Availability = 4000/(4000+2) = 0.9995
		- On the average, this unit would be available 9995 out of every 10000 hours
		- How many failures? 5

	- and reliability. 
		- Reliability is similar to availability, but it measures the probability that a unit will not fail during a given time period (t), and it’s a function of MTBF. 
		- ![](../res/Pasted%20image%2020250212111337.png)
		- (where e is the mathematical constant approximately equal to 2.71828) 
		- Example:
		- Let’s say you absolutely need to use a certain device for the 10 minutes before an upcoming deadline. With time expressed in hours, the unit’s reliability is given by:
			- Reliability (t) = $e^{-(1/4000)(10/60)}$
					      - = $e^{-(1/24000)}$
					      - = 0.09999584
			- This is the probability that it will be available (wont fail) during the critical 1o minute time period.

### Feedback Loops
- To prevent the processor from spending more time doing overhead than executing jobs, the operating system must continuously monitor the system and feed this information to the Job Scheduler. 
- Then the Scheduler can either allow more jobs to enter the system or prevent new jobs from entering until some of the congestion has been relieved. 
- This is called a feedback loop and it can be either negative or positive. 


### Negative feedback loop 
- A negative feedback loop mechanism monitors the system and, when it becomes too congested, it will signals the Job Scheduler to slow down the arrival rate of the processes. 
- ![](../res/Pasted%20image%2020250212111558.png)
	- A simple negative feedback loop. It monitors system activity and goes into action only when the system is too busy.

### Positive feedback loop
- A positive feedback loop mechanism works in the opposite way: it monitors the system, and when the system becomes underutilized, the positive feedback loop causes the arrival rate to increase 
- ![](../res/Pasted%20image%2020250212111633.png)
	- A simple positive feedback loop. It monitors system activity and goes into action only when the system is not busy enough. System activity monitoring is critical here because the system can become unstable.








