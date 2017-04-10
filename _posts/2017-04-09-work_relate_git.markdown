---
layout: post
title:  "Git related"
date:   2017-04-09 +0800
categories: work
---

# Git operation I encount in work

When we work in group we can't avoid cooperate with each other. Today I want to show something that I do not know previously.

## Change the mode of file

When we want to change the mode of the file in git project. The mode will not change if you just chmod locally. We need to use update-index command to change the file. If we want to make the file not excutable, we can use following command.

```
 git update-index --chmod=-x yourcode.py

```

## Just test with one branch

In my work, everyone has his own git repo. When we want to do modify, we create our own branch. After we finish local test, we commit code to our local branch and merge the code to master. After we do merge request, others will go code review and accept our request. Because we use ElectricFlow as Devops tool, I need to test my code on it. The command to only test application on my branch is as follow.

```
 ssh://git@bitbucket.ss.com/test.git -b [your branch] --single-branch

```

Continue...





