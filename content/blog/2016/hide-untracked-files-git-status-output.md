---
title: "Hide untracked files in Git status output"
date: 2016-02-09
---

Use `git status -uno` or `git config status.showUntrackedFiles no`.

I’m trying out a technique of only tracking the active theme files in
Git and not touching anything else. This left me with tons of
untracked files (other themes, uploads, plugins, core files,
etc). Instead of fiddling with .gitignore (what I usually do), I’m
keeping all of that untracked and just hiding it.
