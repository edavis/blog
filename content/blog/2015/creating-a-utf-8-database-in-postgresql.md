+++
date = "2015-02-06 09:04:56"
title = "Creating a UTF-8 database in PostgreSQL"
draft = "false"
categories = ["Technology"]
author = "edavis215"
original_url = "https://ttboj.wordpress.com/2015/02/06/creating-a-utf-8-database-in-postgresql/"
+++

<p>I always forget the proper incantation for creating UTF-8 databases in PostgreSQL. I just had to do this for a project so I'm writing it down for future reference. Maybe it'll be useful to somebody else out there.</p>
```
<code>sudo -u postgres createdb -E UTF8 -T template0 --locale=en_US.utf8 template_utf8</code>
```
<p>Now use this UTF-8 "template database" when creating your project database:</p>
```
<code>createdb -T template_utf8 new_database</code>
```

