---
layout: post
title: Stemming and Lemmatization with Python and NLTK
explanation: We are going to explore how Python and NLTK provide us easy ways to lemmatize and stem our text.
category: Text-mining
meta: Using Python library nltk for stemming and lemmatization.
tags: [ text-mining] 
excerpt_separator: <!--more-->
---

Stemming and lemmatization are essential for many text mining tasks such as information retrieval,
text summarization, topic extraction as well as translation. 
<!--more-->
##  Stemming
It allows us to remove the prefixes, suffixes from a word and and change it to its base form. However, this stem form might not exist in dictionary. Let's take a look at how NLTK stems words. 

#### Using PorterStemmer
Porter stemmer is the most commonly used stemmer because of its good results.
```python
#let's import the libraries
from nltk.stem import PorterStemmer

# the most commonly used stemmer
ps = PorterStemmer()
print ps.stem("lying"), ps.stem("lies"), ps.stem("lied")
```

```output
lie lie lie
```
#### Using LancasterStemmer
Lets compare our results with LancesterStemmer which is based on  is based on the Lancaster stemming algorithm. It has more than 120 rules for getting stem words.
```python
#let's import the libraries
from nltk.stem import LancesterStemmer

# the most commonly used stemmer
ls = LancesterStemmer()
print ls.stem("lying"), ls.stem("lies"), ls.stem("lied")
```

```output
lying lie lied
```
We can see the difference between the outputs of these two algorithms. There is also SnowballStemmer, which supports other languages besides english. 

##  Lemmatization
Lemmatization is quite similar to stemming, as it also converts a word into its base form. However the root word also called lemma, is present in dictionary.
It is considerably slower than stemming becasue an additonal step is perfomed to check if the lemma formed is present in dictionary.

Note: We also have to specify the parts of the speech of the word in order to get the correct lemma. Words can be in the form of Noun(n), Adjective(a), Verb(v), Adverb(r).
Therefore, first we have to get the POS of a word before we can lemmatize it.

First let's import the libraries.
```python
from collections import Counter 

from nltk.corpus import wordnet # To get words in dictionary with their parts of speech
from nltk.stem import WordNetLemmatizer # lemmatizes word based on it's parts of speech
```

Okay, now we have to get the POS of a word. For this pupose, we can use Wordnet corpus.
It returns all the POS rating of a word in a list. I have written a function for it. 
```python
def get_pos( word ):
    synset = wordnet.synsets(word)

    pos_counts = Counter()
    pos_counts["n"] = len(  [ item for item in synset if item.pos()=="n"]  )
    pos_counts["v"] = len(  [ item for item in synset if item.pos()=="v"]  )
    pos_counts["a"] = len(  [ item for item in synset if item.pos()=="a"]  )
    pos_counts["r"] = len(  [ item for item in synset if item.pos()=="r"]  )
    
    most_common_pos_list = pos_counts.most_common(3)
    return most_common_pos_list[0][0] # first indexer for getting the top POS from list, second indexer for getting POS from tuple( POS: count )
```

Okay, now lets create the WordNetLemmatizer object and then perform the lemmantization. It lemmatize method takes two arguments, one is the word to lemmatize and second is the POS of the word.
```python
words = ["running","lying","cars","m!spleed"]
wnl = WordNetLemmatizer()
for word in words:
    print wnl.lemmatize( word, get_pos(word) ), #printing without newline character
``` 
```output
run lie car m!spleed
```
Alright, that concludes our demonstration for stemming and lemmatization using NLTK in Python.

