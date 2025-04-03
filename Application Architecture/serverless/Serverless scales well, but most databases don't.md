https://stackoverflow.blog/2023/02/15/serverless-scales-well-but-most-databases-dont/
What is serverless? 
- Computing model where you don't need to think about the underlying infrastructure
- Running code on-demand
Benefits:
- Don't have to worry about how infrastructure will have to scale to support traffic - availability, scalability is done automatically and no need to provision resources
- Only pay for resources that you use while your requests are being handled
	- No longer pay for resources when traffic drops
Drawbacks:
- Can encounter high bills due to unexpectedly high usage
Challenges for traditional Relational Database Management System (RDBMS):
- You still need to provision infrastructure resources for the database
- Will need to scale as traffic increases or decreases
- Potentially overwhelmed with too many connections
	- Serverless functions may create a new connection for every request then destroy it when the connection is finished. 
	- **Dry connections**: open connections that aren't sending or receiving data, but add to the number of total open connections and can potentially block new connections
- Can pool connections to improve performance and avoid running dry connections, but still risk read/write conflicts if multiple connections are accessing the same data
- Has structural rigidity of the database schema - each record must conform to the structure the table implements
	- Data with new values may need a new column and data already entered into the table will require an update to include that new column
	- Difficult and slow to iterate and evolve on database structure alongside application logic
Serverless databases:
- Can scale (up or down) in accordance with your application needs
- Has pooling or some form of load balancer built in to mitigate issue with read/write conflicts
- Document-model databases (e.g. MongoDB) work better with serverless:
- The structure of each document is defined separately by each document allowing more increased flexibility
	- Can retroactively update the document structure 
- 