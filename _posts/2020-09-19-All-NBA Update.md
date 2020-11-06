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
A first pass at modeling had given me a set of predictions for the coming season. But with knowledge of the domain, a few things just didn't look right..

### What is a Center?
For starters, Anthony Davis is conspicuously missing. And this is because according to [basketball-reference](https://www.basketball-reference.com/players/d/davisan02.html#pbp::none) he'd actually spent 51% of his minutes at Power Forward at the time of prediction. And because he's listed as a Power Forward he doesn't show up in the Centers-only dataset used. 

Problematically for us, voters had no such issue with calling him a Center. In fact, prior to this season he'd been named the best "Center" in the NBA __twice__. This in spite of the fact that he self-identifies as a Power Forward.

Beyond voters having positional flexibility in casting ballots, other oddities arose in part because recently Centers have turned in historically unprecedented performances.

### Since when can a Center pass like this?
Nikola Jokić is a problem. Not only in basketball slang, meaning his presence has to be respected whenever he's on the court, but also because he confounds any model based on historical data. Looking at a partial dependence plot for the Centers-Only model, you can see there is simply _no point of reference_ for Jokić's __7.3__ assists per game. 

![Graph](/img/PTS_AST.png){: .center-block :}

No Center in the history of basketball has ever before breathed that rarified air. Then it isn't all that surprising my original model significantly underestimates how voters value what he contributes. He's facilitating offense in a way no "big man" ever has.

### S p a r s e    D a t a
Two huge factors in the accuracy of predictions are the amount and quality of historical reference data. There is only __one__ spot available for a Center on each All-NBA Team, so we have precious-little data to work with. 60 award winners over a 20 year period simply isn't enough data for the model to learn from. 

It isn't completely without predictive power. When validated on the 2018-19 Season it gave reasonable predictions, correctly identifying the top seven vote recipients(_in very recent years full voting totals are available_). But only after accounting for Davis and Jokić does it order them correctly. 

And it isn't only a "Power Forward" playing Center or a Center posting statistics in an unprecedented way that causes issues with sparse data. Another important type of edge case, discussed in [greater detail](https://davidvollendroff.github.io/2020-01-10-All-NBA-Centers/) in the original post, is the effect injuries have on swaying voters. So few All-NBA-level Centers have succumbed to injury at inopportune times that the model has no chance of dealing with those rare occurrences when they appear.

Luckily we can do _much_ better

## Throwing out positions
Instead of building a model that only cares about what it means to be an All-NBA Center, what if instead we ask, "What does it mean to be an All-NBA __player__?" With a flexible definition of "Center", plus using statistics from __all__ NBA players irrespective of position, we go from predictions of:

| __1st Team__ | Karl-Anthony Towns |
| :------ |:--- |
| __2nd Team__ | __Joel Embiid__ |
| __3rd Team__ | __Andre Drummond__ |
| __Runner Up__ | __Rudy Gobert__ |

To instead predicting:

| __1st Team__ | Anthony Davis |
| :------ |:--- |
| __2nd Team__ | __Nikola Jokić__ |
| __3rd Team__ | __Rudy Gobert__ |
| __Runner Up__ | __Joel Embiid__ |

Which turns out to be __perfectly__ correct.

In fact when we end up with the ability to make high-quality predictions for all positions. Below you can see the "Top 8" as determined by the expanded model which considers all players.

![Graph](/img/all_positions.png){: .center-block :}

There is one place where these outputs don't perfectly predict the All-NBA 1st Team. These predictions show that Lillard is favored by our model over Dončić, but as it turned out, Lillard was named to the 2nd Team behind Dončić. However I am encouraged to see the confidence levels in __our predictions are consistent with this outcome__. 

I am pleased with the end-stage output of this project. But beyond that I'm happier about what the process itself brought me.

## Learning along the way
My favorite aspect of this project is the real-world complexity that comes along with trying to join domain knowledge with machine-learning driven insight. Numerous challenges and considerations came along with undertaking this project. And each taught me about, or reinforced my knowledge of, the practical realities of Data Science.

### Error404: DataSetNotFound
For starters, this data set doesn't exist as some perfect _'data.csv'_ file I could go download from Kaggle. To even get started I'd have to gather, join, process and clean it all myself. And even before all of that, I needed to use anecdotal evidence about how voters made decisions to guide what information I'd seek. In the end I incorporated sources of traditional box scores, advanced metrics, and even team statistics. I decided to include team statistics because I've personally heard many of the voters for this _individual award_ declare they won't ignore team records.

My ability to successfully create the data set which is project uses is essentially my ability to __read the__ Pandas __documentation__. It's amazing how powerful the ability to read and the desire to learn can be when combined.

### The strange world of voting

![Graph](/img/ballot_box.png){: .center-block :}

There is no comprehensive archive of voting numbers, only award results. That means all we've got for supervision in this supervised machine-learning exercise are the three players who were the top three vote recipients. The hundreds of other players are labeled as equally non-winners. 

And according to my research, there is no ready-made loss function that suits our purpose perfectly here. One vote cast for a player is at the expense of another. Even if a loss function based on rank order were easily available, within the limitations of our data, reordering players 4-400 wouldn't change the loss values whatsoever. Hardly ideal.

But with this in mind I converted the "labels" of the dataset, that is their "Vote-worthiness" as follows:

__Named 1st Team__ = 5 points
{: style="text-align: center"}
__Named 2nd Team__ = 3 points
{: style="text-align: center"}
__Named 3rd Team__ = 1 point
{: style="text-align: center"}
__Otherwise__ = 0 points
{: style="text-align: center"}

There's a reason behind this particular schema. Because by definition the players who received the awards are the **right** choices. And by labeling players in the way we have, we are essentially recreating the ballot of a hypothetical voter who over 20 years hasn't given a single point to the wrong player. 

It's like having the voting record of only one person. But one who has never been wrong. And with that we can construct a Random Forest regression model to ask ourselves, "What would the perfect voter's ballot look like?" We end up with a 'vote-worthiness' metric for all players with which we can make predictions.

### Decisions in the face of uncertainty

Considering that the impact some of these award races might have, it made sense for me to calculate and display some measure of confidence in model outputs. Unfortunately for me Scikit-Learn doesn't(at the time of publication at least) have tools at hand for retrieving confidence intervals in Random Forest models.

However, I was able to find an open-source library called ForestCI that does have that functionality! But it was also terrifically out of date. Hours and hours of Googling later and I was able to perform something I have learned is called "monkey-patching" in order to make the library function for me. That's a topic for an entire other post.

## Predicting Awards at Every Position


## Future avenues of exploration
Given the amount of time and energy invested into this project I am happy with where it stands. But that doesn't mean that if I had unlimited time and resources I couldn't find ways to improve upon what I've done here.

### "Podium" Loss Function
For starters, I think the best improvement might come from what I would call a "podium" model. That is, calculating loss in a batch over all players in a given season while predicting the three players who would 'make the podium'. But because I was completely unable to find anything like this in _any_ machine-learning framework I researched I will likely never know.

Forgive me for saying, but the effort required to fabricate my own such function seems like the sort of thing that I ought to be paid for.

### Hyperparameter Tuning
In hindsight I realize that a significant portion of time was spent working on high-level and domain-knowledge influenced factors. So tuning my predictions often ended up being focused on having a 'good enough' model and determining where errors in the end product were coming from. 

I think this was a great method for making progress. I was able to refine my model and adjust my thinking rather than sitting back to watch a hyperparameter sweep that might take ages. But I see little harm from performing more hyperparameter tuning in the future. I anticipate there would be improvement, if only minimal.

### Interpretation of Random Forests
Given that I've used a Tree-Based model, I don't have to worry much about colinearity of things like __Player Efficiency Rating__ and __Wins Above Replacement__ skewing predictions. ___But___ I have read that it can lead to lowering reported levels of importance for other related features. And this can hinder interpretation. 

Fortunately a there is a technique to calculate what are called "permutation importances" which are generally more reliable. The calculated permutation importances of my model are shown below

![Graph](/img/importances.png){: .center-block :}

Buuuuuuut, even with all of the things permutation importance does well, ["it tends to over-estimate the importance of correlated variables"](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-9-307#citeas). Luckily there exists another method that works fantastically to fix even this issue!

Unfortunately though, __Drop-Column Importance__ calculation is computationally very expensive. Still, it remains true that springing for a fancier EC2 instance would in fact drive easier model interpretation. Which could go a long way when examining some of the stranger predictions the model makes.

Or put another way, it could help shine a light on the strange preferences human voters often have.
