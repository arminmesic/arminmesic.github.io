---
layout: post
title:  "Change the latest commit message"
date:   2015-02-10
tag: [til, git]
---

You're in a hurry and made a commit message but you realized later on you've forgotten something or you made 
a type, how to fix it:

This will open an editor where you can enter a new message:

`git commit --amend` 

This will instantly update the latest message without editor:

`git commit --amend -m "This is the new message"`
