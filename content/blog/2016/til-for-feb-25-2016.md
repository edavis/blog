+++
date = "2016-02-25 17:00:04"
title = "TIL for February 25, 2016"
draft = "false"
categories = ["Technology"]
author = "edavis215"
original_url = "https://ttboj.wordpress.com/2016/02/25/til-for-feb-25-2016/"
+++

<h3>Disable SSL for a given host in lftp</h3>
Add "set ftp:ssl-allow/&lt;host&gt; false" to ~/.lftprc.

I had a client's FTP server that was redirecting me to FTP-SSL after the initial connection was made, but there was some mismatch on the certificates so lftp would error out. This setting prevents the redirection from happening.
<h3>Hide untracked files in Git status output</h3>
Use "git status -uno" or "git config status.showUntrackedFiles no".

I'm trying out a technique of only tracking the active theme files in Git and not touching anything else. This left me with tons of untracked files (other themes, uploads, plugins, core files, etc). Instead of fiddling with .gitignore (what I usually do), I'm keeping all of that untracked and just hiding it.
<h3>Set the cache key for nginx's uwsgi caching</h3>
Add 'uwsgi_cache_key "$request_method $scheme://$host$request_uri"' to the nginx config.

By default, "uwsgi_cache_key" is an empty string. This leads to the first cachable response being delivered for all future requests (because the same key is always used).

With this, cache each response under a key like: "GET http://example.com/about/?p=1​"

(I like this style because it mirrors what a proper HTTP request looks like.)

(h/t to <a href="http://cagrimmett.com/til/">Chuck Grimmett</a> for the style and format of this TIL post)

