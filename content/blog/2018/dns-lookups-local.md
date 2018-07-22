---
title: "Speed up DNS lookups when using the .local TLD pointing to 127.0.0.1 on macOS"
slug: "speed-up-local-tld-dns-lookups"
date: 2018-07-21T14:33:54-07:00
---

I was using [httpstat][] to test out some nginx changes when I noticed
it was taking over five seconds just to perform the DNS lookup. As the
host I was hitting was running on 127.0.0.1, this seemed crazy to
me. Something like that should be instant as I had mapped the entry in
`/etc/hosts`.

I eventually stumbled upon [this writeup][writeup] which explained
what was going on. Apparently Bonjour intercepts requests for .local
TLDs instead of following configured DNS settings (or, in my case,
`/etc/hosts`).

The fix is to add IPv6 entries alongside the IPv4 entry inside `/etc/hosts`:

```text
::1 example.local
fe80::1%lo0 example.local
127.0.0.1 example.local
```

To keep things simple for myself, I also whipped up a shell function to handle it going forward:

```bash
# ~/.bashrc
addhost() {
  cat <<EOF | sudo tee -a /etc/hosts >/dev/null

# Start of $1
::1 $1
fe80::1%lo0 $1
127.0.0.1 $1
# End of $1
EOF
}

$ addhost example.local
$ tail /etc/hosts
# [... snip ...]

# Start of example.local
::1 example.local
fe80::1%lo0 example.local
127.0.0.1 example.local
# End of example.local
$
```

After making the change, DNS lookups dropped from around 5.5s to about 14ms.

Given that I do *all* of my personal and professional web development
work on localhost mapped to .local TLDs the thought of how much time
I've wasted over the years waiting for these slow DNS lookups is... 😬

[httpstat]: <https://github.com/reorx/httpstat>
[writeup]: <https://www.bram.us/2011/12/12/mamp-pro-slow-name-resolving-with-local-vhosts-in-lion-fix/>
