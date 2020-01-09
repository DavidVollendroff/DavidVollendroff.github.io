---
layout: post
title: All-NBA Centers in 2020
subtitle: Using machine-learning to model voting
bigimg: /img/centers.jpg
image: /img/shaq_logo.png
tags: [NBA, Machine Learning, Sports Prediction]
---

# 2020 All-NBA Centers
![Graph](/img/predictions.png){: .center-block :}
Congratulations to Karl-Anthony Towns, Joel Embiid and Andre Drummond on being named to the 2020 All-NBA squads.

If only it were that simple.

While these are the honest results of my predictive models, there are some things to consider before you go placing bets in your favorite sports book.

## Times are changing

Some of the difficulty involved in modeling which Centers are likely to be named to the 2020 All-NBA Teams comes from the fact that the role of the Center in modern basketball isn't what it used to be. Consider Anthony Davis, the 1st Team Center in 2018. According to [BasketballReference](https://www.basketball-reference.com/players/d/davisan02.html#all_pbp) he was a Power Forward rather than a Center. The data I scraped from the site reflected him as a Power Forward, and my models never had the chance to even consider him. But in 2018 voters simply saw him as talented player who was the best answer to the question, "Who is the best Center in basketball?"

### The scarcity of data
Furthermore, the role of a Center in the modern NBA is different than it has been historically in a non-trivial way. Big factors in making good predictions is the amount and quality of historical reference data. But because fewer players are playing the Center position than in years past, and there is only one spot available per All-NBA Team, we have precious-little data to work with.

This manifests itself with the fact that..

### Nikola Jokić's passing is literally off the charts
When Nikola Jokić earned his place as an All-NBA Center for the first time he did so while dishing out more assists than anyone since Wilt Chamberlain. But the modern All-NBA voting system has only existed since the '89-'90 season, and therefore Wilt's stats are unknown to our model. So when we examine how it learned to value playmaking there is _no_ point of reference for Jokić's __7.3__ assists per game.

![Graph](/img/PTS_AST.png){: .center-block :}

It should be no wonder then that when evaluating players in 2019, where Jokić's assist numbers were again were off the charts, he's ranked fourth by the model rather than first where voters placed him.

This blindness to the value of high-level passing as well as one other significant weakness keeps my model from nailing last year's voting results near perfectly. That other blind spot is..

### Injuries

The one other glaring miscalculation my model seems prone to make is that it fails to recognize the impact of injuries on a player receiving voter support.

Anthony Davis suffered an injured that effectively sidelined him after participating in his 41st game of the 2018-19 season. He would miss long stretches of games, playing with heavy minutes-restrictions on the few occasions he would participate thereafter. And demanding a trade with multiple years left on his contract didn't help his case with voters, I'm sure.

Model Predicted: __2nd Team Honors__

Voters Said: a single 3rd team vote

Similarly, my model says DeMarcus Cousins ought to have been the 1st Team All-NBA Center in 2017-18. And by a large margin too. In reality he received only one vote, and it was for the 3rd team, after having his season cut short by an achilles injury only 48 games in. 

There simply aren't enough examples in the Centers dataset to properly learn this voter preference. Spaces on the All-NBA teams seem to be awarded by voters based on productivity more than raw talent. Apparently voters believe the old adage that, "The best ability is availability."

# Thoughts and considerations
## On accuracy
Defining accuracy for these sorts of predictions is difficult in part because >90% of Centers receive no votes whatsoever in a given year, and only three receive recognition. There is no comprehensive archive of voting numbers, only award results. So a baseline classification model would guess that _every_ player it considered would fail to make an All-NBA Team and that would be correct ~98% of the time. As it is, my models use random forest regression and linear regression to rank players by something akin to a vote-worthiness metric. One fun note; linear models are absolutely garbage for this sort of task. Dwight Howard for 1st Team in 2018?? I'm sure you won't mind if I don't mention these trash factories again.

Considering that my tree-based model correctly predicted the top seven vote recipients for last year, with only Davis and Jokić out of perfect order, I'm lead to believe it isn't completely without predictive power.

But..

## If you've read this far, consider holding off on placing your bets for another week

I'm currently working on a follow-up post that uses data from players of all positions to more broadly determine what good play is, rather than what has been traditional work for a Center. Preliminary results show that adding this extra data helps not only better classify non-traditional Centers, but also to eliminate the propensity for models to ignore injury.

Excitingly, not only does it improve accuracy with regard to ranking Centers, but it seems to do an incredible job of predicting *all of the voting outcomes* for the entire All-NBA selection process. Kristian Winfield wrote [an excellent piece](https://www.sbnation.com/2019/5/23/18637496/all-nba-voting-winners-losers-damian-lillard-kemba-walker-klay-thompson-reaction) for SBNation detailing the multimillion-dollar ramifications these votes can have. And with this in mind, in my next post I'll take a look at predictions for every position and the implications they have for players and teams alike. 
