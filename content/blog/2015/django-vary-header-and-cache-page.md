+++
date = "2015-02-27 22:30:22"
title = "Using the Vary header with the @cache_page decorator"
draft = "false"
categories = ["Technology"]
author = "edavis215"
original_url = "https://ttboj.wordpress.com/2015/02/27/django-vary-header-and-cache-page/"
+++

<strong>Problem</strong>

Earlier today I needed to cache a view with the @cache_page decorator. The output of this view changes depending on whether the user making the request is logged in or not. Pretty standard stuff.

However, I quickly discovered that @cache_page was caching both authenticated and anonymous requests under the same cache key. This led to the cache serving either the authenticated or anonymous version of the page, whichever was cached first. Not good.

I eventually found this <a href="http://www.technomancy.org/python/django-cache_page-useless/">blog post</a> and this <a href="https://code.djangoproject.com/ticket/15855">Django ticket</a> and between the two figured it out.

<strong>Solution</strong>

In short, @cache_page created the same cache key for both authenticated and anonymous versions because a Vary header hadn't been set yet on the response. If the <code>Vary: Cookie</code> HTTP header had been set, the cache key would have changed depending on the value of the Cookie header and everything would have worked just fine.

The cleanest fix I could find is to use two decorators. First is to wrap the real view function with @vary_on_cookie (to set the <code>Vary: Cookie</code> header) and then wrap that function with @cache_page (to actually cache the page). Like so:
```
<code>@cache_page(60*60)
@vary_on_cookie
def expensive_func(request):
    # ...
</code>
```
After doing this, everything worked.

