# :mag: Search Topics, Terminology

## Search Topics & Terminology

> Cross referenced with Natural Language Processing (NLP) notes.

* Text Analysis / Text Mining
  * [Tokenization](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#tokenization)
  * [Stemming](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#stemming)
  * [Lemmatization](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#lemmatization)
  * [Stop Words Removal](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#stop-words-removal)
  * [Parts of Speech (POS) Tagging](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#parts-of-speech)
  * [TF-IDF](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#tf-idf)
  * [Word Embeddings](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#word-embeddings)
* [Topic Mining](#topic-mining)
* [Search Indexing & Pipelines](#indexing)
* [Query Understanding](#query-understanding)
* [Query Expansion](#query-expansion)
* [Entity Recognition](#entity-recognition)
* [Typeahead](#typeahead)
* [Autocomplete Suggestions](#auto-completeauto-suggest)
* [Did you mean](#did-you-mean)
* [Guided Search](#guided-search)
* [Spell Correction](#spell-correction)
* [Fuzziness](#fuzziness)
* [Faceted Search](#faceted-search)
* [Spam-Resilient Signals](#span-resilient-signals)
* [Ranking & Scoring](#scoring)

### Search - A real-world e-Commerce Implemenation

?|Type|Topic
------------: | ------------- | -------------
:star::star::star:|:newspaper:|[On-Site Search Design Patterns for E-Commerce: Schema Structure, Data Driven Ranking & More](https://project-a.github.io/on-site-search-design-patterns-for-e-commerce/)
:star:|:newspaper:|[Explantion to above article](https://medium.com/@johntucker_48673/elasticsearch-by-example-part-1-a4a38cd97f55)
:star:|:newspaper:|[Reviving an e-commerce search engine using Elasticsearch](https://medium.com/quantyca/reviving-an-e-commerce-search-engine-using-elasticsearch-e540751c6d99)

### Indexing

?|Type|Topic
------------: | ------------- | -------------
:star:|:newspaper:|[How to Reindex One Billion Documents in One Hour at SoundCloud](https://developers.soundcloud.com/blog/how-to-reindex-1-billion-documents-in-1-hour-at-soundcloud)
:star:|:newspaper:|[Facebook - Under the Hood: Indexing and ranking in Graph Search](https://www.facebook.com/notes/facebook-engineering/under-the-hood-indexing-and-ranking-in-graph-search/10151361720763920/)
:star:|:newspaper:|[GraphQL Search Indexing](https://netflixtechblog.com/graphql-search-indexing-334c92e0d8d5)

### Query Understanding

| |Type|Topic
------------: | ------------- | -------------
|:star::star:|:newspaper:|[Query Understanding At TripAdvisor](https://www.tripadvisor.com/engineering/query-understanding-at-tripadvisor/)|
|:star::star:|:computer:|[Better Search Through Query Understanding](https://www.slideshare.net/dtunkelang/better-search-through-query-understanding)|
|:star::star:|:computer:|[Reading Between the Lines: How We Make Sense of Users' Searches](https://engineeringblog.yelp.com/2015/02/reading-between-the-lines-how-we-make-sense-of-users-searches.html)|
:star:|:newspaper:|[Food Discovery with Uber Eats: Building a Query Understanding Engine](https://eng.uber.com/uber-eats-query-understanding/)
:star:|:newspaper:|[Query recommendation by search filters and criteria prediction](http://www.slideshare.net/dhwajr/query-recommendation-by-search-criteria-prediction)
:star:|:newspaper:|[Pinterest - Building a platform to understand search queries](https://medium.com/pinterest-engineering/building-a-platform-to-understand-search-queries-7138e923c06a)
:star:|:newspaper:|[Pinterest - Building a universal search system for Pinterest](https://tech.olx.com/understanding-language-through-search-78ea37be7ac8)

### Query Expansion

| |Type|Topic
------------: | ------------- | -------------
|:star::star:|:newspaper:|[OLX/Avito - Understanding language through search](https://www.tripadvisor.com/engineering/query-understanding-at-tripadvisor/)|
|:star:|:newspaper:|[Grubhub - Query2vec: Search query expansion with query embeddings](https://bytes.grubhub.com/search-query-embeddings-using-query2vec-f5931df27d79)|

### Entity Recognition

| |Type|Topic
------------: | ------------- | -------------
|:star::star:|:newspaper:|[?](?)|

### Topic Mining

### Auto-Complete/Auto-Suggest

Auto Complete – offers search query completions based on what the user has typed.
There are at least two broad types of autocomplete,

* Search Suggest
* Result Suggest

Search Suggest returns suggestions for search phrases, usually based on previously logged searches, ranked by popularity or some other metric. This approach requires logging users' searches and ranking them so that the autocomplete suggestions evolve over time.

The second type of autocomplete is Result Suggest. In this case the suggestions are actual results rather than search phrase suggestions.

Elasticsearch provides a convenient way to get autocomplete up and running quickly with its completion suggester feature.

?|Type|Topic
------------: | ------------- | -------------
:star:|:newspaper:|[Autocomplete best practices](https://blog.griddynamics.com/smart-autocomplete-best-practices/)
:star:|:newspaper:|[Autocomplete with Elasticsearch - Part 1: Prefix Queries](https://blog.mimacom.com/autocomplete-elasticsearch-part1/)
:star:|:newspaper:|[Implementing Autosuggest in Elasticsearch](https://www.rea-group.com/blog/implementing-autosuggest-in-elasticsearch/)
:star:|:newspaper:|[On the Road to a Better ElasticSearch Location Typeahead](https://eatcodeplay.com/on-the-road-to-a-better-elasticsearch-location-typeahead-b75e3eb6dd41)
:star:|:newspaper:|[Multi-Term Auto Completion](https://documentation.spryker.com/docs/multi-term-auto-completion)

#### Guided Search

### Spell Correction

| | Type | Topic
------------: | ------------- | -------------
|:star:|:newspaper:|[Query Segmentation and Spelling Correction](https://towardsdatascience.com/query-segmentation-and-spelling-correction-483173008981)|

#### Did you mean

did-you-mean (DYM)

### Typeahead

? | Type | Topic
------------: | ------------- | -------------
:star:|:newspaper:|[Facebook - The Life of a Typeahead Query](https://www.facebook.com/notes/facebook-engineering/the-life-of-a-typeahead-query/389105248919/)
:star:|:newspaper:|[Pinterest - Rebuilding the user typeahead](https://medium.com/pinterest-engineering/rebuilding-the-user-typeahead-9c5bf9723173)
:star:|:newspaper:|[Cleo: the open source technology behind LinkedIn's typeahead search](https://engineering.linkedin.com/open-source/cleo-open-source-technology-behind-linkedins-typeahead-search)

### Faceted Search

faceted search refers to a method of navigation that allows users to filter data. This term can also be interchanged with other terms such as “guided navigation” or “layered navigation.

Facets allow you to have an overview of your query that corresponds to the summary data within its result set. Let's say that you search for a laptop. You probably would've noticed the counts of entries that fall in that particular group alongside the facet. This lets you guide your search in such a way that you can refine your result set to include or eliminate results according to your choice. You'd also probably notice a distribution histogram like that of a price histogram that lets you select your product that falls in that particular price range.

As faceting evolves and product catalogs become more complex, “nested faceting” has become something of a necessity. Nested faceting -- or hierarchical faceting -- refers to a facet located within another facet. Nesting a facet inside another would give faceting yet another dimension, enabling a user to go on to add more filters (which is a logical OR on the results) to any level they prefer.

Prior to Elasticsearch v1, creating nested faceting was difficult. But the uber-powerful Aggregations feature changes this. Think of aggregations as “facets of facets.”

? | Type | Topic
------------ | ------------- | -------------
:star: | :computer: | [LinkedIn](https://engineering.linkedin.com/faceting/many-facets-faceted-search)

### Fuzziness

### Spam-Resilient Signals

### Scoring

We generally define scoring as giving a higher weight to documents (or data) that meet specific criteria. The objective is often to get a list of documents, sorted on the relevance to the search. Typically, relevance is the numerical output of an algorithm that determines which documents are most textually similar to the query. Elasticsearch employs and enhances standard scoring algorithms and encapsulates these within script_score and function_score.

? | Type | Topic
------------ | ------------- | -------------
:star: | :computer: | [How scoring works in Elasticsearch](https://www.compose.com/articles/how-scoring-works-in-elasticsearch/)
:star: | :computer: | [Scoring using Elasticsearch Scripts](http://qbox.io/blog/scoring-using-elasticsearch-scripts-part1)
:star: | :computer: | [PageRank in Spark](https://developers.soundcloud.com/blog/pagerank-in-spark)
:star: | :computer: | [Search Precision and Recall By Example](https://www.eventbrite.com/engineering/search-precision-and-recall-by-example/)
:star: | :computer: | [Search Engine Marketing](https://www.tripadvisor.com/engineering/improving-sem-landing-page-quality-for-our-experiences-business/)

## ElasticSearch Tutorials

? | Type | Topic
------------ | ------------- | -------------
:star: | :computer: | [Data Exploration With Elasticsearch](http://www.slideshare.net/astensby/data-exploration-with-elasticsearch)
:star: | :computer: | [The Ultimiate Guide for Elasticsearch Plugins](http://www.slideshare.net/synhershko/the-ultimate-guide-for-elasticsearch-plugins)

## Search articles form Engineering Blogs

? | Type | Topic
------------: | ------------- | -------------
:star: |:tv:|[Shopify](https://www.youtube.com/watch?v=HZw70MbjuGE)
:star: | :newspaper: | [Tumblr Search Architecture](http://www.slideshare.net/otisg/search-at-tumblr-nyc-search-meetup)
:star: | :newspaper: | [Twitter](http://www.slideshare.net/lucenerevolution/twitter-search-lucenerevolutioneu2013-copy)
:star: | :newspaper: | [Twitter Search](https://blog.twitter.com/engineering/en_us/a/2011/the-engineering-behind-twitter-s-new-search-experience.html)
:star: | :newspaper: | [Evolution of e-commerce search @ shopping24](https://speakerdeck.com/tboeghk/evolution-of-e-commerce-search-at-shopping24)
:star: | :newspaper: | [Pnterest - Manas: A high performing customized search system](https://medium.com/pinterest-engineering/manas-a-high-performing-customized-search-system-cf189f6ca40f)
:star: | :newspaper: | [Eventbrite](https://www.eventbrite.com/engineering/fundamental-problem-search/)
:star: | :newspaper: | [A Dive into Stack Overflow Jobs Search](https://medium.com/@aurelien.gasser/a-dive-into-stack-overflow-jobs-search-62bc6e628f83)
:star: | :newspaper: | [[In]formation Retrieval: Search at LinkedIn](https://www.slideshare.net/dtunkelang/information-retrieval-search-at-linkedin)
:star: | :newspaper: | [Structure, Personalization, Scale: A Deep Dive Into LinkedIn Search](https://www.slideshare.net/dtunkelang/structure-personalization-scale-a-deep-dive-into-linkedin-search)
:star: | :newspaper: | [Search Quality at LinkedIn](https://www.slideshare.net/dtunkelang/search-quality-at-linkedin)
:star: | :newspaper: | [Find and be Found: Information Retrieval at LinkedIn](https://www.slideshare.net/dtunkelang/find-and-be-found-information-retrieval-at-linked-in)
:star: | :newspaper: | [Search at Linkedin](https://www.slideshare.net/HiveData/20140521-hivev3shareable)
:star: | :newspaper: | [Personalizing Search at LinkedIn](https://www.slideshare.net/VietHaThuc/personalizing-search-at-linkedin)
:star: | :newspaper: | [Search at Linkedin](https://www.slideshare.net/HiveData/20140521-hivev3shareable)
:star: | :newspaper: | [Fast Order Search Using Yelp’s Data Pipeline and Elasticsearch](https://engineeringblog.yelp.com/2018/06/fast-order-search.html)
:star: | :newspaper: | [Search at Linkedin](https://www.slideshare.net/HiveData/20140521-hivev3shareable)
:star: | :newspaper: | [Moving Yelp's Core Business Search to Elasticsearch](https://engineeringblog.yelp.com/2017/06/moving-yelps-core-business-search-to-elasticsearch.html)
:star: | :newspaper: | [Maptype — fast doc-value lookups for map data in Elasticsearch](https://engineeringblog.yelp.com/2019/07/maptype-fast-doc-value-lookups-for-map-data-in-elasticsearch.html)
:star: | :newspaper: | [Performance Improvements for Search on The Yelp Android App - Part 1](https://engineeringblog.yelp.com/2018/05/android-search-perf-improvements-part-1.html)
:star: | :newspaper: | [Reading Between the Lines: How We Make Sense of Users' Searches](https://engineeringblog.yelp.com/2015/02/reading-between-the-lines-how-we-make-sense-of-users-searches.html)

### Facebook Search

 ? | Type | Topic
------------: | ------------- | -------------
:star: |:tv:|[Intro to Facebook Search](https://www.facebook.com/notes/facebook-engineering/intro-to-facebook-search/365915113919/)
:star: |:tv:|[Facebook Search](https://www.facebook.com/notes/facebook-engineering/under-the-hood-building-posts-search/10151755593228920/)
:star: |:tv:|[Under the Hood: The natural language interface of Graph Search](https://www.facebook.com/notes/facebook-engineering/under-the-hood-the-natural-language-interface-of-graph-search/10151432733048920/)

### Search Architecture

| | Type | Topic
------------: | ------------- | -------------
|:star: |:newspaper:|[Search Federation Architecture at LinkedIn](https://engineering.linkedin.com/blog/2018/03/search-federation-architecture-at-linkedin)|
|:star: |:newspaper:|[Architecture of Nautilus, the new Dropbox search engine](https://dropbox.tech/machine-learning/architecture-of-nautilus-the-new-dropbox-search-engine)|

## NLP Vs ElasticSearch

ElasticSearch uses parts of NLP (e.g., tokenization and stemming). ElasticSearch also includes software engineering elements to ensure a search solution is performant.
? | Type | Topic
------------: | ------------- | -------------
:star::star:|:newspaper:|[Semantic search with NLP and elasticsearch](https://stackoverflow.com/questions/8772692/semantic-search-with-nlp-and-elasticsearch)
:star: |:newspaper:|[Marrying Elasticsearch with NLP to solve real-world search problems](https://www.slideshare.net/GrokkingVN/techtalk-13-grokking-marrying-elasticsearch-with-nlp-to-solve-realworld-search-problems)
:star: |:newspaper:|[How natural language processing helps LinkedIn members get support easily](https://engineering.linkedin.com/blog/2019/04/how-natural-language-processing-help-support)
:star: |:newspaper:|[Machine Learning for Smarter Search With Elasticsearch](https://dzone.com/articles/learning-to-rank-in-elasticsearch-machine-learning)
:star: |:newspaper:|[Improving Elastic Search Query Result with Query Expansion using Topic Modeling](https://pkghosh.wordpress.com/2018/07/18/improving-elastic-search-query-result-with-query-expansion-using-topic-modeling/)
