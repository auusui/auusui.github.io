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

I found X-Ray to be very easy to understand and use.  It was easy to write it into a JSON file, which is what the last line under URL does where it will writ to "results.json".  The paginate function allows the scraper to keep going through all of the pages that list jobs.  The limit function basically limits the amount of pagination to n, the number you insert, requests to write onto the JSON results file.  The example code shown above will go through 3 pagination pages.  It was hard for me to scrape some websites and I tried to play around with the attribute selectors I used and the class scopes.  I found that it was easier to find something if you narrowed it down to the inner box that it was placed in.  The materials that I was able to scrape from the website were the date the internship was posted, description, internship header/name, company name, and the location.  

X-Ray has many attributes that are useful for scraping a big website.  I have gone over a few of them in the previous paragraph.  Collections are like a list of fields within a field.  X-Ray makes it easier to get collections using this code: 
```ruby
//selecting only the first list item in unordered list
 x('ul', 'li') 
 
 //selecting the whole list
 x('ul', ['li'])
 
 //selects all list items in all lists
 x(['ul'], ['li'])
```

Other attributes are crawling, scoping, and filtering.  By using them together, the search becomes even better because it helps with being more specific with what you want out of the website.  What helped me understand how to use the different properties was Matthew Muellerʻs [GitHub page](https://github.com/matthewmueller/x-ray).  It shows examples of the selector (simple string selector), collections (selects an object), arrays (selects an array), collections of collections (selects an array of objects), and array of arrays (selects an array of arrays).  Overall, I think that X-Ray was a great experience for trying out scraping for the first time.  
