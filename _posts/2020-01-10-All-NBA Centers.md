---
layout: post
title: All-NBA Centers in 2020
subtitle: What has changed and what remains the same about receiving this honor.
bigimg: /img/centers.jpg
image: /img/shaq_logo.png
tags: [NBA]
---
# Games Played
It seems to me that my machine learning models had a hard time grasping the connection between number of games a player plays in and the propensity for humans to vote for that player. In 2017-18, Stephen Curry was clearly not the 5th or 6th best guard in the League, but he made the 3rd team because he played only 51 games due to injury. In 2018-19 Lebron James similarly made the 3rd team as he sat out the end of the season after 55 games.

My model predicts that DeMarcus Cousins ought to have been the 1st Team All-NBA Center in 2018, and by a decent margin. But he played only 48 games, suffering a season-ending injury like Steph and Lebron. He received one vote for the 3rd team.

Anthony Davis suffered an injured that effectively sidelined him after participating in his 41st game of the 2018-19 season. He would miss long stretches of games, playing with restrictions on the few occasions he would participate moving forward. He also would receive only a single 3rd team vote.

# First headline stuff n stuff
First of all, the linear regression does an absolutely awful job of ranking players. [calculated.gg](http://calculated.gg/) Presently the .

![Graph](/img/speeds.png){: .center-block :}


A paragraph of stuff.  

More stuff and stuff.

# Tree Based Regression
The tree-based model seems to perform more sensibly, but not without it's own set of issues. Encouragingly it finds the top seven players, suffering a bit  Validating the model on data from the 2017-18 NBA Season sees it predicting that DeMarcus Cousins would 
![Graph](/img/speed chart.png){: .center-block :}

Paragraphs of information.

### Another visualization
![Graph](/img/attacking_third.png)

Stuff about that visualization.

# In closing
Summary of stuff.

### Ideas to improve the model

Using all of the data gathered for every position, not just Centers. Perhaps this would provide insight into what voters view as being a good basketball player in a general sense, and not only what has historically been done by Centers because it was what was expected in that role.

### The curious case of Anthony Davis
Several oddities are brought to light when we consider the odd case of Anthony Davis. In the 2017-18 season he was considered to be a Power Forward rather than a Center according to [BasketballReference.com](https://www.basketball-reference.com/players/d/davisan02.html#all_pbp) by a 51% to 49% margin. But voters simply saw him as the best candidate for 1st Team All-NBA at the Center position. The model never had the chance to even consider him.

And although our data does regard him as a Center during the 2018-19 season, something our data doesn't account for is that he demanded a trade. To say it was perceived poorly would be understatement. Despite being the best Center in the minds of many, he received only a single 3rd team vote. Using NLP to analyze articles and social media posts for sentiment might allow for the ability to address situations like Anthony Davis only receiving a single 3rd team vote

Perhaps using data from all Power Forwards and Centers and using their position estimates as features might be possible. It sounds like it may create more issues than it solves in the short term.
