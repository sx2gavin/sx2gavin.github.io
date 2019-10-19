# sx2gavin.github.io Github page
This repository is the github page for sx2gavin.github.io, AKA Gavin's portfolio. This website is written using Jekyll static website framework.

## How to Test This Offline
If you would like to test this offline, run the following command in bash:
```
bundle exec jekyll serve
```
This will start the Jekyll server on `http://localhost:4000`.

You can modify anything and see the changes in real time in your browser.

## How to Add a New Post
To add a new post, go to `_posts` folder and create a new file and name it with the following template:
```
year-month-day-title-separate-with-dash.md
```
For example: 2019-10-13-how-to-add-images.md

Once you've created this file, add a front matter header at the top of the file, something like this:
```
---
layout: post
title:  "How to Add Images"
date:   2019-10-13 20:45:00 -0500
categories: [jekyll]
---
```
Remember to update all the necessary fields.

After that, you can start writing the content of the blog post. Once you are done, save the file and see the change in the browser.