---
layout: post
title: Parts of Speech Tagging with Python and NLTK
explanation: We are going to explore different ways of using Python library nltk to tokenize text into sentences and words.
category: Text-mining
meta: Using Python library nltk for sentence and word tokenziation.
tags: [ text-mining, feature-extraction] 
excerpt_separator: <!--more-->
---

**POS tagging** is the process of tagging words in a text with their appropriate Parts of Speech. Meanwhile
parts of speech defines the class of words based on how the word functions in a sentence/text. Parts of speech are also known as word classes or lexical categories. Common parts of speech in english are Noun, Verb, Adjective, Adverb, Pronoun and Conjunction.
<!--more-->

POS tags are often taken as features in NLP tasks. In this post, we are going to use Python's NLTK to create POS tags from text. NLTK has a POS tager that takes tokens of word in order to provide POS tags. Now even though, the input to tagger is individual words, yet it performs analysis on the words like they are in a sequence, thus its accuracy is better as it is able to differentiate between words when are being used as noun and verb.

```python
import nltk

# triple quotes represent multi-line text
text = """Most important thing in this life is love 
        and I love to eat chocolates."""

tokens = nltk.word_tokenize( text )
pos_tags = nltk.pos_tag( tokens )

```
```output
[('Most', 'RBS'),
 ('important', 'JJ'),
 ('thing', 'NN'),
 ('in', 'IN'),
 ('this', 'DT'),
 ('life', 'NN'),
 ('is', 'VBZ'),
 ('love', 'JJ'),
 ('and', 'CC'),
 ('I', 'PRP'),
 ('love', 'VBP'),
 ('to', 'TO'),
 ('eat', 'VB'),
 ('chocolates', 'NNS'),
 ('.', '.')]
```

This function returns a list of tuples. Each tuple contains the word and it's tag. Now these Tag names might be overwhelming on start, but we'll take a look at them in detail. But first, notice how the word "love" is assigned different tag based on the role it is playing in the sentence.


Now we can take a look at which tags are present in NLTK and what to they mean. Btw, if you want to check the tags yourself, you can use the following fuction:

```python
# prints all the available POS tags and their description
nltk.help.upenn_tagset()
```
Following are the main POS categories. Now there are about 12 families in this category and you'll need to use them most of the times. Also, there are minor variations of naming convention and pos tags in different libraries.
<table>
        <colgroup>
                <col width="10%" />
                <col width="16%" />
                <col width="19%" />
                <col width="55%" />
        </colgroup>
        <thead>
                <tr class="header">
                        <th>Tag</th>
                        <th>Family</th>
                        <th>Full form</th>
                        <th>Description/ Example</th>
                </tr>
        </thead>
<tbody>
        <tr>
                <td markdown="span">NN</td>
                <td markdown="span">Noun</td>
                <td markdown="span">noun common, singular or mass</td>
                <td markdown="span">A word (other than a pronoun) used to identify      any of a class of people, places, or things.
                <br/>
                Example: common-carrier, cabbage, knuckle-duster, Casino, Afghan
                </td>
        </tr>
        <tr>
                <td markdown="span">NNP</td>
                <td markdown="span">Noun</td>
                <td markdown="span">noun, proper, singular</td>
                <td markdown="span">A word(singular) directly associated with an entity and primarily used to refer to that entity.
                <br/>
                Example: San Francisco, Sarah, The Library of Congress
                </td>
        </tr>
        <tr>
                <td markdown="span">NNPS</td>
                <td markdown="span">Noun</td>
                <td markdown="span">noun, proper, plural</td>
                <td markdown="span">A word(plural) directly associated with an entity and primarily used to refer to that entity.
                <br/>
                Example: Oreos, Johns, Americans, Museums of Mongols       
                </td>
        </tr>
        <tr>
                <td markdown="span">NNS</td>
                <td markdown="span">Noun</td>
                <td markdown="span">noun, common, plural</td>
                <td markdown="span">A word that is used to name general items rather than specific ones
                <br/>
                Example:  Big city, Jeans, Stadium     
                </td>
        </tr>
        <tr>
                <td markdown="span">VB</td>
                <td markdown="span">Verb</td>
                <td markdown="span">verb, base form</td>
                <td markdown="span">A word used to describe an action, state, or occurrence.
                <br/>
                Example:  Ask, Assemble, Build
                </td>
        </tr>
        <tr>
                <td markdown="span">VBD</td>
                <td markdown="span">Verb</td>
                <td markdown="span">verb, past tense</td>
                <td markdown="span">A word used to describe an action, state, or occurrence.
                <br/>
                Example:  Dipped, Pleaded, Swiped
                </td>
        </tr>
        <tr>
                <td markdown="span">VBG</td>
                <td markdown="span">Verb</td>
                <td markdown="span">verb, present participle or gerund</td>
                <td markdown="span"> A word that is formed from a verb and can be used as an adjective or used to form verb tense
                <br/>
                Example:  Telegraphing, Stirring, Focusing
                </td>
        </tr>
       <tr>
                <td markdown="span">VBN</td>
                <td markdown="span">Verb</td>
                <td markdown="span">verb, past participle</td>
                <td markdown="span"> A word that is formed from a verb and can be used as an adjective or used to form verb tense
                <br/>
                Example:  Multihulled, Dilapidated, Aerosolized
                </td>
        </tr>
        <tr>
                <td markdown="span">VBP</td>
                <td markdown="span">Verb</td>
                <td markdown="span">verb, present tense, not 3rd person singular</td>
                <td markdown="span"> A verb in present tense form that is not being used in third person.
                <br/>
                Example:  Predominate, Wrap, Resort, Sue, Twist
                </td>
        </tr>
        <tr>
                <td markdown="span">VBZ</td>
                <td markdown="span">Verb</td>
                <td markdown="span">verb, present tense, 3rd person singular</td>
                <td markdown="span"> A verb in present tense form that is being used in third person.
                <br/>
                Example:  Bases, Reconstructs, Marks, Mixes, Displeases
                </td>
        </tr>
        <tr>
                <td markdown="span">CC</td>
                <td markdown="span">Conjunction</td>
                <td markdown="span">conjunction, coordinating</td>
                <td markdown="span"> A word that joins two elements of equal grammatical rank and syntactic importance.
                <br/>
                Example:  &, and, and, but, therefore, yet
                </td>
        </tr>
        <tr>
                <td markdown="span">CD</td>
                <td markdown="span">Numeric & Dates</td>
                <td markdown="span">numeral, cardinal</td>
                <td markdown="span"> Used to represent numeric values
                <br/>
                Example:  Mid-1890, Twenty, 271,124, Ten million
                </td>
        </tr>
        <tr>
                <td markdown="span">DT</td>
                <td markdown="span">Determiner</td>
                <td markdown="span">determiner</td>
                <td markdown="span"> A modifying word that determines the kind of reference a noun or noun group has.
                <br/>
                Example:  All, An, Both, Half, No, Some, Each
                </td>
        </tr>
        <tr>
                <td markdown="span">FW</td>
                <td markdown="span">Foreign word</td>
                <td markdown="span">foreign word</td>
                <td markdown="span"> A word that is not present in the language(English).
                <br/>
                Example:  Gemeinschaft, Objets, Corporis
                </td>
        </tr>
        <tr>
                <td markdown="span">IN</td>
                <td markdown="span">Conjunction</td>
                <td markdown="span">preposition or conjunction, subordinating</td>
                <td markdown="span"> A word which joins together a dependent (subordinate) clause and an independent clause.
                <br/>
                Example:  Among, Uppon, Whether, Within
                </td>
        </tr>
        <tr>
                <td markdown="span">JJ</td>
                <td markdown="span">Adjective</td>
                <td markdown="span">adjective or numeral, ordinal</td>
                <td markdown="span"> A word naming an attribute of a noun.
                <br/>
                Example:  Third, Ill-mannered, Pre-war, Regrettable, Oiled, Calamitous
                </td>
        </tr>
        <tr>
                <td markdown="span">JJR</td>
                <td markdown="span">Adjective</td>
                <td markdown="span">adjective, comparative</td>
                <td markdown="span"> A word used to compare one noun to another noun.
                <br/>
                Example:  Cheaper, Cleaner, Cuter, Calmer
                </td>
        </tr>
        <tr>
                <td markdown="span">JJS</td>
                <td markdown="span">Adjective</td>
                <td markdown="span">adjective, superlative</td>
                <td markdown="span"> A word is used to compare three or more objects
                <br/>
                Example:  Cheapest, Cleanest, Cutest, Calmest
                </td>
        </tr>
        <tr>
                <td markdown="span">PRP</td>
                <td markdown="span">Pronoun</td>
                <td markdown="span">pronoun, personal</td>
                <td markdown="span"> A word that take the place of specific nouns that name people, places and things.
                <br/>
                Example:  Hers, Herself, It, Itself, Ourselves
                </td>
        </tr>
        <tr>
                <td markdown="span">PRP$</td>
                <td markdown="span">Pronoun</td>
                <td markdown="span">pronoun, possessive</td>
                <td markdown="span"> A word that is a pronoun and is used to refer to possession or 'belonging'.
                <br/>
                Example:  Her, His, Mine, My, Our, Ours
                </td>
        </tr>
        <tr>
                <td markdown="span">RB</td>
                <td markdown="span">Adverb</td>
                <td markdown="span">adverb</td>
                <td markdown="span">  A word that describes or gives more information about a verb.
                <br/>
                Example:  Unabatingly, Amazingly, Swiftly, Adventurously
                </td>
        </tr>
        <tr>
                <td markdown="span">RBR</td>
                <td markdown="span">Adverb</td>
                <td markdown="span">adverb, comparative</td>
                <td markdown="span">  A word that compares two actions.
                <br/>
                Example:  Greater, Heavier, Higher, Lonelier
                </td>
        </tr>
        <tr>
                <td markdown="span">RBS</td>
                <td markdown="span">Adverb</td>
                <td markdown="span">adverb, superlative</td>
                <td markdown="span">   A word is used to compare three or more actions.
                <br/>
                Example:  Greatest, Heaviest, Highest, Loneliest
                </td>
        </tr>
        <tr>
                <td markdown="span">UH</td>
                <td markdown="span">Interjection</td>
                <td markdown="span">interjection</td>
                <td markdown="span">  A word that demonstrates the emotion or feeling of the author.
                <br/>
                Example:   Goodbye, Dammit, Heck, Whodunnit
                </td>
        </tr>
        <tr>
                <td markdown="span">MD</td>
                <td markdown="span">Modal auxiliary</td>
                <td markdown="span">modal auxiliary</td>
                <td markdown="span">  A modal is a type of auxiliary (helping) verb that is used to express: ability, possibility, permission or obligation
                <br/>
                Example:   Can, Cannot, Could, Couldn't 
                </td>
        </tr>
        <tr>
                <td markdown="span">RP</td>
                <td markdown="span">Particle</td>
                <td markdown="span">particle</td>
                <td markdown="span">  A word that has a grammatical function but does not fit into the main parts of speech
                <br/>
                Example:   Aboard, By, Off, Upon
                </td>
        </tr>
        <tr>
                <td markdown="span">SYM</td>
                <td markdown="span">Symbol</td>
                <td markdown="span">symbol</td>
                <td markdown="span">  Special characters.
                <br/>
                Example:   *, +, ., <, =, >, @, A, ,[fj] 
                </td>
        </tr>
</tbody>
</table>

Some other not so common categories
<table>
        <colgroup>
                <col width="10%" />
                <col width="16%" />
                <col width="19%" />
                <col width="55%" />
        </colgroup>
        <thead>
                <tr class="header">
                        <th>Tag</th>
                        <th>Family</th>
                        <th>Full form</th>
                        <th>Description/ Example</th>
                </tr>
        </thead>
<tbody>
        <tr>
                <td markdown="span">WDT</td>
                <td markdown="span">WH-words</td>
                <td markdown="span">WH-determiner</td>
                <td markdown="span">When used as determiners, what, which, or whose can be used to ask questions.
                <br/>
                Example: Which, Whichever, What, That
                </td>
        </tr>
        <tr>
                <td markdown="span">WP</td>
                <td markdown="span">WH-words</td>
                <td markdown="span">WH-pronoun</td>
                <td markdown="span">The pronouns who, whose, which, and what can be the subject or object of a verb.
                <br/>
                Example: That, What, Whatever, Whatsoever
                </td>
        </tr>
        <tr>
                <td markdown="span">WP$</td>
                <td markdown="span">WH-words</td>
                <td markdown="span">WH-pronoun, possessive</td>
                <td markdown="span">Used in this way, WH-pronoun represent possession,
                <br/>
                Example: whose
                </td>
        </tr>
        <tr>
                <td markdown="span">WRB</td>
                <td markdown="span">Wh-words</td>
                <td markdown="span">Wh-adverb</td>
                <td markdown="span">WH-words used as adverbs.
                <br/>
                Example: How, However, Whence, Whenever, Where 
                </td>
        </tr>
        <tr>
                <td markdown="span">PDT</td>
                <td markdown="span">Pre-determiner</td>
                <td markdown="span">pre-determiner</td>
                <td markdown="span"> A word that is sometimes used before a determiner to give more information about a noun in a noun phrase
                <br/>
                Example: All, Both, Half, Many, Quite
                </td>
        </tr>
        <tr>
                <td markdown="span">EX</td>
                <td markdown="span">Existential there</td>
                <td markdown="span">existential there</td>
                <td markdown="span"> "There" ...it's a word that has no meaning by itself other than to fill out a syntactic position. 
                <br/>
                Example: There
                </td>
        </tr>
        <tr>
                <td markdown="span">TO</td>
                <td markdown="span">To</td>
                <td markdown="span">"to" as preposition or infinitive marker</td>
                <td markdown="span"> "To" can be used as both preposition and infinitive
                <br/>
                Example: To
                </td>
        </tr>
        <tr>
                <td markdown="span">LS</td>
                <td markdown="span">List item marker</td>
                <td markdown="span">list item marker</td>
                <td markdown="span"> Represents the item number of a list 
                <br/>
                Example: A, A., First, 1, 1. 
                </td>
        </tr>
        <tr>
                <td markdown="span">POS</td>
                <td markdown="span">Genitive marker</td>
                <td markdown="span">genitive marker</td>
                <td markdown="span"> The suffix -'s on nouns is a marker of genitive case in English
                <br/>
                Example: 's
                </td>
        </tr>
   
</tbody>
</table>


Additionally there are also tags for dollar sign, opening and closing quotation marks, opening and closing parenthesis, comma, dash, sentence terminator and colon. You will be able to find them on [Treebank POS Tag link](https://www.ling.upenn.edu/courses/Fall_2003/ling001/penn_treebank_pos.html).