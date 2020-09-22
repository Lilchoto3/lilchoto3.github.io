---
title: Tackling Police Brutality Part 2
subtitle: Further insights into data processing, location identification, and NLP
---

## Preface

This is a followup blog post to the previous one, if you haven't already, please read [part one here](https://zacharyluck.github.io/2020-08-24-Processing-Reddit-Data-to-Tackle-Police-Brutality/) to get the context behind the project I'll be talking about and how my team and I spent the last four weeks getting the API set up and fine-tuning everything.

## The Second Four Weeks

### Week Five: Extracting Location Information

While extracting the data from reddit wasn't too hard, getting stuff like the article text and publishing date is something that takes a bit more effort, thankfully we discovered the module [newspaper3k](https://newspaper.readthedocs.io/en/latest/) which made text extraction way easier and allowed us to move on to tokenization, now that we had a decent set of text that properly represented what the articles were about.

![example of newspaper3k](https://i.imgur.com/Vvap8xq.png)

###### Example from newspaper3k's website

### Week Six: SpaCy, Tokenization, and Location Extraction

In addition to newspaper3k, we also implemented spaCy's 
