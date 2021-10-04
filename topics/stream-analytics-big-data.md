# :mount_fuji: Big Data :chart_with_upwards_trend: Stream Analytics

Data Availability, Data Accuraccy, Data Qualiity 

Data Profiling to examin data available. It provide stats such as,
1. Column stats: type, unique values, missing values
2. Potential keys and foreign keys
3. data quality at column level. missing values, distinct values, ...

## Analytics
|Rating|Type|Topic
------------: | ------------- | -------------
||:newspaper:|[NextRoll - Making 1M Click Predictions per Second using AWS ](https://tech.nextroll.com/blog/data-science/2018/04/26/just-binary-classifier.html)

## Probabalistic Algorithms

### Sorted Sets

Sorted Sets are a near-perfect data structure for leaderboards. 

|Rating|Type|Topic
------------: | ------------- | -------------
:star::star::star:|:newspaper:|[Redis - Leaderboard for online game](https://redislabs.com/blog/redis-game-mechanics-scoring/)


### Top-K 

- Maintains a list of K most frequent items.
- Finding the largest K elements in a data set or a stream.

|Rating|Type|Topic
------------: | ------------- | -------------
||:newspaper:|[Realtime tracking of top 100 twitter words per min/hour/day](https://stackoverflow.com/questions/10189685/realtime-tracking-of-top-100-twitter-words-per-min-hour-day)
||:newspaper:|[How to find high frequency words in a book in an environment low on memory?](https://stackoverflow.com/questions/742125/how-to-find-high-frequency-words-in-a-book-in-an-environment-low-on-memory/742132#742132)
||:newspaper:|[Stock ticker data structure for getting top k stock prices](https://stackoverflow.com/questions/43550873/stock-ticker-data-structure-for-getting-top-k-stock-prices)
||:newspaper:|[Find out top 10 companies with highest volume trades](https://stackoverflow.com/questions/20213589/find-out-top-10-companies-with-highest-volume-trades)
||:newspaper:|[Give the k most frequent IP addresses from the large stream of IP address in constant time and constant space](https://stackoverflow.com/questions/30149732/give-the-k-most-frequent-ip-addresses-from-the-large-stream-of-ip-address-in-con)
||:newspaper:|[Design a service to calculate the top k listened to songs in past 24 hrs](https://stackoverflow.com/questions/50207691/design-a-service-to-calculate-the-top-k-listened-to-songs-in-past-24-hrs)
||:newspaper:|[Algorithm to find 100 closest stars to the origin](https://stackoverflow.com/questions/9202315/algorithm-to-find-100-closest-stars-to-the-origin)
|:star:|:newspaper:|[Redis - Leaderboard benchmark using Sorted Set vs. Top-K](https://redislabs.com/blog/meet-top-k-awesome-probabilistic-addition-redisbloom/)

### Rate Limiting

|Rating|Type|Topic
------------: | ------------- | -------------
:star::star::star:|:newspaper:|[Figma - An alternative approach to rate limiting](https://www.figma.com/blog/an-alternative-approach-to-rate-limiting/)
:star::star:|:newspaper:|[Kong - How to Design a Scalable Rate Limiting Algorithm](https://konghq.com/blog/how-to-design-a-scalable-rate-limiting-algorithm/)
:star::star:|:newspaper:|[Introduction to rate limiting with Redis [Part 2]](https://www.binpress.com/rate-limiting-with-redis-2/)

## Realtime Streaming Data Pipelines

|Rating|Type|Topic
------------: | ------------- | -------------
|:star::star::star:|:newspaper:|[Yelp: Realtime data pipelines](https://engineeringblog.yelp.com/2016/07/billions-of-messages-a-day-yelps-real-time-data-pipeline.html)
||:newspaper:|[A hashtag recommendation system for twitter data streams](https://computationalsocialnetworks.springeropen.com/articles/10.1186/s40649-016-0028-9)
||:newspaper:|[Mining Twitter: Exploring Trending Topics, Discovering What People Are Talking About, and More](https://www.oreilly.com/library/view/mining-the-social/9781449368180/ch01.html)
||:newspaper:|[Real-time Twitter data analysis using Hadoop ecosystem](https://www.tandfonline.com/doi/full/10.1080/23311916.2018.1534519)

## Probabilistic Data Structures

- Probabilistic data structures and algorithms (PDSA) are a family of advanced approaches that are _*optimized to use fixed or sublinear memory and constant execution time*_.
- They are often based on hashing and have many other useful features.- However, they also have some disadvantages such as they cannot provide the exact answers and have some probability of error (that, actually, can be controlled).

![](https://www.gakhov.com/static/www/images/articles/kdnuggets/pdsa-in-big-data.jpg)

:star::star: [Exceeding Classical: Probabilistic Data Structures in Data Intensive Applications](https://www.slideshare.net/gakhov/exceeding-classical-probabilistic-data-structures-in-data-intensive-applications)

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

#### Solution 2

- Create a fresh set of per-site HLL counters every day and maintain this set during 30 days, i.e. 30 sets of counters are active at any moment of time.

#### Case Study 3

- Number of users doing-action (view, click...) on site objects (banner, button, …) 1-times, 2-times, …., 10+-times
- Report looks like below
  - Filter: Object=X
    - 1-times: 98765
    - 2-times: 76543
    - 3-times: 54321
    - …
    - 9-times: 1234
    - 10+-times: 343

#### Solution 5

- Use scalable layered-BF to track k-times user actions on objects
- Use HLL to count users on each k-times action
