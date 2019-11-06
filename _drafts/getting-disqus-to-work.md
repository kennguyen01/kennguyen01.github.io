---
title: Getting Disqus to Work
date:
categories: web-development
---

My blog is chugging along so far but it's still missing a vital component, the comment section. When I was running my blog on WordPress, the feature was already included so I never thought much about it. After migrating over to Jekyll, I noticed the missing comment box at the bottom. It wasn't a big deal for me because barely anyone dropped by my blog anyway.

Now that I have some free time to update my blog more often, it feels incomplete. While my blog is a way for me to write about programming, it's also something I want to share with others. Not having a comment box defeats that purpose. In this post, I will go over the process of adding Disqus.

<!--more-->

## Installing Disqus

Sign up for an account on [Disqus](https://disqus.com/) and you'll be taken to the intent page, choose to install Disqus.

<p align="center">
  <img alt="Disqus intent" src="https://i.imgur.com/0EmMd54.jpg" />
</p>

After entering your site information and receiving a shortname, you'll be taken to the **Plan** page. Ignore the three paid options and scroll down to select the free **Basic** plan. It will then ask you to select the platform your site is currently using. They listed the majority of popular CMS on the page but if you don't find yours, you can install it manually using the button at the bottom.

I'm using Jekyll so the next page gave me instructions on the platform.

<p align="center">
  <img alt="Disqus Jekyll install instructions" src="https://i.imgur.com/wue1bTY.jpg" />
</p>

Open the link for the **Universal Embed Code** in a new tab, we'll get back to it later. Then click on **Configure** and move on to the next page. Here, enter your site full URL along with any information you want to enter and click **Complete Setup**. That's it, you're done with the setup.

## Adding Disqus to Your Site

Of course you're not completely done yet, you still need to actually put Disqus on your site. Remember the tab we opened earlier for the Universal Embed Code? Come back to it now and copy everything inside the box. It should be something like this:

```javascript
<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
  this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
  this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
  var d = document, s = d.createElement('script');
  s.src = 'https://SHORTNAME.disqus.com/embed.js';
  s.setAttribute('data-timestamp', +new Date());
  (d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>    
```
In the second function, you should see the line `s.src = 'https://SHORTNAME.disqus.com/embed.js';`. THe `SHORTNAME` is simply the shortname that Disqus uses to identify you. You don't need to worry about this. If you copied the code directly from Disqus, your shortname is automatically added.

Now create a file named `disqus.html` in your `_includes` folder and paste the code. Now uncomment the `disqus_config` function by deleting the opening and closing `/* */`. In the body of the function, you will see two variables that you need to modify: `PAGE_URL` and `PAGE_IDENTIFIER`. You simply need to change both of them to `'{{ page.url | absolute_url }}'`. Afterward your function should look like this:

```javascript
var disqus_config = function () {
  this.page.url = '{{ page.url | absolute_url }}';
  this.page.identifier = '{{ page.url | absolute_url }}';
};
```

For those who want to know what it means, refer to [Jekyll Variables](https://jekyllrb.com/docs/variables/) and [Jekyll 3.3](https://jekyllrb.com/news/2016/10/06/jekyll-3-3-is-here/). Basically, `page.url` is the URL of the post, while `absolute_url` adds your site's URL to the front of it. This makes sure that Disqus loads the appropriate comment thread for each post.

The last thing you need to do is open your `post.html` inside the `_layouts` directory. You will need to include the file at the end of each post. This is what I have:

```
{% if page.comments != false and jekyll.environment == 'production' %}
  {% include disqus.html %}
{% endif %}
```

The `if` condition is a good way to make sure that you are able to disable the comment section as necessary. You can set `comments: false` in the **front-matter** of a specific post to do that. The environment is set to `production` so Disqus won't load when you are developing the site locally.

## Wrapping Up

Now that I have a working comment system, it feels good. My blog is finally working as intended. Hopefully someone finds this information useful and drop me a comment along the way.
