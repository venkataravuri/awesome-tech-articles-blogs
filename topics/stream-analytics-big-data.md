# :chart_with_upwards_trend: Stream Analytics, 🗻:mount_fuji: Big Data

## Probabilistic Data Structures

Probabilistic (P11c) data structures allow you to cheat the storage requirements and computational load of many common data tasks.

### Rate Limiting (Non Probabilistic)

||Type|Topic
------------: | ------------- | -------------
:star::star::star:|:newspaper:|[An alternative approach to rate limiting](https://www.figma.com/blog/an-alternative-approach-to-rate-limiting/)
:star::star:|:newspaper:|[How to Design a Scalable Rate Limiting Algorithm](https://konghq.com/blog/how-to-design-a-scalable-rate-limiting-algorithm/)
:star::star:|:newspaper:|[Introduction to rate limiting with Redis [Part 2]](https://www.binpress.com/rate-limiting-with-redis-2/)

### HyperLogLog

||Type|Topic
------------: | ------------- | -------------
:star::star::star:|:newspaper:|[HLL in PostresSQL](http://tech.nextroll.com/blog/dev/2019/08/06/hll-in-postgresql.html)

### Bloom Filters

Bloom filters can be used to answer such questions as:

    Is this URL malicious? - Say you are using a cloud based security service which protects you from accessing malicious urls. That service might host a database of millions of malicious urls, might cater to millions of request per minute worldwide. In this scenario, searching a url in their database or cache is huge challenge — what about using some approximation or probability here also to quickly identify if the url is safe or not?
    Is this word contained in the document?
    Has this URL already been crawled?
    Was this entry already present in the stream?

Real World Use cases:

    If you have written a story, then you might have noticed that before publishing the story Medium asks us to tag the story with 5 strings. The reason behind the tagging is this itself. Medium uses Bloom Filters to recommend stories to its members.
    Ethereum uses Bloom filters for quickly finding logs on the Ethereum blockchain.
    Google chrome uses Bloom Filters to identify malicious websites by their URLs. Google’s Chrome web browser uses a Bloom filter as a first level screen of suspicious URLs, and positive results are subjected to a second level test to confirm the issue before a warning is issued to the user.
    Bitcoin uses Bloom Filters to speed up wallet synchronization.

    Trying to find if some item exists in a set of similar items,

    It is used to check the membership of an item in a set of items. If you ask it whether an item exists in a set, it can provide you any of the 2 answers — ‘May be present’ or ‘No’. So you see clearly that Bloom filter guarantees ‘No’ answer for membership check if the item does not exist in the set, but it’s not so sure about the item when it exists in the set — there is a very high chance that the item exists in the set, but not necessarily it exists. That’s why Bloom filter is probabilistic in nature & this trade-off makes member searching quite fast also.

||Type|Topic
------------: | ------------- | -------------
:star:|:newspaper:|[Redis - Streaming Analytics with Probabilistic Data Structures](https://redislabs.com/blog/streaming-analytics-with-probabilistic-data-structures/)
:star:|:newspaper:|[Redis - Data structure for leaderboards](https://redislabs.com/blog/redis-game-mechanics-scoring/)
:star:|:newspaper:|[Redis - Bloom Filters introduction](https://redislabs.com/blog/redis-redisbloom-bloom-filters/)
:star:|:newspaper:|[Bloom Filter: A simple but interesting data structure](https://medium.com/datadriveninvestor/bloom-filter-a-simple-but-interesting-data-structure-37fd53b11606)
:star:|:newspaper:|[Bloom Filter: A Probabilistic Search Approach in Data Structures](https://medium.com/techspace-usict/bloom-filter-a-probabilistic-search-approach-in-data-structures-cb3dd48c6632)
||:newspaper:|[When Bloom filters don't bloom](https://blog.cloudflare.com/when-bloom-filters-dont-bloom/)

### TopK

### Count-min Sketch

||Type|Topic
------------: | ------------- | -------------
|:star::star:|:newspaper:|[Big Data with Sketchy Structures, Part 1 — the Count-Min Sketch](https://towardsdatascience.com/big-data-with-sketchy-structures-part-1-the-count-min-sketch-b73fb3a33e2a)

### Realtime Data Pipelines

||Type|Topic
------------: | ------------- | -------------
:star::star::star:|:newspaper:|[Yelp: Realtime data pipelines](https://engineeringblog.yelp.com/2016/07/billions-of-messages-a-day-yelps-real-time-data-pipeline.html)