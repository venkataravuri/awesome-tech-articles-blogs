# :chart_with_upwards_trend: Stream Analytics, :mount_fuji: Big Data

## Probabilistic Data Structures

- Probabilistic data structures and algorithms (PDSA) are a family of advanced approaches that are _*optimized to use fixed or sublinear memory and constant execution time*_.
- They are often based on hashing and have many other useful features.- However, they also have some disadvantages such as they cannot provide the exact answers and have some probability of error (that, actually, can be controlled).

![](https://www.gakhov.com/static/www/images/articles/kdnuggets/pdsa-in-big-data.jpg)

:star::star: [Exceeding Classical: Probabilistic Data Structures in Data Intensive Applications](https://www.slideshare.net/gakhov/exceeding-classical-probabilistic-data-structures-in-data-intensive-applications)

### Rate Limiting (Non Probabilistic)

||Type|Topic
------------: | ------------- | -------------
:star::star::star:|:newspaper:|[Figma - An alternative approach to rate limiting](https://www.figma.com/blog/an-alternative-approach-to-rate-limiting/)
:star::star:|:newspaper:|[Kong - How to Design a Scalable Rate Limiting Algorithm](https://konghq.com/blog/how-to-design-a-scalable-rate-limiting-algorithm/)
:star::star:|:newspaper:|[Introduction to rate limiting with Redis [Part 2]](https://www.binpress.com/rate-limiting-with-redis-2/)

## Membership

### Bloom Filters

- Bloom Filters used to check the membership of an item in a set of similar items.
- If you ask Bloom Filter whether an item exists in a set, it can provide you any of the 2 answers — ‘May be present’ or ‘No’.
- Bloom filter guarantees ‘No’ answer for membership check if the item does not exist in the set, but it’s not so sure about the item when it exists in the set — there is a very high chance that the item exists in the set, but not necessarily it exists.
- Bloom filter is probabilistic in nature & this trade-off makes member searching quite fast also.

#### Bloom Filter Real World Use Cases

- _*Is this URL malicious?*_ - A cloud based security service which protects you from accessing malicious urls. That service might host a database of millions of malicious urls, might cater to millions of request per minute worldwide. Traditional approach, searching a url in their database or cache is huge challenge. Rather use some approximation or probability here quickly identifies if the url is safe or not?
- Google Chrome web browser used to use a Bloom filter to identify malicious URLs. Any URL was first checked against a local Bloom filter, and only if the Bloom filter returned a positive result was a full check of the URL performed.
- Google chrome uses Bloom Filters to identify malicious websites by their URLs. Google’s Chrome web browser uses a Bloom filter as a first level screen of suspicious URLs, and positive results are subjected to a second level test to confirm the issue before a warning is issued to the user.
- Is this word contained in the document?
- Has this URL already been crawled?
- Was this entry already present in the stream?
- Akamai's web servers use Bloom filters to prevent "one-hit- wonders" from being stored in its disk caches
- Google BigTable, Apache HBase and Apache Cassandra use Bloom filters to reduce the disk lookups for non-existent rows or columns
- The Squid Web Proxy Cache uses Bloom filters for cache digests
- Bitcoin uses Bloom filters to speed up wallet synchronization
- Ethereum uses Bloom filters for quickly finding logs on the Ethereum blockchain.
- The Exim mail transfer agent (MTA) uses Bloom filters in its rate-limit feature
- Medium uses Bloom Filters to recommend stories to its members.

#### Case Study

There is a system that tracks a huge number of web events and each event is marked by a number of tags including a user ID this event corresponds to. It is required to report a number of unique users that meet the specified combination of tags (like users from the city C that visited site A or site B).

- Solution 1
  - Maintain a BF that tracks user IDs for each tag value and a BF that contains user IDs that correspond to the final result.
  - A user ID from each incoming event is tested against the per-tag filters – does it satisfy the required combination of tags or not.
  - If the user ID passes this test, it is additionally tested against the additional BF that corresponds to the report itself and, if passed, the final report counter is increased.
- Solution 2: using HLL for each tag value

||Type|Topic
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

A space-efficient probabilistic data structure to estimate frequencies of elements in data streams, can address heavy hitters problem.

To Estimate number of times an element occurs in a set.

Count-Min Sketch is a solution to the _*"heavy hitters problem"*_

Top-K maintains a list of K most frequent items.

||Type|Topic
------------: | ------------- | -------------
|:star::star:star:|:newspaper:|[Probabilistic data structures. Part 3. Frequency](https://www.slideshare.net/gakhov/probabilistic-data-structures-part-3-frequency)
|:star::star:|:newspaper:|[Big Data with Sketchy Structures, Part 1 — the Count-Min Sketch](https://towardsdatascience.com/big-data-with-sketchy-structures-part-1-the-count-min-sketch-b73fb3a33e2a)

#### Realworld Use Cases

- Find the most trending hashtags on Twitter
- AT&T has used Count-Min Sketch in network switches to perform analyses on netowrk traffic using limited memory.

#### Case Study

There is a system that tracks traffic by IP address and it is required to detect most traffic-intensive addresses.

#### Solution

- CMS?!!
- The problem is not trivial because we need to track the total traffic for each address, not a frequency of items.
- Counters in the CMS implementation can be incremented not by 1, but by absolute amount of traffic for each observation (i.e, size of IP packet if sketch is updated for each packet)
- In this case, sketch will track amounts of traffic for each address and a heap with the most traffic-intensive addresses can be maintained (top-k or heavy-hitter).

## Counting

### HyperLogLog

A hash-based probabilistic algorithm for counting number of distinct values in te presence of dublicates.

HyperLogLog++ is improved version of HyperLogLog.

||Type|Topic
------------: | ------------- | -------------
:star::star::star:|:newspaper:|[HLL in PostresSQL](http://tech.nextroll.com/blog/dev/2019/08/06/hll-in-postgresql.html)

#### Real world use cases

- Count the number of unique visitors
- Redis uses the HyperLogLog data structure to count unique elements in a set

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

### Realtime Data Pipelines

||Type|Topic
------------: | ------------- | -------------
:star::star::star:|:newspaper:|[Yelp: Realtime data pipelines](https://engineeringblog.yelp.com/2016/07/billions-of-messages-a-day-yelps-real-time-data-pipeline.html)

[A hashtag recommendation system for twitter data streams](https://computationalsocialnetworks.springeropen.com/articles/10.1186/s40649-016-0028-9)
[Mining Twitter: Exploring Trending Topics, Discovering What People Are Talking About, and More](https://www.oreilly.com/library/view/mining-the-social/9781449368180/ch01.html)
[Real-time Twitter data analysis using Hadoop ecosystem](https://www.tandfonline.com/doi/full/10.1080/23311916.2018.1534519)