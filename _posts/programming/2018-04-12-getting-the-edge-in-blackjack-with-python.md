---
title: Getting the Edge in Blackjack with Python
date: 2018-04-12
categories: programming
---

![Casino chips](/images/casino-chips.jpg)

For the past several years in Maryland, there seemed to be a new casino opening up every other year. My first experience of going to the casino was for a friend’s birthday party back in college. We thought it would be an interesting experience to come in and check out the newest casino, Maryland Live!, that just opened up back then. When we got there, I was in awe at how much money people were blowing on games. People were laughing, yelling, and drinking while putting stacks and stacks of chips on the table. Then a friend pulled me over to a Blackjack table that had open seats and asked me to join him.

<!--more-->

## First Game (and Loss)

I sat down and the dealer asked me to place my money on the table so she could exchange it for chips. The minimum bet was $15 so I took $60 from my wallet and placed it on the table. She counted the money, pushed it down a little slot next to the chips and gave me a bunch of red chips. Then she told the players to place their bets. Everyone was putting three chips down on the bet circle so I followed suit. The dealer quickly dealt all the players their cards. I got a 20 while the dealer only has 18.

I just won $15 in less than three minutes. It felt awesome!

I continued to play and I also won the next three hands. Now my chips were stacking up. I thought to myself there was no way I could lose so I bet even more. Then the dealer got herself a Blackjack. She took every chip on the table and placed them in her stacks.

Ok! No problem, I just need to win back that money so I bet the same amount again. What followed next was a blur. I remembered the dealer keeps giving me low cards and I kept hitting until I bust. Fifteen minutes later, the dealer took away my last chips. I stumbled out of my chair, $60 less than when I began.

## Learning the Count

After that loss. I planned to come back there and get my money back. I did research on the game and learned the best action given each particular hand. Basically, I wanted to see whether it was possible to consistently win in Blackjack. Eventually, I found out about card counting systems like High-Low.

The idea of counting card is relatively simple. Every card is assigned a numerical value, either 0, +1, or -1. Low cards like 2, 3, 4, 5, 6 have +1 value while high cards like 10, Jack, Queen, King, Ace have -1 value. All other cards are not factored into the count so their values are 0.

However, if it was this easy everyone would have already done it. If I waltz into the casino with pen and paper to record the cards, I’d be (not so politely) escorted out of the casino. The casinos have lots of ways to stop card counters. This [question](https://www.quora.com/How-do-casinos-catch-card-counters?redirected_qid=2461612) on Quora contains answers that gave me insights on methods casinos employ to stop card counters. Some of those methods are talking with the player to disrupt his concentration, ask former card counters to check the table to see if the player is counting, or outright banning the player from casinos.

To be completely honest, I don’t know how practical learning to count card would be in a brick-and-mortar casino since I have never done it myself. What I can do is writing a program that can capture the idea of card counting. That would give player the freedom to make best choices with the information provided.

## Advanced Omega II Card Counting System

Let’s go over the system I’ll be using to write the program. The system is called Advanced Omega II. The value for each card in this system is shown in the table below:

**Advanced Omega II Card Values**

| 2| 3| 4| 5|	6| 7|8|	9|10|	J| Q|	K|A|
|+1|+1|+2|+2|+2|+1|0|-1|-2|-2|-2|-2|0|


As you can see, this system is more complicated than the more popular High-Low system. The values are not just 0, +1, -1 but tend to vary more. For a player counting in their head, this makes it difficult to keep track of the count. But for a computer, this is a simple matter. The best way to represent this is to use a dictionary. We can use a list to record each value from user’s input from the dictionary values and add them up together for the running count.

{% highlight python %}
def card_value(cards):
    values = {'2': 1, '3': 1, '7': 1,
              '4': 2, '5': 2, '6': 2,
              '1': 0, '8': 0,
              '9': -1,
              '0': -2}
    l = [values[card] for card in cards if card in values]
    return sum(l)
{% endhighlight %}

## Initializing The Game

In AOII system, the player is also expected to keep track of how many aces are dealt. For example, if the game uses eight decks, the player can input that integer. The total number of aces is 32 (8 decks x 4 aces = 32 aces). If two aces have already been dealt, there are still 30 aces left in the deck. Other important variables to keep track of are how many cards are already dealt and how much of the deck remained. These two variables let us calculate the true count.

{% highlight python %}
decks = int(input('Number of decks: '))
count, cards = 0, 0
decks_used = 0
aces = decks * 4
{% endhighlight %}

The true count is simply our running count divided by the number of remaining decks in the shoe. Since a +2 running count at the start is different from +2 the end even though the numbers are the same. This is because the number of cards left are different. This gives us the most accurate count for the whole deck. In a real game, players can approximate the amount of decks left by looking at the discard tray. Our program keeps track of that for us.

To keep the game constantly running, we just need to wrap all our logic into a while loop. The only ways to break out of this loop is if the player wants to quit or if there are no more cards left to play.

{% highlight python %}
while True:
    user_cards = input('Enter cards: ')
    if user_cards == 'quit':
      break

    # Keeping track of aces left in deck
    if '1' in user_cards:
      aces -= 1

    # Calculate running count and true count
    cards += len(user_cards)
    count += card_value(user_cards)
    decks_used = cards / 52
    remain = decks - decks_used
    true_count = count / remain

    # Check if deck is done
    if remain <= 0:
      print('Finished deck')
      break
{% endhighlight %}

## Counting Statistics

This program now precisely calculates both the running count and the true count. Of course it’s not very useful if all the statistics are calculated silently in the background. To solve this problem, we can add conditions to display recommendations to the user based on the true count. If the true count is high, we recommend the player to increase his bet. And vice versa. We can also display all the information calculated so far each time through the loop.

{% highlight python %}
# Make recommendations based on true count
if true_count >= 1:
    print('Increase your bet')
elif true_count <= -1:
    print('Decrease your bet')

# Print out deck information
print('>>> Running Count: {}'.format(count))
print('>>> True Count: {}'.format(round(true_count, 2)))
print('Cards Dealt: {}'.format(cards))
print('Aces Left: {}'.format(aces))
print('Deck Remain: {}'.format(round(remain, 2)))
{% endhighlight %}

With that, our program now does the heavy lifting for the player. He doesn’t need to worry about keeping track of the count. It frees up his brain to make decision about the amount of money he should bet. I put the whole program in the interactive window below. Feel free to play around with it and let me know if you find it useful. I cannot guarantee that you will make money from casinos using this program so don’t play what you can’t afford to lose.

## Card Counting Interactive Program

<iframe src="https://trinket.io/embed/python/19d0063c8d" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>
