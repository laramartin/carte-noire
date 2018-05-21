---
layout:     post
title:      Why I added licenses to my Udacity projects
date:       2017-11-07 00:00
author:     Lara Martín
summary:    And the problem with plagiarism
categories: programming
tags:
  - Android
  - Android Dev
  - Software Development
  - Android App Dev
---


I use GitHub to host my repositories including [all the projects I did for the Udacity Android Nanodegrees](https://medium.com/udacity/a-year-of-android-ffba9f3e40b6). This helps me to organise them, check in the future how I implemented things and most importantly **personal visibility**.

I used GitHub as my Android portfolio. In each repository I added a README file describing the project, the Android goodies it contained and also added some screenshots of the final app.

## The problem

One of the most popular repos I have is a project I did for Udacity's Android Basics Nanodegree, that consisted in building an [Inventory App](https://github.com/laramartin/android_inventory). This project required creating a simple app using a local SQLite Database, cursors, a ListView and some permissions.

Since I uploaded it to GitHub it started to get forked frequently (even got some stars! ⭐). I realised that most of the people that forked it, deleted it afterwards. This means that maybe it wasn't what they expected, right? Well, I noticed that some people forked it and later deleted my name, uploading my same project (sometimes without even changing the name!) on a new repo. This is the same as downloading the repo to your local machine and uploading it to your GitHub, **removing all git history and any trace of my authorship**.

> […] some people forked it and later deleted my name, uploading my same project […] on a new repo.


At this point I was curious about this fact and started checking periodically the traffic of my repositories. Unfortunately GitHub only displays analytics for the last 14 days, but as far as I've seen, the average number of unique visitors is 150 every 2 weeks. I find it a lot for a project like this!

However I’m not getting only visitors, but also clones. An average of 5 clones every 2 weeks.

![My Android Inventory App GitHub traffic](https://raw.githubusercontent.com/laramartin/laramartin.github.io/master/assets/posts_art/2017-11-07-udacity-licenses/visitors.png)
![My Android Inventory App GitHub clones](https://raw.githubusercontent.com/laramartin/laramartin.github.io/master/assets/posts_art/2017-11-07-udacity-licenses/clones.png)



The real problem comes when people just copy-paste all the project content or just change my name to submit it to Udacity as their own work. When you enroll in a Udacity Nanodegree you have to agree on the [**Udacity Honor Code**](https://udacity.zendesk.com/hc/en-us/articles/210667103-What-is-the-Udacity-Honor-Code-), that states that you are submitting your own work. Therefore breaking this can end in getting you expelled from a program without refund.


## So why use GitHub for your Udacity projects then?

First of all, **Udacity encourages you to upload your projects to GitHub**, as this will help you to build your portfolio. During the Android Nanodegrees I took, Udacity suggested to use GitHub, also referring to their course ["How to Use Git and GitHub"](https://www.udacity.com/course/how-to-use-git-and-github--ud775). There are two ways of submitting a project, either linking your GitHub repository or uploading a ZIP file.

Secondly, uploading my Udacity projects to GitHub is my portfolio and **gives me visibility to potential employers**. If you google "Udacity inventory app" you will probably see my project as one of the first results.

Furthermore **it helps students**: Having a guidance helps them to get unstuck. And how do I know? I got some messages from students thanking me for my repos as they helped them. Only a few, but it always makes my day! 😍

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Today someone wrote me to thank me for my GitHub projects from the Android Nanodegree. Made my day! 😍❤️ <a href="https://t.co/VImYK2PaXq">pic.twitter.com/VImYK2PaXq</a></p>&mdash; Lara Martín (@lariki) <a href="https://twitter.com/lariki/status/890557312766758912?ref_src=twsrc%5Etfw">July 27, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>



## The license

As I want to keep these repos public to showcase my work and potentially help others, I figured out that adding a license could help to warn about the plagiarism issue.

The license I add is the MIT license plus some personal words about Udacity Honor Code:

<script src="https://gist.github.com/laramartin/7796d730bba8cf689f628d9b011e91d8.js"></script>


I added this license to the README files and in all project files. Thankfully Android Studio helps you with it, let me explain how to achieve this.

## Adding a license to all files with Android Studio

To add a license to your project, first you need to create a template with the text. Go to *Preferences -> Editor -> Copyright -> Copyright Profiles*. Here add a new profile, give it a name and paste your license.

![Creating a copyright profile](https://raw.githubusercontent.com/laramartin/laramartin.github.io/master/assets/posts_art/2017-11-07-udacity-licenses/add_license.gif)

Once you have a copyright profile you want to use, you can add it to a specific file you want or to all:

1. Add it as your default project copyright: *Preferences -> Editor -> Copyright -> select the desired copyright file*
2. Update the copyright: *select the file(s) you want to add the license to -> right click -> Update copyright*. There is also a shortcut when adding a copyright in a single file, just use `cmd + N` in mac or `Alt + Insert` for Windows.

![Adding a copyright to a project](https://raw.githubusercontent.com/laramartin/laramartin.github.io/master/assets/posts_art/2017-11-07-udacity-licenses/update_copyright.gif)

and done!

Now with these licenses I feel I have warned the students enough about the dangers of plagiarism. Nevertheless, I hope my repos help you to progress in your learning! 💚

[Originally posted in my medium blog.](https://medium.com/@laramartin/why-i-added-licenses-to-my-udacity-projects-3070f602006e)
