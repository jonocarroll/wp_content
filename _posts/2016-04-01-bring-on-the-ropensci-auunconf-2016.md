---
ID: 671
post_title: 'Bring on the ROpenSci #auunconf 2016!'
author: Jonathan Carroll
post_date: 2016-04-01 06:25:01
post_excerpt: ""
layout: post
permalink: >
  http://jcarroll.com.au/2016/04/01/bring-on-the-ropensci-auunconf-2016/
published: true
---
I'll be heading to the <a href="http://auunconf.ropensci.org" target="_blank">2016 ROpenSci un-conference</a> (hackathon) in Brisbane later this month to smash out a heap of open-science R code. Ideas are already flowing quite nicely, and I'm confident that any ideas we don't end up officially working on will get their chance in the very near future.

<!--more-->

One thing I noticed from the organisers was that coffee won't be provided in an official sense. As a physicist at heart, that's strange (scary) yet understandable (physics conferences go through an astounding amount of coffee; we once had a full-time barista on deck). There are supposedly plenty of nearby places to get a good coffee, but where? Time for some R code!

<script src="https://gist.github.com/jonocarroll/603be338bffc2c379ee54ae3e25698c3.js"></script>

This ended up being a little easier than I first thought thanks to <a href="http://stackoverflow.com/a/34802126/4168169" target="_blank">someone already identifying the right Google Places API endpoint and providing an example function</a>. I re-wrote the function to be a bit more general and to suit my needs a little better. After that it's just a matter of extracting and plotting locations, adding a 2d density, and prettifying the output.

[caption width="2400" align="aligncenter"]<a href="https://s3-ap-southeast-2.amazonaws.com/jcarroll1/coffee_near_auunconf_2016.png"><img src="https://s3-ap-southeast-2.amazonaws.com/jcarroll1/coffee_near_auunconf_2016.png" width="2400" height="2400" class /></a> Where to get coffee; the R solution![/caption]

I'm loving <a href="http://rud.is/b/2016/03/16/supreme-annotations/" target="_blank">hrbrmstr's annotations additions</a> to <code>ggplot2</code>; I think they really bring R graphics into a professional appearance. I have a feeling that my locations when not at the hackathon itself will correlate well with this density map as I try to find the best local coffee.

Stay tuned for updates on the projects we end up developing. I have a good feeling that they're going to be somewhat awesome.

Suggestions on the above code most welcome. Also, if you happen to know of a great coffee house near there that isn't listed, hit the comments section!