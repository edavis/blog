+++
date = "2017-05-07 08:50:26"
title = "How to track traffic in Google Analytics without JS"
draft = "false"
categories = ["Technology"]
author = "edavis215"
original_url = "https://ttboj.wordpress.com/2017/05/07/how-to-track-traffic-in-google-analytics-without-js/"
+++

I've long wanted to hook up the RSS feeds on <a href="https://hnrss.org/">hnrss.org</a> to Google Analytics so I could get a better sense of what kind of traffic the site got. But because the feeds are delivered as XML, I had to figure out a way to do it without JavaScript.

After some poking around yesterday, I finally figured out a way.

Google Analytics has a <a href="https://developers.google.com/analytics/devguides/collection/protocol/v1/">Measurement Protocol API</a> built for this sort of thing. You send a HTTP request (POST and GET both work) with the necessary parameters, and it'll register the hit in your Analytics property.

After testing it out locally using <code>curl</code> and seeing it all work, it was time to integrate with the app.

After searching around for awhile, the eureka moment came when I <a href="https://github.com/lebinh/nginx-conf#sub-request-upon-completion">discovered the <code>post_action</code> feature</a> of NGINX. This enabled me to hit the Measurement Protocol API after serving the feed.

Here's the necessary bits that I had to add to my NGINX config to get it all working:
```
# replace UA-XXXXXXXX-Y with your Analytics property ID
location @GA {
  internal;
  resolver 8.8.8.8 ipv6=off;
  proxy_pass https://www.google-analytics.com/collect?v=1&tid=UA-XXXXXXXX-Y&cid=$remote_addr&t=pageview&dp=$request_uri&uip=$remote_addr;
}

server {
  # the standard stuff (server_name, listen, etc.)
  location / {
    # no changes needed other than adding post_action
    post_action @GA;
  }
}
```
Also, directly passing the User-Agent (e.g., <code>ua=$http_user_agent</code>) gave me all sorts of problems (I think it wasn't being properly URL encoded) so I sanitized them with a <code>map</code>:
```
# N.B. maps have to exist in the http context
map $http_user_agent $user_agent {
  ""                    empty;
  "~Android"            android;
  "~^Slackbot"          slackbot;
  "~^curl"              curl;
  "~^Feedbin"           feedbin;
  "~^Tiny Tiny"         ttrss;
  "~^NewsBlur"          newsblur;
  "~^Feedly"            feedly;
  "~^Go-http"           golang;
  "~^UniversalFeed"     feedparser;
  "~^Zapier"            zapier;
  "~^PHP"               php;
  "~^python-requests"   python-requests;
  "~^Mozilla"           mozilla;
  default               other;
}
```
Then I added <code>ua=$user_agent</code> to the URL. Not ideal, but good enough for me.

