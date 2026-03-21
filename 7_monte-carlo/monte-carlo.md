# Monte Carlo Methods

One of the most useful (and sometimes creative) ideas in computational methods!

## Idea, and a structural analysis example

It is not always clear how to formulate a problem "deterministically"/"explicitly", i.e. with a simple equation. An example:

A manufacturing process produces structural beams whose yield strength follows a Weibull Distribution with known statistical parameters. The beams are destined to be used in a structure that supports a known applied load, equally shared by six beams. If any beam fails, its load is redistributed among the remaining intact beams (increasing the chances of a successive failure). If two beams fail, the structure fails. What is the probability that structural failure occurs for a given applied load?

Whoa! How could we calculate this? If there are six perfect beams, no problem, just make it so the worst-case applied load is less than six times the yield strength. But with the probability distribution for failure, we might have a beam whose yield stress is 20% lower, so we'd need to be more conservative... but also, we aren't fully failed until two beams fail, so having one bad beam isn't necessarily going to doom the structure... but also, if one beam fails, the other beams are going to face a higher load. So complicated!

A Monte Carlo approach would be:
1. Sample six values from the Weibull Distribution to represent the strength of our six beams.
2. Simulate loading with a known applied force, including allowing for component failure and load redistribution. Judge if the overall structure fails.
3. Repeat 1000 times... choosing six new beams, testing them for a given force, determining if the structure fails.

In the end, we will have a relationship between the probability of failure and the applied load based on the statistics of our beams.



## NCAA Basketball Tournament brackets

I don't follow sports much, but the NCAA [Women's](https://www.espn.com/womens-college-basketball/bracket) and [Men's](https://www.espn.com/mens-college-basketball/bracket) Basketball Tournaments just began, and these provide a really interesting opportunity to discuss Monte Carlo Methods.

For those who are unfamiliar, these tournaments each include 64 teams and it is "single elimination": all 64 teams play one game in the first round, and the 32 winners move on to the second round. These 32 teams all play one game in the second round, and the 16 winners move on to the third round. The fourth round will have 8 teams, the fifth round will have 4, the sixth round will have 2, and then a single champion is declared. In total there are 63 games.
:::{aside}
I am aware there are 68 teams now, for some reason.
:::

For any single game, even a hypothetical one, it is perhaps reasonable to talk about a team's win probability. It is vastly more complicated to rigorously calculate that team's chance of being the overall champion. Team A plays against Team B in the first round; then, if they win, Team A plays against Team C or D in the second round; then, if they win, they play against Team E, F, G, or H in the third round; then, if they win, they play against Team I, J, K, L, M, N, O, or P in the fourth round; then, ... . There are so many possibilities! Even if we trust the probabilities for a single game, how can we compute the probability that Team A wins the tournament?
:::{aside}
[The Elo Rating System](https://en.wikipedia.org/wiki/Elo_rating_system), for example, has been adapted to sports, and it can be translated into a probability.
:::

An answer: use a Monte Carlo Approach. Simulate the tournament 100,000 times using those win probabilities. In how many of those did Team A win the championship?

:::{tip}
Don't gamble.
:::