1. Understand what's expected
2. Refresh your fundamentals
3. Familiarize yourself with the basic building blocks
4. Work backwards from common problems and iterate

- What is a system design interview?
	- Tests your ability to architect complex, scalable systems that solve real world problems
	- Different types:
		- Product Design
			- Design Uber, Ticketmaster, etc.
		- Infrastructure Design
			- Design ad click aggregator, message queue, etc.
		- OOP (Low-level) design
		- Frontend design
- What framework should you follow to present your design?
	- Requirements --> Core entities --> API or interface --> Data flow --> High level design --> Deep dives
	- Requirements: interviewer and I agree on what we will be designing
		- Includes functional and non-functional requirements
			- Functional: E.g. Ticketmaster - book a ticket
			- Non-functional: Quality of a system E.g. booking tickets should be low latency or system should be able to scale to however many number of users
	- Core entities
		- Map directly to tables in the database
		- Entities that the system will persist and the API will exchange
		- E.g. user, event, ticket
	- API or interface
		- REST endpoints
		- Potentially GraphQL or something else
	- High-level design
		- Drawing boxes on a whiteboard
		- Goal is to meet the functional requirements
	- Deep dives
		- Enhance the high level design
		- Goal is to satisfy the non-functional requirements
		- E.g. how to ensure low latency? consistency? make sure it can scale?
- How are System Design Interviews Evaluated?
	- Problem Solving: identify & prioritize the core challenges
		- And don't focus on what's not important
	- Solution Design: Create scalable architectures with balanced trade-offs
		- High-level design: weigh tradeoffs, and have a solution that meets the functional requirements
	- Technical Excellence: Demonstrate deep knowledge and expertise
		- Deep-dives: do you have technical knowledge in some, not all, of the areas of the system? (i.e. specific technologies, where things can break)
	- Communication: clearly explain complex concepts to stakeholders
		- Talking for 35 minutes to an hour. Can you be clear and competent?

- Fundamentals
	- *Have a foundational understanding of these*
	1. Storage
		1. Be able to discuss various data storage models and appropriate use-cases
			1. E.g. how data is organized in relational database (normalized tables with relationships) vs document based (nested JSON-like structure) vs Key-Value stores (simple lookup mechanism based on a key)
		2. Also ACID compliance  for transactional systems vs BASE (Basically Available, Soft state, Eventually consistent) for distributed databases
		3. Articulate when each storage paradigm makes sense based on access patterns and given the consistency requirements of the system (from non-functional requirements)
	2. Scalability
		1. Scale compute - Vertical Scaling vs Horizontal scaling
		2. Scale storage - Sharding and Consistent Hashing
	3. Networking'
		1. OSI layers
			1. Application layer
				1. API design
			2. Transport layer
				1. Infra-style interviews 
				2. TCP vs UDP
				3. Request-Response lifecycle
			3. Network layer (less likely)
				1. Load balancing
				2. Firewalls, ACLs (Access control lists)
	4. Latency, Throughput & Performance
		1. Possible to have to optimize performance in your system
		2. Recall approx. latency numbers for common operations such as memory access, disk reads, network calls
		3. Demonstrate ability to understand some throughput limitations, and perform some basic capacity planning estimations
		4. Identify performance bottlenecks and propose solutions in the architecture (e.g. adding a cache to reduce latency)
	5. Fault Tolerance & Redundancy
		1. Communicate to interviewers that failures are inevitable
		2. Ready to discuss things like replication strategies, and failure detection mechanisms
		3. System design should incorporate redundancy at the appropriate levels, server, racks, maybe data centers so that you can recover from these failures gracefully
	6. CAP Theorem
		1. Talk about earlier in the interview with non-functional requirements
		2. System upholds whatever you make in as it pertains to cap theorem
		3. Consistency, Availability, Partition tolerance
			1. Only two of the three
			2. Partition tolerance is a guarantee. So should my system prioritize availability or consistency

- Components
	- Database
		- E.g. PostGreSQL - clear tables with clear and defined rules
		- E.g. MongoDB - store information in documents and JSON blobs
		- E.g. Redis - Key-Value pairs
		- Don't focus on SQL vs NoSQL - most modern databases can scale well and maintain data integrity
			- Choose database based on how does the app need to read and write data, and makes those common operations fast and simple for your user-case
		- Cache is short-term memory
			- Frequently accessed data so don't have to hit the database
			- Need to figure out how long data can stay valid
			- Managing cache adds complexity to your design
	- Message Queue
		- Allow different parts of your system to communicate without having to wait around (asynchronous)
		- E.g. Kafka, Rabbit MQ
		- Instead of making direct calls, one service can drop a message into the queue and another service can pick up and process the message when it's ready
			- e.g. texting, both sides do not need to be available at the same time
		- Can help the system handle traffic spikes, and keeps things running if one service crashes 
		- Challenge is making sure messages actually get delivered in the first place
			- Does the message get sent once or multiple times?
			- Need strategies to handle this
	- Load balancer
		- Traffic control for your system
		- Take incoming requests and direct them to different servers so no single machine get overwhelmed (servers will be horizontally scaled)
	- Blob storage
		- Database is normally for organized structured data like user accounts or product information
			- Not designed for storing large files like images or videos
			- Will slow down your queries and make backups a nightmare
		- E.g. Amazon S3
		- Specifically built to handle unstructured data
	- CDN (Content Delivery Network)
		- Simply a cache
		- Serves as global distribution system
		- Place content closer to users around the world when storing copies of the images and videos and other static files (hosted in blob storage) 
			- Makes it faster for users to download the resources
		- E.g. Cloudflare

- Problems
	- Work backwards from common problems
	- Bitly --> Dropbox --> Ticketmaster --> Facebook newsfeed --> WhatsApp --> Leetcode --> Uber --> Web crawler --> Ad click aggregator --> Facebook post search
![[Pasted image 20251031085214.png]]