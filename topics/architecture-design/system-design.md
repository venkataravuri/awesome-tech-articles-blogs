
# System Design Articles

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


## Design a Food/Grocery Delivery System
### Overview
System design approaches for applications similar to DoorDash, Dunzo, Zomato, Swiggy, Blinkit and more ...
### Data Structures & Algorithms

### Design Patterns

| | Article / Blog |
------------: | ------------- |
|:star::star:|[System Design: DoorDash — a prepared food delivery service](https://medium.com/partha-pratim-sanyal/system-design-doordash-a-prepared-food-delivery-service-bf44093388e2)
|:star::star:|[Vehicle Routing Problem - Google OR Tools](https://developers.google.com/optimization/routing/vrp)<br />[Vehicle Routing Problem - OptaPlanner](https://www.optaplanner.org/learn/useCases/vehicleRoutingProblem.html)|
|:star:|[Food Delivery Time Prediction using ML](https://towardsdatascience.com/is-the-food-here-yet-f13a7bb0cd20)|
|:star:|[Architecture and Design Principles for Online Food Delivery System](https://sandesh-deshmane.medium.com/architecture-and-design-principles-for-online-food-delivery-system-33bfda73785d)
|:star:|[Yelp System Design](https://systemdesigntutorial.com/yelp/)
|:star:|[Find Restaurants with Geospatial Queries - MongoDB](https://www.mongodb.com/docs/manual/tutorial/geospatial-tutorial/)
|:star:|[Geo-Proximity Search — 5 Approaches](https://medium.com/@ibrahim.zananiri/proximity-searching-four-approaches-78c626500e43)

## Design a Flash Sale System

### Overview
- Handle write heavy traffic & high concurrency
- Avoid overselling inventory
- Multiple requests from same user (different browser sessions)### Data Structures & Algorithms

### Data Structures & Algorithms

### Design Patterns

||Article / Blog| Notes
------------: | ------------- | -------------
|:star::star:|[Flash Sale](https://george24601.github.io/2019/10/24/flash-sale.html)|  |
|:star:|[Flash Sale](https://www.alibabacloud.com/blog/high-concurrency-practices-of-redis-snap-up-system_597858)| |
|:star:|[Flash Sale Engineering](https://www.usenix.org/conference/srecon16europe/program/presentation/stolarsky)| |

## Design a Search Engine

### Overview

### Data Structures & Algorithms

### Design Patterns

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design a Search Engine](https://medium.com/double-pointer/system-design-interview-search-engine-edb66b64fd5e)

## Design a Parking Lot

### Overview

### Data Structures & Algorithms

### Design Patterns

||Article / Blog| Notes
------------: | ------------- | -------------
|:star::star::star:|[Design a Parking Lot System](https://medium.com/double-pointer/system-design-interview-parking-lot-system-ff2c58167651)

## Design a Rate Limiter

### Overview

### Data Structures & Algorithms

### Design Patterns

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Rate limiter](https://hechao.li/2018/06/25/Rate-Limiter-Part1/)
|:star::star:|[Introduction to rate limiting with Redis [Part 2]](https://www.binpress.com/rate-limiting-with-redis-2/)
|:star::star:|[Figma - An alternative approach to rate limiting](https://www.figma.com/blog/an-alternative-approach-to-rate-limiting/)
|:star:|[Kong - How to Design a Scalable Rate Limiting Algorithm](https://konghq.com/blog/how-to-design-a-scalable-rate-limiting-algorithm/)


## Design a Vending Machine

### Overview

### Data Structures & Algorithms

### Design Patterns

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design vending system](https://careercup.com/question?id=5768722967429120)
|:star:|https://medium.com/interviewnoodle/vending-machine-system-architecture-ce28c215c2b1
|:star:|https://javarevisited.blogspot.com/2016/06/design-vending-machine-in-java.html#axzz7bO38EcZi

## Design a Ride Share App

### Overview

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

### Overview
- Scheduling millions of jobs.

### Data Structures, Algorithms
- On single computer, Sorted Set + HashMap + Multiprocessing Queues
- Must be disttibued for scaling, ...

### Design Patterns

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[System Design — Distributed Job Scheduler](https://mecha-mind.medium.com/system-design-distributed-job-scheduler-19c2758f0d6b)
|:star:|[A design for large-scale job schedulers](https://towardsdatascience.com/ace-the-system-design-interview-job-scheduling-system-b25693817950)

## Design Payments System

### Overview
- Relaibility with high throughput
- Payment processing should be idempotent and crash-tolerant
- Resiliencey when service crash
- Charged once and exactly once.

- ront-end service accepts a user’s payment request. The first order of business is to set up a record in a database 
- front-end service also puts a message on the payment queue
- Centralized Orchestrator like Netflix Conducutor. 

### Data Structures, Algorithms

### Design Patterns

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design payments system like Google Pay or PayTM](https://careercup.com/page?pid=system-design-interview-questions)
|:star:|[System design practice: designing a payment system](https://www.linkedin.com/pulse/system-design-practice-designing-payment-avik-das)

## Design a Video Streaming Service
||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design a video streaming service](https://medium.com/double-pointer/system-design-interview-video-streaming-service-e-g-netflix-or-youtube-design-adc2402e54a1)

## Design a Typeahead Search

### Overview

### Data Structures, Algorithms

### Design Patterns

||Article / Blog| Notes
------------: | ------------- | -------------
|:star::star:|[Proximity-Based Typeahead Search as a Service](https://engblog.nextdoor.com/typeahead-search-at-nextdoor-1875e70c67e8)
|:star:|https://medium.com/double-pointer/system-design-interview-autocomplete-type-ahead-system-for-a-search-box-1ac968f9f121
|:star:|[Design Yelp or Nearby Places/Friends a proximity server](https://codeburst.io/design-a-proximity-server-like-yelp-part-2-d430879203a5)

## Design a Chat Service


### Overview

### Data Structures, Algorithms

### Design Patterns

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design a Chat Service - Whatsapp Architecture](https://www.cometchat.com/blog/whatsapps-architecture-and-system-design)

## How to Scan Malware?

### Overview

### Data Structures, Algorithms

### Design Patterns

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design a service to scan photos/videos for any malware?](https://careercup.com/question?id=5091933672701952)

## Design a Voting System

### Overview

### Data Structures, Algorithms

### Design Patterns

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design a voting system](https://careercup.com/question?id=5630501784649728)

## Design a Finate Sate Machine

### Overview

### Data Structures, Algorithms

### Design Patterns

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|https://medium.datadriveninvestor.com/state-machine-design-pattern-why-how-example-through-spring-state-machine-part-1-f13872d68c2d
|:star:|[Finate State Machine](https://github.com/davidmoten/state-machine)

## Design a Elevator

### Overview

### Data Structures, Algorithms

### Design Patterns

|Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Elevator System Design](https://medium.com/geekculture/system-design-elevator-system-design-interview-question-6e8d03ce1b44)

## Design TinyURL Service

### Overview

URL Shortening logic: 6 or 7 or 8 char random ID

Base 62/64 Vs. MD5
Base 62: Take int/long and gives out base62 output which contains int or char(small/caps), safest bet.
MD5:Take unique string (long URL) and gives base62 output, gives a lengthy output of which we take only 7 chars which can result in lots of collisions. same unique id leads to data corruption.

Base62 Python Code: https://miro.medium.com/max/4800/1*R5qb0AC0joNblNhPy5g9Pw.png

Unquiness of Short URL & Concurrency 

Pre-generated IDs and allocate.

Zookeeper to maintain a range of counter values that each app server can use for generating short URLs. However, this adds extra complexity to the design as now you also need to maintain another service. 

key-generation service (KGS), which generates unique short URLs and returns them to the app servers. If KGS has more than one server, it adds lots of complexity to KGS service's design that how the KGS service will be generating unique keys and passing them to the app server when several app servers contact KGS service. 

data store, we are storing a counter key-value. Now when an app-server comes up, it will go to the datastore and read and increment this counter value in a database transaction by some increment value. The increment value could be passed to the server as a starting configuration and could be 10, 100, or 1000. Let us take 100 as an example increment value right now. Now when after reading and incrementing the counter by 100 when the app server commits the transaction successfully, then it can safely assume that it can use all the counter values starting from the read value up to read value plus 99 for generating short URLs.

Twitter Snowflake

generate the roughly-sorted 64 bit ids in an uncoordinated manner, we settled on a composition of: timestamp, worker number and sequence number.
Sequence numbers are per-thread and worker numbers are chosen at startup via zookeeper (though that’s overridable via a config file).

https://www.thinksoftwarelearning.com/pages/tiny-url-design

### Data Structures, Algorithms

### Design Patterns

## Design a Twitter

### Overview

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

Data Partitioning

To scale out our databases we will need to partition our data. Horizontal partitioning (aka Sharding) can be a good first step. We can use partitions schemes such as:

    Hash-Based Partitioning
    List-Based Partitioning
    Range Based Partitioning
    Composite Partitioning

The above approaches can still cause uneven data and load distribution, we can solve this using Consistent hashing.

### Data Structures, Algorithms

### Design Patterns

