---
title: Scraping for Jobs on Indeed
date: 2020-03-17
categories: programming
---

A couple months back I started applying for jobs on Indeed. I expected the process to be slow. Pretty much everyone understood that applying online is one of the worst ways to find a job. But I wasn't as discouraged because I wasn't desperate to find a job right away. After applying to a dozen jobs or so on Indeed, I realized that I much prefer having all of these jobs in a CSV file for easy organization. Since Indeed is a well known company, I thought they would have an easy to use API for people to use. Unfortunately, that feature is only available to Indeed publishers.

<!--more-->

To become one, I would need to complete the application to become a publisher:

<p align="center">
  <img src="https://i.imgur.com/XhwF1Of.jpg" alt="Indeed Publisher Application">
</p>

I doubt my application would be approved because I only intend to use the API for myself. So I did the next best thing, I wrote a program to scrape job postings and export all the data to a CSV file: 

[Job Applications Backlog](https://github.com/kennguyen01/job-applications-backlog)

I told my friend about the program and he said he wanted to try it out. Since he doesn't write any code, I wrote a very detailed installation instructions for him on how to install and run Python programs on Windows.

The program is not fully tested yet but it does what it's supposed to do, mostly. I added some delays during the scraping process to avoid overloading the site. The links for the job postings are shortened so they can fit nicely within the data cell. The only downside is that there is no option to add new jobs to a CSV already existed. Maybe I'll add that feature in the future.