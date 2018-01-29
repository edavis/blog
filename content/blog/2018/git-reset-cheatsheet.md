---
title: "git reset for the impatient"
date: 2018-01-29T14:33:19-08:00
---

A cheatsheet for what `git reset` does in each mode of operation.

----

`git reset --hard <commit>`

Current branch, index, and working directory set to the tree of `<commit>`.

`git reset [--mixed] <commit>`

Current branch and index set to the tree of `<commit>`. Working
directory not modified.

`git reset --soft <commit>`

Current branch set to the tree of `<commit>`. Index and working
directory not modified.
