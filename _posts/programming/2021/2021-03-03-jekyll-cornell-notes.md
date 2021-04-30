---
title: Jekyll Cornell Notes
date: 2021-03-03
categories: programming
---

![Jekyll Cornell Notes](https://i.imgur.com/Chu2ow7.jpg)

I wrote a [flashcards generator](https://raisingexceptions.com/programming/jekyll-flashcards-generator.html) a few months back. I used it a lot when I was studying for the Food Manager exam. Flashcards are very useful when there are a lot of facts to memorize, but it's not as effective if the topic has concepts to be understood rather than memorized. I noticed this when I read self-help books. The lessons in these books are helpful but they fade over time if I don't review them. When I want to find a specific concept but don't remember where it is in the book, it can be time-consuming to find it. 

The Cornell notes system is great for organizing this type of information. I combined the system with the interactivity of JavaScript for my project.

Link to project: [Jekyll Cornell Notes](https://github.com/kennguyen01/jekyll-cornell-notes)

<!--more-->

## Interactive Notes

There are three features that I wanted with my Cornell notes as I built it: collapsible sections, internal anchors, and links to similar notes.

With a regular Cornell notes, the paper is divided into 3 sections: ideas, notes, and summary.

![Cornell Notes](https://i.imgur.com/g6foUwA.png)

First, making the ideas and summary sections collapsible, I can choose to read the notes alone. Sometimes I prefer to do this so I can get a holistic understanding of the concepts and examples.

Second, the ideas section help with recalling the important concepts. But if I've forgotten what the ideas were about, I need to find it in the notes. Turning headers and ideas into internal links allow me to quickly jump to that specific point.

![Collapsible Sections](https://i.imgur.com/rpzRb9s.png)

Lastly, reviewing multiple notes in the same topic means shuffling through pages of paper. Having a menu of similar notes makes it simpler to find exactly what I need from that list. 