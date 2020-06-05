---
layout: essay
type: essay
title: "X-Ray Scraper"
# All dates must be YYYY-MM-DD format!
date: 2020-06-05
labels:
  - InternBit
  - Scrapers
  - X-Ray
---

# X-Ray Scraper

[X-Ray](https://www.npmjs.com/package/x-ray) is a Javascript library that I used to scrape internship websites.  The website I chose to target was CoolWorks.  With X-Ray, the code is formatted as following: 

## URL
```ruby
const Xray = require('x-ray');
const x = Xray();

x('URL', 'scope', [
  {
    title: 'h1 a',
    link: '.article-title@href'
  }
])
  .paginate('.nav-previous a@href')
  .limit(3)
  .write('results.json')
```
## HTML
```ruby
const Xray = require('x-ray');
const x = Xray();

var html = '<body><h2>Pear</h2></body>'
x(html, 'body', 'h2')(function(err, header) {
  header // => Pear
})
```

I found X-Ray to be very easy to understand and use.  It was easy to write it into a JSON file, which is what the last line under URL does.  The paginate function allows the scraper to keep going through all of the pages that list jobs.  The limit function basically limits the amount of sources you want to show on the JSON results file.  It was hard for me to scrape some websites and I tried to play around with the attribute selectors I used and the class scopes.  I found that it was easier to find something if you narrowed the box that it was placed in.  
