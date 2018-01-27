+++
date = "2016-02-26 17:00:41"
title = "TIL for February 26, 2016"
draft = "false"
categories = ["Technology"]
author = "edavis215"
original_url = "https://ttboj.wordpress.com/2016/02/26/til-for-feb-26-2016/"
+++

<h3>Enable WordPress maintenance mode</h3>
Create a ".maintenance" file and include the following:

{{< highlight php >}}

<?php $upgrading = 1455233470; ?&gt;
{{< /highlight >}}
Place the file in the root of a WordPress installation.

The number is a UNIX timestamp. If the timestamp is less than 10 minutes ago, the "maintenance mode" screen will be displayed. After 10 minutes, WordPress bypasses maintenance mode and loads the site as normal.

Maintenance mode will also be bypassed if the file exists but is empty.

