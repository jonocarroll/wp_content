---
ID: 938
post_title: Images as x-axis labels
author: Jonathan Carroll
post_date: 2016-06-02 21:55:59
post_excerpt: ""
layout: post
permalink: http://jcarroll.com.au/?p=938
published: false
---
Open-source software is awesome. If I found that a piece of closed-source software was missing a feature that I wanted, well, bad luck. I probably couldn't even tell if was actually missing or if I just didn't know about it. When the source is available, maintained, and documented however, things get fun.

<!--more-->

I've thought for a couple of projects which had bar-graphs that it would be neat to have the categories labelled by an icon or a picture. Say, the logo for a company or an illustrative example. There are probably very few cases for which this is technically a good idea (trying to be a featured author on <a href="http://junkcharts.typepad.com/" target="_blank">JunkCharts</a> might very well be one of those reasons). Nonetheless, there are at least a couple of requests for this floating around on Stackoverflow; <a href="http://stackoverflow.com/questions/29939447/icons-as-x-axis-labels-in-r-ggplot2" target="_blank">here</a> and <a href="http://stackoverflow.com/questions/8905101/how-can-i-use-a-graphic-imported-with-grimport-as-axis-tick-labels-in-ggplot2-u" target="_blank">here</a> for example.

The <a href="http://stackoverflow.com/questions/8905101/how-can-i-use-a-graphic-imported-with-grimport-as-axis-tick-labels-in-ggplot2-u" target="_blank">second link there</a> has a working example, but the big update to <code>ggplot2</code> breaks that pretty strongly; <code>opts</code> was deprecated and now <code>element_text()</code> has a gatekeeper validation routine that prevents any such messing around. The <a href="http://stackoverflow.com/questions/29939447/icons-as-x-axis-labels-in-r-ggplot2" target="_blank">here</a>first link</a> however takes a different route. I couldn't get that one to work either, but in any case the answer is a year out of date (updates in <code>ggplot</code> can easily have broken the <code>gTree</code> relations), not particularly flexible, and relies on saving intermittent image files for <code>PostScriptTrace</code> to read back in which I'm not a fan of (and couldn't get to work in anyway).