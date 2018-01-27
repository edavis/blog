---
title: "Understanding the WordPress Homepage Template Hierarchy"
date: 2016-01-29
---

I've spent a few hours trying to wrap my head around how WordPress
determines which template to use depending on which "Front page
displays" option has been set. I'm writing this as the guide I wish
existed when I was looking into this.

If "Front page displays" is set to "Your latest posts," WordPress will
use front-page.php to render your homepage if the file exists. If
front-page.php doesn't exist, WordPress will use home.php with a
fallback to index.php.

If "Front page displays" is set to "A static page," you'll also have
to set which pages to use for "Front page" and "Posts page."

For "Front page," WordPress will use front-page.php to render the page
if the file exists. If front-page.php doesn't exist, WordPress will
use the standard Page template hierarchy (<em>i.e.,</em> custom page
template, page-slug.php, page-id.php, page.php, index.php).

For "Posts page," WordPress will only ever look to home.php with a
fallback to index.php. The existence (or non-existence) of
front-page.php doesn't affect anything here.

In a nutshell, front-page.php can be used to render either a list of
posts ("Your latest posts") or a static page ("A static page -&gt;
Front page") depending on the site settings.

Refs:
<ul>
	<li><a href="https://make.wordpress.org/themes/2014/06/28/correct-handling-of-static-front-page-and-custom-blog-posts-index-template/">https://make.wordpress.org/themes/2014/06/28/correct-handling-of-static-front-page-and-custom-blog-posts-index-template/</a></li>
	<li><a href="https://developer.wordpress.org/themes/basics/template-hierarchy/">https://developer.wordpress.org/themes/basics/template-hierarchy/</a></li>
	<li><a href="http://wphierarchy.com/">http://wphierarchy.com/</a></li>
</ul>
