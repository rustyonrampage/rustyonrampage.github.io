---
layout: post
title: Tokenization with Python and NLTK
explanation: We are going to explore different ways of using Python library nltk to tokenize text into sentences and words.
category: Text-mining
meta: Using Python library nltk for sentence and word tokenziation. 
excerpt_separator: <!--more-->
---
**Tokenization** is the process of splitting up text into independent blocks that can describe syntax and semantics. Even though text can be split up into paragraphs, sentences, clauses, phrases and words, but the most popular ones are sentence and word tokenization.


Python's NLTK provides us sentence and word level tokenizers. These tokenizers can get our work done for the most part. <!--more-->
First of all, let's import the essential libraries.


```python
#let's import the libraries
import nltk

#text we'll use for the demonstration
text = "Hello world! This is the sentence #2. This is the sentence #3. This is a multiline \n sentence."
```

## 1) Sentence Level Tokenization
These tokenizers return a list of sentences from the text provided. NLTK provides several types of  sentence level tokenizer implemenations. Now don't worry, their usage is quite simple and similar.
* sent_tokenize()
* PunktSentenceTokenizer()
* RegexpTokenizer()

#### 1.1) Using sent_tokenize()
It is the default tokenizer that nltk recommends. It uses an instance of PunktSentenceTokenizer class internally. We simply have to pass the text in it and it returns a list of sentences. We can also optionally specify the language for tokenization text. Supported languages can be seen at [this github link](https://github.com/teropa/nlp/tree/master/resources/tokenizers/punkt).
```python
sentences  = nltk.sent_tokenize( text ,language="english" )

print "Total setences in text: ", len(sentences)
print "Sentences are: ", sentences
```


```output
Total sentences in text:  4
Sentences are:  ['Hello world!', 'This is the sentence #2.', 'This is the sentence #3.', 'This is a multiline \n sentence.']
```

#### 1.2) Using PunktSentenceTokenizer()
This is the actual tokenizer that is being called in sent_tokenizer. It's is also quite straight forward.
```python
punkt_tk = nltk.tokenize.PunktSentenceTokenizer()
sample_sentences = punkt_tk.tokenize(sample_text)

print "Total setences in text: ", len(sentences)
print "Sentences are: ", sentences
```

```output
Total sentences in text:  4
Sentences are:  ['Hello world!', 'This is the sentence #2.', 'This is the sentence #3.', 'This is a multiline \n sentence.']
```

#### 1.3) Using RegexpTokenizer()
This method gives the control to the programmer. We can provide regular expressions according to our requirements and get the result. 
```python
pattern = r'(?<!\w\.\w.)(?<![A-Z][a-z]\.)(?<![A-Z]\.)(?<=\.|\?|\!)\s'
regex_tk = nltk.tokenize.RegexpTokenizer(pattern=pattern,gaps=True)
sentences = regex_tk.tokenize(text)

print "Total setences in text: ", len(sentences)
print "Sentences are: ", sentences
```

```output
Total sentences in text:  4
Sentences are:  ['Hello world!', 'This is the sentence #2.', 'This is the sentence #3.', 'This is a multiline \n sentence.']
```

## 2) Word Level Tokenization
Word tokenization is the process of splitting of text into words. NLTK provides many ways to get word tokens. For the demonstration purpose, we can use the following sentence.
```python
sentence = "Let's see how the tokenizer split's this! :)" 
```

#### 2.1) Using word_tokenize()
This tokenizer can split based on punctuation and non-aphabet characters. It basically invokes the Treebank word tokenizer so both of their outputs are identical. 
```python
sentence = "Let's see how the tokenizer split's this! :)" 
words = nltk.word_tokenize(sentence)
print "Total words are ", len(words)
print words
```

```output
Total words are  12
['Let', "'s", 'see', 'how', 'the', 'tokenizer', 'split', "'s", 'this', '!', ':', ')']
```

#### 2.2) Using WordPunctTokenizer()
NLTK recommends word_tokenize and WordPunctTokenize for most purposes. This method also separates the punctuations.
```python
sentence = "Let's see how the tokenizer split's this! :)" 
words = nltk.WordPunctTokenizer(sentence)
print "Total words are ", len(words)
print words
```
```output
Total words are  13
['Let', "'", 's', 'see', 'how', 'the', 'tokenizer', 'split', "'", 's', 'this', '!', ':)']
```
#### 2.3) Using WhitespaceTokenizer()
It tokenizes text on whitespace characters. Alternatively we can  use string split() function, if this functionality is desered.
```python
whitespace_wt = nltk.WhitespaceTokenizer() 
words = whitespace_wt.tokenize(sentence) 
print "Total words are ", len(words)
print words 
```
```output
Total words are  8
["Let's", 'see', 'how', 'the', 'tokenizer', "split's", 'this!', ':)']
```
#### 2.4) Using RegexpTokenizer()
Same as sentence tokenization we can also get words using regular expressions. It gives us a lots of control to get tweek tokenization to our requirements.
```python
GAP_PATTERN = r'\s+'         
regex_wt = nltk.RegexpTokenizer(pattern=GAP_PATTERN, gaps=True) 
words = regex_wt.tokenize(sentence) 
print "Total words are ", len(words)
print words 
```
```output
Total words are  8
["Let's", 'see', 'how', 'the', 'tokenizer', "split's", 'this!', ':)']
```
