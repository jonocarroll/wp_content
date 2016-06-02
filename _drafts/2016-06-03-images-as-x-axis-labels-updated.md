---
ID: 952
post_title: Images as x-axis labels (updated)
author: Jonathan Carroll
post_date: 2016-06-03 08:00:51
post_excerpt: ""
layout: post
permalink: http://jcarroll.com.au/?p=952
published: false
---
They say "if you want to find an answer on the internet, first present a wrong one presented as fact. Then wait."

<!--more-->

It didn't take long, actually. Despite my searches while trying to get <a href="http://jcarroll.com.au/2016/06/02/images-as-x-axis-labels/" target="_blank">images into x-axis labels</a> it seems I overlooked a working, <a href="http://stackoverflow.com/questions/14070953/photo-alignment-with-graph-in-r/14078391" target="_blank">significantly less hacky implementation</a>. My Google-fu had in fact let me down.

Baptiste Auguié (<a href="https://twitter.com/tpab" target="_blank">@tpab</a> / <a href="https://github.com/baptiste" target="_blank">@baptiste</a>) had this working a while ago (seemingly before the <code>ggplot2</code> update that broke other methods), and in a definitively less hacky way. I've added a <a href="https://gist.github.com/jonocarroll/2f9490f1f5e7c82ef8b791a4b91fc9ca" target="_blank">new gist</a> (if you're reading this on R-bloggers, the gist isn't embedded, so either follow the link or view on my site) which implements it on the same graph as earlier, and I like this significantly more.

[gist id="2f9490f1f5e7c82ef8b791a4b91fc9ca]

This method
<ul>
	<li> Places the factor labels on the graph along with the picture, covering some concerns about people not knowing which maps are for which country,</li>
	<li> Leaves room for the <code>caption</code> to go back in, which I wanted,</li>
	<li> Automatically scales the grob better,</li>
	<li> Doesn't involve creating an external <code>grob</code> and thus turning off clipping; using <code>axis.text.x</code> is exactly what I was hoping for.</li>
</ul>

[caption id="attachment_953" align="alignnone" width="680"]<a href="http://jcarroll.com.au/wp-content/uploads/2016/06/GDP_updated.png"><img src="http://jcarroll.com.au/wp-content/uploads/2016/06/GDP_updated-1024x640.png" alt="Updated version using @baptiste&#039;s method; much better." width="680" height="425" class="size-large wp-image-953" /></a> Updated version using @baptiste's method; much better.[/caption]