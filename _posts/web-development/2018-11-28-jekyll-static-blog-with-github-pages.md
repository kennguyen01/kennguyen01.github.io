---
title: Jekyll Static Blog with Github Pages
date: 2018-11-28
categories: web-development
---

For the past couple weeks I've been looking for a new host for my websites. My hosting plan with NameCheap expired last week so I've been shopping around to find a better host. Initially I considered renewing the hosting plan again since it's only $38.88 per year, plus $8.88 for the SSL certificate, and $13.16 for the domain name. But I decided against it because if I just renew my hosting plan, I would just end up using WordPress again. There's nothing wrong with using WordPress but I would not learn anything new from it.

<!--more-->

## Cheap Hosting and Github Pages

I scoured the web to find another hosting plan. There are so many different web hosting services at vastly different price points. I didn't know which one to pick so I went on Reddit to ask for advice. One person recommended [BuyShared](https://buyshared.net/shared-cpanel-hosting/) for website with little traffic. I went and check it out. To my surprise, the cheapest plan is only $5 per year. I was blown away by that price. On top of that, they also offered free SSL using [Let's Encrypt](https://letsencrypt.org/). Naturally, I purchased it right away and used it for my business website.

The set up was a breeze since I already had a backup of my site in WordPress. Setting up the SSL was just one click. The only thing that took time was waiting for my DNS to propagate from NameCheap to the nameservers of BuyShared. After 24 hours, my business site was up and running on the new host. Once that was done, I went on to find a place to host my blog. I knew I wouldn't use WordPress for it so the only logical choice was a static website. And if it's a static website, the best place for it would be [Github Pages](https://pages.github.com/).

## Jekyll Static Site Generator

When creating a new repository on Github, there's an option to turn that repo into a simple website by naming it `username.github.io`. The only caveat is that you would need to know some HTML/CSS and JavaScript to modify the site. However, other developers have already created a tool called [Jekyll](https://jekyllrb.com/) to generate the site for you. The documentation for Jekyll is straightforward so I just followed it to install Ruby development environment on Ubuntu.

{% highlight shell %}
sudo apt install ruby-full build-essential

echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME=$HOME/gems' >> ~/.bashrc
echo 'export PATH=$HOME/gems/bin:$PATH' >> ~/.bashrc
source ~/.bashrc

gem install jekyll bundler

jekyll new my_blog
{% endhighlight %}

The default theme for a new Jekyll site is Minima. Of course you can always change it to something else. Github supported a bunch of different [themes](https://pages.github.com/themes/). At first I thought I would need to also learn Ruby to modify my site but Jekyll uses [Liquid](https://shopify.github.io/liquid/) templating language, which looks just like Jinja2 for Flask. Since I already knew Jinja2, that made it very simple for me to bring all my posts and code snippets over.

## Github A Records and HTTPS

Github supports custom domain name, you just go to the **Settings** of the repo and scroll down to where it says **GitHub Pages**. I changed the custom domain to my own domain name. That automatically created a CNAME file in my repo. But the domain name still doesn't point to Github yet. To do that, I need to configure the [A records](https://help.github.com/articles/setting-up-an-apex-domain/#configuring-a-records-with-your-dns-provider) with my NameCheap domain.

![Namecheap A records](/images/namecheap-a-records.jpg)

A free SSL certificate is also provided by Github. I had to wait for some time while the certificate is being issued. After that's done, I just click on **Enforce HTTPS**.

![Github pages settings](/images/github-pages-settings.jpg)

## A Huge Saving

Finally, my static blog is hosted on Github for free. There's a bit of work involved with setting it up but it was a good learning experience for me. The blog is still a work in progress since I need to figure out how to enable pagination. My blog currently display all my posts on one page but that's something I can work on later.

I also saved a lot of space with this. The WordPress backup I had for the old blog was 98.6MB while the size of the new repo is only 1.1 MB. And the images actually took up 941KB of the total space. Once I use an image hosting service like imgur to host all my images, the total size of my current blog would only be 159KB. I literally just saved 99.8% of the used space by switching over to a static blog. Overall, I'm very happy with the new blog.
