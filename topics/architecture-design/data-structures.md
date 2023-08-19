||Article / Blog||
------------: |:------------- | -------------
|:star::star::star:|[Realtime tracking of top 100 twitter words per min/hour/day](https://stackoverflow.com/questions/10189685/realtime-tracking-of-top-100-twitter-words-per-min-hour-day)
||[How to find high frequency words in a book in an environment low on memory?](https://stackoverflow.com/questions/742125/how-to-find-high-frequency-words-in-a-book-in-an-environment-low-on-memory/742132#742132)
||[Stock ticker data structure for getting top k stock prices](https://stackoverflow.com/questions/43550873/stock-ticker-data-structure-for-getting-top-k-stock-prices)
||[Find out top 10 companies with highest volume trades](https://stackoverflow.com/questions/20213589/find-out-top-10-companies-with-highest-volume-trades)
||[Give the k most frequent IP addresses from the large stream of IP address in constant time and constant space](https://stackoverflow.com/questions/30149732/give-the-k-most-frequent-ip-addresses-from-the-large-stream-of-ip-address-in-con)
||[Design a service to calculate the top k listened to songs in past 24 hrs](https://stackoverflow.com/questions/50207691/design-a-service-to-calculate-the-top-k-listened-to-songs-in-past-24-hrs)
||[Algorithm to find 100 closest stars to the origin](https://stackoverflow.com/questions/9202315/algorithm-to-find-100-closest-stars-to-the-origin)


# Probabilistic Data Structures

## Top Trends

An efficient data structure to answer below,
- Most frequent keywords on Google search engine
- Most watched videos on Youtube
- Most played songs on Spotify
- Most shared posts on Facebook
- Most retweeted tweet on Twitter
- Find top trending products for last hour/day/monthly?

- Maintains a list of K most frequent items.
- Finding the largest K elements in a data set or a stream.



## Leaderboards

Sorted Sets are a near-perfect data structure for leaderboards. 

||Article / Blog|
------------: | ------------- | -------------
:star::star::star:|[Redis - Leaderboard for online game](https://redislabs.com/blog/redis-game-mechanics-scoring/)
|:star:|[Redis - Leaderboard benchmark using Sorted Set vs. Top-K](https://redislabs.com/blog/meet-top-k-awesome-probabilistic-addition-redisbloom/)
:star:|[Redis - Data structure for leaderboards](https://redislabs.com/blog/redis-game-mechanics-scoring/)


## Membership

### Bloom Filters
A data structure that enables you to store information about the presence of an element in a set in a very small space of a fixed size. If you ask Bloom Filter whether an item exists in a set, it can provide you any of the 2 answers — ‘May be present’ or ‘No. Bloom filter guarantees ‘No’ answer for membership check if the item does not exist in the set, but it’s not so sure about the item when it exists in the set — there is a very high chance that the item exists in the set, but not necessarily it exists.

It checks for presence of an element in a set.

- Is this URL malicious? Google Chrome Browser uses Bloom Filters to identify malicious websites by their URLs. Google’s Chrome web browser uses a Bloom filter as a first level screen of suspicious URLs, and positive results are subjected to a second level test to confirm the issue before a warning is issued to the user.
- Is this word contained in the document?
- Is this IP address blacklisted?
- Has this URL already been crawled?
- Was this entry already present in the stream?
- Is this record in the database?
- Determine if their desired username is taken or not. 
- Akamai's web servers use Bloom filters to prevent "one-hit-wonders" from being stored in its disk caches
- Google BigTable, Apache HBase and Apache Cassandra use Bloom filters to reduce the disk lookups for non-existent rows or columns
- The Squid Web Proxy Cache uses Bloom filters for cache digests
- Bitcoin uses Bloom filters to speed up wallet synchronization
- Ethereum uses Bloom filters for quickly finding logs on the Ethereum blockchain.
- The Exim mail transfer agent (MTA) uses Bloom filters in its rate-limit feature
- Medium uses Bloom Filters to recommend stories to its members.
- a simple _*spellchecker*_. You get the whole dictionary and add every word to the bloom filter. When you get a text you need to spellcheck, check every word against the filter. If you get a negative result back for a word, you’re sure that it’s misspelled and you can feel confident in highlighting it as one. Sometimes, however, you’d have a misspelled word that the filter marked as “maybe present” and then you’d fail to mark it as misspelled. But considering we didn’t need to store the entire dictionary in memory and we control the rate of false positives, this is probably an acceptable trade-off.

<img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse2.mm.bing.net%2Fth%3Fid%3DOIP.r1yGhcx0IT-dT1JRa3uQ1QHaGj%26pid%3DApi&f=1&ipt=9f82933fcc8bdb3eb62ab3689c7bf8ddd4100c3c54f4b1f2a0ee09ac2b9d194d&ipo=images" width="50%" height="50%" />

#### How does a Bloom filter work?
https://redislabs.com/blog/redis-redisbloom-bloom-filters/
Bloom filters varients for streaming data,
 - Rotating Bloom Filters. e.g. remember everthing in last hour
 - Scalable Bloom Filters. e.g. Dynamically allocating chained filters
 - Stable Bloom Filters. e.g. Continuously evict stale data 

|Rating|Type|Topic
------------: | ------------- | -------------
:star:|:newspaper:|[Redis - Streaming Analytics with Probabilistic Data Structures](https://redislabs.com/blog/streaming-analytics-with-probabilistic-data-structures/)
:star:|:newspaper:|[Redis - Bloom Filters introduction](https://redislabs.com/blog/redis-redisbloom-bloom-filters/)
:star:|:newspaper:|[Bloom Filter: A simple but interesting data structure](https://medium.com/datadriveninvestor/bloom-filter-a-simple-but-interesting-data-structure-37fd53b11606)
:star:|:newspaper:|[Bloom Filter: A Probabilistic Search Approach in Data Structures](https://medium.com/techspace-usict/bloom-filter-a-probabilistic-search-approach-in-data-structures-cb3dd48c6632)
||:newspaper:|[When Bloom filters don't bloom](https://blog.cloudflare.com/when-bloom-filters-dont-bloom/)

## Frequency

### Count-Min Sketch
A space-efficient probabilistic data structure to estimate frequencies of elements in data streams. To Estimate number of times an element occurs in a set.

[Count-Min Sketch](https://coblob.com/blogs/Count-Min-Sketch-to-solve-Top-K-or-Frequent-K-Heavy-Hitters-System-Design-problems-5b21ca3eeb7f6fbccd473689)

- Finding Heavy Hitters - A common task in many analytics application is finding heavy hitters, elements that appear a lot of times. For example, given a huge log of website visits, we might want to determine the most popular pages and how often they were visited. Again, building up a full hash table could scale badly if there is a long tail of unpopular pages that have few visits.

- To solve the problem with CMS, we simply iterate through the log once and build up the sketch [2] . To query the sketch, we need to come up with candidate keys to check for. If we do not have an existing candidate set, we can simple go through the log again and look up each page in the CMS, remembering the most important ones.

|Rating|Type|Topic|
------------: | ------------- | -------------
|:star::star:star:|:newspaper:|[Probabilistic data structures. Part 3. Frequency](https://www.slideshare.net/gakhov/probabilistic-data-structures-part-3-frequency)
|:star::star:|:newspaper:|[Big Data with Sketchy Structures, Part 1 — the Count-Min Sketch](https://towardsdatascience.com/big-data-with-sketchy-structures-part-1-the-count-min-sketch-b73fb3a33e2a)

- Find the most trending hashtags on Twitter
- AT&T has used Count-Min Sketch in network switches to perform analyses on netowrk traffic using limited memory.
- To find frequent items sold for an online retailer: the product sold can be the item and frequency can the number of times the item was sold.
- To make a password strong, we can keep track of how many times a password was used for a given website. In this scenario, the password is the item and frequency is the number of times the given string was used as a password.

## Counting

- Count the number of unique visitors for the specified date range, visited site and geography, etc.
- How many different words are used in Wikipedia?
- How do we count distinct things in a stream?

### HyperLogLog
HyperLogLog (HLL) is a useful and interesting probabilistic data structure used to count unique values in a given data set with good accuracy and speed. Normally, to count unique values accurately requires memory proportional to the number of unique values. This becomes a problem when working with large data sets. HyperLogLog solves this problem by allowing us to trade memory consumption for (tunable) precision, making it possible to estimate cardinalities larger than 1 billion with a standard error of 2% using only 1.5 kilobytes of memory.

- A hash-based probabilistic algorithm for counting number of distinct values in te presence of duplicates.
- HyperLogLog++ is improved version of HyperLogLog.
- HLL counts unique items in a stream, without having to remember the whole history. 
In fact, an HLL counter takes up to 12KB of memory regardless of how many items you put into it. Lastly, an HLL counter will have a standard error rate of 0.81%, which is a perfectly sustainable error rate for most streaming analytics use cases.
- HLL can be used to aggregate information about visitor IDs for each day and site, masks for each day are saved, and a query can be processed using bitwise OR-ing of the daily masks.
- Redis uses the HyperLogLog data structure to count unique elements in a set

|| Article / Blog |
------------: | ------------- | -------------
:star::star::star:|[HLL in PostresSQL](http://tech.nextroll.com/blog/dev/2019/08/06/hll-in-postgresql.html)
|:star:|[Redis](https://redislabs.com/blog/streaming-analytics-with-probabilistic-data-structures/)

