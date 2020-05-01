# :mag: Search Topics, Terminology :thumbsup: Recommendation Engines
## Search Topics & Terminology
> Cross referenced with Natural Language Processing (NLP) notes.
* Text Analysis / Text Mining
   * [Tokenization](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#tokenization)
   * [Stemming]()
   * [Lemmatization]()
   * [Stop Words Removal]()
   * [Parts of Speech (POS) Tagging]()
   * [TF-IDF]()
   * [Word Embeddings]()
* Topic Mining
* Indexing Pipelines
* Query Understanding
* Typeahead
* Autocomplete Suggestions
* Guided Search
* Spell Correction
* Fuzziness
* Faceted Search
* Spam-Resilient Signals
* [Ranking & Scoring](#scoring)

## Recommendation Engine Topics
- Trending
- Recommendations

- https://www.eventbrite.com/engineering/building-a-marketplace-search-and-recommendation-at-eventbrite/
- [Can a machine surprise you? We believe so.](https://developers.soundcloud.com/blog/introducing_suggested_tracks)
- https://netflixtechblog.com/highlights-from-prs2016-workshop-57f36fa34b44
- https://netflixtechblog.com/recommending-for-the-world-8da8cbcf051b

### Search - A real-world e-Commerce Implemenation
-|Type|Topic
------------: | ------------- | -------------
:star::star::star:|:newspaper:|[On-Site Search Design Patterns for E-Commerce: Schema Structure, Data Driven Ranking & More](https://project-a.github.io/on-site-search-design-patterns-for-e-commerce/)
:star:|:newspaper:|[Explantion to above article](https://medium.com/@johntucker_48673/elasticsearch-by-example-part-1-a4a38cd97f55)
:star:|:newspaper:|[Reviving an e-commerce search engine using Elasticsearch](https://medium.com/quantyca/reviving-an-e-commerce-search-engine-using-elasticsearch-e540751c6d99)

### Indexing
-|Type|Topic
------------: | ------------- | -------------
:star:|:newspaper:|[How to Reindex One Billion Documents in One Hour at SoundCloud](https://developers.soundcloud.com/blog/how-to-reindex-1-billion-documents-in-1-hour-at-soundcloud)
:star:|:newspaper:|[Facebook - Under the Hood: Indexing and ranking in Graph Search](https://www.facebook.com/notes/facebook-engineering/under-the-hood-indexing-and-ranking-in-graph-search/10151361720763920/)
:star:|:newspaper:|[GraphQL Search Indexing](https://netflixtechblog.com/graphql-search-indexing-334c92e0d8d5)

### Query Understanding
-|Type|Topic
------------: | ------------- | -------------
:star:|:newspaper:|[Query Understanding At TripAdvisor](https://www.tripadvisor.com/engineering/query-understanding-at-tripadvisor/)
:star:|:newspaper:|[Query recommendation by search filters and criteria prediction](http://www.slideshare.net/dhwajr/query-recommendation-by-search-criteria-prediction)
:star:|:newspaper:|[Pinterest - Building a platform to understand search queries](https://medium.com/pinterest-engineering/building-a-platform-to-understand-search-queries-7138e923c06a)

### Auto-Complete/Auto-Suggest
Auto Complete – offers search query completions based on what the user has typed.
There are at least two broad types of autocomplete,
* Search Suggest
* Result Suggest

Search Suggest returns suggestions for search phrases, usually based on previously logged searches, ranked by popularity or some other metric. This approach requires logging users' searches and ranking them so that the autocomplete suggestions evolve over time.

The second type of autocomplete is Result Suggest. In this case the suggestions are actual results rather than search phrase suggestions.

-|Type|Topic
------------: | ------------- | -------------
:star:|:newspaper:|[Autocomplete best practices](https://blog.griddynamics.com/smart-autocomplete-best-practices/)
:star:|:newspaper:|[Autocomplete with Elasticsearch - Part 1: Prefix Queries](https://blog.mimacom.com/autocomplete-elasticsearch-part1/)
:star:|:newspaper:|[Implementing Autosuggest in Elasticsearch](https://www.rea-group.com/blog/implementing-autosuggest-in-elasticsearch/)
:star:|:newspaper:|[On the Road to a Better ElasticSearch Location Typeahead](https://eatcodeplay.com/on-the-road-to-a-better-elasticsearch-location-typeahead-b75e3eb6dd41)
:star:|:newspaper:|[Multi-Term Auto Completion](https://documentation.spryker.com/docs/multi-term-auto-completion)

#### Completion Suggest
Elasticsearch provides a convenient way to get autocomplete up and running quickly with its completion suggester feature.

#### Did you mean?
did-you-mean (DYM)

### Typeahead
-|Type|Topic
------------: | ------------- | -------------
:star:|:newspaper:|[Facebook - The Life of a Typeahead Query](https://www.facebook.com/notes/facebook-engineering/the-life-of-a-typeahead-query/389105248919/)
:star:|:newspaper:|[Pinterest - Rebuilding the user typeahead](https://medium.com/pinterest-engineering/rebuilding-the-user-typeahead-9c5bf9723173)
:star:|:newspaper:|[Cleo: the open source technology behind LinkedIn's typeahead search](https://engineering.linkedin.com/open-source/cleo-open-source-technology-behind-linkedins-typeahead-search)

### Faceted Search
faceted search refers to a method of navigation that allows users to filter data. This term can also be interchanged with other terms such as “guided navigation” or “layered navigation.

Facets allow you to have an overview of your query that corresponds to the summary data within its result set. Let's say that you search for a laptop. You probably would've noticed the counts of entries that fall in that particular group alongside the facet. This lets you guide your search in such a way that you can refine your result set to include or eliminate results according to your choice. You'd also probably notice a distribution histogram like that of a price histogram that lets you select your product that falls in that particular price range.

As faceting evolves and product catalogs become more complex, “nested faceting” has become something of a necessity. Nested faceting -- or hierarchical faceting -- refers to a facet located within another facet. Nesting a facet inside another would give faceting yet another dimension, enabling a user to go on to add more filters (which is a logical OR on the results) to any level they prefer.

Prior to Elasticsearch v1, creating nested faceting was difficult. But the uber-powerful Aggregations feature changes this. Think of aggregations as “facets of facets.”

### Engineering Blogs
:star: | :link: | [LinkedIn](https://engineering.linkedin.com/faceting/many-facets-faceted-search)

### Scoring
Scoring
We generally define scoring as giving a higher weight to documents (or data) that meet specific criteria. The objective is often to get a list of documents, sorted on the relevance to the search. Typically, relevance is the numerical output of an algorithm that determines which documents are most textually similar to the query. Elasticsearch employs and enhances standard scoring algorithms and encapsulates these within script_score and function_score.

- https://www.compose.com/articles/how-scoring-works-in-elasticsearch/
- Great Article: http://qbox.io/blog/scoring-using-elasticsearch-scripts-part1
- [PageRank in Spark](https://developers.soundcloud.com/blog/pagerank-in-spark)
- [Search Precision and Recall By Example](https://www.eventbrite.com/engineering/search-precision-and-recall-by-example/)
- [Search Engine Marketing](https://www.tripadvisor.com/engineering/improving-sem-landing-page-quality-for-our-experiences-business/)

## ElasticSearch Tutorials
-: | Type | Topic
------------ | ------------- | -------------
:star: | :computer: | [Data Exploration With Elasticsearch](http://www.slideshare.net/astensby/data-exploration-with-elasticsearch)
:star: | :computer: | [The Ultimiate Guide for Elasticsearch Plugins](http://www.slideshare.net/synhershko/the-ultimate-guide-for-elasticsearch-plugins)
:star: | :link: | []()


## Search articles form Engineering Blogs
-: | Type | Topic
------------ | ------------- | -------------
:star: | :link: | [Tumblr Search Architecture](http://www.slideshare.net/otisg/search-at-tumblr-nyc-search-meetup)
:star: | :computer: | [Twitter](http://www.slideshare.net/lucenerevolution/twitter-search-lucenerevolutioneu2013-copy)
:star: | :link: | [LinkedIn](http://www.slideshare.net/dtunkelang/structure-personalization-scale-a-deep-dive-into-linkedin-search/23-Life_of_a_Query23Query_RewriterPlannerResultsMergingUserQuerySearchResultsSearch)
:star: | :link: | [LinkedIn](http://www.slideshare.net/VietHaThuc/personalizing-search-at-linkedin)
:star: | :link: | [](http://www.slideshare.net/HiveData/20140521-hivev3shareable)
:star: | :link: | [](http://www.slideshare.net/dtunkelang/search-quality-at-linkedin/65-EFFICIENCY_VS_EXPRESSIVENESS_Build_tree)
:star: | :link: | [](https://speakerdeck.com/tboeghk/evolution-of-e-commerce-search-at-shopping24)
:star: | :tv: | [Shopify](https://www.youtube.com/watch?v=HZw70MbjuGE)
:star: | :link: | [Twitter Search](https://blog.twitter.com/engineering/en_us/a/2011/the-engineering-behind-twitter-s-new-search-experience.html)
:star: | :link: | [Pnterest - Manas: A high performing customized search system](https://medium.com/pinterest-engineering/manas-a-high-performing-customized-search-system-cf189f6ca40f)
:star: | :link: | [Eventbrite](https://www.eventbrite.com/engineering/fundamental-problem-search/)
:star: | :link: | [A Dive into Stack Overflow Jobs Search](https://medium.com/@aurelien.gasser/a-dive-into-stack-overflow-jobs-search-62bc6e628f83)
:star: | :slide: | [[In]formation Retrieval: Search at LinkedIn](https://www.slideshare.net/dtunkelang/information-retrieval-search-at-linkedin)
:star: | :slide: | [Structure, Personalization, Scale: A Deep Dive Into LinkedIn Search](https://www.slideshare.net/dtunkelang/structure-personalization-scale-a-deep-dive-into-linkedin-search)
:star: | :slide: | [Search Quality at LinkedIn](https://www.slideshare.net/dtunkelang/search-quality-at-linkedin)
:star: | :slide: | [Find and be Found: Information Retrieval at LinkedIn](https://www.slideshare.net/dtunkelang/find-and-be-found-information-retrieval-at-linked-in)
:star: | :slide: | [Search at Linkedin](https://www.slideshare.net/HiveData/20140521-hivev3shareable)
:star: | :slide: | [Personalizing Search at LinkedIn](https://www.slideshare.net/VietHaThuc/personalizing-search-at-linkedin)
:star: | :link: | []()

#### Facebook Search
https://www.facebook.com/notes/facebook-engineering/intro-to-facebook-search/365915113919/
[Facebook Search](https://www.facebook.com/notes/facebook-engineering/under-the-hood-building-posts-search/10151755593228920/)
https://www.facebook.com/notes/facebook-engineering/under-the-hood-the-natural-language-interface-of-graph-search/10151432733048920/

*** https://engineeringblog.yelp.com/2018/06/fast-order-search.html
https://engineeringblog.yelp.com/2017/06/moving-yelps-core-business-search-to-elasticsearch.html
Maptype — fast doc-value lookups for map data in Elasticsearch
https://engineeringblog.yelp.com/2019/07/maptype-fast-doc-value-lookups-for-map-data-in-elasticsearch.html

https://engineeringblog.yelp.com/2018/06/android-search-perf-improvements-part-3.html

Reading Between the Lines: How We Make Sense of Users' Searches
https://engineeringblog.yelp.com/2015/02/reading-between-the-lines-how-we-make-sense-of-users-searches.html

## NLP Vs ElasticSearch
[Semantic search with NLP and elasticsearch](https://stackoverflow.com/questions/8772692/semantic-search-with-nlp-and-elasticsearch)
https://www.slideshare.net/GrokkingVN/techtalk-13-grokking-marrying-elasticsearch-with-nlp-to-solve-realworld-search-problems
https://engineering.linkedin.com/blog/2019/04/how-natural-language-processing-help-support
https://dzone.com/articles/learning-to-rank-in-elasticsearch-machine-learning
[Improving Elastic Search Query Result with Query Expansion using Topic Modeling](https://pkghosh.wordpress.com/2018/07/18/improving-elastic-search-query-result-with-query-expansion-using-topic-modeling/)

ElasticSearch uses parts of NLP (e.g., tokenization and stemming). ElasticSearch also includes software engineering elements to ensure a search solution is performant.

## Software
### Lucene
Lucene is a powerful search engine framework that lets us add search capability to our application. It exposes easy-to-use API while hiding all the search-related complex operations. Any application can use this library, not just Solr.
### Solr
Solr is built around Lucene. It is not just a http-wrapper around Lucene but has been known to add more arsenal to Lucene. Solr is ready-to-use out of box. It is a web application that offers infrastructure related and a lot more features in addition to what Lucene offers.

Solr/Lucene or Elastic search are very power search engine frameworks that are used to provide quick search on large text based data. The documents are indexed using inverted index which makes the search very fast while compromising on the speed while adding new documents. The documents once indexed can be easy queried. Both the frameworks come with REST api using which the data can be indexed , queries and deleted.

