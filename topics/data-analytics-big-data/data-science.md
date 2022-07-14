# Machine Learning

## Feature Engineering

|Rating|Type|Topic
------------: | ------------- | -------------
|:star:|:newspaper:|[Dealing with missing values](https://www.kaggle.com/alexisbcook/missing-values)

# NLP

## Text Analysis / Text Mining

### Tokenization

Break the text into words.

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

## Neural Networks

### Deep Learning

|Rating|Type|Topic
------------: | ------------- | -------------
|:star:|:tv:|[MIT Deep Learning Course - Lex Fridman](https://www.youtube.com/playlist?list=PLrAXtmErZgOeiKm4sgNOknGvNjby9efdf)

#### CNN

|Rating|Type|Topic
------------: | ------------- | -------------
|:star:|:tv:|[Nice intution about CNN, Convolutional Neural Networks](https://www.youtube.com/watch?v=xg2ajb3csgk&list=PLXAoLgwZtKcgGE2-Wy23EUE4Q03s-YVwF&index=3)|

#### RNN

|Rating|Type|Topic
------------: | ------------- | -------------
|:star:|:tv:|[A friendly introduction to Recurrent Neural Networks](https://www.youtube.com/watch?v=UNmqTiOnRfg)

#### PyTorch

|Rating|Type|Topic
------------: | ------------- | -------------
|:star:|:newspaper:|[Pytorch introduction - www.kdnuggets.com](https://www.kdnuggets.com/2019/09/gentle-introduction-pytorch-12.html)
