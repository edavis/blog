+++
date = "2016-02-22 11:26:29"
title = "WordPress Desktop App on OSX 10.8"
draft = "false"
categories = ["Technology"]
author = "edavis215"
original_url = "https://ttboj.wordpress.com/2016/02/22/wordpress-desktop-app-on-osx-10-8/"
+++

Last week, WordPress rolled out an update to their desktop app. Come to find out, this updated version (1.2.7) only works on OSX 10.9 and above. As a result, the update broke the app on my OSX 10.8 box. Seems like this fact should have been advertised beforehand or not even displayed to people running OSX 10.8 and below.

So I decided this morning I wanted to get the app back up and running. Head to the desktop download site, but doesn't have any downloads for previous versions. Nothing in the FAQ or support sections that I could find. Nothing in the Github repository.

Start poking around the source of the download site to see if I can see how the files are being delivered (and maybe figure out if there is a URL scheme I can manipulate to get an old version) but no dice.

Finally, I figure I probably still have the old (1.2.5) version in my Trash and sure enough I do. So I pull it out of the trash, replace 1.2.7 with 1.2.5, and everything picks right back up.

I'm sure the app will try to get me to upgrade to 1.2.7 every so often, but I'll just have to remember to click no.

As a public service to anybody else hit by this issue, here is the DMG of version 1.2.5: <a href="http://files.davising.com.s3.amazonaws.com/2016/02/22/wordpress-com-installer-1-2-5.dmg">wordpress-com-installer-1.2.5.dmg</a>.

Update (2016-02-25): The desktop app somehow got auto-updated and broke again. Updating this via wordpress.com now. Not going through all this again. YMMV.

