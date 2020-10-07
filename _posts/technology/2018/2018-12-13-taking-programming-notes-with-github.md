---
title: Taking Programming Notes with Github
date: 2018-12-13
categories: technology
---

I used to take programming notes with pen and paper. It was helpful in the beginning because it forced me to focus on the code so I can write it down. The drawback is that it's really slow and sometimes the code can go over several pages. Trust me, flipping through pages of code is not fun.

<!--more-->

After I filled up a bunch of notebooks, I believed that it's time for me to go digital. Taking notes by hand is not efficient for me anymore. If I'm on the computer I can easily type in the notes and open a new tab on Firefox to research when I get stuck.

My main criteria for a note taking tool is ease of use and syntax highlighting, everything else is secondary.

## Google Docs and Code Blocks

The first contender to replace my notebook was Google Docs. I've been using Google Docs for a long time so it's only natural that it's the first thing that came to my mind. Google Docs doesn't come with built-in syntax highlighting so I had to install the [Code Blocks](https://chrome.google.com/webstore/detail/code-blocks/ebieibfdjgmmimpldgengceekpfefmfd?hl=en-US) add-on.

Everything was great at first. It does exactly what I needed. I could type in notes and code, then format them later with Code Blocks. The formatting is a bit wonky since I'm putting code inside a word document. But that was not a big deal, the notes are for me anyway so it doesn't need to look perfect.

But the speed became an issue once the notes grew longer. Around 60 pages of notes, it takes at least 10 seconds for Code Blocks to format a block of code. For each section of my notes, I have more than a dozen blocks. At one point I felt like I was waiting longer for Code Blocks to format the code than actually writing them down.

## Notion.so

I didn't feel that Google Docs was a good choice for me moving forward so I looked around for other options. I found [notion.so](https://www.notion.so/). I was excited to try it out because the interface looks very clean. Inside a Notion document, you can type `/` to open up a menu of commands. I scrolled down and it does have code highlighting.

So I started to import all my notes into Notion. But at one point I could not bring in anymore. I suspected it had something to do with my free account. So I read up on the pricing of Notion. For a free account, I only had 1000 blocks of storage. And each block is basically a paragraph of text or a code block.

While I think Notion is an awesome tool. I just didn't feel the need to spend a monthly subscription fee just to be able to take notes. Notion is aimed more toward a team working together rather than just one person take notes for classes.

## Good Old Github

So without any fancy web app to take notes with, I fell back to Github. In my last post I talked about how I used Github Pages to host my blog. I'm actually doing the same thing again with all my notes, albeit in a different way.

The default markup language for Github to display is Markdown. And it comes with simple syntax highlighting too. I'm currently taking notes for JavaScript so what I do to start a block of code is to type in three backticks follow by `js` to tell Github that the highlighted language is JavaScript.

For example, here's the code for problem from Free Code Camp: return the lowest index at which value `num` should be inserted into array `arr` once it has been sorted.

```javascript
function getIndexToIns(arr, num) {
    if (arr) {
        arr.sort((a, b) => a - b);
        for (let i of arr) {
            if (num <= i) {
                return arr.indexOf(i);
            }
        }
        return arr.length;
    }
    return 0;
}
```

When I checked the page that Github generated, it looked great. The notes and code are nicely displayed and highlighted. The only caveat is that I have to type everything in Markdown first but that's not a big deal. Github is an awesome tool and the folks who built it deserve serious kudos.
