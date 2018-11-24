---
title: Managing Attention Leaks
date: 2018-09-27
categories: rants
---

If I need memory for something I don’t know the size of in C, I have to dynamically allocate it. `malloc` does this by allocating memory from the heap. Then I use a pointer to point to this block of memory. But there is no garbage collection in C. That means after I finish with it, I have to call `free` to deallocate the memory so it can be used for something else.

What happens when I just keep asking for memory without freeing it? Memory leaks. Over time, the program will hog all the memory until the system runs out of memory. When this happens, the whole program will crash.

<!--more-->

## A Limited Amount of Attention

Using the computer as analogy to our brains, we have only a limited amount of attention that we can spare to perform any given task. Driving to work is a good example. When we step inside the car, we’re allocating a specific chunk of attention so we can operate it. This chunk of attention will be used until we get to work and step out of the car. Afterward the attention will be freed because we do not need it anymore.

Of course we don’t use the same amount of attention every time we drive. I’ve been driving for a long time so the skill does not require much attention for me. I don’t have to focus on how to change lanes or merging onto the highway. However, if I allocate another chunk of attention to something else while I’m driving, then I’m in trouble. I’ve been guilty of this before when I look at texts on my phone, only to swerve a bit toward the next lane.

The human brain is designed in such a way that multitasking negatively affects our performance. We perform best when we focus only on one task at a time and get it done. But I didn’t believe this before. If I do two things at once in the same span of time, I would get twice the amount of tasks done. Right?

## Attention Fragmentation

I had this brilliant idea before about how I was going to listening to self-help audiobooks while driving to and from work. I used to commute about an hour each way so this would give me two solid hours of listening. So I got a bunch of audiobooks on my phone and connected it to the Bluetooth in my car. I did this for several months.

At first it was interesting, I was able to listen to a lot of different books. But the inefficiency of this habit slowly dawned on me later. Even though I was going through the audiobooks much faster than reading them, I was not comprehending and retaining a book deeply. Sure, I finished a ton of audiobooks but finishing something is not the same thing as remembering and applying it later. My attention was fragmented between navigating rush hour traffic and listening to [The Subtle Art of Not Giving a F*ck](https://www.amazon.com/Subtle-Art-Not-Giving-Counterintuitive/dp/B01I29Y344/ref=zg_bs_2402172011_8?_encoding=UTF8&psc=1&refRID=KRH217AQ19N6Y9VSKYTP).

I remembered that it was a good book. But if you asked me later about the specifics of the book and how it affected me, I would stare at you blankly. This is because between cursing out at some assholes who cut me on the high way and people who do not let me merge in even though it’s the end of the merging lane, I could not properly pay attention to the audiobook.

In contrast to this, when I sat down to read [Deep Work](https://www.amazon.com/Deep-Work-Focused-Success-Distracted-ebook/dp/B00X47ZVXM/ref=sr_1_1?ie=UTF8&qid=1538059544&sr=8-1&keywords=deep+work), I would carefully read through it. I made mental notes to myself about different ways to improve my quality of work. I reflect on what the author wrote to my own experience of shallow work. It was a completely different experience. Even though my level of work is nowhere near deep yet, I can confidently say that I try to apply what I’ve read to my own work regularly.

## Attention Leaks Are common

This brings me to another point I want to talk about, attention leaks. I’m guilty of having a long to do list because sometimes that’s just how I could remember to do things. Some of the things on my list include schedule a doctor appointment and filing sales tax for my business. However, because those tasks are not urgent, I tend to push them back until I absolutely have to do them. But as the list grows longer without me taking care of them, it starts to consume my attention more and more.

Every time I put a task down on my to do list, that’s the equivalent of allocating some attention to it. The issue is that some tasks are never truly finished. I have to to file my quarterly taxes to the IRS and sales tax with my state every four months. A recurring task like that is terrible for attention management. It’s always at the back of my mind and it saps away my attention from other things. Other tasks, such as going to the doctor, require multiple steps. I need to pick a date and time. Then because it’s more than six months since my last visit, there will be blood work. I’ll need to remember not to eat anything the night before.

You see where I’m going with this. Attention leaks are sometimes unavoidable while we’re going through our daily lives. Some tasks have inherent costs associated with them. While I would like to have a tool like `valgrind` to check for the leaks in my attention, it has yet to be built.

## Filter Each task

The second best thing we can do is be very intentional about what tasks we want to focus on. One thing I learned about software application security is that you cannot trust any input. Not even from yourself. I tend to just put down whatever tasks were thrown at me before. But as I talked about earlier, it caused attention problem for me down the road. The best way I prevented my attention from being a fragmented mess was to filter the tasks before I commit serious attention to them.

While it takes me a bit longer to process each task rather than just throwing it onto the to do pile, it helps me with prioritization. I try to break down complicated tasks so I don’t start having a panic attack by merely glancing at the monstrosity. I picked up this technique from programming and it helped me with my daily lives. While the approach I use to filter the tasks is still experimental at best, it gave my attention some much-needed relief. Instead of having a few dozen things clamoring for my attention at once, the important tasks are processed first.
