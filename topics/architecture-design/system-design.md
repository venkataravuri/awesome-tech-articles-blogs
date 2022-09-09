
# System Design Articles

## Design Food / Grocery Delivery System

System design approaches for applications similar to DoorDash, Dunzo, Zomato, Swiggy, Blinkit and more ... 

| | Article / Blog | Notes |
------------: | ------------- | -------------
|:star:|[Food Delivery Time Prediction](https://towardsdatascience.com/is-the-food-here-yet-f13a7bb0cd20)|Design Patterns: ? <br/>Data Structures: ? <br/>Algroithms: ?
|:star::star:|[Vehicle Routing Problem - Google OR Tools](https://developers.google.com/optimization/routing/vrp)<br />[Vehicle Routing Problem - OptaPlanner](https://www.optaplanner.org/learn/useCases/vehicleRoutingProblem.html)|
|:star:|[System Design: DoorDash — a prepared food delivery service](https://medium.com/partha-pratim-sanyal/system-design-doordash-a-prepared-food-delivery-service-bf44093388e2)
|:star:|[Architecture and Design Principles for Online Food Delivery System](https://sandesh-deshmane.medium.com/architecture-and-design-principles-for-online-food-delivery-system-33bfda73785d)

## Design a Flash Sale System

||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Flash Sale Engineering](https://www.usenix.org/conference/srecon16europe/program/presentation/stolarsky)| |
|:star:|[Flash Sale](https://george24601.github.io/2019/10/24/flash-sale.html)|  |
|:star:|[Flash Sale](https://www.alibabacloud.com/blog/high-concurrency-practices-of-redis-snap-up-system_597858)| |

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
||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|https://www.geeksforgeeks.org/system-design-of-uber-app-uber-system-architecture/
|:star:|https://www.educative.io/blog/uber-backend-system-design

## Design Payments System
||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design payments system like Google Pay or PayTM](https://careercup.com/page?pid=system-design-interview-questions)

## Design a Video Streaming Service
||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|[Design a video streaming service](https://medium.com/double-pointer/system-design-interview-video-streaming-service-e-g-netflix-or-youtube-design-adc2402e54a1)

## Design a Typeahead Search
||Article / Blog| Notes
------------: | ------------- | -------------
|:star::star:|[Proximity-Based Typeahead Search as a Service](https://engblog.nextdoor.com/typeahead-search-at-nextdoor-1875e70c67e8)
https://medium.com/double-pointer/system-design-interview-autocomplete-type-ahead-system-for-a-search-box-1ac968f9f121
|:star:|[Design Yelp or Nearby Places/Friends a proximity server](https://codeburst.io/design-a-proximity-server-like-yelp-part-2-d430879203a5)

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
|:star:|[Design a voting system](https://careercup.com/question?id=5630501784649728)

## Design a Finate Sate Machine
||Article / Blog| Notes
------------: | ------------- | -------------
|:star:|https://medium.datadriveninvestor.com/state-machine-design-pattern-why-how-example-through-spring-state-machine-part-1-f13872d68c2d

## Probabilistic Data Structures

![](https://www.gakhov.com/static/www/images/articles/kdnuggets/pdsa-in-big-data.jpg)

:star::star: [Exceeding Classical: Probabilistic Data Structures in Data Intensive Applications](https://www.slideshare.net/gakhov/exceeding-classical-probabilistic-data-structures-in-data-intensive-applications)

[Hashmap design](https://medium.com/interviewnoodle/how-does-hashmap-works-internally-619debad797f)


### Top-K, Top Trends & Leaderboards

- Maintains a list of K most frequent items.
- Finding the largest K elements in a data set or a stream.

Sorted Sets are a near-perfect data structure for leaderboards. 

|Rating|Type|Topic
------------: | ------------- | -------------
:star::star::star:|:newspaper:|[Redis - Leaderboard for online game](https://redislabs.com/blog/redis-game-mechanics-scoring/)
||:newspaper:|[Realtime tracking of top 100 twitter words per min/hour/day](https://stackoverflow.com/questions/10189685/realtime-tracking-of-top-100-twitter-words-per-min-hour-day)
||:newspaper:|[How to find high frequency words in a book in an environment low on memory?](https://stackoverflow.com/questions/742125/how-to-find-high-frequency-words-in-a-book-in-an-environment-low-on-memory/742132#742132)
||:newspaper:|[Stock ticker data structure for getting top k stock prices](https://stackoverflow.com/questions/43550873/stock-ticker-data-structure-for-getting-top-k-stock-prices)
||:newspaper:|[Find out top 10 companies with highest volume trades](https://stackoverflow.com/questions/20213589/find-out-top-10-companies-with-highest-volume-trades)
||:newspaper:|[Give the k most frequent IP addresses from the large stream of IP address in constant time and constant space](https://stackoverflow.com/questions/30149732/give-the-k-most-frequent-ip-addresses-from-the-large-stream-of-ip-address-in-con)
||:newspaper:|[Design a service to calculate the top k listened to songs in past 24 hrs](https://stackoverflow.com/questions/50207691/design-a-service-to-calculate-the-top-k-listened-to-songs-in-past-24-hrs)
||:newspaper:|[Algorithm to find 100 closest stars to the origin](https://stackoverflow.com/questions/9202315/algorithm-to-find-100-closest-stars-to-the-origin)
|:star:|:newspaper:|[Redis - Leaderboard benchmark using Sorted Set vs. Top-K](https://redislabs.com/blog/meet-top-k-awesome-probabilistic-addition-redisbloom/)

- [Most frequent keywords on Google search engine, Most watched videos on Youtube, Most played songs on Spotify, Most shared posts on Facebook, Most retweeted tweet on Twitter](https://coblob.com/blogs/Count-Min-Sketch-to-solve-Top-K-or-Frequent-K-Heavy-Hitters-System-Design-problems-5b21ca3eeb7f6fbccd473689)

- [How do find out the top trendings products on a last hour/day/monthly basis? Given that we have access to a real-time stream of sold product ids.](https://careercup.com/question?id=5386246879707136)

## Membership

### Bloom Filters

- Checks the membership of an item in a set of similar items.
- Checking for presence of an element in a set.
- A data structure that enables you to store information about the presence of an element in a set in a very small space of a fixed size.
- If you ask Bloom Filter whether an item exists in a set, it can provide you any of the 2 answers — ‘May be present’ or ‘No’.
- Bloom filter guarantees ‘No’ answer for membership check if the item does not exist in the set, but it’s not so sure about the item when it exists in the set — there is a very high chance that the item exists in the set, but not necessarily it exists.

#### Bloom Filter Real World Use Cases

- _*Is this URL malicious?*_ - A cloud based security service which protects you from accessing malicious urls. That service might host a database of millions of malicious urls, might cater to millions of request per minute worldwide. Traditional approach, searching a url in their database or cache is huge challenge. Rather use some approximation or probability here quickly identifies if the url is safe or not?
- Google Chrome Browser uses Bloom Filters to identify malicious websites by their URLs. Google’s Chrome web browser uses a Bloom filter as a first level screen of suspicious URLs, and positive results are subjected to a second level test to confirm the issue before a warning is issued to the user.
- Is this word contained in the document?
- Is this IP address blacklisted?
- Has this URL already been crawled?
- Was this entry already present in the stream?
- Is this record in the database?
- Determine if their desired username is taken or not. 

- Akamai's web servers use Bloom filters to prevent "one-hit- wonders" from being stored in its disk caches
- Google BigTable, Apache HBase and Apache Cassandra use Bloom filters to reduce the disk lookups for non-existent rows or columns
- The Squid Web Proxy Cache uses Bloom filters for cache digests
- Bitcoin uses Bloom filters to speed up wallet synchronization
- Ethereum uses Bloom filters for quickly finding logs on the Ethereum blockchain.
- The Exim mail transfer agent (MTA) uses Bloom filters in its rate-limit feature
- Medium uses Bloom Filters to recommend stories to its members.

- a simple _*spellchecker*_. You get the whole dictionary and add every word to the bloom filter. When you get a text you need to spellcheck, check every word against the filter. If you get a negative result back for a word, you’re sure that it’s misspelled and you can feel confident in highlighting it as one. Sometimes, however, you’d have a misspelled word that the filter marked as “maybe present” and then you’d fail to mark it as misspelled. But considering we didn’t need to store the entire dictionary in memory and we control the rate of false positives, this is probably an acceptable trade-off.

#### How does a Bloom filter work?
https://redislabs.com/blog/redis-redisbloom-bloom-filters/

Bloom filters varients for streaming data,
 - Rotating Bloom Filters. e.g. remember everthing in last hour
 - Scalable Bloom Filters. e.g. Dynamically allocating chained filters
 - Stable Bloom Filters. e.g. Continuously evict stale data 

#### Case Study

There is a system that tracks a huge number of web events and each event is marked by a number of tags including a user ID this event corresponds to. It is required to report a number of unique users that meet the specified combination of tags (like users from the city C that visited site A or site B).

- Solution 1
  - Maintain a BF that tracks user IDs for each tag value and a BF that contains user IDs that correspond to the final result.
  - A user ID from each incoming event is tested against the per-tag filters – does it satisfy the required combination of tags or not.
  - If the user ID passes this test, it is additionally tested against the additional BF that corresponds to the report itself and, if passed, the final report counter is increased.
- Solution 2: using HLL for each tag value

|Rating|Type|Topic
------------: | ------------- | -------------
:star:|:newspaper:|[Redis - Streaming Analytics with Probabilistic Data Structures](https://redislabs.com/blog/streaming-analytics-with-probabilistic-data-structures/)
:star:|:newspaper:|[Redis - Data structure for leaderboards](https://redislabs.com/blog/redis-game-mechanics-scoring/)
:star:|:newspaper:|[Redis - Bloom Filters introduction](https://redislabs.com/blog/redis-redisbloom-bloom-filters/)
:star:|:newspaper:|[Bloom Filter: A simple but interesting data structure](https://medium.com/datadriveninvestor/bloom-filter-a-simple-but-interesting-data-structure-37fd53b11606)
:star:|:newspaper:|[Bloom Filter: A Probabilistic Search Approach in Data Structures](https://medium.com/techspace-usict/bloom-filter-a-probabilistic-search-approach-in-data-structures-cb3dd48c6632)
||:newspaper:|[When Bloom filters don't bloom](https://blog.cloudflare.com/when-bloom-filters-dont-bloom/)

### Quotient Filter

### Cuckoo Filter

## Frequency

### Count-Min Sketch

- A space-efficient probabilistic data structure to estimate frequencies of elements in data streams. 
- To Estimate number of times an element occurs in a set.
- Count-Min Sketch is a solution to the _*"heavy hitters problem"*_

- Finding Heavy Hitters - A common task in many analytics application is finding heavy hitters, elements that appear a lot of times. For example, given a huge log of website visits, we might want to determine the most popular pages and how often they were visited. Again, building up a full hash table could scale badly if there is a long tail of unpopular pages that have few visits.

- To solve the problem with CMS, we simply iterate through the log once and build up the sketch [2] . To query the sketch, we need to come up with candidate keys to check for. If we do not have an existing candidate set, we can simple go through the log again and look up each page in the CMS, remembering the most important ones.

|Rating|Type|Topic|
------------: | ------------- | -------------
|:star::star:star:|:newspaper:|[Probabilistic data structures. Part 3. Frequency](https://www.slideshare.net/gakhov/probabilistic-data-structures-part-3-frequency)
|:star::star:|:newspaper:|[Big Data with Sketchy Structures, Part 1 — the Count-Min Sketch](https://towardsdatascience.com/big-data-with-sketchy-structures-part-1-the-count-min-sketch-b73fb3a33e2a)

#### Realworld Use Cases

- Find the most trending hashtags on Twitter
- AT&T has used Count-Min Sketch in network switches to perform analyses on netowrk traffic using limited memory.
- To find frequent items sold for an online retailer: the product sold can be the item and frequency can the number of times the item was sold.
- To make a password strong, we can keep track of how many times a password was used for a given website. In this scenario, the password is the item and frequency is the number of times the given string was used as a password.

#### Case Study

There is a system that tracks traffic by IP address and it is required to detect most traffic-intensive addresses.

#### Solution

- CMS?!!
- The problem is not trivial because we need to track the total traffic for each address, not a frequency of items.
- Counters in the CMS implementation can be incremented not by 1, but by absolute amount of traffic for each observation (i.e, size of IP packet if sketch is updated for each packet)
- In this case, sketch will track amounts of traffic for each address and a heap with the most traffic-intensive addresses can be maintained (top-k or heavy-hitter).

## Counting

### HyperLogLog
HyperLogLog (HLL) is a useful and interesting probabilistic data structure used to count unique values in a given data set with good accuracy and speed. Normally, to count unique values accurately requires memory proportional to the number of unique values. This becomes a problem when working with large data sets. HyperLogLog solves this problem by allowing us to trade memory consumption for (tunable) precision, making it possible to estimate cardinalities larger than 1 billion with a standard error of 2% using only 1.5 kilobytes of memory.

- How do we count distinct things in a stream?
- A hash-based probabilistic algorithm for counting number of distinct values in te presence of duplicates.
- HyperLogLog++ is improved version of HyperLogLog.

- HLL counts unique items in a stream, without having to remember the whole history. 
In fact, an HLL counter takes up to 12KB of memory regardless of how many items you put into it. Lastly, an HLL counter will have a standard error rate of 0.81%, which is a perfectly sustainable error rate for most streaming analytics use cases.

#### Real world use cases

- Count the number of unique visitors
- Redis uses the HyperLogLog data structure to count unique elements in a set
- How many different words are used in Wikipedia?


|Rating|Type|Topic
------------: | ------------- | -------------
:star::star::star:|:newspaper:|[HLL in PostresSQL](http://tech.nextroll.com/blog/dev/2019/08/06/hll-in-postgresql.html)
|||[Redis](https://redislabs.com/blog/streaming-analytics-with-probabilistic-data-structures/)

#### Case Study 1

- There is a system that receives events on user visits from different internet sites.
- This system enables analysis to query a number of unique visitors for the specified date range and site.
  
#### Solution 1

- HLL can be used to aggregate information about visitor IDs for each day and site, masks for each day are saved, and a query can be processed using bitwise OR-ing of the daily masks.

#### Case Study 2

- There is a system that monitors traffic and counts unique visitors for different criteria (visited site, geography, etc.)
- It is required to compute 100 most popular sites using a number of unique visitors as a metric of popularity.
- Popularity should be computed every day on the basis of data for last 30-day, i.e. every day one-day partition added, another one is removed from the scope.
