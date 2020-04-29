# :mag: Search Technologies, :thumbsup: Recommendation Engines

## Search Topics & Terminology
- Indexing & Pipelines
- Autocomplete Suggestions
- Guided suggestions
- Spell Correction
- Typeahead
- Fuzziness
- Spam-Resilient Signals
- Faceted Search
- Ranking & Scoring
- Textual Relevancy
    how: exact match, query proximity
    where: name, title, tag, mention, body, etc
    
    Search Precision and Recall By Example
    https://www.eventbrite.com/engineering/search-precision-and-recall-by-example/
    
    Search Engine Marketing
    https://www.tripadvisor.com/engineering/improving-sem-landing-page-quality-for-our-experiences-business/
    
## Recommendations

Trending
Recommendations
https://www.eventbrite.com/engineering/building-a-marketplace-search-and-recommendation-at-eventbrite/

[Can a machine surprise you? We believe so.](https://developers.soundcloud.com/blog/introducing_suggested_tracks)

https://netflixtechblog.com/highlights-from-prs2016-workshop-57f36fa34b44

https://netflixtechblog.com/recommending-for-the-world-8da8cbcf051b

## Software
### Lucene
Lucene is a powerful search engine framework that lets us add search capability to our application. It exposes easy-to-use API while hiding all the search-related complex operations. Any application can use this library, not just Solr.
### Solr
Solr is built around Lucene. It is not just a http-wrapper around Lucene but has been known to add more arsenal to Lucene. Solr is ready-to-use out of box. It is a web application that offers infrastructure related and a lot more features in addition to what Lucene offers.

Solr/Lucene or Elastic search are very power search engine frameworks that are used to provide quick search on large text based data. The documents are indexed using inverted index which makes the search very fast while compromising on the speed while adding new documents. The documents once indexed can be easy queried. Both the frameworks come with REST api using which the data can be indexed , queries and deleted.

### ElasticSearch Tutorials
Stars | Type | Topic
------------ | ------------- | -------------
:star: | :computer: | [](http://www.slideshare.net/astensby/data-exploration-with-elasticsearch)
:star: | :computer: | [](http://www.slideshare.net/synhershko/the-ultimate-guide-for-elasticsearch-plugins)
:star: | :link: | []()

### e-commerce search real-world implemenation
:star::star::star::star::star: https://project-a.github.io/on-site-search-design-patterns-for-e-commerce/
Explanation article, https://medium.com/@johntucker_48673/elasticsearch-by-example-part-1-a4a38cd97f55

https://medium.com/quantyca/reviving-an-e-commerce-search-engine-using-elasticsearch-e540751c6d99

### Articles form Engineering Blogs
Stars | Type | Topic
------------ | ------------- | -------------
:star: | :link: | [Tumblr Search Architecture](http://www.slideshare.net/otisg/search-at-tumblr-nyc-search-meetup)
:star: | :computer: | [Twitter](http://www.slideshare.net/lucenerevolution/twitter-search-lucenerevolutioneu2013-copy)
:star: | :link: | [LinkedIn](http://www.slideshare.net/dtunkelang/structure-personalization-scale-a-deep-dive-into-linkedin-search/23-Life_of_a_Query23Query_RewriterPlannerResultsMergingUserQuerySearchResultsSearch)
:star: | :link: | [LinkedIn](http://www.slideshare.net/VietHaThuc/personalizing-search-at-linkedin)
:star: | :link: | [LinkedIn](https://engineering.linkedin.com/faceting/many-facets-faceted-search)
:star: | :link: | [](http://www.slideshare.net/HiveData/20140521-hivev3shareable)
:star: | :link: | [](http://www.slideshare.net/dtunkelang/search-quality-at-linkedin/65-EFFICIENCY_VS_EXPRESSIVENESS_Build_tree)
:star: | :link: | [](http://www.slideshare.net/dhwajr/query-recommendation-by-search-criteria-prediction)
:star: | :link: | [](https://speakerdeck.com/tboeghk/evolution-of-e-commerce-search-at-shopping24)
:star: | :tv: | [Shopify](https://www.youtube.com/watch?v=HZw70MbjuGE)
:star: | :link: | [Twitter Search](https://blog.twitter.com/engineering/en_us/a/2011/the-engineering-behind-twitter-s-new-search-experience.html)
:star: | :link: | [Pinterest - Building a platform to understand search queries](https://medium.com/pinterest-engineering/building-a-platform-to-understand-search-queries-7138e923c06a)
:star: | :link: | [Pnterest - Manas: A high performing customized search system](https://medium.com/pinterest-engineering/manas-a-high-performing-customized-search-system-cf189f6ca40f)
:star: | :link: | [Eventbrite](https://www.eventbrite.com/engineering/fundamental-problem-search/)
:star: | :link: | []()
:star: | :link: | []()
:star: | :link: | []()
:star: | :link: | []()
:star: | :link: | []()
:star: | :link: | []()
:star: | :link: | [A Dive into Stack Overflow Jobs Search](https://medium.com/@aurelien.gasser/a-dive-into-stack-overflow-jobs-search-62bc6e628f83)

[How to Reindex One Billion Documents in One Hour at SoundCloud](https://developers.soundcloud.com/blog/how-to-reindex-1-billion-documents-in-1-hour-at-soundcloud)

[PageRank in Spark](https://developers.soundcloud.com/blog/pagerank-in-spark)


[Query Understanding At TripAdvisor](https://www.tripadvisor.com/engineering/query-understanding-at-tripadvisor/)

[Facebook Search](https://www.facebook.com/notes/facebook-engineering/under-the-hood-building-posts-search/10151755593228920/)

https://www.facebook.com/notes/facebook-engineering/under-the-hood-indexing-and-ranking-in-graph-search/10151361720763920/

https://www.facebook.com/notes/facebook-engineering/the-life-of-a-typeahead-query/389105248919/

https://www.facebook.com/notes/facebook-engineering/intro-to-facebook-search/365915113919/

https://www.facebook.com/notes/facebook-engineering/under-the-hood-the-natural-language-interface-of-graph-search/10151432733048920/






https://netflixtechblog.com/graphql-search-indexing-334c92e0d8d5


*** https://engineeringblog.yelp.com/2018/06/fast-order-search.html
https://engineeringblog.yelp.com/2017/06/moving-yelps-core-business-search-to-elasticsearch.html
Maptype — fast doc-value lookups for map data in Elasticsearch
https://engineeringblog.yelp.com/2019/07/maptype-fast-doc-value-lookups-for-map-data-in-elasticsearch.html

https://engineeringblog.yelp.com/2018/06/android-search-perf-improvements-part-3.html



Reading Between the Lines: How We Make Sense of Users' Searches
https://engineeringblog.yelp.com/2015/02/reading-between-the-lines-how-we-make-sense-of-users-searches.html



### Inverted Index
The inverted index is at the core of the Lucene technology, its duty is to map terms to documents, so that these documents can easily be found.

Figure: Mapping back a set of ingredients to the original recipes. Flour is used in all the bakery products, eggs are only in the Sacher cake, water (ice) is mixed even into the bratwurst (proteins would “melt” during meat mincing).

Great Article: https://qbox.io/blog/introduction-to-elasticsearch-analyzers
Scoring
We generally define scoring as giving a higher weight to documents (or data) that meet specific criteria. The objective is often to get a list of documents, sorted on the relevance to the search. Typically, relevance is the numerical output of an algorithm that determines which documents are most textually similar to the query. Elasticsearch employs and enhances standard scoring algorithms and encapsulates these within script_score and function_score.


### Typeahead

https://medium.com/pinterest-engineering/rebuilding-the-user-typeahead-9c5bf9723173
https://engineering.linkedin.com/open-source/cleo-open-source-technology-behind-linkedins-typeahead-search


Great Article: http://qbox.io/blog/scoring-using-elasticsearch-scripts-part1

Autocomplete/Auto-Suggest
 did-you-mean (DYM)

AutoComplete – offers search query completions based on what the user has typed.

There are at least two broad types of autocomplete, what I will call Search Suggest, and Result Suggest. Search Suggest returns suggestions for search phrases, usually based on previously logged searches, ranked by popularity or some other metric. This approach requires logging users' searches and ranking them so that the autocomplete suggestions evolve over time.


The second type of autocomplete is Result Suggest. In this case the suggestions are actual results rather than search phrase suggestions.

[Autocomplete best practices](https://blog.griddynamics.com/smart-autocomplete-best-practices/)
:star::start::star::star: [Autocomplete with Elasticsearch - Part 1: Prefix Queries](https://blog.mimacom.com/autocomplete-elasticsearch-part1/)
https://www.rea-group.com/blog/implementing-autosuggest-in-elasticsearch/
https://eatcodeplay.com/on-the-road-to-a-better-elasticsearch-location-typeahead-b75e3eb6dd41
https://documentation.spryker.com/docs/multi-term-auto-completion

Completion Suggest

Elasticsearch provides a convenient way to get autocomplete up and running quickly with its completion suggester feature.


faceted search refers to a method of navigation that allows users to filter data. This term can also be interchanged with other terms such as “guided navigation” or “layered navigation.

Facets allow you to have an overview of your query that corresponds to the summary data within its result set. Let's say that you search for a laptop. You probably would've noticed the counts of entries that fall in that particular group alongside the facet. This lets you guide your search in such a way that you can refine your result set to include or eliminate results according to your choice. You'd also probably notice a distribution histogram like that of a price histogram that lets you select your product that falls in that particular price range.


As faceting evolves and product catalogs become more complex, “nested faceting” has become something of a necessity. Nested faceting -- or hierarchical faceting -- refers to a facet located within another facet. Nesting a facet inside another would give faceting yet another dimension, enabling a user to go on to add more filters (which is a logical OR on the results) to any level they prefer.

Prior to Elasticsearch v1, creating nested faceting was difficult. But the uber-powerful Aggregations feature changes this. Think of aggregations as “facets of facets.”

### Scoring
https://www.compose.com/articles/how-scoring-works-in-elasticsearch/

