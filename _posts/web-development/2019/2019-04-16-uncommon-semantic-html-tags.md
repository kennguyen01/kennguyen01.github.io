---
title: Uncommon Semantic HTML Tags
date: 2019-04-16
categories: web-development
---

I've been using HTML for a while now to build websites but every now and then, I learn something new about the language. There are a lot of different tags in HTML, some provide the structure of the page while others provide the meaning to it. With HTML5, there's some new semantic markup that I learned and want to share in this post.

<!--more-->

## Quotations

Usually with quotations, I tend to use `<blockquote>` as the default element for them. But there's also the `<q>` element for short quotes. It will put the quotation marks around the quote instead of you having to type it out.

```html
<p>Colin Powell said, <q>There are no secrets to success. It is the result of preparation, hard work, and learning from failure.</q></p>
```

I will wrap the output of the examples in `<blockquote>` so they are clearly separated and visible.

<blockquote>
    <p>Colin Powell said, <q>There are no secrets to success. It is the result of preparation, hard work, and learning from failure.</q></p>
</blockquote>

I can see how it's not being used often. Instead of typing out `<q>` and `</q>`, I can just type out the double quotes `""`. There's less keystrokes and it's much easier to remember.

## Abbreviations and Acronyms

The elements used for abbreviations and acronyms are `<abbr>` and `<acronym>`, respectively. They give the user the full version of the term when hovered. Of course you need to define the full term with the `title` attribute inside those elements. Otherwise they will just appear as normal text.

```html
<p>I live in <abbr title="Maryland">MD</abbr> and went to <acronym title="University of Maryland">UMD.</acronym></p>
```

<blockquote>
    <p>I live in <abbr title="Maryland">MD</abbr> and went to <acronym title="University of Maryland">UMD.</acronym></p>
</blockquote>

## Citations and Definitions

I did not know that you could `<cite>` a book with HTML. When I think of citing something, I think of the long citation in either <acronym title="American Psychological Association">APA</acronym> or <acronym title="Modern Language Association">MLA</acronym> format. But citing in HTML simply means that you are referencing a book or research paper.

```html
<p><cite>Hyperion</cite> by Dan Simmons was one of the best science fiction books I've read.</p>
```

<blockquote>
    <p><cite>Hyperion</cite> by Dan Simmons was one of the best science fiction books I've read.</p>
</blockquote>

If you want to define a new term that's not clear to the user, you can use the `<dfn>` element to specify the defining instance of it. This is only done on the first time you used the term. In Firefox, the defined term appears Italic but it varies based on browser.

```html
<p><dfn>Cryptocurrency</dfn> is a digital currency in which encryption techniques are used to regulate the generation of units of currency and verify the transfer of funds, operating independently of a central bank.</p>
```

<blockquote>
    <p><dfn>Cryptocurrency</dfn> is a digital currency in which encryption techniques are used to regulate the generation of units of currency and verify the transfer of funds, operating independently of a central bank.</p>
</blockquote>

## Address

The `<address>` element means exactly that, it contains the contact details of the author of the page. It may contain physical address, phone number, or email address. This element is usually used together with <dfn>hCard</dfn>, a microformat used for publishing people, companies, and organizations on the web.

```html
<address class="vcard">
    <span class="url fn org" href="https://about.google/intl/en/">Google LLC</span>
    <br />
    <span class="adr">
        <span class="street-address">1600 Amphitheatre Pkwy</span>
        <br />
        <span class="locality">Mountain View</span>,
        <span class="region" title="California">CA</span>,
        <span class="postal-code">94043</span>
    </span>
</address>
```

<blockquote>
<address class="vcard">
    <span class="url fn org" href="https://about.google/intl/en/">Google LLC</span>
    <br />
    <span class="adr">
        <span class="street-address">1600 Amphitheatre Pkwy</span>
        <br />
        <span class="locality">Mountain View</span>,
        <span class="region" title="California">CA</span>,
        <span class="postal-code">94043</span>
    </span>
</address>
</blockquote>

While this seems like a lot of code to type out, it's the semantically correct way to provide contact information to the user for the page.

These are some of the semantic elements that I do not use regularly. I will start to incorporate these elements into my code as I work on different projects so I can make it clear to browsers and search engines the meaning of my pages.
