---
title:
date:
categories:
---

This post drew from [MIT 6.00.1x](https://www.edx.org/course/6-00-1x-introduction-to-computer-science-and-programming-using-python-3) course on edX. I saw something very interesting in a lecture when professor Grimson compared two different implementations of bisection search. The algorithm for bisection search given a sorted list is:
1. Pick an index `i` that divides the list in half
2. Ask if `L[i] == e`
3. If not, ask if `L[i]` is larger or smaller than `e`
4. Depending on answer, search left or right half of `L` for `e`

After every iteration, the list is cut in half so the complexity of this algorithm should be O(log n). But as we'll see, this is not always the case.

<!--more-->

## First Implementation

{% highlight python %}
def bisect_search1(L, e):
    if L = []:
        return False
    elif len(L) == 1:
        return L[0] == e
    else:
        half = len(L) // 2
        if L[half] > e:
            return bisect_search1(L[:half], e)
        else:
            return bisect_search1(L[half:], e)
{% endhighlight %}

The base cases for this recursive implementation are when the list is empty or only has one element. Otherwise, we find the halfway point and ask whether it's greater than or less than `e`. Then we can throw away half of the list since the element cannot be there.

The problem is the argument being supplied to the recursive call. By calling `bisect_search1` with either `L[:half]` or `L[half:]`, we are making a copy of half of the list. This will add to a higher complexity. The cost of copying a list in Python is O(n). So in the end this implementation is going end up O(n log n) as opposed to just O(log n).

## Second Implementation

This second implementation requires more work but has a lower complexity. We are going to keep track of where we are in the list instead of making copies.

{% highlight python %}
def bisect_search2(L, e):

    def bisect_search_helper(L, e, low, high):
        if high == low:
            return L[low] == e
        mid = (low + high) // 2
        if L[mid] == e:
            return True
        elif L[mid] > e:
            if low == mid:
                return False
            else:
                return bisect_search_helper(L, e, low, mid - 1)
        else:
            return bisect_search_helper(L, e, mid + 1, high)

    if len(L) == 0:
        return False
    else:
        return bisect_search_helper(L, e, 0, len(L) - 1)
{% endhighlight %}

The base case for this implementation is when the list is empty. Otherwise we'll call the helper function with `low` argument at index 0 and `high` argument at last index. Inside the helper function, we first check to see if the element has already been found. If it's not then we just set the mid point to be the average of high and low.

The recursive calls to helper function is straightforward. We use the mid point as the `high` argument if it's greater than `e`, throwing away the upper half of the list. And vice versa if it's less than `e`. This implementation does the same thing as the first but it uses indices as arguments and not copies of the list. The reward for this is a lower complexity of O(log n) for our function.

## Ease of Implementation

While the second implementation is more efficient, I see that the first example is easier to implement. These two examples provided in the class were simple and straightforward. However, I can imagine a scenario where the difficulty of one implementation is much higher than the other. It's preferable to use an algorithm with lower complexity but if it takes a lot more time to implement or difficult to debug, the choice might not be clear then.
