---
layout: post
title: All-NBA Centers in 2020
subtitle: What has changed and what remains the same about receiving this honor.
bigimg: /img/centers.jpg
image: /img/shaq_logo.png
tags: [NBA]
---
# Times are changing

Some of the difficulty involved in modeling which Centers are likely to be named to the 2020 All-NBA Teams comes from the fact that the role of the Center in modern basketball isn't what it used to be. Consider Anthony Davis, the 1st Team Center in 2018. According to [BasketballReference.com](https://www.basketball-reference.com/players/d/davisan02.html#all_pbp) he was considered to be a Power Forward rather than a Center by a 51% to 49% margin. The dataset I scraped from the site reflected his definition as a Power Forward, and my models never had the chance to even consider him. But in 2018 voters simply saw him as the best available candidate for 1st Team All-NBA at the Center position.

## The scarcity of data
Another problem that needs consideration when thinking about making good predictive models is the amount of training data available. But because fewer players are playing the Center position than in years past, and the fact that there is only one spot available per All-NBA Team, we have less data available than we'd like. And this causes real issues.

For starters..

### Nikola Jokić's passing is literally off the charts
When Nikola Jokić earned his place as an All-NBA Center for the first time he did so while dishing out more assists than anyone since Wilt Chamberlain. The modern All-NBA voting system has only existed since the '89-'90 season. So when we look at how our model values points and assists there is _no_ point of reference.

![Graph](/img/PTS_AST.png){: .center-block :}

It should be no wonder then that when asked to evaluate players in 2019 where Jokić 

### Injuries

It seems to me that my machine learning models had a hard time grasping the connection between number of games a player plays in and the propensity for humans to vote for that player. In 2017-18, Stephen Curry was clearly not the 5th or 6th best guard in the League, but he made the 3rd team because he played only 51 games due to injury. In 2018-19 Lebron James similarly made the 3rd team as he sat out the end of the season after 55 games.

My model predicts that DeMarcus Cousins ought to have been the 1st Team All-NBA Center in 2018, and by a decent margin. But he played only 48 games, suffering a season-ending injury like Steph and Lebron. He received one vote for the 3rd team.

Anthony Davis suffered an injured that effectively sidelined him after participating in his 41st game of the 2018-19 season. He would miss long stretches of games, playing with restrictions on the few occasions he would participate moving forward. He also would receive only a single 3rd team vote.

There simply aren't enough examples in the Centers dataset to properly learn this distinction.

# First headline stuff n stuff
First of all, the linear regression does an absolutely awful job of ranking players. [calculated.gg](http://calculated.gg/) Presently the .

# What the model thinks is important
![Graph](/img/nba_feature_weights.png)



A paragraph of stuff.  

More stuff and stuff.

# Tree Based Regression
The tree-based model seems to perform more sensibly, but not without it's own set of issues. Encouragingly it finds the top seven players, and would place them in perfect ordering if not for suffering from what appears to be two main errors in judgment. 



# In closing
Summary of stuff.

### Ideas to improve the model

Using all of the data gathered for every position, not just Centers. Perhaps this would provide insight into what voters view as being a good basketball player in a general sense, and not only what has historically been done by Centers because it was what was expected in that role.

### The curious case of Anthony Davis
Several oddities are brought to light when we consider the odd case of Anthony Davis. 

And although our data does regard him as a Center during the 2018-19 season, something our data doesn't account for is that he demanded a trade. To say it was perceived poorly would be understatement. Despite being the best Center in the minds of many, he received only a single 3rd team vote. Using NLP to analyze articles and social media posts for sentiment might allow for the ability to address situations like Anthony Davis only receiving a single 3rd team vote

Perhaps using data from all Power Forwards and Centers and using their position estimates as features might be possible. It sounds like it may create more issues than it solves in the short term.
