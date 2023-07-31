
# System Design Articles

### Quick Guidance

Focus on,
- Identity subsystem components that make up solution - Functional modules, services, APIs, ...
- Identify Data Structures and Algorithms
- Identify Design Methdolgoies & Tradeoffs - Pub/Sub, Microservices, Read-Write Heavy, DDD, SOLID Princples, CAP, ...
- 4 + 1 views - Functional Architecture, Layered Technical Architecture, Deployment Architecture, Security Architecture, ...
- Make technology choices - Polyglot Databases, Frameworks, ...

## Popular System Design Articles

- [Design a Gorcery/food Delvery Application](system-design.md#design-a-food--grocery-delivery-system)
- [Design a Flash Sale System](system-design.md#design-a-flash-sale-system)
- [Design a Search Engine](system-design.md#design-a-search-engine)
- [Design a Parking Lot System](system-design.md#design-a-parking-lot)
- [Design a Rate Limiter](system-design.md#design-a-rate-limiter)
- [Design a Vending Machine](system-design.md#design-a-vending-machine)
- [Design a Ride Share Applicaiton](system-design.md#design-a-ride-share-app)
- [Design a Distributed Job Schedular](system-design.md#design-a-distributed-job-schedular)
- [Design a Payments System](system-design.md#design-payments-system)
- [Design a Video Streaming Service](system-design.md#design-a-video-streaming-service)
- [Design a Typeahead Search](system-design.md#design-a-typeahead-search)
- [Design a Chat Service](system-design.md#design-a-chat-service)
- [How to Scan a Malware?](system-design.md#how-to-scan-malware)
- [Design a Voting System](system-design.md#design-a-voting-system)
- [Design a Finate State Machine](system-design.md#design-a-finate-sate-machine)
- [Design a Elevator](system-design.md#design-a-elevator)
- [Design a TinyURL Service](system-design.md#design-a-tinyurl-service)

**Design Concepts**

- [Data Partitioning & Sharding](#data-partitioning--sharding)


### Design a Food/Grocery Delivery System

System design approaches for aps such as DoorDash, Dunzo, Zomato, Swiggy, Blinkit and more ...

| | Article / Blog |
------------: | ------------- |
|:star::star:|[System Design: DoorDash — a prepared food delivery service](https://medium.com/partha-pratim-sanyal/system-design-doordash-a-prepared-food-delivery-service-bf44093388e2)
|:star::star:|[Vehicle Routing Problem - Google OR Tools](https://developers.google.com/optimization/routing/vrp)<br />[Vehicle Routing Problem - OptaPlanner](https://www.optaplanner.org/learn/useCases/vehicleRoutingProblem.html)|
|:star:|[Food Delivery Time Prediction using ML](https://towardsdatascience.com/is-the-food-here-yet-f13a7bb0cd20)|
|:star:|[Architecture and Design Principles for Online Food Delivery System](https://sandesh-deshmane.medium.com/architecture-and-design-principles-for-online-food-delivery-system-33bfda73785d)
|:star:|[Yelp System Design](https://systemdesigntutorial.com/yelp/)
|:star:|[Find Restaurants with Geospatial Queries - MongoDB](https://www.mongodb.com/docs/manual/tutorial/geospatial-tutorial/)
|:star::star:|[Geo-Proximity Search — 5 Approaches](https://medium.com/@ibrahim.zananiri/proximity-searching-four-approaches-78c626500e43)

## Design a Flash Sale System

### Design Considerations
- Handle write heavy traffic & high concurrency
- Avoid overselling inventory
- Multiple requests from same user (different browser sessions)### Data Structures & Algorithms

||Article / Blog| Notes
------------: | ------------- | -------------
|:star::star:|[Flash Sale](https://george24601.github.io/2019/10/24/flash-sale.html)|  |
|:star:|[Flash Sale](https://www.alibabacloud.com/blog/high-concurrency-practices-of-redis-snap-up-system_597858)| |
|:star:|[Flash Sale Engineering](https://www.usenix.org/conference/srecon16europe/program/presentation/stolarsky)| |

## Design a Search Engine

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design a Search Engine](https://medium.com/double-pointer/system-design-interview-search-engine-edb66b64fd5e)

## Design a Parking Lot

||Article / Blog| Notes
------------: | ------------- | -------------
|:star::star::star:|[Design a Parking Lot System](https://medium.com/double-pointer/system-design-interview-parking-lot-system-ff2c58167651)

## Design a Rate Limiter

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Rate limiter](https://hechao.li/2018/06/25/Rate-Limiter-Part1/)
|:star::star:|[Introduction to rate limiting with Redis [Part 2]](https://www.binpress.com/rate-limiting-with-redis-2/)
|:star::star:|[Figma - An alternative approach to rate limiting](https://www.figma.com/blog/an-alternative-approach-to-rate-limiting/)
|:star:|[Kong - How to Design a Scalable Rate Limiting Algorithm](https://konghq.com/blog/how-to-design-a-scalable-rate-limiting-algorithm/)


## Design a Vending Machine

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design vending system](https://careercup.com/question?id=5768722967429120)
|:star:|https://medium.com/interviewnoodle/vending-machine-system-architecture-ce28c215c2b1
|:star:|https://javarevisited.blogspot.com/2016/06/design-vending-machine-in-java.html#axzz7bO38EcZi

## Design a Ride Share App

### Data Structures & Algorithms

- Quadtrees are a data structure that encode a two-dimensional space into adaptable cells. quadtrees are a tree structure where every non-leaf node has exactly four children. In the context of location, these nodes represent the four quadrants: NW, NE, SW, and SE. 
- Google S2 library (which uses a quadtree data structure). This library divides the map data into tiny cells (for example 2km) and gives the unique ID to each cell. Suppose you want to figure out all the cabs available within a 2km radius of a city. Using the S2 libraries you can draw a circle of 2km radius and it will filter out all the cells with IDs lies in that particular circle. This way you can easily match the rider to the driver and you can easily find out the number of cab available in a particular region.
- Uber's H3 algorithm partitions the Earth’s surface into a network of hexagons. You can select the amount of detail each hexagon contains by choosing among the available sixteen levels. You can think of these as “zoom” levels on a map. Each hexagon is unique and is identifiable through a unique sixty-four-bit identifier, an ideal key for a database table, or an in-memory dictionary. These identifiers are consistent across “zoom” levels, so you can mix and match them as you please.

The QuadKeys in leaf nodes has reference to SortedSet in Redis, where drivers information is stored by priority (rating, distance?)

#### Driver Location servers
Driver Location Hash Table - Stores DriveID in the hash table along with driver’s current and previous location. Distribute DriverLocation HT on multiple servers based on the DriverID. This will help with scalability, performance, and fault tolerance. We will refer to the  this information as the Driver Location servers.

1. Server will also notify the respective QuadTree server to refresh the driver’s location.
2. Once server receives an update on a driver’s location, it will broadcast that information to relevant customers. 

Update data structures to reflect active drivers’ reported locations every three seconds. To update a driver to a new location, we must find the right grid based on the driver’s previous location.
If the new position doesn’t belong to the current grid, we remove the driver from the current grid and reinsert them to the right grid. If the new grid reaches a maximum limit, we have to repartition it.
We need a quick mechanism to propagate the current location of nearby drivers to customers in the area. Our system needs to notify both the driver and customer on the car’s location throughout the ride’s duration.

#### Broadcasting driver locations

When a customer opens the Uber app, they’ll query the server to find nearby drivers. On the server side, we subscribe the customer to all updates from nearby drivers. Each update in a driver’s location in DriverLocation HT will be broadcast to all subscribed customers. This ensures that each driver’s current location is displayed.

Customers will send their current location so that the server can find nearby drivers from our QuadTree. 

We’ve assumed one million active customers and 500 thousand active drivers per day. Let’s assume that five customers subscribe to one driver. We’ll store this information in a hash table for quick updates.

### Design Patterns

||Article / Blog| Notes
------------: | ------------- | -------------
|:star::star::star:|https://www.educative.io/blog/uber-backend-system-design
|:star::star:|https://engblog.yext.com/post/geolocation-caching
|:star:|https://www.geeksforgeeks.org/system-design-of-uber-app-uber-system-architecture/


## Design a Distributed Job Schedular

How to schedule millions of jobs?

### Data Structures, Algorithms
- On single computer, Sorted Set + HashMap + Multiprocessing Queues
- Must be disttibued for scaling, ...

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[System Design — Distributed Job Scheduler](https://mecha-mind.medium.com/system-design-distributed-job-scheduler-19c2758f0d6b)
|:star:|[A design for large-scale job schedulers](https://towardsdatascience.com/ace-the-system-design-interview-job-scheduling-system-b25693817950)

## Design Payments System

### Design Considerations
- Relaibility with high throughput
- Payment processing should be idempotent and crash-tolerant
- Resiliencey when service crash
- Charged once and exactly once.

- ront-end service accepts a user’s payment request. The first order of business is to set up a record in a database 
- front-end service also puts a message on the payment queue
- Centralized Orchestrator like Netflix Conducutor. 

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design payments system like Google Pay or PayTM](https://careercup.com/page?pid=system-design-interview-questions)
|:star:|[System design practice: designing a payment system](https://www.linkedin.com/pulse/system-design-practice-designing-payment-avik-das)

## Design a Video Streaming Service
||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design a video streaming service](https://medium.com/double-pointer/system-design-interview-video-streaming-service-e-g-netflix-or-youtube-design-adc2402e54a1)

## Design a Typeahead Search

||Article / Blog| Notes
------------: | ------------- | -------------
|:star::star:|[Proximity-Based Typeahead Search as a Service](https://engblog.nextdoor.com/typeahead-search-at-nextdoor-1875e70c67e8)
|:star:|https://medium.com/double-pointer/system-design-interview-autocomplete-type-ahead-system-for-a-search-box-1ac968f9f121
|:star:|[Design Yelp or Nearby Places/Friends a proximity server](https://codeburst.io/design-a-proximity-server-like-yelp-part-2-d430879203a5)

https://medium.com/@prefixyteam/how-we-built-prefixy-a-scalable-prefix-search-service-for-powering-autocomplete-c20f98e2eff1

## Design a Chat Service

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design a Chat Service - Whatsapp Architecture](https://www.cometchat.com/blog/whatsapps-architecture-and-system-design)

## How to Scan Malware?

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design a service to scan photos/videos for any malware?](https://careercup.com/question?id=5091933672701952)

## Design a Voting System

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design a voting system]()

## Design a Finate Sate Machine

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|https://medium.datadriveninvestor.com/state-machine-design-pattern-why-how-example-through-spring-state-machine-part-1-f13872d68c2d
|:star:|[Finate State Machine](https://github.com/davidmoten/state-machine)
|:star::star:|[Python - State Machine Implementation](https://github.com/pytransitions/transitions)

## Design a Elevator

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Elevator System Design](https://medium.com/geekculture/system-design-elevator-system-design-interview-question-6e8d03ce1b44)

## Design TinyURL Service

#### Design Considerations & Challenges

- URL Shortening logic: 6 or 7 or 8 random characters
- Unquiness of Short URL & Concurrency 

|:star:|[Tiny URL Design](https://www.thinksoftwarelearning.com/pages/tiny-url-design)
|:star:|[Twitter Snowflake](https://blog.twitter.com/engineering/en_us/a/2010/announcing-snowflake)

## Design a Twitter

Twitter is read-heavy

Publishing

Publishing is the step where the feed data is pushed according to each specific user. This can be a quite heavy operation, as a user may have millions of friends or followers. To deal with this, we have three different approaches:

Pull Model (or Fan-out on load)

When a user creates a tweet, and a follower reloads their newsfeed, the feed is created and stored in memory.

Push Model (or Fan-out on write)

In this model, once a user creates a tweet, it is "pushed" to all the follower's feeds immediately. This prevents the system from having to go through a user's entire followers list to check for updates.

Hybrid model allows only users with a lesser number of followers to use the push model and for users with a higher number of followers celebrities, the pull model will be used.

- Fanout approach for writes -Do a lot of processing when tweets arrive to figure out where tweets should go. This makes read time access fast and easy. Don’t do any computation on reads.
- 

https://systemdesigntutorial.com/design-twitter/

### Data Partitioning & Sharding

Partitioning of relational data, usually refers to decomposing your tables either row-wise (horizontally) or column-wise (vertically).

🔹 Vertical partitioning: means some columns are moved to new tables. Each table contains the same number of rows but fewer columns.
🔹 Horizontal partitioning (often called sharding): Divides a table into multiple smaller tables. Each table is a separate data store, and it contains the same number of columns, but fewer rows.

The routing algorithm decides which partition (shard) stores the dat,

**Range Based Partitioning**: This algorithm uses ordered columns, such as integers, longs, timestamps, to separate the rows. For example, the diagram below uses the User ID column for range partition: User IDs 1 and 2 are in shard 1, User IDs 3 and 4 are in shard 2.

**Hash-based sharding**: This algorithm applies a hash function to one column or several columns to decide which row goes to which table. For example, the diagram below uses User ID mod 2 as a hash function. User IDs 1 and 3 are in shard 1, User IDs 2 and 4 are in shard 2.

**Geo-Hashing?**

[Source](https://blog.bytebytego.com/p/vertical-partitioning-vs-horizontal)

#### How MongoDB sharding works?

"Shards" in MongoDB are just replica sets with something called a "router" in front of them. Your application will connect to the router, issue queries, and it will decide which replica set (shard) to forward things on to. It's significantly more complex than a single replica set because you have the router and config servers to deal with (these keep track of what data is stored where).

A collection is sharded based upon the Shard Key. Shard key determines how the collection data will be distributed across the shards. The shard key is also important in the read operation performance.

In a sharded cluster a database can have number of sharded and unsharded collections. You can decide which collections need to be sharded (distribute a collection's data across shards).

In MongoDB with the autosharding feature, a sharded collection will be distributed somehow evenly along all the shards you have.

With those collections which you not likely to shard (which are not sharded) you can specify a primary shard which will they reside on. This primary shard is a given one for a specific database, so it is on per database level.

A mongos (the router) receives all the queries in a sharded cluster before routing to specific shard(s). When you submit a query, it is like submitting a query to a standalone server, the syntax is same; it is transparent to the application (or code). The router determines which shards the query must visit to get your data.


#### How AWS Redshift sharding works?

#### How PostgreSQL sharding works?

- PostgreSQL provides built-in sharding feature, uses a FDW-based approach (foreign data wrappers - FDW).
- The partitions are created on foreign servers and PostgreSQL FDW is used for accessing the foreign servers 

- [PostgreSQL Sharding](https://wiki.postgresql.org/wiki/WIP_PostgreSQL_Sharding)
- [PostgreSQL Sharding Documentation](https://www.postgresql.org/docs/11/ddl-partitioning.html)
- [Sharding JDBC](https://shardingsphere.apache.org/document/legacy/4.x/document/en/manual/sharding-jdbc/)

**How to manage DB connection pool under sharded environment?**
```
In-appliction connection pool Vs. server-side connection pooling with PGPool-II or PGBouncer.

In-application pooling - create per-shard connection pools and pick a connection out of the appropriate pool for the shard. Since this will result in potentially large numbers of connections sitting around and lots of connects/disconnects, it will be very important to also run a server-side connection pool to limit and share connections to each shard. Use something like pgbouncer or pgpool-II in transaction pooling mode on each shard to share a relatively small number of real PostgreSQL connections out among the larger number of connections from web workers.
```
[Source](https://stackoverflow.com/questions/13118595/how-to-manage-db-connection-pool-under-sharded-environment)

The above approaches can still cause uneven data and load distribution, we can solve this using Consistent hashing.

#### Consistent Hasshing
[Consistent Hashing](https://www.toptal.com/big-data/consistent-hashing)
