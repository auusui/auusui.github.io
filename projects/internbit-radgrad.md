---
layout: project 
type: project
image: images/ui-page.png
title: "Internbit - RadGrad"
permalink: projects/internbit-radgrad
# All dates must be YYYY-MM-DD format!
date: 2020-07-31
labels:
  - Software Development
  - Research Project
  - Javascript
  - Web Scrapers
  - Internship
summary: InternBit is a research project that aims to aid ICS students in finding internships via an internship recommendation system and increase RadGrad engagement.   
---

=======================================================================

<img class="ui huge centered rounded image" src="../images/poster.jpg">

# InternBit for RadGrad

For eleven weeks of Summer 2020, I had the greatest opportunity to partake in a research and software development project.  I learned so much during this process, and it gave me a real life experience of what software development is like.  This project was challenging and time-consuming yet very rewarding once you see results.  I learned to scrape websites using Javascript Libraries such as X-Ray, Tatooine, Osmosis, and Puppeteer.  I think that X-Ray was a super easy tool to use if your goal is to grab surface information.  If you want to grab more in depth information like going to the #href source, then Puppeteer was a great too for that.  I got to experience the libraries' strengths and weaknesses and compare the usage.  I came out of this internship with a better knowledge of what I want to do in the future and I feel confident that I could ace a course on all of the activities we did over this summer.  I think that is what internships are for.  You want to get a taste of what it would be like in a specific field and if you would enjoy doing it.  This is why I was happy to be working on this project because I want other students to be able to experience this.  An internship can assure a student's dream job or steer them to a new direction if it isn't what they enjoy.  I think it matters to be passionate about what you're doing, but that was just a bonus to this internship.  I believe this project can help a lot of students find the path they want to take in life, and I am glad I was able to contribute to this.  

## Abstract 

InternBit is a research project that aims to aid ICS students in finding internships via an internship recommendation system and increase RadGrad engagement. It works by scraping internship results from popular internship sites, which is then analyzed for related skills so that both the internship and its related skills are inputted into the internship recommendation system. Upon using the system, users input their own skills into the system. This matches the users with internships that use similar skills via the internship recommendation system, so they can get recommendations for internships they both qualify for and are likely interested in. Integration with RadGrad streamlines this process further, as RadGrad gathers data from users, such as courses taken and ICS experience outside of school, which provides a better profile for the internship recommendation system to work with. If opted in, students will be able to receive weekly emails regarding the recommendations. This will also provide insight to the institution because they can trace back to see which courses/opportunities they learned the skills from to see if the institution is adequately preparing their students for the workforce.

Here is a link to the [InternBit](https://radgrad.github.io/docs/internbit/goals) main page where we explained the goals of this project, our resources, the javascript libraries, our canonical schema, and evaluation.  

This picture is a screenshot of our UI design, which was mainly designed by Jenny Hsu. Here you can see the filters on the left, and the job cards on the right side.  

<img class="ui large right floated rounded image" src="../images/ui-page.png">

## My Contribution

During this internship, we had tasks that were assigned to us every week or so to work on.  I learned a lot of new skills with these tasks and increased my experience with javascript.  



### Figma 

Figma is a framework website that allows users to create UI designs.  When we first started this internship, one of our first tasks was to create 6 UI mock-ups of what we think our static site would look like.  Here is an example of one of my designs to give you a peek into what Figma allows us to do.  

<img class="ui large left floated rounded image" src="../images/Figma.png">

Figma was a super cool tool to use and I would always lose track of time when using it.  I had to switch to a mouse because my hand was getting a cramp using my touchpad.  I was always in a flow state of mind when using Figma because it allowed my creativity to just run wild.  I could create the UI design in my head and put it on paper basically.  It had different frames you could work with like iPhone 11, 6s, or MacBook Pro, Windows 10,  etc.  It had a wide variety of color hex codes that you can play around with and also create different shapes.  You could also upload images to use in the design.  I would definitely recommend Figma to a friend if they needed a framework website.  

### Javascript Libraries

* [X-Ray](https://www.npmjs.com/package/x-ray)
* [Tatooine](https://www.npmjs.com/package/tatooine)
* [Pupeteer](https://www.npmjs.com/package/puppeteer)
* [NightMare](https://github.com/segmentio/nightmare#api)

Our first step to gathering information was to get comfortable with different javascript libraries.  My first was X-Ray, and it took me a while to understand how to work it.  After I started to get the hang of it, I felt dumb because it was so easy!  I did a lot of research on the different functions I could use and how to scope on certain areas of websites.  I found it hard to get more in detail information, though, so I decided to try Tatooine and Nightmare once I finished scraping my websites with X-Ray.  I wanted to see what different results I could get.   

A snippet of my X-Ray code:

```ruby
const Xray = require('x-ray');
const x = Xray();

x('https://www.coolworks.com/search?utf8=%E2%9C%93&q=internships&commit=Search+Jobs', {
  jobs: x('.job-post-row', [{
    extra: x('.holder', [{
      posted: '.time',
      subtext: x('.text', 'p'),
      description: x('.top-meta', [{
        title: 'h4',
        company: 'h5',
        location: '.location',
      }]),
    }]),
  }]),
}).paginate('.paging a@href')
    .limit(5)
    .write('coolworks.data.json');
```

Tatooine was way different than X-Ray, whereas Nightmare was similar to Cheerio and Puppeteer.  I couldn't quite understand how it all worked, and I even tried working on it with my teammate using CodeTogether.  Before I could figure it out though, the group decided it would be best to focus on X-Ray and Puppeteer so we would all use the same library.  We then decided on a [canonical schema](https://radgrad.github.io/docs/internbit/canonical-schema) that we would format our JSON file in.  An example of our canonical format is:
```ruby
    {
        "position": "Intern - Probe Software Engineer",
        "location": {
            "city": " Boise",
            "state": "ID"
        },
        "company": "Micron Technology, Inc.",
        "posted": "2020-07-22T07:04:57.624Z",
        "url": "https://www.ihiretechnology.com/candidate/jobs/view/276128490?resultset=c488e709-1351-4cae-8a37-cf17e46e5eff&result=7",
        "lastScraped": "2020-07-28T07:04:57.618Z",
        "description": "Req. ID: 209082Micron Technologys vision is to transform how the world uses information to enrich life and our commitment to people, innovation, tenacity, collaboration, and customer focus allows us to fulfill our mission to be a global leader in memory and storage solutions. This means conducting business with integrity, accountability, and professionalism while supporting our global community....",
        "contact": [
            "to request assistance with the application process, please contact microns human resources department at 1-800-336-8918 (or 208-368-4748)."
        ],
        "skills": [
            "communication skills",
            "software engineering",
            "software design",
            "information technology",
            "critical thinking",
            "teamwork",
            "analytical skills",
            "NodeJS",
            "AngularJS",
            "data visualization",
            "JSON",
            "AJAX"
        ],
        "qualifications": "N/A",
        "start": September 2020
    }
```

Puppeteer was probably my favorite scraper to use because I could code each step that I wanted it to do.  I had to login to some of the sites so I used functions like type() and click().  Here is a snippet of my code for inserting search keywords to filter the internships: 

```ruby
    await page.waitForSelector('input[class=form-control]');
    await page.type('input[class=form-control]', 'technology');
    await page.waitFor(3000);

    // focus on location field- type nothing
    await page.focus('#location');
    await page.keyboard.down('Control');
    await page.keyboard.press('A');
    await page.keyboard.up('Control');
    await page.keyboard.press('Backspace');
    await page.type( "#location", " ");
```

It was easy to create the JSON canonical format.  Puppeteer made it easy to scrape websites that needed a login to access the internship listings.  Between all of the javascript libraries I tried, I love Puppeteer the most.  

### Remote Pairing

Since this internship was during the Covid-19 pandemic, we weren't allowed to see each other in person.  I think face-to-face interaction is way better than just chatting online because you can achieve more in less time.  The way we tried to replicate this was using [CodeTogether](https://www.codetogether.com/).  This allowed us to simultaneously work on the code on the same page.  We then connected over Discord to talk over the phone, basically, while working on the code.  I think CodeTogether was a great tool to use with my teammates because it made it easier to assist in fixing issues since both people could see the entire code physically instead of snippets.  It was a little more difficult than talking in person, but under the forced circumstances of social distancing, it was actually easier than I thought it would be.  Technical difficulties happened like my internet cutting out or having to set time aside to go on Discord at the same time, but other than that, remote pairing went smoothly.  I think this was a great experience because now people know that there are other ways to be efficient in a group project but also being safe from the pandemic.  With improvements in technology, people probably figured out that not everything needs to be in person.  

### Semantic UI React Design 

The scraping was gathering all of the information we needed for the first part of InternBit.  The next step was to integrate those scraped job listings into a static website.  We wanted to make something that would reflect the purpose of InternBit.  Each of my teammates and I made our own UI designs, then we would combine then in the end.  [Semantic UI React](https://react.semantic-ui.com/) is a great tool to use and probably my favorite for designing interfaces.  The back end engineering is tricky and frustrating at times, but if we don't wanna through our computer sometimes, then are we really coding?  My design was going for a filter bar on the top and it would show all the listings below.  I wanted a lot of space for the cards because I figured a user would want to read as much information as they can before they click to see the job listing on a new page.  I also wanted to implement a favorites button where it would add the job to a section that basically saves it for later.  The color scheme I was working with was a light blue and grey scale along with black.  I was sad that the internship ended and that I couldn't really finish the design.  I had so much fun working on it with my teammates.

### Presentation for UROP

My last tasks for InternBit was to get ready for the presentation for the Undergraduate Research Opportunities Program (UROP) SURE Symposium event.  It was held completely online this year due to the COVID-19 situation.  Our jobs were to create a poster for our presentation that let our audience know what we are and our purpose of the project.  We also had to come up with an abstract for the application.  Our process was for all of us to make our own abstract and posters then we would come together and combine what we wanted to use.  The presentation took up the 20 minute slot and we also got to watch our other teammates from different projects present their creations over the course of this internship.  There were hundreds of people presenting online.  It was a great way to end the internship. If you want to see our poster, then scroll back up to the first image that shows up on this page. 

## My GitHub Repos

These are my GitHub repositories that will take you straight to my code.  They will be my scraper code or my UI design code.  My UI design code isn't completely finished due to the ending of our internship.  

* [Puppeteer Repo](https://github.com/radgrad/internbit-scraper-au-Youtern)
* [UI Repo](https://github.com/radgrad/internbit-ui-au)
* [X-Ray Repo](https://github.com/radgrad/internbit-scraper-au-xray)


## Websites

These are the websites that I scraped using the javascript libraries I had mentioned above.  

* [CoolWorks](https://www.coolworks.com/search?q=technology) -- X-Ray & Puppeteer & Tatooine & Nightmare
* [Youtern](https://www.youtern.com/candidate/job_search/quick/results) -- X-Ray & Puppeteer
* [IHireTechnology](https://www.ihiretechnology.com/search?k=technology&loc=Honolulu,%20HI#!/search/c=&loc=Honolulu,%20HI&d=75&k=technology&o=14&searchtype=page-load) -- Puppeteer


## Essays

Over the course of the internship, I wrote technical essays that talked about my experiences and knowledge I gained from my tasks.  RadGrad Level Up is basically about what you need to do to level up as well as reflections on improvements and compliments on it.  A Piece of InternBit is an essay on recommendation systems and how it relates to what we are trying to do in InternBit.  Remote Pairing Program shares my first experience using CodeTogether with my teammates and my reflection upon it.  Lastly, X-Ray Scraper summarizes how X-Ray works and what I thought about it.  

* [RadGrad Level Up](https://auusui.github.io/essays/radgrad-level-up.html)
* [A Piece of InternBit](https://auusui.github.io/essays/a-piece-of-internbit.html)
* [Remote Pairing Program](https://auusui.github.io/essays/remote-pairing-program.html)
* [X-Ray Scraper](https://auusui.github.io/essays/x-ray-scraper.html)






