---
title: Mini Cactpot Algorithm Part 2
date: 2018-01-07
categories: programming
---

This is the second part of the mini cactpot algorithm. This post is about calculating potential values of each line on the ticket and recommend the highest line of value to the user. If you want to see how to set up the mini cactpot ticket, use this link: [Part 1](/programming/mini-cactpot-algorithm-part-1.html).

<!--more-->

## Class Calculate

Similar to class `Game`, class `Calculate` will also take one argument, the dictionary of ticket positions. I’m going to initialize the class.

```python3
class Calculate:
    def __init__(self, ticket):
        self.positions = ticket
```

Since I want to calculate each three number lines, I use dictionary to map each line to its three positions on the ticket.

```python3
def lines(self):
    ticket_lines = {
        1: [self.ticket['g'], self.ticket['h'], self.ticket['i']],
        2: [self.ticket['d'], self.ticket['e'], self.ticket['f']],
        3: [self.ticket['a'], self.ticket['b'], self.ticket['c']],
        4: [self.ticket['a'], self.ticket['e'], self.ticket['i']],
        5: [self.ticket['a'], self.ticket['d'], self.ticket['g']],
        6: [self.ticket['b'], self.ticket['e'], self.ticket['h']],
        7: [self.ticket['c'], self.ticket['f'], self.ticket['i']],
        8: [self.ticket['c'], self.ticket['e'], self.ticket['g']]
    }
    return ticket_lines
```

My next method, `combinations`, is actually a Python built-in. The reason why I wrote out the code was because my free [Trinket.io](https://trinket.io/) did not support itertools.

```python3
@classmethod
def combinations(cls, iterable, r):
    pool = tuple(iterable)
    n = len(pool)
    if r > n:
        return
    indices = list(range(r))
    yield tuple(pool[i] for i in indices)
    while True:
        for i in reversed(range(r)):
            if indices[i] != i + n - r:
                break
        else:
            return
        indices[i] += 1
        for j in range(i+1, r):
            indices[j] = indices[j-1] + 1
        yield tuple(pool[i] for i in indices)
```

The method takes an iterable and return tuples of combination for those elements at specific length. You can read more about it here: [itertools.combinations](https://docs.python.org/3.6/library/itertools.html#itertools.combinations). Suppose if you have a list of 4 items and you want to get all 2 item combinations, you can use `itertools.combinations(list, length)` for that.

```python3
import itertools

a = [1, 2, 3, 4]
b = list(itertools.combinations(a, 2))

>>> [(1, 2), (1, 3), (1, 4), (2, 3), (2, 4), (3, 4)]
```

With this method, I can calculate possible combinations for the numbers the user has not picked. So if the user picked 1, 2, 3, 4 then 5, 6, 7, 8, 9 are still available. Consequently, I just need to find out which positions on the ticket that is still hidden and replace those with the available numbers. I received help from Francisco Couzo on StackOverflow on the method to replace hidden values with combinations. Here’s the link for the question I posted: [question](https://stackoverflow.com/questions/47765021/how-to-get-combinations-of-list-with-values-from-another-list).

```python3
def lists_combinations(self, list_1, list_2):
    indices = [i for i, x in enumerate(list_1) if isinstance(x, str)]
    for combo in self.combinations(list_2, len(indices)):
        for index, char in zip(indices, combo):
            list_1[index] = char
        yield tuple(list_1)
```

His function finds the indices of all the string in the first list and replace them with combinations from second list. I modified the function to fit with the class. In my case, `list_1`  is the value of each line for the dictionary I created earlier. While `list_2` is the available numbers.

## Calculating Payout

The actual calculation happens in the method `lines_combinations`. I used another dictionary to map each line to its possible combinations. It uses the method earlier to do that. `num_lines` and `num_list` are simply the same arguments for `list_combinations`.

```python3
def lines_combinations(self, num_lines, num_list):
    lines_combo = {}
    for line in num_lines:
        lines_combo[line] = list(self.lists_combinations(num_lines[line], num_list))
    return lines_combo
```

With the combinations for each line calculated, I can go on crunching out the potential payout of each line. The payout varies depend on the sum for each line. By summing up each combinations returned from `lines_combination` and multiply them with the payout, I can get all potential payouts. Finally, I can find the average potential payout by using floor division of the total sum with the length of the list.

```python3
@classmethod
def lines_payout(cls, combinations):
    payout = {6: 10000, 7: 36, 8: 720, 9: 360, 10: 80, 11: 252, 12: 108,
              13: 72, 14: 54, 15: 180, 16: 72, 17: 180, 18: 119,
              19: 36, 20: 306, 21: 1080, 22: 144, 23: 1800, 24: 3600}

    sum_payout = {}
    for line in combinations:
        sum_payout[line] = [sum(combo) for combo in combinations[line]]

    for line in sum_payout:
        sum_payout[line] = sum([payout[value] for value in sum_payout[line]]) // len(sum_payout[line])
    return sum_payout
```

However, the user does not need to know what happens in the code. Therefore I used another method to print out a message notifying the user which line has the best possible payout. There are cases where multiple lines can have the best payout. `recommendation` takes the dictionary with each line average payout and find the maximum value. It returns a string containing the line(s) recommended and the potential payout value(s).

```python3
@classmethod
def recommendation(cls, user_payout):
    print('---------------')
    highest = max(user_payout.values())
    recommend = [key for key, value in user_payout.items() if value == highest]
    string = ''
    for key in recommend:
        string += Color.BOLD + '> Line {} has the highest payout of {}!\n'.format(key, user_payout[key]) + Color.END
    return string
```

All that’s left to do now is to write a function to set up the game and calculate the potential payout. That should be a simple matter so I’m going to end the post here.
