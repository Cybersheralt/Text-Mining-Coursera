# Applied Text Mining Coursera
> Here lies my assignments for course [Applied Text Mining in Python](https://www.coursera.org/learn/python-text-mining).
> There were 4 assignments based on using Python and its libraries for Text Mining.
> Numeration of assignments responds to numeration on Coursera.


## Table of Contents
* [Assignment 1](#assignment-1)
* [Assignment 2](#assignment-2)
* [Assignment 3](#assignment-3)
* [Assignment 4](#assignment-4)
* [List of used libraries](#list-of-used-libraries)
* [List of used ML models](#list-of-used-ml-models)


## Assignment 1
This assignment is about *"working with messy medical data and using regex to extract relevant infromation from the data."*.

Firstly I found all dates using regex. These are examples of date format in dataset:

- 04/20/2009; 04/20/09; 4/20/09; 4/3/09
- Mar-20-2009; Mar 20, 2009; March 20, 2009; Mar. 20, 2009; Mar 20 2009
- 20 Mar 2009; 20 March 2009; 20 Mar. 2009; 20 March, 2009
- Mar 20th, 2009; Mar 21st, 2009; Mar 22nd, 2009
- Feb 2009; Sep 2009; Oct 2010
- 6/2008; 12/2009
- 2009; 2010

After that I sorted all dates in ascending chronological order, which was the main task.


## Assignment 2
This assignment is called ***Introduction to NLTK***. It is divided in 2 parts.

### Part 1 - Analyzing Moby Dick
This part consists of 8 questions which are based on making some basic text mining using `nltk` library.

#### Example of question
What are the 5 most frequent parts of speech in this text? What is their frequency?

### Part 2 - Spelling Recommender
This part consists of 3 tasks which goal is to *"create three different spelling recommenders, that each take a list of misspelled words and recommends a correctly spelled word for every word in the list"*.

#### Distance metrics
Following metrics were used in this part:

- Jaccard distance on the trigrams of the two words
- Jaccard distance on the 4-grams of the two words
- Edit distance on the two words with transpositions.


## Assignment 3
This assignment is about exploring text message data and creating models to predict if a message is spam or not.

### List of used models
- Multinomial Naive Bayes classifier with smoothing `alpha=0.1` and training data transformed using a Count Vectorizer with default parameters (AUC-score was ***0.972***)
- Multinomial Naive Bayes classifier with smoothing `alpha=0.1` and training data transformed using a Tfidf Vectorizer ignoring terms that have a document frequency strictly lower than **3** (AUC-score was ***0.942***)
- `SVC` with regularization `C=10000` and training data transformed using a Tfidf Vectorizer ignoring terms that have a document frequency strictly lower than **5** + additional feature, **the length of document (number of characters)** (AUC-score was ***0.958***)
- Logisitic regression classifier with regularization `C=100` and training data transformed using a Tfidf Vectorizer ignoring terms that have a document frequency strictly lower than **5** and using **word n-grams from n=1 to n=3** (AUC-score was ***0.965***). Two additional features were added to this model:
  - the length of document (number of characters)
  - number of digits per document
- Logisitic regression classifier with regularization `C=100` and training data transformed using a Count Vectorizer ignoring terms that have a document frequency strictly lower than **5** and using **word n-grams from n=2 to n=5** (AUC-score was ***0.979***). Three additional features were added to this model:
  - the length of document (number of characters)
  - number of digits per document
  - number of non-word characters (anything other than a letter, digit or underscore).
 
 
## Assignment 4
This assignment is called ***Document Similarity & Topic Modelling*** and divided in 2 parts.

### Part 1 - Document Similarity
For the first part of this assignment I completed the functions `doc_to_synsets` and `similarity_score` which were used by `document_path_similarity` to find the path similarity between two documents.

#### Provided functions:
- `convert_tag`: converts the tag given by `nltk.pos_tag` to a tag used by `wordnet.synsets`. Function is used in `doc_to_synsets`.
- `document_path_similarity`: computes the symmetrical path similarity between two documents by finding the synsets in each document using `doc_to_synsets`, then computing similarities using `similarity_score`.

#### Written functions:
- `doc_to_synsets`: returns a list of synsets in document. This function tokenizes and part of speech tags the document using `nltk.word_tokenize` and `nltk.pos_tag`. Then it finds each tokens corresponding synset using `wn.synsets(token, wordnet_tag)`. The first synset match is used. If there is no match, that token is skipped.
- `similarity_score`: returns the normalized similarity score of a list of synsets (s1) onto a second list of synsets (s2). For each synset in s1, finds the synset in s2 with the largest similarity value. Sums all of the largest similarity values together and normalizes this value by dividing it by the number of largest similarity values found. Missing values are ignored.
- `most_similar_docs`: using `document_path_similarity`, finds the pair of documents in paraphrases which has the maximum similarity score.
- `label_accuracy`: provides labels for the twenty pairs of documents by computing the similarity for each pair using `document_path_similarity`. If the score is greater than 0.75, label is paraphrase (1), else label is not paraphrase (0). Reports accuracy of the classifier using scikit-learn's `accuracy_score`.


### Part 2 - Topic Modelling
For the second part of this assignment, I used Gensim's LDA (Latent Dirichlet Allocation) model to model topics. I used `gensim.models.ldamodel.LdaModel` constructor to estimate LDA model parameters on the corpus, and saved it to the variable `ldamodel`.

Using `ldamodel`, I found a list of the 10 topics and the most significant 10 words in each topic.

For the new document `new_doc`, I found the topic distribution.
```
new_doc = ["\n\nIt's my understanding that the freezing will start to occur because \
of the\ngrowing distance of Pluto and Charon from the Sun, due to it's\nelliptical orbit. \
It is not due to shadowing effects. \n\n\nPluto can shadow Charon, and vice-versa.\n\nGeorge \
Krumins\n-- "]
```

In the end, from the list of given topics, I assigned topic names to the topics I found.
Topics: Health, Science, Automobiles, Politics, Government, Travel, Computers & IT, Sports, Business, Society & Lifestyle, Religion, Education.


## List of used libraries
- Pandas
- Numpy
- Scipy
- Scikit-learn
- re
- nltk
- pickle
- gensim

## List of used ML models
- Support Vector Classifier
- Logisitic regression
- Multinomial Naive Bayes classifier
