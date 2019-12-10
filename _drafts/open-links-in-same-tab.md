---
title: Open Links in Same Tab
date:
categories: web-development
---

In all my posts, the attribute I always put in a new link is `target="_blank"`. Ever since I learned that you can open a link in a new tab, I defaulted to that behavior. I never thought about how I'm forcing my users to do things the way I wanted instead of leaving the choice to them. Personally I tend to hold the `Ctrl` button when I click on the new link so I don't lose track of what I'm current reading. While that's something that I preferred, that is not the default option that browsers enforce. 

<!--more-->

## Breaking Built-In Functionality

All browsers have the Back button. By opening in a new tab with each link, I break a functionality that many people are used to. I did not think about how users with screen readers access the site. If someone is going through an article with links in them and it opens in a new tab, that presents an additional obstacle to accessibility. By using an additional tab on a browser, it will also consumes additional resources. If the link opens in the same tab, the users can browse what they want to see and go back to the previous article. The browser should have already cached the content and it will load quickly.

By implementing what I think the users are supposed to do, I break a vital functionality that all browsers have.

## Task Switching Slowdown

Another problem I did not think about was the cost of switching from one tab to another. There's a slight pause for the brain to process new information when it views the new tab. After the information in the new tab is viewed, the act of closing it and go back to the previous tab causes another pause. While the pauses are minute, they present additional burden on processing the information. I'm not saying that opening the link in the same tab does not cause a task switch, but it gives the users the choice.

By defaulting to opening in the same tab, the users have the choice whether they want to see it in a new tab or not. If they find the information in the first article interesting enough, they can choose to either `Ctrl + Click` or right click and select `Open Link in New Tab` and continue reading the first article before moving on to the second. By robbing them of that choice, I'm being selfish because I'm afraid the users will just go away and never come back to my site.

While that's a real possibility that users will disappear into the ether of never ending links, I have to consider what's the best option for all users. That's why I'm going to remove all `target="_blank"` in all my links now.