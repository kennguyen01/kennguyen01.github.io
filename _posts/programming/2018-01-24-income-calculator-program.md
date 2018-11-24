---
title: Income Calculator Program
date: 2018-01-24
categories: programming
---

The first thing I built with Python was an income calculator program. At the time, my job paid me an hourly rate. I had no fixed schedule and had to often come in to cover for my coworkers. My wages vary a lot every other week or so. I used to have to bring up the calculator app every week to crunch out the numbers. I had to remember how many hours I worked on each day of the week, add them all up together and multiply that to my wage. Thinking back on it now, it was really slow and tedious.

<!--more-->

## A Handwritten Income Calculator

Back when I had a rudimentary knowledge of programming, I set out to write a program that could calculate my income for me. I remembered spending hours trying to make my program works properly. I did not even know what a function was or how to write one. All my code was jumbled together and very hard to read. However, I was really proud of myself when I hit run on my IDE and it finally worked.


Now let’s work on another income calculator. I promise this one is not going one big block of code like my first version. I’m going to separate them into different functions so you won’t strain your eyes reading them. There are three main parts to this program: income, taxes, and an income display.

## Calculating Income

There are two main types of income we will figure out, wages and salary. Each one is calculated differently. If you are on salary, your monthly income will be whatever your annual salary is divided by twelve months. For example, a public school teacher average salary in Baltimore, MD is $56,000 so her monthly income is $4,666.67 ($56,000 / 12 months). Then the function simply gets user input for the annual salary in float and divide that amount by 12.

```python3
def salary():
    s = float(input('\nEnter your annual salary: '))
    return s / 12
```

On the other hand, a person with wages gets paid an hourly rate per hour. If a plumber makes $26 per hour and he works a standard 40 hours per week, he would make $1,040 ($26 x 40 hours) per week, or $4,160 per month. The main difference is that a person with wages gets paid 1.5 times the hourly rate if he works more than 40 hours per week. For the wages function, we need to take into account how many hours that person work per week. If the hours are more than 40, we need to add the overtime into the total wages.

```python3
def wages():
    w = float(input("\nEnter hourly wage: "))
    h = int(input("Enter hours per week: "))
    if 0 < h <= 40:
        return w * h * 4
    elif h > 40:
        return (w * 40 + w * 1.5 * (h - 40)) * 4
```

## Federal Tax Brackets

With income out of the way, let’s talk a bit about taxes. There are a lot of different categories of taxes you have to pay including federal, state, and local taxes. In this post I will keep it simple by only talking about the Federal Income Tax Brackets. Specifically, I will be looking at the 2017 tax brackets since 2018 has only started. There are seven tax brackets for 2017, ranging from 10% all the way to 39.6%. Your bracket is determined by how much income you earned during that year. For complete information, please refer to this link: [2017 Single Tax Brackets](https://taxfoundation.org/2017-tax-brackets/).

There are two functions in this category, `taxes` calculates how much taxes the user has to pay based on annual gross income while `tax_brackets` return what tax bracket the user is in.

```python3
def taxes(i):
    if 0 < i <= 9325:
        return i * 0.1
    elif i <= 37950:
        return 932.5 + .15 * (i - 9325)
    elif i <= 91900:
        return 5226.25 + .25 * (i - 37950)
    elif i <= 191650:
        return 18713.75 + .28 * (i - 91900)
    elif i <= 416700:
        return 46643.75 + .33 * (i - 191650)
    elif i <= 418400:
        return 120910.25 + .35 * (i - 416700)
    else:
        return 121505.25 + .396 * (i - 418400)
```

```python3
def tax_bracket(i):
    if 0 < i <= 9325:
        return '10%'
    elif i <= 37950:
        return '15%'
    elif i <= 91900:
        return '25%'
    elif i <= 191650:
        return '28%'
    elif i <= 416700:
        return '33%'
    elif i <= 418400:
        return '35%'
    else:
        return '39.6%'
```

## Dictionary of 12-Month Income

Now that we have a way to calculate user’s income and taxes, we can use a dictionary to store those values. I multiply the `income` parameter by 12 since the functions `wages` and salary return a monthly income value. After that, we can find total annual taxes and divide that by 12 to get to the user’s monthly taxes. I do this because it makes it easier later when I want to calculate 12-month net income of the user.

```python3
def annual_income(income):
    d = {}
    annual = income*12
    tax = taxes(annual) / 12
    bracket = tax_bracket(annual)
    print('\nYour gross monthly income is ${:.2f}. You are in the {} tax bracket'.format(income, bracket))
    print('Your monthly taxes is ${:.2f}'.format(tax))
    for i in range(1, 13):
        d[i] = income*i - tax*i
    return d
```

## Displaying the Income Table

Finally, we can present the user with a 12-month income table simply by printing out all the values of the dictionary from previous function. This function is optional but I think it’s nice for the user to be able to see how much his net income is for 12 months.

```python3
def table(d):
    print('\n12 Months Net Income Breakdown')
    for m in d:
        if m < 10:
            print('{}  : ${:.2f}'.format(m, d[m]))
        else:
            print('{} : ${:.2f}'.format(m, d[m]))
```
