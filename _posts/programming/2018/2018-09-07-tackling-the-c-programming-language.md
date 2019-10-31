---
title: Tackling the C Programming Language
date: 2018-09-07
categories: programming
---

I’m finally back from hiatus. It’s been a while since I wrote my last blog post. I’ll take some time in this post to share what I’ve learned during the time period. One of the thing I was always hesitant to approach while learning to program was C. This is because I had this image in my head that C is an extremely difficult language to learn. I remembered my friends told me that they hated writing C code because it is a low level language. They had to manually allocate memory, fiddling with pointers, and all the other good stuff C provided. Since I had time this summer, I decided to bite the bullet and finally sit down to learn C.

<!--more-->

## Learning C One Variable at a Time

I looked around for good resources to learn C and everyone online seemed to point to one book. That book is [The C Programming Language](https://www.amazon.com/Programming-Language-2nd-Brian-Kernighan/dp/0131103628) by Brian W. Kernighan and Dennis M. Ritchie. I checked it out on Amazon and I was surprised at how small the book is. There are only 272 pages. I can easily read a novel of that size in one sitting. In comparison, one of the Python book I also saw on Amazon was a whopping 1,648 pages! For those of you who want to take a look at this massive tome, it’s [Learning Python](https://www.amazon.com/Learning-Python-5th-Mark-Lutz/dp/1449355730/ref=sr_1_4?s=books&ie=UTF8&qid=1535703779&sr=1-4&keywords=learning+python) by Mark Lutz.

So I bought the book and get started right away. The writing style was easy to follow and the first chapter was great. It introduced me to the syntax of C and give me a quick introduction to writing the code right away. The only caveat with this tutorial is that the book assumed you have some prior knowledge of programming. Programming concepts such as variables, functions, and control flow are briefly mentioned but not fully explained. A beginner might have to struggle a bit in the beginning.

A difference I found between C and Python is that I must declare the data type of the variables before using them. Python is dynamically typed, so there is no way to declare a data type. I simply name a variable and then assign it to an object. The name will then bind to the object in Python. Since C is a compiled language, the compiler does static type checking when the program is compiled. It’s not a bad thing because it forces me to look at the structure of the program before I sit down and write the code.

## You Want a String? Here’s an Array and Some Characters

For me, one of the most jarring experience learning C is that it does not support a string type. Instead, what C has is an array of characters terminated by a null character. So for a string such as `"hello, world"` there are actually 13 characters even though you can only see 12 characters, including space, in that string. The null character `\0`  is at the end of every string to signify the end of the string. For example, if I want to count how many characters does `"hello, world"`  have, I just increment `i` by one until I encounter a null character.

```c
#include <stdio.h>

int main(void) {
    int i;
    char s[] = "hello, world";

    for (i = 0; s[i] != '\0'; i++)
        ;

    printf("%d\n", i);

    return 0;
}

>>>12
```

The for loop does not need to have anything in it since I already increment `i` by one each time through the loop. As far as the size of the string goes, I can declare to array to contain 13 bytes, 1 for each character, by explicitly writing `char s[13] = "hello, world"` or I can let the compiler handle that for me. This is the part where C can be particularly nitpicky. If for some reason I decide that the size of my array is less than 13, I can run into buffer overflow issue if I decide to use that string in another function.

This is where a high level language like Python becomes more convenient. For example, if I want to copy a string in Python, I just copy the whole string or part of it to another variable. In C, I would need to copy every character individually. C does have a function called `strcpy` from the library that does this for me. But it’s still good practice to know how to implement simple string operations.

## The Wonders of Pointers

Now we come to the part where I spent quite a bit of time on, pointers. Simply put, a pointer is a variable that points to an address in memory of another variable. So why would you want to use pointers instead of the variable itself? Apart from making the program faster, since you can access the data directly in memory, it actually makes the program simpler. In C, arguments are passed by values to functions. That means the function accesses a local copy of the arguments and not the actual arguments themselves. If you want to change the argument values in the function, your code will not affect the arguments. But if you pass the pointers of the values to be changed, now the function can change the objects outside of it.

That was a lot of explanation so let me give an example directly from the book. say you want to swap variables `x` and `y`, you assign the addresses of those variables to the function swap with the operator `&`. So the function looks like `swap(&x, &y)`. Inside the function `swap`, you use the operator `*` to access the objects the pointers point to.

```c
void swap(int *x, int *y) {    /* interchange *x and *y */
    int temp;

    temp = *x;
    *x = *y;
    *y = temp;
}
```

Pointers are used to access an array more efficiently. If you assign variable `p` to point to array `a[]`, it will point to the first element, or `a[0]` of the array. Consequently, `*(p + 1)` points to the address of the next element `a[1]. Pointers and arrays in C are closely linked. Accessing elements of an array in pointers are faster than using array subscripting. Pointers can also be used to point to functions and other pointers so they are extremely convenient when used properly.

## Pointers and Data Structures in C

One of the reason why pointers are covered extensively in C is because of its importance in data structures. Take a linked list for example. The typical way to implement one is as followed:

```c
typedef struct list {
    int item;
    struct list *next;
} list;
```

`typedef` defines a new data type that you created while `struct` denotes a structure that can contain multiple data types. There are only two things in the brackets, an `item` that you want to hold and a pointer pointing to the next node of the linked list. Of course you can implement a linked list without pointers by using arrays. But using pointers is just more efficient.

Let’s look at another example, a binary search tree implementation:

```c
typedef struct tree {
    int item;
    struct tree *left;
    struct tree *right;
} tree;
```

Similar to the example above, the tree contains one item. The only difference is that instead of only one pointer to point to next node, there are two pointers. One pointing to the left node and the other to the right node. Again, you can do this without pointers by using array indices but there’s a chance where you might run into problem if you call `malloc` to allocate memory for each node of the tree individually.

## So Why Learn C?

At this point I asked myself the question, will I ever actually use C extensively in the future? The answer is a definite no. However, I learn C because I view it as the foundation for my computer science knowledge. There are times when I first learn Python that things just do not work and I just cannot understand why. Python abstracts away a large chunk of the low level details and let the programmers worry more about the higher level logic of the program. At the same time, I feel like I just depend a lot on what somebody else has already wrote before me without having an understanding of it.

By taking the step to learn C, now I can actually see how certain things work below the surface, so to speak. I actually come away having more appreciation for Python because certain things are so much simpler to do with a high level language. I’m glad I took the time to learn because it gave me new insights into programming that I did not have before.
