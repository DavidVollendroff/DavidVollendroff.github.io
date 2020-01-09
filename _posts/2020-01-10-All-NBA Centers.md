---
layout: post
title: All-NBA Centers in 2020
subtitle: Using traditional and advanced metrics to model voting
bigimg: /img/centers.jpg
image: /img/shaq_logo.png
tags: [NBA, Machine Learning, Sports Prediction]
---

# 2020 All-NBA Centers
![Graph](/img/predictions.png){: .center-block :}
Congratulations to Karl-Anthony Towns, Joel Embiid and Andre Drummond on being named to the 2020 All-NBA squads.

If only it were that simple..

While these are the honest results of my predictive models, there are some things to consider before you go placing bets in your favorite sports book.

## Times are changing

Some of the difficulty involved in modeling which Centers are likely to be named to the 2020 All-NBA Teams comes from the fact that the role of the Center in modern basketball isn't what it used to be. Consider Anthony Davis, the 1st Team Center in 2018. According to [BasketballReference.com](https://www.basketball-reference.com/players/d/davisan02.html#all_pbp) he was considered to be a Power Forward rather than a Center by a 51% to 49% margin. The dataset I scraped from the site reflected his definition as a Power Forward, and my models never had the chance to even consider him. But in 2018 voters simply saw him as the best available candidate for 1st Team All-NBA at the Center position.

### The scarcity of data
Furthermore, the role that a Center plays in the modern NBA is different than it has been historically in a non-trivial way. And this can cause issues in ways you might not expect. Because when he look to predict the future, we look back at historical data first.

A big factor in making good predictive models is the amount and quality of available training data. But because fewer players are playing the Center position than in years past, and there is only one spot available per All-NBA Team, we have precious-little data to work with.

This manifests itself with the fact that..

### Nikola Jokić's passing is literally off the charts
When Nikola Jokić earned his place as an All-NBA Center for the first time he did so while dishing out more assists than anyone since Wilt Chamberlain. The modern All-NBA voting system has only existed since the '89-'90 season, and therefore so does our corresponding statistical data. So when we look at how our model values points and assists there is _no_ point of reference.

![Graph](/img/PTS_AST.png){: .center-block :}

It should be no wonder then that when asked to evaluate players in 2019, where Jokić's assist numbers were again were off the charts, he's misclassifed as being the 4th most worthy candidate instead of the best.

This error in judgment as well as one other weakness keeps my model from nailing last year's voting results near perfectly. That blind spot is..

### Injuries

The one other glaring miscalculation my model seems prone to make is that of failing to recognize the impact of injuries on a players chances at receiving voter support.

Anthony Davis suffered an injured that effectively sidelined him after participating in his 41st game of the 2018-19 season. He would miss long stretches of games, playing with restrictions on the few occasions he would participate moving forward. The fact that he demanded a trade with multiple years left on his contract seemed to sour voters as well. He also would receive only a single 3rd team vote, rather than the 2nd Team honors my model anticipated from his statistics.

Similarly, my model says DeMarcus Cousins ought to have been the 1st Team All-NBA Center in 2018. And by a very large margin. But Cousins played only 48 games before suffering a season-ending injury. In reality he received only vote, and it was for the 3rd team.

There simply aren't enough examples in the Centers dataset to properly learn this rule of thumb. Spaces on the All-NBA teams seem to be significantly swayed by productivity more than raw talent. It makes one think of the old adage, "The best ability is availability."

# Thoughts and considerations
## On accuracy
Defining accuracy for these sorts of predictions is difficult, because >90% of Centers receive no votes whatsoever in a given year, and only three receive recognition. There is no comprehensive archive of voting numbers, only award results. So a baseline classification model would guess that no one makes the All-NBA Team and be correct ~98% of the time. As it is my models use random forest regression and linear regression to rank players by something akin to a vote-worthiness metric. One fun note; linear models are absolutely garbage for this sort of task. Dwight Howard for 1st Team in 2018?? I'm sure you won't mind if I don't mention these trash factories again.

Considering that my tree-based model correctly predicted the top seven vote recipients for last year, with only Davis and Jokić out of perfect order, leads me to believe it isn't completely without predictive power.

## If you've read this far, consider hold off on placing your bets for another week

I'm currently working on a follow-up blog post that uses data from players of all positions to more broadly determine what good play is, rather than what has been traditional work for a Center. Preliminary results show that adding this extra data helps not only better classify non-traditional Centers, but also to eliminate the propensity for models to ignore injury. Not only does it improve accuracy with regard to ranking Centers, but it seems to do an incredible job of predicting *all of the voting outcomes* for the entire All-NBA selection process. Kristian Winfield wrote [an excellent piece](https://www.sbnation.com/2019/5/23/18637496/all-nba-voting-winners-losers-damian-lillard-kemba-walker-klay-thompson-reaction) for SBNation describing the multimillion-dollar ramifications these votes can have, and with this in mind I'll take a look at predictions for every position and the implications they have for players and teams alike. 
