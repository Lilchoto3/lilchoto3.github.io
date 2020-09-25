---
title: Tackling Police Brutality Part 2
subtitle: Further insights into data processing, location identification, and NLP
---

## Preface

This is a followup blog post to the previous one, if you haven't already, please read [part one here](https://zacharyluck.github.io/2020-08-24-Processing-Reddit-Data-to-Tackle-Police-Brutality/) to get the context behind the project I'll be talking about and how my team and I spent the last four weeks getting the API set up and fine-tuning everything.

## The Second Four Weeks

### Week Five: Extracting Location Information

While extracting the data from reddit wasn't too hard, getting stuff like the article text and publishing date is something that takes a bit more effort, thankfully we discovered the module [`newspaper3k`](https://newspaper.readthedocs.io/en/latest/) which made text extraction way easier and allowed us to move on to tokenization, now that we had a decent set of text that properly represented what the articles were about.

![example of newspaper3k](https://i.imgur.com/Vvap8xq.png)

###### Example from newspaper3k's website.

### Week Six: SpaCy, Tokenization, and Location Extraction

In addition to newspaper3k, we also implemented [`spaCy`'s natural language processing and entity recognition capabilities](https://spacy.io/usage/linguistic-features) to extract location information from the text of the article. From there, we could take the location information gathered, being the city and the state, and compare it to a local .csv file stored in the app which contains geolocation data pertaining to those cities. That data is sourced from [SimpleMaps](https://simplemaps.com/data/world-cities), a database that contains coordinate data for millions of cities across the world, but for our app, we used the free version, which we filtered from its original 15,000 entries down to about 7,000, keeping only cities within the United States.

![spaCy in action](https://i.imgur.com/eYvcswq.png)

###### SpaCy in action, extracting just location features from the text of an article.

### Week Seven: Finishing the API

This week was dedicated more to finishing up the API and making it run automatically to so that the process of updating the back-end's database isn't done manually. For this, we used [`fastapi-utils`](https://fastapi-utils.davidmontague.xyz/), a third-party module to [FastAPI](https://fastapi.tiangolo.com/), from the module specifically, we moved the route that held the code to update the local backlog to the main python file for the app and used the `@repeat_every` function to have that route update the backlog automatically.

Again, I had some struggles here, although this was more based in me trying to figure out how `@repeat_every` and FastAPI in general worked. Initially, our API had the keys that PRAW used embedded in the app itself in an `.env` file. In week six, I tried to remove the need for an `.env` file because I thought it would be a security risk to build a Docker image and push it to Docker Hub and AWS with the `.env` file inside of it. I tried fixing this problem by adding a route that you could post the API keys for PRAW to so that they wouldn't be stored on the machine, but that ended up not working, so I had to revert it back to the way it originally worked. In addition to that, I had to move the entire route that updated the backlog manually to the main file for the app, as it wouldn't work otherwise.

![example from fastapi utils website](https://i.imgur.com/KLhZ0cd.png)

###### Example from `fastapi-utils` website.

### Week Eight and Conclusion: Looking Back

Overall, I'd say that I learned a lot, both in terms of just refreshing my memory about Python's toolkit when it comes to data science, such as the functionality from `spaCy` and its tokenizing capabilities, but also in terms of learning new things, such as FastAPI and ElasticBeanstalk, as well as learning about modules I'd never heard of before like `newspaper3k`. I can definitely say that this project is one that I'm proud of in terms of both results and in the work I did with my team. It's been a great learning experience and I can only hope that I get to work with great teams like this again.
