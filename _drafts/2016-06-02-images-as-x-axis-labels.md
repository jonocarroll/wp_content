---
ID: 938
post_title: Images as x-axis labels
author: Jonathan Carroll
post_date: 2016-06-02 22:00:00
post_excerpt: ""
layout: post
permalink: http://jcarroll.com.au/?p=938
published: false
---
Open-source software is awesome. If I found that a piece of closed-source software was missing a feature that I wanted, well, bad luck. I probably couldn't even tell if was actually missing or if I just didn't know about it. When the source is available, maintained, and documented however, things get fun.

<!--more-->

I've thought for a couple of projects which had bar-graphs that it would be neat to have the categories labelled by an icon or a picture. Say, the logo for a company or an illustrative example. There are probably very few cases for which this is technically a good idea (trying to be a featured author on <a href="http://junkcharts.typepad.com/" target="_blank">JunkCharts</a> might very well be one of those reasons). Nonetheless, there are at least a couple of requests for this floating around on Stackoverflow; <a href="http://stackoverflow.com/questions/29939447/icons-as-x-axis-labels-in-r-ggplot2" target="_blank">here</a> and <a href="http://stackoverflow.com/questions/8905101/how-can-i-use-a-graphic-imported-with-grimport-as-axis-tick-labels-in-ggplot2-u" target="_blank">here</a> for example.

The <a href="http://stackoverflow.com/questions/8905101/how-can-i-use-a-graphic-imported-with-grimport-as-axis-tick-labels-in-ggplot2-u" target="_blank">second link there</a> has a working example, but the big update to <code>ggplot2</code> breaks that pretty strongly; <code>opts</code> was deprecated and now <code>element_text()</code> has a gatekeeper validation routine that prevents any such messing around. The <a href="http://stackoverflow.com/questions/29939447/icons-as-x-axis-labels-in-r-ggplot2" target="_blank">here</a>first link</a> however takes a different route. I couldn't get that one to work either, but in any case the answer is a year out of date (updates in <code>ggplot</code> can easily have broken the <code>gTree</code> relations), not particularly flexible, and relies on saving intermittent image files for <code>PostScriptTrace</code> to read back in which I'm not a fan of (and couldn't get to work anyway).

I decided that I perhaps had enough ammunition to hack something together myself, and sure enough it seems to have worked (for a limited definition of "worked" with no attached or implied guarantees whatsoever).

[caption id="attachment_939" align="alignnone" width="680"]<a href="http://jcarroll.com.au/wp-content/uploads/2016/06/GDP.png"><img src="http://jcarroll.com.au/wp-content/uploads/2016/06/GDP-1024x731.png" alt="GDP per capita with flags for x-axis labels. This is harder to make than it seemed." width="680" height="485" class="size-large wp-image-939" /></a> GDP per capita with flags for x-axis labels. This is harder to make than it seemed.[/caption]

The way to go about making your own is as follows;

 1. Stop and carefully re-evaluate the choices that you've made to bring you to this decision. Are you sure? Okay...
 2. Build your bar graph with categorical x-axis as per normal, using <code>theme()</code> to remove the labels.
 3. Source this function (at your own risk... copy and paste if you prefer):