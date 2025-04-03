Aka document-oriented database or document store
Is a database that stores information in documents
Can provide schema validation
Advantages:
- An intuitive data model that is fast and easy for developers to work with
- A flexible schema that allows for the data model to evolve as application needs change
- The ability to horizontally scale out
- Documents map to data structures so developers don't have to worry about manually splitting related data across multiple tables when storing it or joining it back when retrieving it
- Don't need to use an ORM to handle manipulating data
Considered to be non-relational (or NoSQL) databases
https://www.mongodb.com/resources/basics/databases/nosql-explained
- Typically refer to any non-relational database
- NoSQL is a database management approach, whereas SQL is just a query language.
**What is a document?**
- Record in a document database
- Store data in field (key)-value pairs
- Documents can be stored in formats like JSON, BSON, and XML
**What id a collection?**
- Group of documents
- Typically store documents that have similar contents
Still leverage CRUD operations
**Features**:
- Document model
	- Can map to objects allowing for rapid development
- Flexible schema
	- Not all documents in a collection need to have the same fields
- Distributed and resilient
	- Allows for horizontal scaling (typically cheaper than vertical scaling) and data distribution
	- Resiliency through replication
- Querying through an API or query language
	- Can query documents through unique identifiers or field values
Vs relational database
- Relational database need to store user data, # of likes, businesses in separate tables, but document databases can store that data in one document
- Writing a query to get the document is easier without joins
Relationship between other data models:
- **Key-value pairs**:
	- Any field in a document can be indexed
- **Relational data**:
	- Keep related data together in single or separate documents
	- Database references can be used to connect the related data
- **Documents map to objects in most popular programming languages**
- **Graph nodes and/or edges**:
	- Can be modelled as documents
- **Geospatial data as arrays in documents**
