---
title: "How to fix \"SSLRead() return error -9806\" in WordPress"
date: 2018-04-25T08:37:37-07:00
---

**tl;dr:** Use HTTP/1.1 by setting `'httpversion' => '1.1'` inside `wp_remote_get()`.

[At one point in time][old-fix], the suggested fix for this was to recompile
PHP against Homebrew's keg-only version of curl via
`--with-homebrew-curl` but recent versions of PHP in Homebrew no
longer have that option.

[old-fix]: https://gist.github.com/ryanscherler/fea4bb75379c1564df7e027c45615cc9
