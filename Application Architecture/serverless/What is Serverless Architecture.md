https://www.mongodb.com/products/capabilities/serverless
Serverless does not imply the absence of servers, but instead reflects the fact that server provisioning and management has been abstracted (or hidden) from the end-user
Cloud provider will take care of the server provisioning and scaling as your applications demand and will only charge you based on your usage
Traditional architecture: development teams have to worry about spinning up virtual machines, or purchasing the servers required to run their applications for a high cost upfront
- You pay for the instance as long as it is up, whether or not it's doing anything
- Scaling is manual - need to keep an eye on the usage and scale up or down as needed
- You may not need all the resources when you scale
**Function as a Service (FaaS)**:
- Event driven 
- When serverless function is called, the service instantiates it in a container where it runs as required
- Have the **cold start problem**:
	- If a function hasn't been called for a while, a response can have an extra wait time while the instance is being set up
**Backend as a Service (Baas)**:
- Runs the full backend of an application using a serverless execution model
- E.g. Google Firebase or AWS Amplify
**Database as a Service (DBaaS)**:
- Database is fully managed and hosted for you and deployed as a specific pre-provisioned instance size with a specific price 
- In contrast to FaaS, DBaaS must still maintain state in order to securely store the data for the application and likely will have to pay a small amount for data storage even though there is no traffic
Serverless vs Container Architecture:
- Containers are ephemeral packages of both application code and their dependencies that run in an isolated environment that can be scaled up or down in size as needed
- Developers must update the configurations and dependencies of each deployment and maintain the container's system, whereas, maintenance on serverless services is entirely managed by the vendor
- Container architecture can be automated by using a container orchestration platform (e.g. Kubernetes)
Benefits of serverless architecture:
- **Faster time to market**
	- No operational overhead of provisioning and managing your own infrastructure
- **Elastic Scalability**
	- Automatically handled
- **Increased Developer productivity**
	- Less time spent on operational tasks like scaling servers
- **Cost Effectiveness**
	- Only paying for what you use. Not charged for infrastructure sitting idle
	- Not paying for unused resources
When to use serverless computing:
- You don't know what scale of workload to expect
- You don't want to pay for unused resources
- You want to avoid infrastructure management as much as possible
- Your application logic can be broken apart into discrete functions
- You want to host your entire application backend without managing infrastructure
- You need a small piece of custom functionality in a workflow of other services
- You want to connect a large number of edge devices to a backend (for example, mobile or IoT)
When not to use serverless computing:
- Already on board with the cloud
- Need to host your own infrastructure for regulatory reasons
- Applications that experience steady ongoing traffic, require low latency, or have strict security or compliance requirements
Use cases for serverless applications:
- **Rapid application development**
	- Easy to get started and iterate quickly without operational overhead
- **Event-based or event-driven tasks/application**
	- Respond to events like user actions or system changes to trigger/execute serverless functions automatically
- **CI/CD**
	- Automation of the stages of CI/CD pipelines (e.g. code commits to trigger a function to create a build)
- **Edge Computing**
	- Related to IoT
