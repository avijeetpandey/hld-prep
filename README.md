# Concepts

The concepts used in system desing

## Api Gateway
An API gatetway is a piece of software that acts as a front door for the entry to certain services it acts as a validator as well as routing the request to relevant service, it also works as a load balancer.

Some examples of api gateways are
- AWA API gateway

## Load Balancer
A load balancer is a piece of software that handles the responsibilites of routing the traffic to servers , given the servers are healthy and up, the primary goal of a load balancer is to avoid one server choking due to large number of requests.
Examples
- AWS ELB etc

## Types of DB and their ussage
- Relational DB ( MySQL and Postgres)
    - we can use the relational database in case our data is highly structured and ACID compliance is non-negotiable and also if there are complex joins 
- Non relational DB ( MongoDB , CouchDB)
    - These databases store the data in an document, highly used when the data is unstructured , mostly used for rapid development or for catalog data
- Key Value DB (Redis, DynamoDB)
    - They are lighting fast, they are mostly used for chaching , session managmenet or simple lookups
- Columnar DB ( Cassandra, HBase )
    - These databases are optimised for massive writes and analytical queries , mostly used for logging or timeseries data
- Graph DB ( Neo4j )
    - These databases stores the data in the form of relation ships, mostly used by social media platforms

## Indexes
Indexes are basically the lookup tables that points to the data locations, so that the DB doesnot have to scan everyrow
`CREATION` CREATE INDEX idx_name on table_name (column_name);
Indexs definately speeds up the reads but they become bottlenecks when the writes happen , because with every data change the indexes needs to be updated.

## Latency
Latency basically stands for the time it took for the response to comes from the server to the client, latency could be optimised via the following ways
- Caching
- Use of CDNS to serve static data
- Database indexing
- Messaging queues or Async processing

## Fault tolerance
The ability of the system to work independently in case of some issue and recover is called fault tolreance , in order to achieve fault tolerenace somethings like
- Health check setups
- In databases we enable replication ( having copies of the database )

## Consistency
The ability of data to remain unocrrupted or change as needed is called consistency and it could be achieved in many ways in distributed systems like
- Use of distributed locks

## Database migrations
The ability to change the database schema like adding or removing the columns without stopping the application is called database migration
we can achieve this by following
- create the new column 
- make changes so the data is filled in both new and old
- Backfill the old data to new column
- update to read from new column
- remove the old column

## Websockets
These are bi directional systems of protocols that are mostly used in real time communication systems ex Messaging , Gaming , Stocks etc
- In order to scale the websockets we can use a PUB-SUB system like redis via a messaging bus

## Redis
Redis a key value store , that is basically used to query data lightning fast sometime it is used as follows
- As a cache
- Rate limiter
- Leaderboard
When it comes to scaling redis we can use redis clusters and master slave for availability.

## Kafka
Kafka is a messaing queue that is maninly used for log aggregation , stream processing etc.
When it comes to scale kafka we can add more partitions to the topics , that encourages more parallel reads
When a consumer leave or join kafka pauses to redistribute work, in this case it could become a bottleneck

## Elasticsearch
Elasticsearch is an open source search and analytics engine built on top of apacehe leucine, while traditional databases are mostly build for looking up a particular item in the database, elastic search is used to search the entire library.

it works with something called *Inverted index* , it breaks every word into map of words and then when you search it gives the index which contains the key.

Useful for 
- Search operations
- Scalability
- Agregations
- Logging mechanism

Cons
- Cant be used for storing records as not optimised for heavy ready
- Very expensive on ram to keep the indexes hot
- No ACID properties like SQL