---
layout: post
title: All-NBA Voting Part 2
subtitle: Addressing shortcomings of the "Centers Only" approach
bigimg: /img/2020_all_nba.jpg
image: /img/damian_luka.jpg
tags: [NBA, Machine Learning, Sports Prediction]
---

# 2020 All-NBA Voter Prediction
![Graph](/img/damian_luka.jpg){: .center-block :}
Kristian Winfield wrote [an excellent piece](https://www.sbnation.com/2019/5/23/18637496/all-nba-voting-winners-losers-damian-lillard-kemba-walker-klay-thompson-reaction) for SBNation detailing the multimillion-dollar ramifications these votes can have. And now that the official voting results are in, let's take a look at what understanding and added value we can generate through Data Science.

## The Trouble With Centers 

In the [previous post](https://davidvollendroff.github.io/2020-01-10-All-NBA-Centers/) I attempted to answer the question, "Who will be voted as the NBA's best Center?" And after gathering data, modeling and plotting predictions I had this very simple and clear output.
![Graph](/img/predictions.png){: .center-block :}
A quick and dirty stroll through the data had given me a set of predictions for the coming season. But with knowledge of the domain, a few things just didn't look right..

### What is a Center?
For starters, Anthony Davis is conspicuously missing. And this is because he actually playing [60% of his time](https://www.basketball-reference.com/players/d/davisan02.html#pbp::none) at Power Forward and is therefore ommitted from the Centers-only dataset used. But voters had no such problem calling him a Center, and the best in the NBA at that.

And beyond this weirdness of voters having positional flexibility in voting, we also had to contend with historically unprecedented performances.

### And since when do Centers pass like this?
While working on this model the most recent data available was woefully unprepared for what Nikola Jokić had set about doing. If you look at the model's valuation of points and assists you can see there was simply _no point of reference_ for Jokić's __7.3__ assists per game in the history of basketball. 

![Graph](/img/PTS_AST.png){: .center-block :}

No Center had ever breathed that rarified air. It isn't all that surprising then that my original model significantly underestimates how voters value what he contributes to his team.

### S p a r s e  d a t a
Furthermore, two huge factors in the accuracy of predictions are the amount and quality of historical reference data. And because there is only one spot available for a Center on each All-NBA Team, we have precious-little data to work with. 60 award winners over a 20 year period simply isn't enough data for the model to learn from. It can give you reasonable predictions, correctly identiftying the top seven vote recipients. But only after accounting for Davis and Jokić. The model still struggles with edge cases. Another important type of edge case, discussed in [greater detail](https://davidvollendroff.github.io/2020-01-10-All-NBA-Centers/) in the original post, is the effect injuries have on swaying voters. So few All-NBA-level Centers have succumbed to injury at inopportune times that the model has no chance of dealing with those rare situations where they do.

Luckily we can do _much_ better


# Thoughts and considerations
## On accuracy
Defining accuracy for these sorts of predictions is difficult in part because >90% of Centers receive no votes whatsoever in a given year, and only three receive recognition. There is no comprehensive archive of voting numbers, only award results. So a baseline classification model would guess that _every_ player it considered would fail to make an All-NBA Team and that would be correct ~98% of the time. As it is, my models use random forest regression and linear regression to rank players by something akin to a vote-worthiness metric. One fun note; linear models are absolutely garbage for this sort of task. Dwight Howard for 1st Team in 2018?? I'm sure you won't mind if I don't mention these trash factories again.

Considering that my tree-based model correctly predicted the top seven vote recipients for last year, with only Davis and Jokić out of perfect order, I'm lead to believe it isn't completely without predictive power.

But..

## If you've read this far, consider holding off on placing your bets for another week

I'm currently working on a follow-up post that uses data from players of all positions to more broadly determine what good play is, rather than what has been traditional work for a Center. Preliminary results show that adding this extra data helps not only better classify non-traditional Centers, but also to eliminate the propensity for models to ignore injury.

Excitingly, not only does it improve accuracy with regard to ranking Centers, but it seems to do an incredible job of predicting *all of the voting outcomes* for the entire All-NBA selection process. Kristian Winfield wrote [an excellent piece](https://www.sbnation.com/2019/5/23/18637496/all-nba-voting-winners-losers-damian-lillard-kemba-walker-klay-thompson-reaction) for SBNation detailing the multimillion-dollar ramifications these votes can have. And with this in mind, in my next post I'll take a look at predictions for every position and the implications they have for players and teams alike. 