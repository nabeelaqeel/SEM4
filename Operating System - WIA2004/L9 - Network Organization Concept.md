# Network Organization Concepts

### Learning Objective
- Conflict resolution procedures that allow a network to share common transmission hardware and software effectively
- The two transport protocol models (OSI and TCP/IP) and how the layers of each one compare

### Basic Terminology
- Network
	- Collection of loosely coupled processors
	- Interconnected by communication links
		- Using cables, wireless technology, both
	- Common goal
		- Provide convenient resource sharing
		- Control access
	- General network configurations
		- Network operating system (NOS)
		- Distributed operating system (D/OS)
- Network operating system (NOS)
	- Networking capability
		- Added to single-user operating system
	- Users aware of specific computers and resources in network
	- Access resources
		- Log on to remote host
		- Data transfer from remote host
- Distributed operating system (D/OS)
	- Users not aware of specific computers and resources in network
		- Access remote resources as if local
	- Good control: distributed computing systems
		- Allows unified resource access
	- Total view across multiple computer systems 
		- No local dependencies for controlling and managing resources
	- Cooperative management
	- Comprised of four managers with a wider scope
	- ![[../images/Pasted image 20250212021455.png]]
	- Advantages over traditional systems
		- Easy and reliable resource sharing
		- Faster computation
		- Adequate load balancing
		- Good reliability
		- Dependable communications among network users
	- Remote
		- Other processors and resources
	- Local
		- Processor’s own resources 
	- Site
		- Specific location in network
			- One or more computers
	- Host
		- Specific computer system at site
			- Services and resources used from remote locations
	- Node
		- Name assigned to computer system 
			- Provides identification
	- ![[../images/Pasted image 20250212021610.png]]
	- Physically or logically connected sites
	- Star, ring, bus, tree, hybrid
	- Topology tradeoffs 
		- Need for fast communication among all sites
		- Tolerance of failure at a site or communication link
		- Cost of long communication lines
		- Difficulty connecting one site to large number of other sites







