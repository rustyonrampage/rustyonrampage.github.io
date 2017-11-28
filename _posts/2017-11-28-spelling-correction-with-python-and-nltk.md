---
layout: post
title: Correcting Words using Python and NLTK
explanation: We are going to discuss how Python and NLTK can be used to handle spelling correction.
category: Text-mining
meta: Using Python library NLTK for spelling and word lengthening correction.
tags: [ text-mining] 
excerpt_separator: <!--more-->
---

Spelling correction is the process of correcting word's spelling for example "lisr" instead of "list". Word Lengthening is also a type of spelling mistake in which characters within a word are repeated wrongly for example "awwwwsome" instead of "awesome". 
<!--more-->
The way we are going to solve spelling correction is by fixing the word lengthening issue first and then deal with spelling mistakes. 

## Fixing Word Lengthening
Word lengthening occurs when characters are wrongly repeated. English words have a max of two repeated characters. Additional characters need to ripped off, otherwise we might add misleading information. I have written a function for this purpose, which rip offs repeated characters more than 2.
```python
def reduce_lengthening(text):
    pattern = re.compile(r"(.)\1{2,}")
    return pattern.sub(r"\1\1", text)

print reduce_lengthening( "finallllllly" )
```
```output
finally
```
Since the character repeated was 'L' and "finally" has two repeated 'L', therefore this example mapped on it perfectly but what if it was some word that has actually no repeated characters at all. It would fail in that case for example, "amazzzzing" will return "amazzing", which is wrong. So we need an spell correction after word lengthening to get the correct word.

## Spell Correction
It is the process of correcting the spellings of a word. Spell correction algorithms are typically based on min-edit functions because brute force comparisons will be too time consuming.

In order for min-edit functions to work effectively, we actually need to use word lengthening first. Therefore, our spell correction is dependent on word lengthening. NLTK has no spell correction module, but there are many other libraries that can perform this task. I'll using [pattern en](https://www.clips.uantwerpen.be/pages/pattern-en) for this purpose. It is also available on anaconda package manager.
```python
from pattern.en import spelling

word = "amazzziiing"
word_wlf = reduce_lengthening(word) #calling function defined above
print word_wlf #word lengthening isn't being able to fix it completely

correct_word = spelling(word_wlf) 
print correct_word
```
```output
amazziing
[('amazing', 1.0)]
```
Alright, this concludes the demonstration for spelling correction using Python and NLTK.