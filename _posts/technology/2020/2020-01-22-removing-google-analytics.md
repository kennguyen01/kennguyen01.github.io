---
title: Removing Google Analytics
date: 2020-01-22
categories: technology
---

Since I first started this blog, I used Google Analytics to track the traffic. Back then, it seemed to be the standard way to track how my blog is doing. I seldomly checked my traffic since this blog is mostly a way for me to document my progress. A few months back I started to use [Cloudflare](https://www.cloudflare.com/) to help me manage my DNS and reduce load times. Then I found out something interesting from Cloudflare. Since Cloudflare sits between the client and my site, it's able to capture all of the traffic on my site accurately compared to Google Analytics.

<!--more-->

## Huge Difference in Traffic

So this is the traffic for my blog for the past 30 days:

{% include image.html url="https://i.imgur.com/kRubti5.jpg" text="loudflare traffic" %}

Meanwhile, Google Analytics told me that my site received 17 visitors during the same time period. That's 184% difference. If increasing traffic was my primary goal, I would be tearing my hair out wondering why there's only 17 people who dropped by for the whole month. The discrepancy was real so I did some research as to why.

### Blocking Them Ads

I found out the biggest reason is ad blockers. Since my blog is mostly about programming, I assume that my visitors are people who are interested in that topic and have ad blockers installed on their browsers. The most popular ad blockers such as uBlock Origin, the one I use for Firefox, will block Google Analytics. Online privacy is a big deal these days so it's understandable that people don't want Google to track them.

Coming from personal experience, I always leave my ad blockers on at all times. I remember that some sites I stumbled upon have asked me to turn off my ad blocker. In that case, I'd rather use a different site than having to turn it off. Ads are so pervasive these days that turning off my ad blocker is walking outside without socks. I can do it but I don't like feeling the sweat being trapped in my shoes.

Coming from that perspective, it's time for me to let Google Analytics go. I learned that I should be more critical of the tool I use. My visitors don't want want to be tracked by Google and neither am I.
