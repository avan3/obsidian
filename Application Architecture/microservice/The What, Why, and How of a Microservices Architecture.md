https://medium.com/hashmapinc/the-what-why-and-how-of-a-microservices-architecture-4179579423a9
Takes the approach of loosely coupled servies that can be developed, deployed, and maintained independently 
Each service is responsible for a discrete task and can communicate with other services through APIs to solve a larger complex business problem
**Benefits**:
- Each service can be built by one or more small teams from the beginning and is easier to scale up the development effort if needed
- Can be developed independently of each other 
	- Identify hot services and scale them independent of the whole application
- If error happens in one service, the whole application doesn't necessarily stop functioning
- When error is fixed, it can be deployed for the respective service instead of redeploying the entire application
- Easier to choose technology stack which is best suited for the required functionality 
E.g. building a user service in Java with a MySQL database, and a product recommendation service with Scala/Spark
CI/CD pipelines can be developed to deploy the services indepdently to different environments
Make sure to design the service carefully by hiding the complexity and implementation details of the service and only expose what is needed by the service's clients
E.g. if two services access the same database, there is less flexibility. One service should access the other service, then access the database
**Services are decentralized**: 
- Developers are the ones who develop, deploy, maintain and support it
- Technical documentation is required and guidance for each service so it would be easy for anyone to pickup and work on the service
- Services can be communicating with a central message bus (e.g. RabbitMQ)
Ideal way of deploying microservice is having **one microservice per operating system**
- This way the service is more isolated and easier to manage dependencies and scale services independently
- Normally solve the issue of multiple OS through Hypervisors whereby multiple virtual machines are provisioned on the same host
- Since VMs are inefficient because the hypervisor itself is consuming some resources, the container model is preferred (e.g. Docker)
How to deploy a microservice while the application is being used in production?
- Version the API and deploy the new version while the first version is still up
However, two versions is difficult to maintain
- Alternate way is having adding another endpoint in the same service when changes are needed
- Once the new endpoint is fully utilized by all the services, then the old endpoint can be deleted
- Only one version of the application is running
Follow standards like Stripe APIs style guide: https://docs.stripe.com/api. Use tools like Swagger (https://swagger.io/) for API documentation
Use API Gateway as a single entry point for all clients and for security and allows to expose different API for each client
Failure in a microservice means trying to ensure the entire application is not impacted when one service goes down
- Bulkhead 
	- One element fails, the others will continue to function
- Circuit breaker 
	- Wraps a protected function call in a circuit breaker object, which monitors for failures and once a threshold is reached, all further calls will return with an error
	- After some timeout, some calls are allowed to pass through the circuit breaker, and if they succeed, the application resumes to a normal state
Logging should be centralized and aggregated from each service
Monitoring works the same way as logging