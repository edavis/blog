---
title: "Set the cache key for nginx’s uwsgi caching"
date: 2016-02-14
---

Add `uwsgi_cache_key "$request_method $scheme://$host$request_uri"` to the nginx config.

By default, “uwsgi_cache_key” is an empty string. This leads to the
first cachable response being delivered for all future requests
(because the same key is always used).

With this, cache each response under a key like: “GET http://example.com/about/?p=1​"

(I like this style because it mirrors what a proper HTTP request looks like.)
