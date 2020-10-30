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

In [my previous](https://davidvollendroff.github.io/2020-01-10-All-NBA-Centers/) All-NBA post I attempted to answer the question, "Who will be voted as the NBA's best Center?" And after gathering data, modeling and plotting predictions I had this very simple and clear output.
![Graph](/img/predictions.png){: .center-block :}
A quick and dirty stroll through the data had given me a set of predictions for the coming season. But with knowledge of the domain, a few things just didn't look right..

### What is a Center?
For starters, Anthony Davis is conspicuously missing. And this is because according to [basketball-reference](https://www.basketball-reference.com/players/d/davisan02.html#pbp::none) he actually spent 51% of his time at Power Forward. And because he's listed as a Power Forward he doesn't show up in the Centers-only dataset used. But problematically for us, voters had no such issue with calling him a Center. In fact, prior to this season he'd been named the best "Center" in the NBA __twice__.

And beyond this weirdness of voters having positional flexibility in voting, some other oddities arose in part because there have been Centers recently with historically unprecedented performances.

### Since when can a Center pass like this?
Nikola Jokić is a problem. Not only in basketball slang sense, but also because if you look at the model's valuation of points and assists you can see there is simply _no point of reference_ for Jokić's __7.3__ assists per game. 

![Graph](/img/PTS_AST.png){: .center-block :}

No Center in the history of basketball has ever before breathed that rarified air. It isn't all that surprising then that my original model significantly underestimates how voters value what he contributes to his team. He's facilitating the offense in a way no "big man" ever has.

### S p a r s e    D a t a
Furthermore, two huge factors in the accuracy of predictions are the amount and quality of historical reference data. There is only one spot available for a Center on each All-NBA Team, so we have precious-little data to work with. 60 award winners over a 20 year period simply isn't enough data for the model to learn from. It can give you reasonable predictions, correctly identiftying the top seven vote recipients. But only after accounting for Davis and Jokić does it order them correctly. The model still struggles with edge cases. Another important type of edge case, discussed in [greater detail](https://davidvollendroff.github.io/2020-01-10-All-NBA-Centers/) in the original post, is the effect injuries have on swaying voters. So few All-NBA-level Centers have succumbed to injury at inopportune times that the model has no chance of dealing with those rare occurrences where they actually do.

Luckily we can do _much_ better

## Widen our view

### Throwing out positions
Instead of building a model that only cares about what it means to be an All-NBA Center, what if instead we ask, "What does it mean to be an All-NBA __player__?" With a flexible definition of "Center", plus using statistics from __all__ NBA players irrespective of position, we go from predictions of:
__1st Team__ Karl-Anthony Towns
__2nd Team__ Joel Embiid
__3rd Team__ Andre Drummond
__Runner Up__ Rudy Gobert

To instead predicting:
__1st Team__ Anthony Davis
__2nd Team__ Nikola Jokić
__3rd Team__ Rudy Gobert
__Runner Up__ Joel Embiid
Which turns out to be perfectly correct.

## Predicting other positions
Along the way we actually ended up building a system for predicting voting outcomes for all positions.

## Learning along the way
My favorite aspect of this project was the real-world complexity that comes along with trying to join domain knowledge with machine-learning driven insight.

### Error404: DataSet Not Found
For starters. The data set didn't exist as some perfect little CSV file. I'd have to gather, join, process and clean it all myself. And before that I needed to use anecdotal evidence about how voters made decisions to guide what information I'd seek. From traditional box scores, advanced metrics, and even team statistics. Some of the voters for this individual award can't be persuaded to ignore team success. I credit my success with putting everything together to my ability to read the Pandas documentation.

### The strange world of voting
There is no comprehensive archive of voting numbers, only award results. That means all we've got for supervision in this supervised machine-learning exercise are the three players who were the top three vote recipients. The hundreds of other players are labeled as equally non-winners. 

And according to my research, there is no ready-made loss function that suits our purpose perfectly here. One vote cast for a player is at the expense of another. Even if a loss function based on rank order were easily available, within the limitations of our data, reordering players 4-400 wouldn't change the loss values whatsoever. Hardly ideal.

But with this in mind I converted the "labels" of the dataset, that is their "Vote-worthiness" as follows:

__Named 1st Team__ = 5 points
__Named 1st Team__ = 3 points
__Named 1st Team__ = 1 point
__All Else__ = 0 points

There's a reason behind this particular schema. If we assume that the 100 voters reach the "right" answer when determining winners we end up with something quite interesting.
By labeling players in this way we are essentially recreating the ballot of a hypothetical voter who over 20 years had never cast a single vote, allotted a single point, other than perfectly. It's like having one voter, but one who has never been wrong.

Then by using a random forest regressor model we can ask our voter how worthy several players are and make comparisons.

### Decisions in the face of uncertainty

Stuff about monkey-patching the old library and why I did it.

So a baseline classification model would guess that _every_ player it considered would fail to make an All-NBA Team and that would be correct ~98% of the time. As it is, my models use random forest regression and linear regression to rank players by something akin to a vote-worthiness metric. One fun note; linear models are absolutely garbage for this sort of task. Dwight Howard for 1st Team in 2018?? I'm sure you won't mind if I don't mention these trash factories again.

### Close calls and toss ups



Considering that my tree-based model correctly predicted the top seven vote recipients for last year, with only Davis and Jokić out of perfect order, I'm lead to believe it isn't completely without predictive power.

But..

## If you've read this far, consider holding off on placing your bets for another week

I'm currently working on a follow-up post that uses data from players of all positions to more broadly determine what good play is, rather than what has been traditional work for a Center. Preliminary results show that adding this extra data helps not only better classify non-traditional Centers, but also to eliminate the propensity for models to ignore injury.

Excitingly, not only does it improve accuracy with regard to ranking Centers, but it seems to do an incredible job of predicting *all of the voting outcomes* for the entire All-NBA selection process. Kristian Winfield wrote [an excellent piece](https://www.sbnation.com/2019/5/23/18637496/all-nba-voting-winners-losers-damian-lillard-kemba-walker-klay-thompson-reaction) for SBNation detailing the multimillion-dollar ramifications these votes can have. And with this in mind, in my next post I'll take a look at predictions for every position and the implications they have for players and teams alike. 
