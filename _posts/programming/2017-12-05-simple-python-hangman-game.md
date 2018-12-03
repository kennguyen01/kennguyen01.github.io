---
title: Simple Python Hangman Game
date: 2017-12-14
categories: programming
---

Hangman is a popular game to implement in programming. You can test your knowledge of concepts like string, boolean, and input when creating the game. It’s also a fun project to do because you can play the game with your friends afterward. If you don’t know about the game, you can read more about it here: [Hangman](https://en.wikipedia.org/wiki/Hangman_(game)). First, you can play around with the interactive console below to see how the game works. Feel free to modify the code, we’ll be going over them.

<!--more-->

In this post, I will walk through the process of writing the game in Python. I’m going to break the game into smaller pieces so we can write function for each piece. This helps with reusing the code and debugging each piece separately. Let’s get started.

## Planning out the game

Hangman is a word guessing game at its core. The game selects a random word and user needs to input each letter per turn. The letter is checked against the word. The game then gives user feedback whether he guessed correctly. User has six chances for incorrect guess before he loses, indicated by the complete picture of the hanging man.

![Hangman](https://i.imgur.com/uJDZJmL.jpg)

We don’t need to worry about the picture since this is only the implementation of the game. We can use text to indicate guesses user has left. The outline of the game is as followed:
- Get random word from list
- Check user input against word
- Tell user what letters are available
- Check if word is guessed correctly
- Looping through the game

## Get Random Word from List

The list of words is either a list we’ve created or a text file. For now, let’s just make a list of random words from the dictionary. We can use the random module to select the word from that list.

{% highlight python %}
import random

words_list = ['acorn', 'bull', 'cactus', 'dragon', 'exercise',
              'food', 'outside', 'shampoo', 'violin', 'yogurt', 'zipper']

def random_word(words_list):
return random.choice(words_list)
{% endhighlight %}

## Check User Input Against Word

Now we need to display the number of letters in the word to the user. Since this function checks each time a new user input is entered, we can start with an empty string. With letters not guessed yet, we simply add an underscore, `“_”`, to to the empty string. With a correct guess, we add the correct letter to the string instead of underscore. Remember to add space to next to the underscore since `“_ _ _”` is easier to read than `“___”`.

The necessary parameters for this function are the random `word` and a list of guesses, `user_guesses`, user made.

{% highlight python %}
def display_letters(word, user_guesses):
    letters_string = ''
    for letter in word:
        if letter in user_guesses:
            letters_string += letter
        else:
            letters_string += '_ '
    return letters_string
{% endhighlight %}

## Tell User What Letters Are Available

Once user enters a letter, we need to remove that letter from the alphabet. This helps user see what letters are still available to use. It is very similar to the function above. It checks the letters inside  `user_guesses` against the alphabet and return a string with available letters.

{% highlight python %}
def available_letters(user_guesses):
    alphabet = 'abcdefghijklmnopqrstuvwxyz'
    letters_left = ''
    for letter in alphabet:
        if letter not in user_guesses:
            letters_left += letter
    return letters_left
{% endhighlight %}

## Check If Word Is Guessed Correctly

Now let’s write a function to check if the letters guessed by user match the word. If each string inside  `word` are also in `user_guesses`, the function return True and False otherwise.

{% highlight python %}
def correct_word(word, user_guesses):
    for letter in word:
        if letter not in user_guesses:
            return False
    return True
{% endhighlight %}

## Looping Through the Game

Finally, we need to put all the pieces together to write the game function hangman. We need to keep a few points in mind:
- Variable for the random word
- List of letters guessed
- Number of mistakes the user is allowed
- Terminating condition for the loop

With that in mind, let’s go over how the game is going to play out. First, the game prints a welcome message to the user. Then it chooses a random word from the list and tells the user how long that word is. Afterward, user is given a number of chances and available letters to choose from the alphabet. The user enters a letter and the game tells him whether that letter is correct or not. The game continues until either user guesses the word correctly or runs out of chances.

The only thing we need to look out for is when the user guesses a letter that he already used. If that’s the case, we need to go back to the beginning of the loop and start over. For the terminating condition, we can either use a `break` statement to exit the loop or use a flag to set the loop condition to False. Either will work.

{% highlight python %}
def hangman():
    word = random_word(words_list)
    print('Welcome to the Hangman game!')
    print('Your word has {0} letters.\n'.format(len(word)))

    chances = 6
    user_guesses = []
    while True:
        print('Your chances: {0}'.format(chances))
        print('Available letters: {0}'.format(available_letters(user_guesses)))

        guess = (input('Enter a letter: ')).lower()
        if guess in user_guesses:
            print('You used that letter already: {0}\n'
                  .format(display_letters(word, user_guesses)))
            continue

        if guess in word:
            user_guesses.append(guess)
            print('Good guess: {0}\n'.format(display_letters(word, user_guesses)))

        elif guess not in word:
            user_guesses.append(guess)
            print('Incorrect: {0}\n'.format(display_letters(word, user_guesses)))
            chances -= 1

        if correct_word(word, user_guesses):
            print('Congratulations, you won!')
            break

        if chances == 0:
            print('You lost! The word was {0}'.format(word))
            break
{% endhighlight %}

Once we combine everything together, the game will work. By having each piece of the program does different thing, we can easily debug the program if we run into a problem.

## Hangman Interactive Program

<iframe src="https://trinket.io/embed/python/9b07ac3230" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>
