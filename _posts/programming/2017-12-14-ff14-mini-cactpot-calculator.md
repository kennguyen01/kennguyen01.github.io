---
title: FF14 Mini Cactpot Calculator
date: 2017-12-14
categories: programming
---

![New ticket](/images/new-ticket.jpg)

**Update:** I made a web app for this program hosted on PythonAnywhere. Here’s the link: [Mini Cactpot Calculator](http://minicactpot.ml/). It does the same thing as this program but it looks much better and is more user-friendly.

Final Fantasy 14 MMO has a minigame called [Mini Cactpot].(https://na.finalfantasyxiv.com/lodestone/error/unsupported_browser/?back_uri=%2Flodestone%2Fplayguide%2Fcontentsguide%2Fgoldsaucer%2Fcactpot%2F) The ticket plays out on a three by three matrix with numbers from one to nine. The interesting thing about the game is that you cannot reveal all the possible numbers on the ticket. You get a number for a new ticket and can scratch off three additional numbers. Therefore the ticket still has five hidden numbers that you have to guess.

<!--more-->

![Filled ticket](/images/filled-ticket.jpg)

## Thoughts on the Game

The game piqued my curiosity. Since the ticket is just another form of a 3×3 matrix. There has to be a way to calculate the line with the best possible payout. So I thought to write the program myself. It was a challenge due to the fact that there is not a right solution to the problem. With many unknown variables, I can only use a brute force program to calculate the potential payout for each line. It is not perfect but it works.

![Ticket payout](/images/ticket-payout.jpg)

In the long run, I believe you can get a better payout with the program than guessing randomly. In this post I’m only going to put the code. I’ll write about the algorithm of the game in separate posts. If you see how improvements can be made to the code, please let me know.

## Mini Cactpot Interactive Program


<iframe src="https://trinket.io/embed/python/fac4b65d9a" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>
