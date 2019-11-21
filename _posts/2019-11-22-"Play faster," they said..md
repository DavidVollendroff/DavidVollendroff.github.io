---
layout: post
title: Why "play faster" is poor advice
subtitle: The trouble with correlation
bigimg: /img/ballchasing.jpg
tags: [Rocket League]
---

# "Play faster."
You'll often hear this advice given to players who find themselves in a rut, heading out to seek answers as to why that next promotion is so elusive. Those offering speed as a solution will often point out, "Look at how fast Grand Champion players are." And they say this because it makes a great deal of sense.

![Graph](/img/speeds.png){: .center-block :}

Speed and player rank have a _0.96_ correlation. That's extremely related. But then again, shooting percentage has a -0.97 correlation. Meaning that you could even more confidently say that as players get more highly ranked they because worse shooters.  

Except that's ridiculous. We all know players are much better shooters as you climb the ladder. It just so happens the number of saves being made rises even more quickly than the number of shots placed on net as you ascend the ranks. Shot accuracy actually rises dramatically. Correlation doesn't tell even close to the whole story. 

For starters, variance plays a large role in telling the story of any data. When you look at the distributions of player average speeds you can see that there is a non-trivial amount of overlap between the lowly Silver 1 population and the Grand Champions(1580 average MMR). Interestingly the overlap occurs such that 1/6th of the players in Silver 1 are playing at average speeds faster than 1/4 of Grand Champions. Put another way, the fastest Silver in a 3v3 lobby has great odds of being faster than the slowest Grand Champion in a 2v2 match.

# What's really going on then?
We're far better off asking questions with more nuance if we want to understand what this correlation between speed and mmr is hinting at. That correlation lets us know that higher ranked players are moving more quickly on average, but other data will show us how. 

![Graph](/img/speed chart.png){: .center-block :}

Gold 1 is the rank where players spend the lowest proportion of their time in a match moving at speeds that throttle alone can't reach. While Grand Champions spend more than half of their time using wavedashes, dodges or good old-fashioned boost to travel. It's unsurprising then that they consistently have the *lowest* average boost level, even though they consistently collect the *highest* number of small boost pads as they move. 

# Some food for thought

I know that many people who've read this far are thinking, "David, 'play faster' isn't meant literally. It's about decisiveness. Do whatever you're going to do, but do it quickly."

If that's the case, that sacrificing the quality of your decisions for the speed you enact them is the path to success then we should be able to find data that supports it. It turns out GC's spend the most time in the attacking third! 

![Graph](/img/attacking_third.png){: .center-block :}

The average MMR of Grand Champions used for this calculations is 1580, for those interested. As far above the top end of Champion 3 as Platinum 1 is above Gold 3.  Just as it's ridiculous to conclude that the 0.99 correlation with turnovers on your own half means that Grand Champions are more likely to give the ball away in critical moments than anyone.
