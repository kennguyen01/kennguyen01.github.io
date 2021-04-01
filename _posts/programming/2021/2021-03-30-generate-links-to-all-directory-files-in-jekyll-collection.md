---
title: Generate Links to All Directory Files in Jekyll Collection
date: 2021-03-30
categories: programming
---

I faced some limitations on Github Pages when I wanted to link all files inside a directory with Jekyll. Jekyll is a decent static site generator if you want to create a blog. Anything more complicated than that require messing around JavaScript and Liquid template language. This hack is meant for Jekyll sites that use collections instead of posts.

<!--more-->

## Collection Directory

My collection is called `_notes`. For Jekyll to recognize a collection, it's need to be included in `_config.yml`:

```yml
include: ["_notes"]

collections:
  notes:
    output: true
  
defaults:
  - scope:
      path: "_notes"
    values:
      layout: note
```

The configuration above tells Jekyll to include the collection directory when generating the site. HTML outputs are created from the markdown files inside the collection. 

### Tagging Files

To categorize each markdown file, include a `tag` variable in the front matter. This tag will be used later to grab similar documents. I had a directory for the book *Peak* so I made a tag with the same title at the top of the markdown file:

```
---
layout: note
title: The Power of Purposeful Practice
tag: Peak
---
```

### Grabbing URL

I created `links.html` inside the `_includes` directory with the following Liquid code:

```
{% raw %}
{% for doc in site.pages %}
  {% if doc.tag == include.tag %}
    {{ doc.url | split: "/" | last }}
    {{ doc.title }}
  {% endif %}
{% endfor %}
{% endraw %}
```

The code above grabs all the documents that have the same tag. Since Jekyll outputs an HTML file for each document, there is a URL to each one of them. Using the same example earlier, the URL to that example is: `/notes/peak/the-power-of-purposeful-practice.html`. I am only interested in the relative link of that URL so I split the string at the forward slash and grab the last part of the URL.

### Includes Links

My directory tree looks similar to this:

```
├── _config.yml
├── _includes
│   └── links.html
└── notes
    └── peak
        └── the-power-of-purposeful-practice.md
```

The last thing I need to do is going back to the markdown file and include `links.html` to where I want to display the links. I pass the front matter tag to the `include` statement. 

```
{% raw %}
{% include links.html tag=page.tag %}
{% endraw %}
```

Now your document will show links to the documents that share the same tag inside that directory.