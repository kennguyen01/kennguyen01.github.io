---
title: Mini Cactpot Algorithm Part 1
date: 2017-12-26
categories: programming
---

Here is the link to part 2: [Part 2](/programming/mini-cactpot-algorithm-part-2.html)

This is the first part of the mini cactpot algorithm. If you want to take a look at the complete code, click on the link: [FF14 Mini Cactpot Calculator](/programming/ff14-mini-cactpot-calculator.html). I will be talking about two main classes of the program, `Game` and `Calculate`. The class `Game` deals with displaying the ticket to the user, getting user inputs, and updating the ticket accordingly. The class `Calculate` does the heavy lifting by calculating all possible combinations of three number lines on the ticket and the payout of each.

<!--more-->

## Class Game

Since the ticket is a 3×3 matrix, I first thought of using a nested list for internal representation of the ticket. I could use a list comprehension for this and use 'x' as default values of each value.

```python3
ticket = [['x' for j in range(3)] for i in range(3)]

>>> ticket = [['x', 'x', 'x'],
>>>           ['x', 'x', 'x'],
>>>           ['x', 'x', 'x']]
```

However, I realized when I tried to update user inputs to the nested list is that it can become complicated. I would need to keep track of each position inside the nested list based on its index value. So the first position is `ticket[0][0]` and the last position is `ticket[2][2]`. Then the user will need to enter their own numbers, which can lead to very messy code and prone to error. I decided against using nested list and just use a dictionary to map letters of the alphabet to each position.

```python3
ticket = {'a': 'a', 'b': 'b', 'c': 'c', 'd': 'd', 'e': 'e',
          'f': 'f', 'g': 'g', 'h': 'h', 'i': 'i'}
```

This helps me out significantly. Now I can pinpoint exactly where each position is based on their letter key. Then I use a class for ANSI escape sequences for text decoration to makes strings stands out in the console. This is optional but it helps with usability.

```python3
class Color:
    BOLD = '\033[1m'
    UNDERLINE = '\033[4m'
    END = '\033[0m'
```

With the appropriate data structure set, now I can start writing out the class `Game` that takes one argument, the dictionary `ticket`.

```python3
class Game:
    def __init__(self, ticket):
        self.ticket = ticket
```

The user will be interacting with the program so a `display` method is needed. In my case I used a list for each line of string. On lines where the ticket numbers are, string formatting is useful. Just join them all together with `\n` in the return statement.

```python3
def new_ticket(self):
    display = [
        '--------------',
        Color.BOLD + '4  5  6  7  8' + Color.END,
        Color.BOLD + '3' + Color.END + '  {}  {}  {}'
                                       .format(self.ticket['a'],
                                               self.ticket['b'],
                                               self.ticket['c']),
        Color.BOLD + '2' + Color.END + '  {}  {}  {}'
                                       .format(self.ticket['d'],
                                               self.ticket['e'],
                                               self.ticket['f']),
        Color.BOLD + '1' + Color.END + '  {}  {}  {}'
                                       .format(self.ticket['g'],
                                               self.ticket['h'],
                                               self.ticket['i']),
        '--------------'
    ]
    return '\n'.join(display)

>>> 4  5  6  7  8
>>> 3  a  b  c
>>> 2  d  e  f
>>> 1  g  h  i
```

The user can easily see where each 3-number lines are on the ticket by number 1-8 surrounding the ticket. The next step is to get the four numbers chosen by the user. The user simply enters the letter of the ticket and the number chosen. I use a for loop to get each letter-number pair, split the inputs and store them in `user_inputs` dictionary. This is static method that doesn’t use the class `Game` object at all.

```python3
@staticmethod
def user_numbers():
    user_inputs = dict()
    for counter in range(1, 5):
        letter, number = input('Number {}: '.format(counter)).split()
        user_inputs[letter] = int(number)
    return user_inputs
```

The next method is `fill_numbers`. It takes the values from the dictionary returned in `user_numbers` and fill them in the class attribute `ticket` if their dictionary keys match each other.

```python3
def fill_numbers(self, numbers):
    """
    Fill in numbers to ticket from dictionary of user's inputs
    """
    for key, value in numbers.items():
        for letter in self.ticket:
            if letter == key:
                self.ticket[letter] = value
    return self.ticket
```

Those are all the initial setups for the program. In the next post I will be talking about the actual calculation of all potential combinations in the class Game.
