---
layout: essay
type: essay
title: "Designing, But Not Clothes"
# All dates must be YYYY-MM-DD format!
date: 2020-05-03
labels:
  - Creativity
  - Design Patterns
---

# Designing, But Not Clothes

## Software Designing Is Not What You Think

When I was younger, my dream was to be a fashion designer among a lot of other dreams, but designing was my favorite thing to do.  It didn't matter if it was on paper, clothes, canvas, or anything, as long as I got to create something.  Years later, I am a Computer Science major learning all the experiences this field has to offer.  I recently took a class in software engineering and I enjoyed it so much.  It was hard because of all the back-end engineering you have to do, and it is like trying to connect a million wires metaphorically.  But the reason I enjoyed it was that I got to learn front-end designing as well.  We created mock-up websites and our own app. I never would've thought this would be the way I would "design" for the rest of my life.  With software engineering, there are so many different definitions to the word designing.

## Behavioral, Creational, Structural

The type of designing I am talking about in software engineering is a whole lot different than designing a floor plan or a new clothing pattern.  Our version of "designing" is three main patterns with 23 subpatterns spread amongst them.  The three main ones are Behavioral, Creational, and Structural.  A design pattern is basically a template that is a reusable solution that you can use to fix commonly occurring problems.  These patterns are a big help to beginners like me to get accustomed to how the systems work by giving us training wheels while also making us still pedal and do the work to learn.  It makes life so much easier.  For my class, we were to create an app that targeted a problem and this app would be the solution to it.  I hadn't noticed how many designs we used in the making of this app until I researched it.  

## Types of Designs Used in Our Project

We used a prototype and singleton design pattern, which is under creational design.  The prototype we used was a simple schema replica, and this allows us to create objects by making a copy of a prototypical instance.  This was used with our api elements to set a certain outline that we wanted out pages to follow or have.  The singleton design is a global variable that you can name a class and can refer to it as that variable in other classes.  We used this design to make it easier for our publishing and subscriptions, which brings me to the other patterns under the behavioral design.  There is observer, which acts as a queen bee and its worker bees, and the publish-subscribe pattern, which is very similar to observer but more of a messaging pattern.  In meteor, we used a publication using the singleton variable we created, and on the page we want to use it, we subscribe to it.  The observer has a subject or object that notifies its dependent or observers when a state changes.  That is where these two patterns go hand in hand.  Another pattern we used is the Model-View-Controller (MVC) where the model for Meteor is MongoDB, the view is our Simple Schema template, and the controller is the withTracker.  This is used with the subscriptions and publications of the singleton variables I explained before.  Our group split up responsibilities in order to make this app faster; this would be a bridge design pattern, which is under structural.  We all work on the same platform of Github, but we work in separate branches and then merge when we are finished with our task.  Another design is the front controller for handling mechanisms, which is used for our authentication of the login and sign up for the user.  As you can see, there are many designs implemented into this single project.  I'm sure there are more, but I am just a beginner. ;) 

For help on what type of design pattern you should be using for certain problems, give this [website](https://scientificprogrammer.net/2020/01/30/an-easy-way-to-learn-design-patterns-in-software-development/) a read!
