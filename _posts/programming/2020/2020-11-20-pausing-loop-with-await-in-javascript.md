---
title: Pausing Loops with Await in JavaScript
date: 2020-11-20
categories: programming
---

When I was working on creating a simple test for my flashcards app, I ran into a problem. I have an object containing the term and answer pairs. The simplest way to go through the test would be to loop through the keys and displays the answer when user clicks on **Answer** button. The problem was that the loop does not stop on each iteration for the user to select whether their answer was correct or not. I looked up different methods to solve this problem because I wasn't aware of how asynchronous functions work. Then I stumbled upon a similar StackOverflow question and somebody suggested in the comment to use async.

<!--more-->

## How Does Async Work Again?

An async function returns a promise and uses the `async` keyword in front of it:

```js
async function hello() {
  return Promise.resolve(1);
}
```

Inside an async function, `await` can be used to pause execution until the promise is returned. This was the main point I needed for my problem. Since execution is paused, I can add an event listener to waits for user input and resolve the promise afterward.

## Pausing the Loop

In my app, I have a function to load the test by looping through the terms:

```js
/**
 * Generate test with shuffled array terms.
 * 
 * @param {Object} termsObj 
 */
const loadTest = async termsObj => {
  let terms = Object.keys(termsObj);

  // Shuffle terms randomly
  terms = shuffle(terms);

  // Number of right and wrong answers
  let right = 0;
  let wrong = 0;

  for (let i = 0; i < terms.length; i++) {
    let question = terms[i]
    let answer = termsObj[question];

    showQuestion(question);
    showAnswer(answer);

    // Wait for user to click answer button
    let score = await userAnswer();
    if (score) right++;
    else wrong++;
  }
  showScore(right, wrong);
  hideControl();
  newTest();
}
```

The loop stops at the line `let score = await userAnswer();`. It is waiting for the promise of the function `userAnswer()` to resolve.

```js
/**
 * Clear answer <div> when either correct or incorrect
 * button is clicked.
 * 
 * Resolve 1 for correct or 0 for incorrect.
 */
const userAnswer = () => {

  function clearAnswer() {
    let answer = document.querySelector('.test-answer');
    answer.innerHTML = '';
  }

  return new Promise((resolve) => {
    clearAnswer();

    let correctBtn = document.querySelector('#correct');
    correctBtn.addEventListener('click', () => {
      resolve(1);
    });

    let incorrectBtn = document.querySelector('#incorrect');
    incorrectBtn.addEventListener('click', () => {
      resolve(0);
    });
  });
}
```

Inside `userAnswer()`, the promise only resolves when either the **Correct** or **Incorrect** button is clicked. If the user does not provide any input, the execution pauses here. `async` and `await` made the process of stopping a loop and wait for input simple.