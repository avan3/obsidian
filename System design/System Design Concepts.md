Reliability:
- The probability that the system will meet certain performance standards and yield correct output for a specific time
Availability:
- The percentage of time that the infrastructure, system, or solution is operational under normal circumstances
https://www.bmc.com/blogs/reliability-vs-availability/

1. Client-server architecture
	- Client sends a request to store, retrieve, or modify data
	- Server receives request, processes it, and performs the necessary actions
2. IP Address
	1. Every publicly deployed server has a unique IP address (think of it like a phone number)
	2. Client sends request to IP address
3. Domain Name System (DNS)
	1. Maps domain name to IP address
	2. Can find IP of domain with ping command
4. Proxy/ Reverse Proxy
	1. Proxy acts as a middle man between your device and the internet
		- Proxy forwards your request to the target server, retrieves the response and sends it back to you
		- Proxy server hides IP address keeping location and identity hidden
	2. Reverse Proxy works the other way around
		- Intercepts the client request and forwards it to backend service based on pre-defined rules
5. Latency
	- Time it takes for a request and response to complete
	- To reduce latency,
		- Deploying server over multiple data centers worldwide so that users can connect to nearest server instead of waiting for data to travel across the world
6. HTTP/HTTPS
	1. Request includes header and sometimes request body
	2. Server responds with response with status code and either error or response body
	3. HTTP has security flaw - sends data in plain text
	4. HTTPS is secure - encrypts data with SSL or TLS protocol
		- Even if someone intercepts the request, they can't read or alter it
7. API
	1. Middleman allowing client to communicate with server
8. Database
	1. Ensures that data is stored, retrieved and managed efficiently while keeping it consistent and durable
	2. SQL:
		1. Predefined schema
		2. ACID properties
		3. Strong consistency
		4. Structured relationships
	3. NoSQL:
		1. High Scalability
		2. Performance
		3. Flexible Schema
		4. E.g. Key-Value, Document, Graph, Wide-Column
9. Vertical scaling
	1. Upgrading the server you are using with more CPU, RAM, Storage
	2. Limitation:
		1. Can't keep upgrading a server forever
		2. Becomes more expensive
		3. Single point of failure
10. Horizontal Scaling
	1. Add more servers to share the load - distribute workload across multiple machines
	2. Improved reliability - if one server goes down, still have others
	3. Limitation:
		1. Load balancer is necessary for clients to figure out which server to connect to
			1. Load balancing algorithms:
				1. Round-Robin
				2. Least Connections
				3. IP Hashing
11. Scaling Database - Indexing
	1. Similar to indexing at the back of a book
	2. Efficient lookup table that helps the database locate the required data without scanning the entire table
	3. Index stores column values along with points to actual data rows in the table
	4. Indexes are created for frequently queried data 
	5. E.g. Primary key, Foreign key
	6. Indexes speed up reads but slow down writes since indexes need to be updated when data changes
		1. So index only most frequently accessed columns
12. Scaling Database - Replication
	1. Creating copies of database across multiple servers
	2. One primary database (replica) that handles all write operations and then multiple read replicas that handle read queries
	3. Whenever write operation comes, it gets copied to the read replicas so they stay in sync
	4. Improves read performance because read requests are spread across multiple replicas reducing the load on each one
	5. Availability is also improved because if primary replica goes down, then another database can take over as primary
	6. Great for read heavy applications
13. Scaling Database - Sharding
	1. Break up database into smaller, more manageable pieces and distribute them across multiple servers
		1. Divide database into smaller parts called shards
		2. Each shard contains subset of data
		3. Data is distributed based on a sharding key (e.g. userID)
		4. Reduces database load since each shard only handles a portion of queries
		5. Improves read and write performance since queries are distributed across multiple shards
	2. Also referred to as horizontal partitioning
14. Scaling Database - Vertical Partitioning
	1. Splitting database by columns
	2. Basically splitting one table into smaller more focused tables (e.g. User_Profile, User_Login, User_Billing)
	3. Scans only relevant columns instead of entire table
	4. Reduces unnecessary disk I/O
	5. AKA Normalization?
15. Scaling Database - Caching
	1. Store frequently accessed data in memory
	2. E.g. Cache-Aside Pattern
		1. User accesses application and requests data
		2. Application checks cache first, and returns if data is in cache
		3. If not in cache, then database returns and stores the data in cache
		4. To prevent outdated data from being server, we use Time To Live (TTL) value
16. Scaling Database - Denormalization
	1. Vertical Partitioning may break up tables into many tables but if need to access data from multiple tables, need to introduce joins which can slow down queries as data grows
	2. Denormalization reduces joins 
	3. E.g. instead of Users table and Orders tables, have a User_Orders Table
	4. Often used in read heavy applications to reduce latency but leads to increased storage
17. CAP Theorem
	1. No distributed system can achieve all of these three:
		1. Consistency
			1. Every read receives the most recent write or an error
		2. Availability
			1. Every request receives a response without ensuring that it contains the most recent write
		3. Partition Tolerance
			1. System continues to function despite network partitions
	2. Since network failures are inevitable, we must choose between Partition tolerance and one of the other two
18. Blob Storage
	1. E.g. Amazon S3
	2. In order to store blobs (e.g. files like images, videos and documents)
	3. Stored in logical buckets
	4. Advantages: 
		1. Scalability
		2. Pay as you go model
		3. Automatic replication
		4. Easy access
	5. Use case: streaming video from blob storage to application (but can be slow if server is hosted far away)
19. Content Delivery Network (CDN)
	1. Global network of distributed servers that work together to serve content such as HTML, JS files, images videos to users based on their geographic location
	2. Since content is server from closet CDN server, users experience faster load times with minimal buffering
20. Websockets
	1. HTTP requests are too slow for real-time applications such as Live chat applications, or stock market dashboards, online multiplayer games
	2. The only way to do this with HTTP requests is through frequent polling sending a request every few seconds, but this is inefficient because it increases the server load and waste bandwidth and most responses are empty when there is no new data
	3. Websockets allow two way communication between client and server over a single persistent connection
	4. Client initiates a websocket connection with the server, and once established, the connection remains open
	5. Server can push updates to client at any time without waiting for a request
	6. Client can also send messages instantly to the server
	7. Enables real-time interactions
21. WebHooks
	1. Allow servers to send an HTTP request to another server as soon as an event occurs
	2. How it works:
		1. The Receiver registers a webhook URL with the Provider
		2. When event occurs, Provider sends an HTTP POST request to the webhook URL with event details
		3. This saves server resources and reduces unnecessary API calls
22. Monolithic architecture
	1. All features are within one codebase
	2. Good for small applications, but difficult to scale and deploy for larger applications
23. Microservices
	1. Broken down monolith into smaller services
	2. Each microservice handles a single responsibility, has it's own database and logic so it can scale independently
	3. Communicates with other services using APIs or message queues
	4. Services can be scaled and deployed independently without affecting the entire system
24. Message queues
	1. Enables services to communicate asynchronously without blocking other operations
	2. How it works:
		1. Producer places message in the queue
		2. Queue temporarily holds the message
		3. Consumer reads message from the queue and processes it
	3. Advantages:
		1. Decouple services 
		2. Improve scalability
		3. Prevent overload on internal services within our system
25. Rate limiting
	1. Prevent overload on public APIs and services that we deploy
	2. If a user made many requests to your servers, it could degrade performance and crash the servers and would cause issues for other users
	3. Rate limiting restricts the number of requests a client can send within a specific time frame
	4. Every user or IP address is assigned a request quota (e.g. 100 requests per minute)
	5. If exceeded, the server temporarily blocks additional requests and returns error
	6. Rate limiting algorithms:
		1. Fixed WIndow
		2. Sliding Window
		3. Token Bucket
26. API Gateway
	1. Handles rate limiting with algorithms mentioned above
	2. API Gateway is a centralized service that handles authentication, rate limiting, logging, monitoring, request routing
	3. Acts a single entry point to other services for client requests
	4. Responses are sent back through the API gateway to the client
	5. Simplifies API management, improves scalability and security
27. Idempotency
	1. Repeated requests produce the same result as if the request is only done once
	2. System checks if request has already been handled. If yes, the duplicate request is ignored
	3. If not, it processes the request normally