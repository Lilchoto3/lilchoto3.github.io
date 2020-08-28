---
title: Processing Reddit Data to Tackle Police Brutality
subtitle: A short dive into the world of Natural Language Processing
---

## To Preface:

This project was made in conjunction with Human Rights First, an independant advocacy and action organization. The work they do is centered around getting America to stand up to its ideals, and in doing so, they sought the help of Lambda School for their project. Their challenge to my group and I, as well as two other groups of students here at Lambda, was to see if we could make a map of continental America that showed events of police brutality, using data aggregated from Reddit and Twitter.

While most of the issues pertaining to the website and getting that to work fell to the Web Development team, the issue of sourcing and cleaning data fell to myself and my team member, Chris. The requirements of the project meant that we would be creating a FastAPI web app deployed via ElasticBeanstalk to Amazon Web Services (AWS), something that neither of us had done before, but other than that, our options for going about sourcing the data and cleaning it were entirely open to us.

### Initial Worries

At first, both Chris and I worried about using FastAPI and AWS; we'd never worked with either framework, so we worried that we'd have to spend a fair amount of time learning how it works and getting it set up. On further inspection, we realised that FastAPI beared a striking resemblance to Flask, another kind of web-app framework, but came with a built-in user interface that allowed us to test the functions of our app. As for the Amazon Web Services, we haven't gotten that far, but we expect to have an app built later this week.

## Preparation, Planning, and Complications

At the start of working on the project, we broke down what we thought we'd need to make in order to get our app running. This included things like finding a source of data, cleaning it, getting the app up and running, and outputting the cleaned data through an endpoint in the app, which contained all the data needed for Back-end to take it and display it on the map.

In addition, there would be a few times during working on the project where there was some confusion with how the data would flow from the API to the backend. At one point, Chris and I had set up a database to hold data, thinking we would be ensuring that there weren't any duplicates in the data, only to realize that it was Back-end who would be dealing with that.

![picture of trello board](https://i.imgur.com/BEg4Eao.png)

###### General overview of what the Data Science team needed to do.

## The First Four Weeks

### Week One: Planning the project

Week one of working on the project consisted of planning things out. We decided on what kind of framework layout we'd be using for the project as well as how each piece of the project was going to communicate with one another. Below is a diagram of the layout we eventually came up with in terms of how the project would be laid out:

![diagram of the project](https://i.imgur.com/0U4nrK7.png)

###### Diagram of our project layout.

### Week Two: Data Exploration

Week Two was where the teams split up and started working more specifically on solving the problems they had to. For Data Science, that meant getting an idea of what our data should look like. While we did get a general idea of how our data was going to leave our API based off of some websites like [846policebrutality.com](https://incidents.846policebrutality.com/) which provided their own API to see how they formatted their data, we didn't make any progress on updating the code for our API, believing that we needed the keys to AWS to actually make any progress towards it. We did, however, make progress on exploring both the data from the 846 API, as well as pulled data from Reddit, of which we explored ways to filter and process.

![an example of the data we pulled from reddit](https://i.imgur.com/b5xe2rG.png)

###### Example data pulled from Deddit.

### Week Three: API Updates 

Week Three consisted mostly of figuring out how to build the API locally in Docker, and before that, getting Docker to work, even. Once that was all sorted, however, it didn't take long to transfer the code we'd written in various notebooks to output the data from the 846 API as a proof that our API was working.

Our first real bit of technical complications happened here, when both Chris and I realized that we could not get our app running since neither of us could use Docker since we were both on Windows 10 Home. Our previous experience had taught us that Windows 10 Home was not capable of doing any sort of visualization without an experimental new update and WSL2, and we worried that we wouldn't be able to build the app. Thankfully, the windows update that contained the ability to create virtualizations on Windows 10 Home had been properly released and wasn't experimental anymore, so all I had to do was update Windows and install WSL2, and I was able to create Docker images and run containers.

![The title card of our API](https://i.imgur.com/NLViiKy.png)

###### Success! The API is working!

### Week Four: Modelling the Data

Week Four is where a large portion of our work on actually serving the data from Reddit and Twitter got done. We updated the app to create new endpoints that served data from Reddit filtered through a model. The model itself uses Natural Language Processing to determine if the post from reddit is about police brutality or not, and only the data returned by the model as being about police brutality gets passed along.

Initially, there were some issues publishing the app to AWS, as I, who was on app-publishing duty, had never used ElasticBeanstalk before. I had some issues installing ElasticBeanstalk, as it kept failing saying that the module `six` was not installed, after telling me that it installed it. It wasn't until I found, in the instructions given by Amazon themselves, that I had to run the installer through PowerShell, since I was on Windows, that it finally installed and I got the app published later that week.

![an example of the app in action](https://i.imgur.com/qQfRtgr.png)

###### An example of the app in action.

## As of Present

Currently, the app is in version 0.2 and still in production, it can be found [here](http://hrf-teamb.eba-3253gq3h.us-east-1.elasticbeanstalk.com/#/) where you can see the four available routes: `predict`, `viz`, `testpath`, and `getdata`. Of these, `predict`, and `viz` are routes inhereted from the base version of the repository we started with and are currently unrelated to the project. `testpath` is, self-descriptingly, a test path created to determine if the API was functioning properly. `getdata` is the path related to our project, requiring a variable, `pullnum`, to be supplied with an integer. The path will then pull that number of posts from the r/news subreddit and return any that pass the built-in model as being about police brutality.

## Into the Future

Current plans for updates include:

* An updated model, which better predicts which news stories coming in are actually about police brutality
* A new route which takes in data from the Back-end and processes it, returning visualizations of events of police brutality over time

### Future Technical Challenges

It goes without saying that work on any code will lead to bugs down the line, if there's anything I worry about, it's making sure that the model is as accurate as possible before sending the data along, without removing too many actual stories about police brutality. In addition, I worry about getting the data from back-end to provide visuals, but that can be solved by communicating with Back-end about how the data will come in.

### What I've learned

Number one: communication is key, between everyone on the team all the time, always. Communication has solved far too many problems for me to count, not only on this project, but on other projects as well. Being able to communicate effectively, even just a simple meetup at the end of the day works wonders. Same with pulling in team members from outside your scope of work and asking about how things will connect together.

Other than that, I've learned that FastAPI is very cool and useful for quickly setting up apps that output data, it's a very nice framework and I'll definitely keep it in mind.
