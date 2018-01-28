---
title: "Perform a conditional redirect with Apache RedirectMap"
date: 2018-01-23
---

[RedirectMap][] is great, but I needed it to perform a redirect only
if the incoming URL was actually in the specified text file. All other
incoming URLs should be passed along and handled as normal.

After some digging and an assist from [StackOverflow][], the key bit
ended up being `RewriteCond`:

```
RewriteCond "${MyRedirectMap:$1|NOT_FOUND}" !NOT_FOUND
RewriteRule ^(.*)$ "${MyRedirectMap:$1}" [R,L]
```

Without `RewriteCond`, every incoming URL is sent to `MyRedirectMap`
which successfully redirects if the URL is found but breaks the site
if the URL is not found.

With `RewriteCond` in place, every incoming URL is first checked for
existence in `MyRedirectMap` and the redirect only occurs if the URL
is found.

[RedirectMap]: https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html
[StackOverflow]: https://stackoverflow.com/a/9266131
