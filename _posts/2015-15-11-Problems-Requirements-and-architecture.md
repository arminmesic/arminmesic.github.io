---
layout: post
title:  "Problems, Requirements and Architecture"
date:   2015-11-15
categories: 
    - Code Complete 2
    - Software Engineering
---
I've started to read Code Complete 2 this is just a short summary about the first
few pages.

### Before writing code
Before starting to write any code you need to have a clear plan and an goal for
the software. [They build the right stuff](http://www.fastcompany.com/28121/they-write-right-stuff)
is a cool article that shows the importance of planing. Not everyone has 35 Millions
available to write code, so the scope of the planing depends on your project.


### Step 1: Defining the Problem
The purpose of software is to solve problems, so you need to a clear idea what problem
you're trying.

Define the problem, it should be a simple statement, make it no longer
than one page. Don't look for solutions.

### Step 2: Requirements
Requirements are there to investigate the problem more in-depth. Try to get the right
the first time, if you need to change some requirements, try to do it in this phase
or else it's going to cost you a lot of time.


Why should I use requirements? They're like a map to your destination, if don't
know which way you should take in your development use requirements. You know trough
the first phase the problem but you'll maybe miss specific points of the problem.

The Shuttle group has 2500 page of requirements for 6k LOC.

As you work with the clients the requirements are going to change, the more they
work with you on solving the problem, they understand it better and their own needs.

I'll need to look more into this topic.

### Step 3: Architecture
Architecture makes sure that you use the right tools to solve your problem.
It gives an high level overview about the building blocks of the software.

There are a lot of different aspects your architecture should focus on.

  * Program organization

      What are the major building blocks(e.g. classes, subsystems) of your application,
      what do these building blocks know about each other.
  * Major classes

      Use the 80/20 rule to just sketch out the most important classes.
  * Data design

      Organization of databases.
  * User interface design
  * Resource management

      How to handle limited resources, such as database connections.
  * Security

      Encryption, Error Messages.
  * Performance

       Defining priorities among the resources.
  * Scalability

      How is the system going to react to growing numbers of users, servers.
  * Interoperability

      If the system uses or offers APIs how is the data shared.
  * Internationalization

      How is the system going to handle translations.

It depends on the software you're developing how much architecture is needed
for you project to succeed.

### Conclusion
There is a lot of work involved before writing any line of code, this work increases
your chance to create a product that solves your problem. For my further projects
I'm going to use this list a guide.
