+++
date = "2014-09-21 11:47:00"
title = "A polyglot guide to package management"
draft = "false"
categories = ["Technology"]
author = "edavis215"
original_url = "https://ttboj.wordpress.com/2014/09/21/a-polyglot-guide-to-package-management/"
+++

Here's something I would love to see: An online guide that explained everything you need to know about installing packages using a particular language's package manager.

I use Python's package manager, pip, on a near-daily basis. I know that even if a package author doesn't mention virtualenv in the docs, I can quickly create one and install the package there to keep things separate if I want to. And if a package author <i>does</i> mention virtualenv, I'll understand the purpose of that step. If something breaks, I know enough about distutils/setuptools to (usually) fix it.

Anybody who develops in a given language eventually learns the ins-and-outs of the language's package infrastructure. None of this is unique to me or to Python. Ruby, Node, and Go developers all learn the same things.

But when it comes to installing packages in other languages, I don't have any of that accumulated knowledge. I don't know which versions to avoid. I don't know if the docs I'm following are years out of date and the language recommends an entirely new approach to installing packages. I don't know if that "sudo" is a requirement or if the package author didn't know any better.

At any given stage in the installation process I have basically no idea what is happening. I'll usually start by following the docs and hope everything just works. And even when it does work, I don't know where these files ended up. I don't know if they'll conflict with other packages in the future. What happens if another package I install requires a different version of an already installed dependency? Will the first package stop working?

If there <i>is</i> a problem during installation, my options are going through the official docs or hoping somebody has 1) encountered the same problem and 2) documented online how to fix it. But, more often than not, I'll just move on and try finding a package in a language I already know.

That's why I think some sort of comprehensive guide maintained at a single location would be great. Any package author using any programming language could link to the guide in their installation instructions and then continue on with the project-specific installation instructions. No more duplication of "here's how to install virtualenv" or "here's the difference between <code>npm install -g</code> and <code>npm install</code>" among thousands of different projects.

