---
layout: essay
type: essay
title: "A Piece of InternBit"
# All dates must be YYYY-MM-DD format!
date: 2020-05-19
labels:
  - InternBit
  - RadGrad
---

A review of these resources. How can the ideas in these resources help InternBIt?
How will InternBit be better/different? Given that InternBit will be integrated with RadGrad, what will InternBit be able to do that these systems can't?

# A Piece of InternBit

## Sum It Up
In our [InternBit Resources Page](https://radgrad.github.io/docs/internbit/resources/), it gives information about the recommendation extension system we are working on for the InternBit part of the RadGrad2 project.  I am a new intern helping out with this project, and in order to know what I have to do, I needed to know what the purpose of InternBit is.  Our goal essentially is to scrape data off of internship websites and be able to deliver an accurate recommendation for students that would match their interests and qualifications.  
### Recommendation System
Ishan Nangia uses a system called hybrid filtering, which includes three types of filtering systems.  One is Collaborative Filtering that finds which user is using which item and also finds user/item pairs that are similar.  This relies on how the users interact in order to compute a metric for understanding similarities between users or items.  The second is Content-Based Filtering that is similar to CF, but doesn't rely on users interacting with items.  Instead, it relies of background information on users or items.  The last is Knowledge-Based Filtering, which takes in information provided by the user and uses preferences to suggest items.  This relies on the user's input.  His process is to collect data scraping from an intership website, cleaning the data preparing it for analysis, analyzing the data using it to answer questions to understand trends, and making the recommendations that are relevant, unique, and serendipitous. 

Testing is also just as important as creating a product.  The two ways in which the project is judged.  One way is to deploy two tests where the control group is recommended internships randomly and the second group (treatment group) is recommended using the model.  The second way is the create a pop-up, and when the user clicks on the recommendation, then that allows the user to rate (on a scale to 5) how relevant the recommendation was.  Obviously, they are two completely different techniques because one is for sure going to get feedback and the other is dependent on whether the user clicks on it.  They both get the same job done, though.  

### AI-Based Recommendation System
Internships are an important step in a students career because it helps her/him gain confidence in their work by becoming familiar with the chosen workplace.  If someone has a bad experience at an internship, then that could leave them back to square one and lost.  That's what this system is for.  It is to help recommend the best internships that fit the user.  
