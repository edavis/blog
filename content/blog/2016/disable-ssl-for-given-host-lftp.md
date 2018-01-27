---
title: "Disable SSL for a given host in lftp"
date: 2016-02-01
---

Add `set ftp:ssl-allow/<host> false` in ~/.lftprc.

I had a client’s FTP server that was redirecting me to FTP-SSL after
the initial connection was made, but there was some mismatch on the
certificates so lftp would error out. This setting prevents the
redirection from happening.
