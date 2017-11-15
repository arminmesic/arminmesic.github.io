---
layout: post
title:  "Implementing Linear Regression"
date:   2016-04-02
categories:
    - Machine Learning
    - NLP
---

## Candidate Entity Generation

I started to learn more about NLP, I've played around with spaCy and coreNLP and
the first thing that I wanted to do is entity recognition, both libraries do this
basically for you and you don't have to care about it. The next step is to get more
data about the entities, to do this a knowledge base is used, such as Wikidata, DBPedia,
Freebase or YAGO. They basically contain information about entities, what categories
they belong to, what other entities they are related to.

This can be used to annotate a text, for example if you try to read a paper but
don't understand some terms, NER and Entity linking can annotate words for you and
link to the corresponding Wikipedia article.

My first intuition was to just take the Entity recognized by spaCy and make a request
to the KB and take the result, but I didn't think about word disambiguation, e.g
Michael Jordan can be a professor as well as a basketball player. So I decided to
learn more about the topic and read the Paper "Entity Linking with a Knowledge Base:
Issues, Techniques, and Solutions". I'm going to give a summary of the paper.

### What is the problem with entity linking?

You have word disambiguation, different surface appearance (TUM, TU München,
Technische Universität München),
Different Entities have the same surface appearance but different meaning
(e.g Michael Jordan and Michael Jordan)

### What do we want to achieve?

We want to link the recognized named entity to a corresponding entry in the KB to
get more information of for the entity

###How is EL done?

There are three steps for entity linking, here is a quick overview
1. Candidate entity generation
  The goals is to find all the possible entities in the KB that
  are interesting for the entity that was recognized by the NER

2. Candidate entity ranking
  Most of the time we will get more that just one possible candidate back, the List
  needs to be ranked to find the entity which is most likely meant

3. Unlinkable mention prediction
  What should happen with unlinkable entities, when the NER has identified some entities
  but these are not in the KB, or this step is also used to check if the top identified entity
  is the target entity for the mention

## Candidate Entity Generation
We want to filter out all irrelevant entries in the KB, we want to generate a set of
candidates, mainly string comparison between the surface form is used

### Name Dictionary Based Technique
You create a name dictionary `<key, value>`, the name of the entity is the key and
the value is the id. (e.g New York, big apple)

To populate the dictionary you can use Wikipedia and it's different types of pages.
* __Entity page__

  This can be used to get the most common name for the entity, take the title
  of the page as the name and add it to the dictionary and store the pointer to
  this page as the value. e.g `<Microsoft, Microsoft_Pointer>`

* __Redirect Pages__

 these pages are useful to get alternative names such as synonyms, abbreviations
 or other variations for the entity, for the Microsoft example you can get
 Microsoft Corporation, store the Title of the page and add a pointer to the
 Microsoft page `<Microsoft Corporation, Microsoft_Pointer>`

* __Disambiguation Pages__

  these types of pages link to multiple entity pages that could be given the same
  name. e.g Michael Jordan. On these pages abbreviations or aliases can be
  extracted. For each of these pages the title is added to the dictionary
  and a pointer for each of the listed entities on the page is added
  `<Michael Jordan, Michael_Jordan_Basketball_Pointer, Michael_Jordan_Professor_Pointer, ...>`

* __Bold Phrases__

  from the first paragraph, the first paragraph is a summary of the article and
  often contains nicknames, aliases of full names. So each bold phrase is added
  as a key and a pointer to this entity page is added.

* __Links in the Wikipedia Article__

  The links in the Wikipedia article link to other entities, the anchor text provides
  synonyms and other name variations. So the anchor text is added and a pointer to the
  entity page of the link is added a value `<Bill Hewlett, William_Reddington_Hewlett_Pointer>`

  ​



Now that the dictionary is constructed we need to find possible candidates, before
the matching you should also think about spelling mistakes in the entity mentions.
There are two ways to add candidates __Exact matching__, the simplest way look
for exact matching between the entity mention and the key in the dictionary.
The second way is partial matching, following methods can be used:
* The entity name is wholly contained in or contains the entity mention.
* The entity name exactly matches the first letters of all words in the entity mention. (Michael Jordansky)
* The entity name shares several common words with the entity mention.
* The entity name has a string string similarity with the entity mention
  (Multiple ways to check for similarity: character Dice score, skip bigram Dice score, Hamming distance,...)

Partial matching leads to higher recall, which means a higher number of true positive,
but also has more noise.

In the next part I'll talk about candidate entity ranking as well as about techniques to implement them.