---
layout: project 
type: project
image: images/hsearch.png
title: "Heuristics Search of Problems"
permalink: projects/heuristic-search
# All dates must be YYYY-MM-DD format!
date: 2021-03-02
labels:
  - Coimmon Lisp
  - Heuristic Search
  - A* Algorithm
  - AI coding
summary: This was an assignment for my AI course where we created heuristic search algorithms for certain problems and implement it into our Depth-First-Search algorithm.
---

=======================================================================

<img class="ui huge centered rounded image" src="../images/hsearch.png">

## About Heuristic Searches

Heuristic searches are apart of the A* algorithms that we use to "guess" the best route from a start state to the goal state.  This can also be known as a Best-First-Search algorithm because it will order the OPEN list based off of the f(n) value of each node.  The list will be order from least to greatest (or greatest to least) f(n) value depending on how you want to count the values.  For these three problems, the list will be least to greatest since I will be counting the amount of "pieces" out of place.  The f(n) value is the sum of the h(n) value and the g(n) value.  The g(n) value is the length of the parent path, and the h(n) value is the heuristic value of, in this case, the number of pieces out of place.  I will be using this f(n) value to organize my OPEN list and call the dfs on that.

## About the Problems Used
I will briefly explain the objective and restrictions in each game as well as state what the start and goal states are for each.  I also attached a website that can give you a better understanding of what each problem is.  

### 1) Cannibals and Missionaries
<img class="ui medium right floated rounded image" src="../images/c&m.jpg">



[C&M Problem Explanation](https://en.wikipedia.org/wiki/Missionaries_and_cannibals_problem#:~:text=In%20the%20missionaries%20and%20cannibals,were%2C%20the%20cannibals%20would%20eat)

### 2) Farmer, Goat, Wolf, and Cabbage
<img class="ui huge left floated rounded image" src="../images/farmer.jpg">


[F,W,G,C Problem Explanation](https://illuminations.nctm.org/BrainTeasers.aspx?id=4992#:~:text=The%20Wolf%2C%20Goat%2C%20and%20Cabbage&text=His%20rowboat%20has%20enough%20room,cabbage%20safe%20from%20their%20enemies.)

### 3) 5-3 Water Jugs
<img class="ui huge right floated rounded image" src="../images/jug.jpg">



[5&3 Jug Problem Explanation](https://www.math.tamu.edu/~dallen/hollywood/diehard/diehard.htm)
