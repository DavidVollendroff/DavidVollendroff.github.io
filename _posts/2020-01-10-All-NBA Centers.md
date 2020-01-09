---
layout: post
title: All-NBA Centers in 2020
subtitle: What has changed and what remains the same about receiving this honor.
bigimg: /img/centers.jpg
image: /img/shaq_logo.png
tags: [NBA]
---

# 2020 All-NBA Centers
# Times are changing

Some of the difficulty involved in modeling which Centers are likely to be named to the 2020 All-NBA Teams comes from the fact that the role of the Center in modern basketball isn't what it used to be. Consider Anthony Davis, the 1st Team Center in 2018. According to [BasketballReference.com](https://www.basketball-reference.com/players/d/davisan02.html#all_pbp) he was considered to be a Power Forward rather than a Center by a 51% to 49% margin. The dataset I scraped from the site reflected his definition as a Power Forward, and my models never had the chance to even consider him. But in 2018 voters simply saw him as the best available candidate for 1st Team All-NBA at the Center position.

## The scarcity of data
Another problem that needs consideration when thinking about making good predictive models is the amount of training data available. But because fewer players are playing the Center position than in years past, and the fact that there is only one spot available per All-NBA Team, we have less data available than we'd like. And this causes real issues.

For starters..

### Nikola Jokić's passing is literally off the charts
When Nikola Jokić earned his place as an All-NBA Center for the first time he did so while dishing out more assists than anyone since Wilt Chamberlain. The modern All-NBA voting system has only existed since the '89-'90 season. So when we look at how our model values points and assists there is _no_ point of reference.

![Graph](/img/PTS_AST.png){: .center-block :}

It should be no wonder then that when asked to evaluate players in 2019, where Jokić's assist numbers were again were off the charts, he's misclassifed as being the 4th most worthy candidate instead of the best. And were it not for this error my model would have correctly predicted last years All-NBA Centers in correct order down to 7th place.

That's not exactly true though. And it's because of..

### Injuries

The one other glaring miscalculation my model seems prone to make is that of failing to recognize the impact of injuries on a players chances at receiving voter support.

Anthony Davis suffered an injured that effectively sidelined him after participating in his 41st game of the 2018-19 season. He would miss long stretches of games, playing with restrictions on the few occasions he would participate moving forward. The fact that he demanded a trade with multiple years left on his contract seemed to sour voters as well. He also would receive only a single 3rd team vote, rather than the 2nd Team honors my model anticipated from his statistics.

Similarly, my model says DeMarcus Cousins ought to have been the 1st Team All-NBA Center in 2018. And by a very large margin. But Cousins played only 48 games before suffering a season-ending injury. In reality he received only vote, and it was for the 3rd team.

Defining accuracy for these sorts of predictions is difficult, because >90% of Centers receive no votes whatsoever in a given year, and only three receive recognition. There is no comprehensive archive of voting numbers, only award results. So a baseline classification model would guess that no one makes the All-NBA Team and be correct ~98% of the time. As it is my models use random forest regression and linear regression to rank players by something akin to a vote-worthiness metric. One fun note; linear models are absolutely garbage for this sort of task.

But considering the fact that apart from these two errors in judgment my model correctly predicted the top seven vote recipients in their order leaves me to believe my model isn't completely without predictive power.

There simply aren't enough examples in the Centers dataset to properly learn this rule of thumb. Spaces on the All-NBA teams seem to be significantly swayed by productivity more than raw talent. It makes one think of the old adage, "The best ability is availability."

# What the model thinks is important
![Graph](/img/nba_feature_weights.png)


### Ideas to improve the model

Using all of the data gathered for every position, not just Centers. Perhaps this would provide insight into what voters view as being a good basketball player in a general sense, and not only what has historically been done by Centers because it was what was expected in that role.
