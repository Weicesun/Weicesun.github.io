---
layout: post
title:  "Git Merge and Linux login Problem"
date:   2017-05-03 +0800
categories: work
---

# Git merge I encount in work

When two person make change to the same file in a project then there will be a merge problem. We need to fix this problem to get our branch to merge to the master.

To avoid conflict we need to first fetch


```
 git fetch origin your_branch_name

```
move to master branch

```
 git checkout master

```

Then we merge the fetched stuff with master branch
```
 git merge FETCH_HEAD

```

Then do git pull

This will show the problem that makes the conflict. We need to fixed the problem manually.

Last but not least:

```
git commit -m "resolving the merge"
git push origin HEAD
```
I do not know the detail but these command saves my day.


## Auto Login Linux

During work there are many worker node. Different components have different function. We need to login to the node to get the information we want however we need to remember so many password when we ssh into the remote machine.

There is a way to help you avoid such problem.

First change directory to .ssh and then use command
```
ssh-keygen -t rsa
```
You will find a file called id_rsa.pub

Copy this file to the remote linux server. When you login that linux you should append the information you have in the pub file to the Linux server's .ssh/authorized_keys

Next time when you want to login you do not need any username or password.






