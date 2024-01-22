# :mag: NLP, NLU, Search Concepts

* [NLP - Text Analysis / Text Mining](../data-analytics-big-data/data-science.md)
  * [Tokenization](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#tokenization)
  * [Stemming](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#stemming)
  * [Lemmatization](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#lemmatization)
  * [Stop Words Removal](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#stop-words-removal)
  * [Parts of Speech (POS) Tagging](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#parts-of-speech)
  * [TF-IDF](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#tf-idf)
  * [Word Embeddings](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#word-embeddings)
* [Search Indexing & Pipelines](#search-indexing)
* [Topic Mining](#topic-mining)
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

# Search

## Lexical or Keyword search

Lexical (or sparse) retrieval, relies upon a data structure called an inverted index to perform efficient keyword matching.

Lexical search algorithms are based upon word frequencies.

Lexical involves more advanced techniques like lemmatization and stemming or vice versa.

Sparse retrieval algorithms exist (e.g., TF-IDF), BM25 achieves impressive performance.

Vector space models represent documents and queries as vectors, a long series of numbers and run a similarity function over them to find the closest document.

TF-IDF with the vector space model is to look at the data in a table format. Below shows a document-term matrix, where each row represents a document, and each column represents a unique term/keyword.

Each document can then be represented as a long series of numbers (one for each unique term in the corpus) or in other words a vector.

<img src="https://miro.medium.com/v2/resize:fit:640/format:webp/0*gdNQx9I2MtAqQw30.png" width="70%" height="70%" />

 traditional vectors space model, you are going to end up with a very long vector where most of the elements, values are zero. This is very inefficient, and you can see why they are often called sparse vector embedding…

 TF-IDF etc which results in sparse embedding vectors where most of the vector is zero.

## Semantic Search

“Semantic Search” which should understand the meaning of the words or terms and not just matching the word or linguistic form.

In this context, after converting your data into meaningful vector values, k-nearest neighbor (kNN) search algorithm is utilized to find vector representations in a dataset that are most similar to a query vector. Elasticsearch supports two methods for kNN search, exact brute-force kNN and approximate kNN, also known as ANN.

### Sparse vs Dense embeddings

One major difference between embedding and the traditional vectors created using TF-IDF is that embeddings have a fixed length and do not depend on the number of unique words in the collection.

## Vector embedding, Vector stores and Vector search methods

Dense embedding better than Sparse embeddings?

 Elasticsearch converts text field data into a searchable format by performing text analysis.
## Text Analysis / Text Mining

### Tokenization

Break the text into words.

Popular subword-based tokenization algorithms are WordPiece, Byte-Pair Encoding (BPE), Unigram, and SentencePiece.	

word-based tokenization (very large vocabulary size, large number of OOV tokens, and different meaning of very similar words) and character-based tokenization (very long sequences and less meaningful individual tokens).

The subword-based tokenization algorithms do not split the frequently used words into smaller subwords. It rather splits the rare words into smaller meaningful subwords. For example, “boy” is not split but “boys” is split into “boy” and “s”. This helps the model learn that the word “boys” is formed using the word “boy” with slightly different meanings but the same root word.

- Bye-Pair Encoding (BPE) used by GPT-2 and RoBERTa.
- WordPiece used by BERT and DistilBERT

### Word Embeddings

Word2Vec - https://www.youtube.com/watch?v=gQddtTdmG_8

### TF-IDF

|Rating|Type|Topic
------------: | ------------- | -------------
|:star::star::star:|:newspaper:|[?](https://www.analyticsvidhya.com/blog/2020/02/quick-introduction-bag-of-words-bow-tf-idf/)
||:newspaper:|[?](https://www.slideshare.net/DanSullivan10/a-first-look-at-tf-idfpdx-data-science-meetup)

### Normalizing

|Rating|Type|Topic
------------: | ------------- | -------------
|:star:|:newspaper:|[?](https://qbox.io/blog/introduction-to-elasticsearch-analyzers)
||:newspaper:|[?](https://engineering.linkedin.com/blog/2019/04/how-natural-language-processing-help-support)
||:newspaper:|[?](https://logz.io/blog/language-analyzers-tokenizers-not-built-elasticsearch-where-find-them/)
||:newspaper:|[?](https://www.elastic.co/blog/text-classification-made-easy-with-elasticsearch)

#### Stemming

Helps normalize the spelling of words, for instance translating the tokens 'sing', 'sings', and 'singing' all into the single stem 'sing'.
In ElasticSeaarch, you can use 'snowball' analyzer.

#### Lemmatization

Find the basic form of each word variation in the context. Examples are "account" from "accounts" and "break" from "broke."

### Stop Word Removal

Stop Word Filter: Filter out common words. In English, there are hundreds of stop words like "a," "my," and "on," to name a few, that have little bearing on relevance or meaning, and thus can safely be removed from the query in order to target the more valuable words.

### Part of Speech (PoS) Tagging

Part of Speech (PoS) Filter: Read through text and give each word a PoS based on the context. There are nine parts in English: adjective, adverb, conjunction, determiner, noun, number, preposition, pronoun, and verb. We only capture nouns, verbs, proper nouns, and adjectives, as they together represent the purpose of a text.

### Word Embeddings

|Rating|Type|Topic
------------: | ------------- | -------------
|:star:|:newspaper:|[?](https://www.analyticsvidhya.com/blog/2017/06/word-embeddings-count-word2veec/)

## NLP Engines

### NLU Pipeline - Rasa

NLU pipeline defines the processing steps that convert unstructured user messages into intents and entities.

[Intents & Entities: Understanding the Rasa NLU Pipeline](https://rasa.com/blog/intents-entities-understanding-the-rasa-nlu-pipeline/)

Different types of components that you can expect to find in a pipeline. The main ones are:
- Tokenizers -  Split an utterance into smaller chunks of text, known as tokens. 
- Featurizers - Featurizers generate numeric features for machine learning models.
- Intent Classifiers
- Entity Extractors

### Semantic Search

Semantic search is basically search with meaning.

Elasticsearch has a very weak semantic search support but you can go around it using faceted searching and bag of words.

> Elasticsearch 7.3 introduced introduced text similarity search with vector fields.

They describe the application of using text embeddings (e.g., word embeddings and sentence embeddings) to implement this sort of semantic similarity measure

Use BERT embedding for your sentences and add an embedding field to your ElasticSearch, as it is described in https://www.elastic.co/blog/text-similarity-search-with-vectors-in-elasticsearch

For BERT embedding I suggest to use sentence-transformers from Huggingface library. You can find sample codes in https://towardsdatascience.com/how-to-build-a-semantic-search-engine-with-transformers-and-faiss-dcbea307a0e8

### Knowledge Base (KB) Article Suggestor

A state-of-the-art search engine paired with a question-answering model. Alternative to Keyword-based search (Elastic/Coveo) which can’t answer questions.

Personas: Customers, TSE, TAM, CSMs

NLP + Col(v)BERT + Document Retriever + Question Answering

1. Index our knowledge base
2. Receive a question
3. Find responsive documents
4. Return the answer to the question

Col(v)BERT, our custom-trained version of ColBERT, then searches for passages that contain the answer to the question.

Major Components
- Website scraping service
- Content management managemnt
- and index management system.




Used machine learning to automate below tasks,

- **Data Clustering** - Measure distance between words and/or documents to automatically discover topics (e.g. by **data clustering**) and **classify** query to one of these topics.

#### Geo spatial queries in Elastic

Map the field as a **geo_point** or for more flexibility to store other types of geolocations (e.g., polygons or linestrings), then map as a **geo_shape**.
```
{
  "mappings" : {
    "TYPE_NAME" : {
      "properties" : {
        "fieldName" : { "type" : "geo_point" }
      }
    }
  }
}
```
Once mapped, you can insert the location details using the point type.
```
{
  "fieldName" : {
    "type" : "point",
    "coordinates" : {
      "lat" : latitude,
      "lon" : longitude
    }
  }
}
```

Run a **geo_distance** filter to find points within the desired distance:
```
{
  "filtered" : {
    "query" : { "match_all" : {} },
    "filter" : {
      "geo_distance" : {
        "distance" : "10mi",
        "fieldName" : [ longitude, latitude ]
      }
    }
  }
}
```

#### Ingestion Pipelines

Ingest pipelines let you perform common transformations on your data before indexing. For example, you can use pipelines to remove fields, extract values from text, and enrich your data.

A pipeline consists of a series of configurable tasks called processors. Each processor runs sequentially, making specific changes to incoming documents. After the processors have run, Elasticsearch adds the transformed documents to your data stream or index.

## e-commerce search solutions

Rating|Type|Topic
------------: | ------------- | -------------
:star::star::star:|:newspaper:|[On-Site Search Design Patterns for E-Commerce: Schema Structure, Data Driven Ranking & More](https://project-a.github.io/on-site-search-design-patterns-for-e-commerce/)
:star:|:newspaper:|[Explantion to above article](https://medium.com/@johntucker_48673/elasticsearch-by-example-part-1-a4a38cd97f55)
:star:|:newspaper:|[Reviving an e-commerce search engine using Elasticsearch](https://medium.com/quantyca/reviving-an-e-commerce-search-engine-using-elasticsearch-e540751c6d99)


## Search Indexing

Rating|Type|Topic
------------: | ------------- | -------------
:star:|:newspaper:|[How to Reindex One Billion Documents in One Hour at SoundCloud](https://developers.soundcloud.com/blog/how-to-reindex-1-billion-documents-in-1-hour-at-soundcloud)
:star:|:newspaper:|[Facebook - Under the Hood: Indexing and ranking in Graph Search](https://www.facebook.com/notes/facebook-engineering/under-the-hood-indexing-and-ranking-in-graph-search/10151361720763920/)
:star:|:newspaper:|[GraphQL Search Indexing](https://netflixtechblog.com/graphql-search-indexing-334c92e0d8d5)

### Query Understanding

|Rating|Type|Topic
------------: | ------------- | -------------
|:star::star:|:newspaper:|[Query Understanding At TripAdvisor](https://www.tripadvisor.com/engineering/query-understanding-at-tripadvisor/)|
|:star::star:|:computer:|[Better Search Through Query Understanding](https://www.slideshare.net/dtunkelang/better-search-through-query-understanding)|
|:star::star:|:computer:|[Reading Between the Lines: How We Make Sense of Users' Searches](https://engineeringblog.yelp.com/2015/02/reading-between-the-lines-how-we-make-sense-of-users-searches.html)|
:star:|:newspaper:|[Food Discovery with Uber Eats: Building a Query Understanding Engine](https://eng.uber.com/uber-eats-query-understanding/)
:star:|:newspaper:|[Query recommendation by search filters and criteria prediction](http://www.slideshare.net/dhwajr/query-recommendation-by-search-criteria-prediction)
:star:|:newspaper:|[Pinterest - Building a platform to understand search queries](https://medium.com/pinterest-engineering/building-a-platform-to-understand-search-queries-7138e923c06a)
:star:|:newspaper:|[Pinterest - Building a universal search system for Pinterest](https://tech.olx.com/understanding-language-through-search-78ea37be7ac8)

### Query Expansion

|Rating|Type|Topic
------------: | ------------- | -------------
|:star::star:|:newspaper:|[OLX/Avito - Understanding language through search](https://www.tripadvisor.com/engineering/query-understanding-at-tripadvisor/)|
|:star:|:newspaper:|[Grubhub - Query2vec: Search query expansion with query embeddings](https://bytes.grubhub.com/search-query-embeddings-using-query2vec-f5931df27d79)|

### Entity Recognition

|Rating|Type|Topic
------------: | ------------- | -------------
|:star::star:|:newspaper:|[?](?)|

### Topic Mining

TODO

### Auto-Complete/Auto-Suggest

Auto Complete – offers search query completions based on what the user has typed.
There are at least two broad types of autocomplete,

* Search Phrase Suggestions
* Serch Result Suggestions

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

|Rating|Type|Topic
------------: | ------------- | -------------
|:star:|:newspaper:|[Query Segmentation and Spelling Correction](https://towardsdatascience.com/query-segmentation-and-spelling-correction-483173008981)|

#### Did you mean

did-you-mean (DYM)

### Typeahead

Rating | Type | Topic
------------: | ------------- | -------------
:star:|:newspaper:|[Facebook - The Life of a Typeahead Query](https://www.facebook.com/notes/facebook-engineering/the-life-of-a-typeahead-query/389105248919/)
:star:|:newspaper:|[Pinterest - Rebuilding the user typeahead](https://medium.com/pinterest-engineering/rebuilding-the-user-typeahead-9c5bf9723173)
:star:|:newspaper:|[Cleo: the open source technology behind LinkedIn's typeahead search](https://engineering.linkedin.com/open-source/cleo-open-source-technology-behind-linkedins-typeahead-search)

### Faceted Search

faceted search refers to a method of navigation that allows users to filter data. This term can also be interchanged with other terms such as “guided navigation” or “layered navigation.

Facets allow you to have an overview of your query that corresponds to the summary data within its result set. Let's say that you search for a laptop. You probably would've noticed the counts of entries that fall in that particular group alongside the facet. This lets you guide your search in such a way that you can refine your result set to include or eliminate results according to your choice. You'd also probably notice a distribution histogram like that of a price histogram that lets you select your product that falls in that particular price range.

As faceting evolves and product catalogs become more complex, “nested faceting” has become something of a necessity. Nested faceting -- or hierarchical faceting -- refers to a facet located within another facet. Nesting a facet inside another would give faceting yet another dimension, enabling a user to go on to add more filters (which is a logical OR on the results) to any level they prefer.

Prior to Elasticsearch v1, creating nested faceting was difficult. But the uber-powerful Aggregations feature changes this. Think of aggregations as “facets of facets.”

Rating | Type | Topic
------------ | ------------- | -------------
:star: | :computer: | [LinkedIn](https://engineering.linkedin.com/faceting/many-facets-faceted-search)

### Fuzziness

### Spam-Resilient Signals

### Scoring

We generally define scoring as giving a higher weight to documents (or data) that meet specific criteria. The objective is often to get a list of documents, sorted on the relevance to the search. Typically, relevance is the numerical output of an algorithm that determines which documents are most textually similar to the query. Elasticsearch employs and enhances standard scoring algorithms and encapsulates these within script_score and function_score.

Rating | Type | Topic
------------ | ------------- | -------------
:star: | :computer: | [How scoring works in Elasticsearch](https://www.compose.com/articles/how-scoring-works-in-elasticsearch/)
:star: | :computer: | [Scoring using Elasticsearch Scripts](http://qbox.io/blog/scoring-using-elasticsearch-scripts-part1)
:star: | :computer: | [PageRank in Spark](https://developers.soundcloud.com/blog/pagerank-in-spark)
:star: | :computer: | [Search Precision and Recall By Example](https://www.eventbrite.com/engineering/search-precision-and-recall-by-example/)
:star: | :computer: | [Search Engine Marketing](https://www.tripadvisor.com/engineering/improving-sem-landing-page-quality-for-our-experiences-business/)

## ElasticSearch Tutorials

Rating | Type | Topic
------------ | ------------- | -------------
:star: | :computer: | [Data Exploration With Elasticsearch](http://www.slideshare.net/astensby/data-exploration-with-elasticsearch)
:star: | :computer: | [The Ultimiate Guide for Elasticsearch Plugins](http://www.slideshare.net/synhershko/the-ultimate-guide-for-elasticsearch-plugins)

## Search articles form Engineering Blogs

Rating | Type | Topic
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

 Rating | Type | Topic
------------: | ------------- | -------------
:star: |:tv:|[Intro to Facebook Search](https://www.facebook.com/notes/facebook-engineering/intro-to-facebook-search/365915113919/)
:star: |:tv:|[Facebook Search](https://www.facebook.com/notes/facebook-engineering/under-the-hood-building-posts-search/10151755593228920/)
:star: |:tv:|[Under the Hood: The natural language interface of Graph Search](https://www.facebook.com/notes/facebook-engineering/under-the-hood-the-natural-language-interface-of-graph-search/10151432733048920/)

### Search Architecture

| Rating | Type | Topic
------------: | ------------- | -------------
|:star: |:newspaper:|[Search Federation Architecture at LinkedIn](https://engineering.linkedin.com/blog/2018/03/search-federation-architecture-at-linkedin)|
|:star: |:newspaper:|[Architecture of Nautilus, the new Dropbox search engine](https://dropbox.tech/machine-learning/architecture-of-nautilus-the-new-dropbox-search-engine)|

## NLP Vs ElasticSearch

ElasticSearch uses parts of NLP (e.g., tokenization and stemming). ElasticSearch also includes software engineering elements to ensure a search solution is performant.
Rating | Type | Topic
------------: | ------------- | -------------
:star::star:|:newspaper:|[Semantic search with NLP and elasticsearch](https://stackoverflow.com/questions/8772692/semantic-search-with-nlp-and-elasticsearch)
:star: |:newspaper:|[Marrying Elasticsearch with NLP to solve real-world search problems](https://www.slideshare.net/GrokkingVN/techtalk-13-grokking-marrying-elasticsearch-with-nlp-to-solve-realworld-search-problems)
:star: |:newspaper:|[How natural language processing helps LinkedIn members get support easily](https://engineering.linkedin.com/blog/2019/04/how-natural-language-processing-help-support)
:star: |:newspaper:|[Machine Learning for Smarter Search With Elasticsearch](https://dzone.com/articles/learning-to-rank-in-elasticsearch-machine-learning)
:star: |:newspaper:|[Improving Elastic Search Query Result with Query Expansion using Topic Modeling](https://pkghosh.wordpress.com/2018/07/18/improving-elastic-search-query-result-with-query-expansion-using-topic-modeling/)

### ElasticSearch Cluster

<img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fimg-blog.csdnimg.cn%2F20191216165538697.png%3Fx-oss-process%3Dimage%2Fwatermark%2Ctype_ZmFuZ3poZW5naGVpdGk%2Cshadow_10%2Ctext_aHR0cHM6Ly9lbGFzdGljc3RhY2suYmxvZy5jc2RuLm5ldA%3D%3D%2Csize_16%2Ccolor_FFFFFF%2Ct_70&f=1&nofb=1&ipt=71ec2d51747b12bd91fe3bfdb807a8f4b92b0c604d4d1e10da991ae86c69c7b8&ipo=images" height="35%" width="35%" />

Master Eligible Nodes

The master node is responsible for lightweight cluster-wide actions such as creating or deleting an index, tracking which nodes are part of the cluster, and deciding which shards to allocate to which nodes.


Voting-only master-eligible node

A voting-only master-eligible node is a node that participates in master elections but which will not act as the cluster’s elected master node

Define a node’s roles by setting node.roles in elasticsearch.yml

Data nodes hold the shards that contain the documents you have indexed. Data nodes handle data related operations like CRUD, search, and aggregations. The main benefit of having dedicated data nodes is the separation of the master and data roles. To create a dedicated data node, set:
```
node.roles: [ data ]
```

Ingest Node

Ingest nodes are able to apply an ingest pipeline to a document in order to transform and enrich the document before indexing. 

Other Nodes

- ml node
- data_content node
- data_hot node
- data_warm, data_cold, data_frozen nodes



<img height="50%" width="50%" src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fimg2020.cnblogs.com%2Fblog%2F794174%2F202005%2F794174-20200508144128041-791009348.png&f=1&nofb=1&ipt=df248ec229a719164cd68d964cf335cde3def91a7b891d74a326e2e2dc020818&ipo=images" />
