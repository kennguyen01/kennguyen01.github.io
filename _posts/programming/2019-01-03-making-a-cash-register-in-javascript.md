---
title: Making a Cash Register with JavaScript
date: 2019-01-03
categories: programming
---

I've been working through the curriculum at [Free Code Camp](https://www.freecodecamp.org/) to learn front end development. Since I already know some HTML and CSS, I spent the majority of my time learning JavaScript. This post is about the solution for last challenge of the JavaScript section, Cash Register.

<!--more-->

## The Problem

Design a cash register drawer function `checkCashRegister()` that accepts purchase price as the first argument `price`, payment as the second argument `cash`, and cash-in-drawer `cid` as the third argument.

`cid` is a 2D array listing available currency.

The function should always return an object with a `status` key and a `change` key.

Return `{status: 'INSUFFICIENT_FUNDS', change: []}` if cash-in-drawer is less than the change due, or if you cannot return the exact change.

Return `{status: 'CLOSED', change: [...]}` with cash-ind-drawer as the value for the key `change` if it's equal to the change due.

Otherwise, return `{status: 'OPEN', change: [...]}`, with the change due in coins and bills, sorted in highest to lowest order, as the value of the `change` key.

## Sample Test and Output

An example test and answer was given on the challenge:

{% highlight js %}
// Test
checkCashRegister(19.5, 20, [["PENNY", 1.01], ["NICKEL", 2.05], ["DIME", 3.1], ["QUARTER", 4.25], ["ONE", 90], ["FIVE", 55], ["TEN", 20], ["TWENTY", 60], ["ONE HUNDRED", 100]]);

// Answer
{status: "OPEN", change: [["QUARTER", 0.5]]}
{% endhighlight %}

## The Solution

From the test, I could see that I needed to find a way to loop through all denominations of bills and coins. The problem specified that the change array should be sorted from highest to lowest. I tried to use an object but immediately ran into the problem or ordering. Since an object is an unordered collection of properties, which is the same as Python's dictionary.

### Two Arrays for Money and Value

So I had to fall back to using two arrays, one for the denominations and the other for the values.

{% highlight js %}
let denom = ['ONE HUNDRED', 'TWENTY', 'TEN', 'FIVE', 'ONE', 'QUARTER', 'DIME', 'NICKEL', 'PENNY'];
let value = [100, 20, 10, 5, 1, .25, .1, .05, .01];
{% endhighlight %}

The elements are from highest to lowest order so I do not have to do an extra step of sorting them.

### Convert 2D Array to Object

`cid` is a 2D array, which can be prone to errors if I'm not careful when working with it. An easier way to work with it is to simply convert the `cid` 2D array into an object. I will also define two variables, `total` and `change`, to keep track of the total amount in the register and change left.

{% highlight js %}
let total = 0;
let change = cash - price;

let register = {};
for (let i of cid) {
    total += i[1];
    register[i[0]] = i[1];
}
{% endhighlight %}

I run the code now and the result is something like this:

{% highlight js %}
total = 335.40999999999997;
register = {
    PENNY: 1.01,
    NICKEL: 2.05,
    DIME: 3.1,
    QUARTER: 4.25,
    ONE: 90,
    FIVE: 55,
    TEN: 20,
    TWENTY: 60,
    'ONE HUNDRED': 100
}
{% endhighlight %}

The total is a bit weird but it's due to rounding error so I can fix it later. The main point is that I have converted `cid` into an object.

### A Function to Round 2 Decimal Places

Before I go any further, I need to have a way to round the intermediate floats to two decimal places. If I don't do that, the answer will not work for every test case. The `Number.toFixed()` method formats a number into string using fixed-point notation. I just need to cast the string back into number again to get what I want:

{% highlight js %}
function twoDecimal(n) {
    return Number(n.toFixed(2));
}
{% endhighlight %}

### Looping and Subtracting

Now comes the main logic of the function. I defined a `cashback` object to hold the money subtracted from the register. Then I loop through the `value` array, if the change is at least the current value and the denomination in the register is not zero, I subtract that from `total`, `change`, and `register` and round the intermediate results.

The `cashback` object will be increased by the amount of the value if the denomination is already in it. Otherwise, it will create a new key for that denomination with the current value.

{% highlight js %}
let cashback = {};
for (let i = 0; i < value.length; i++) {
    let v = value[i];
    let d = denom[i];

    while (change >= v && register[d] > 0) {
        total = twoDecimal(total - v);
        change = twoDecimal(change - v);
        register[d] -= v;

        if (d in cashback) {
            cashback[d] += v;
        } else {
            cashback[d] = v;
        }
    }
}
{% endhighlight %}

### Return the Result

Finally, I defined a `result` object with two keys, `status` and `change` as specified by the problem. The `status` is initially set to `OPEN` and change set to an empty array.

After the previous loop, if `change` is greater than 0, that means there's not enough money in the register. If `total` is equal to 0, the amount of money in the register equal to the change so I just set `result.change` equal to `cid`.

Otherwise, there's more money in the register than the change. I will push all the keys and values in `cashback` object to the `result.change` array and return that.

{% highlight js %}
let result = {status: 'OPEN', change: []};

if (change > 0) {
    result.status = 'INSUFFICIENT_FUNDS';
    return result;
} else if (total === 0) {
    result.status = 'CLOSED';
    result.change = cid;
}

for (let d of denom) {
    if (d in cashback) {
        result.change.push([d, cashback[d]]);
    }
}
{% endhighlight %}

## A Challenging Problem

I spent quite a bit of time on this problem. With `cid` being a 2D array, it forced me to use other data structures to makes my job easier. The problem also required me to sort the output from high to low so that's an additional step I had to think about.

Overall, it's a decently challenging problem for someone who was just getting started with JavaScript. I had to think of ways to manipulate the data and it taught me a few things about array and object manipulation.
