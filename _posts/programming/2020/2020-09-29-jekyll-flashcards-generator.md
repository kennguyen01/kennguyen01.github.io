---
title: Jekyll Flashcards Generator
date: 2020-09-29
categories: programming
---

The last post I wrote was on March, right before the pandemic happened. I never thought things would change this much in the span of six months. I heard the news about coronavirus going on in China before March but never thought it would hit the U.S. as hard as it did. I've just stayed indoor since then most of the time.

In the beginning, I spent a good chunk of that time just playing video games. The news was saying how if everyone practices social distancing and wear masks, the pandemic would be under control in just a couple of months. It's been six months since then and the number has only been increasing. So now I try to use the time to work on a project that create flashcards using Jekyll and Github Pages.

Here is the link to the project: [Jekyll Flashcards](https://raisingexceptions.com/jekyll-flashcards/)

<!--more-->

## The Need for Flashcards

### Free Online Flashcard Systems

I signed up for some online classes and I needed to make some flashcards for studying. I used to make physical flashcards before but they're time-consuming. I tried [Quizlet](https://quizlet.com/) and it has a pretty nice flashcards system. The problem is that it's designed for regular text and not code. When there's some code in the card, it's being rendered as normal text with some formatting issues. Occasionally, there's also some ads in the middle of my study session.

Another really good flashcards program is [Anki](https://apps.ankiweb.net/). This is probably the most robust flashcards program I've ever used. A major advantage of using Anki is the fact that it also has a very good [syntax highlighting add-on](https://ankiweb.net/shared/info/1463041493). Also, you can sign up for a [free account](https://ankiweb.net/about) that sync your cards on different computers.

As far as flashcards go, I don't think it gets much better than Anki.

### Writing My Own

This would be where the post ends if I'm content with using something already invented. But reinventing the wheel is a good opportunity to learn something new. My flashcard system needs to have three important features:

1. Free.
2. Accessible anywhere.
3. Can handle code syntax.

With that in mind, there's only one site that I trust to handle this: Github. Even this blog is hosted on Github for free. Since I'm familiar with Jekyll already, I just need to work on front-end and let Github handles all the heavy lifting.

## It's All About the JavaScript

I started by trying to use JavaScript to read the markdown files in the repo. That didn't work out too well due to the fact that the site is static. Jekyll generates the site with support from Github Pages. That means JavaScript can only access whatever content is already rendered by the time the script loads.

I actually spent about half of my time working with the Firefox Developer Tools instead of just writing code. Mostly from trying to see how the content is generated and manipulate it with JavaScript.

### It's Not Complete Without a Test

The most difficult aspect for me was working on a simple test for each deck of cards. I have the terms inside an object and need to loop through them as the test continues. But at the same time, the loop needs to stop and wait for user to selects whether the answer was correct or not. I did some research and it turned out `async` and `await` are the keywords here.

I've never worked with async before. I spent quite a bit of time figuring out how to resolve the `Promise` so the loop does not get stuck on the first term. After I understand how the promises are consumed, it was a great feeling.