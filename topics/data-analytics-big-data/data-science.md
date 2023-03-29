# Machine Learning

### Model Evaluation Metrics


#### Binary Classfication Metric

Confusion Matrix, Accuracy, Precision, Recall and F1Score

:star::star::star: https://medium.com/analytics-vidhya/confusion-matrix-accuracy-precision-recall-f1-score-ade299cf63cd

You shouldn’t use accuracy on imbalanced problems. Then, it is easy to get a high accuracy score by simply classifying all observations as the majority class.


### Activation Functions

Activation functions transforms the weighted sum of a neuron so that the output is non-linear

#### Sigmoid

The most common sigmoid function used in machine learning is Logistic Function, as the formula below.
https://miro.medium.com/v2/resize:fit:382/format:webp/1*VE7kb7J2lEo5zsUGyHgMWQ.png

The formula is simple, but it is quite useful because it offers us some nice properties:
* It maps the feature space into probability functions
* It uses exponential
* It is differentiable


Sigmoid is used for binary classification

#### Softmax

The Softmax function is a generalized form of the logistic function

the softmax function also has the following advantages so that people are widely using it in multi-class classification problems:

* It maps the feature space into probability functions
* It uses exponential
* It is differentiable

Softmax is used for multi-classification
The probabilities sum will be 1



References: 
* https://towardsdatascience.com/understanding-sigmoid-logistic-softmax-functions-and-cross-entropy-loss-log-loss-dbbbe0a17efb

### Loss Vs. Optimizer

Think of loss function has what to minimize and optimizer how to minimize the loss.

The *loss* is way of measuring difference between target label(s) and prediction label(s).
* Loss could be "mean squared error", "mean absolute error loss also known as L2 Loss", "Cross Entropy" ... and in order to reduce it, weights and biases are updated after each epoch. Optimizer is used to calculate and update them.

The optimization strategies aim at minimizing the cost function.

#### Loss Function Vs. Cost Function
Cost function and loss function are synonymous and used interchangeably, they are different.

A loss function is for a single training example. It is also sometimes called an error function. A cost function, on the other hand, is the average loss over the entire training dataset.

the log magnifies the mistake in the classification, so the misclassification will be penalized much more heavily compared to any linear loss functions. The closer the predicted value is to the opposite of the true value, the higher the loss will be, which will eventually become infinity. That’s exactly what we want a loss function to be. 

* [Tokenization](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#tokenization)
* [Stemming](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#stemming)
* [Lemmatization](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#lemmatization)
* [Stop Words Removal](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#stop-words-removal)
* [Parts of Speech (POS) Tagging](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#parts-of-speech)
* [TF-IDF](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#tf-idf)
* [Word Embeddings](https://github.com/venkataravuri/learning-diary/blob/master/data-science.md#word-embeddings)


#### Cross Entropy Loss 

##### Log Loss - Binary Cross-Entropy Loss




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
