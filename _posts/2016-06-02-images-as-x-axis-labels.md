---
ID: 938
post_title: Images as x-axis labels
author: Jonathan Carroll
post_date: 2016-06-02 22:42:31
post_excerpt: ""
layout: post
permalink: >
  http://jcarroll.com.au/2016/06/02/images-as-x-axis-labels/
published: true
---
Open-source software is awesome. If I found that a piece of closed-source software was missing a feature that I wanted, well, bad luck. I probably couldn't even tell if was actually missing or if I just didn't know about it. When the source is available, maintained, and documented however, things get fun. We can identify, and perhaps fill gaps.

<!--more-->

I've thought for a couple of projects which had bar-graphs that it would be neat to have the categories labelled by an icon or a picture. Say, the logo for a company or an illustrative example. Sure, you could fire up GIMP/Inkscape and manually insert them over the top of the text labels (each and every time you re-produce the graph... no thanks) but that's not how I operate. 

There are probably very few cases for which this is technically a good idea (trying to be a featured author on <a href="http://junkcharts.typepad.com/" target="_blank">JunkCharts</a> might very well be one of those reasons). Nonetheless, there are at least a couple of requests for this floating around on stackoverflow; <a href="http://stackoverflow.com/questions/29939447/icons-as-x-axis-labels-in-r-ggplot2" target="_blank">here</a> and <a href="http://stackoverflow.com/questions/8905101/how-can-i-use-a-graphic-imported-with-grimport-as-axis-tick-labels-in-ggplot2-u" target="_blank">here</a> for example. I struggled to find any satisfactory solutions that were in current working order (though perhaps my Google-fu has failed me).

The <a href="http://stackoverflow.com/questions/8905101/how-can-i-use-a-graphic-imported-with-grimport-as-axis-tick-labels-in-ggplot2-u" target="_blank">second link there</a> has a working example, but the big update to <code>ggplot2</code> breaks that pretty strongly; <code>opts</code> was deprecated and now <code>element_text()</code> has a gatekeeper validation routine that prevents any such messing around. The <a href="http://stackoverflow.com/questions/29939447/icons-as-x-axis-labels-in-r-ggplot2" target="_blank">first link</a> however takes a different route. I couldn't get that one to work either, but in any case the answer is a year out of date (updates in <code>ggplot2</code> can easily have broken the <code>gTree</code> relations), not particularly flexible, and relies on saving intermittent image files for <code>PostScriptTrace</code> to read back in which I'm not a fan of (and couldn't get to work anyway).

I decided that I perhaps had enough ammunition to hack something together myself (emphasis on hack), and sure enough it seems to have worked (for a limited definition of "worked" with no attached or implied guarantees whatsoever).

[caption id="attachment_939" align="alignnone" width="680"]<a href="http://jcarroll.com.au/wp-content/uploads/2016/06/GDP.png"><img src="http://jcarroll.com.au/wp-content/uploads/2016/06/GDP-1024x731.png" alt="GDP per capita with flags for x-axis labels. This is harder to make than it seemed." width="680" height="485" class="size-large wp-image-939" /></a> GDP per capita with flags for x-axis labels. This was harder to make than it seemed, but I've since added a little more flexibility to it.[/caption]

The way to go about making your own is as follows;
<ol>
 <li> Stop and carefully re-evaluate the choices that you've made to bring you to this decision. Are you sure? Okay...</li>
 <li> Save the images (in the correct factor order) into a list (e.g. <code>pics</code>).</li>
 <li> Build your bar graph with categorical x-axis as per normal, using <code>theme()</code> to remove the labels. Save as an object (e.g. <code>g</code>).</li>
 <li> Source the function <a href="https://gist.github.com/jonocarroll/1d1bdb00a7b3910d62bf3eec8a77b4a7" target="_blank">from this gist</a> (at your own risk... copy and paste if you prefer): </li>

[code language="r" light="1"]
devtools::source_gist(&quot;1d1bdb00a7b3910d62bf3eec8a77b4a7&quot;)
[/code]

[gist id="1d1bdb00a7b3910d62bf3eec8a77b4a7"]

 <li> Call (or pipe your <code>ggplot</code> object to) the function: </li>

[code language="r" light="1"]
g %&gt;% add_images_as_xlabels(pics)

## or

add_images_as_xlabels(g, pics)
[/code]

 <li> Your image will be re-drawn with your pictures labelling the categories.</li>
</ol>
Here's an example of the code used to generate the GDP per capita image, featuring some fairly brief (for what it does) <code>rvest</code> scraping (to reiterate; I don't want to have to do any of this by hand, so let's code it up!).

[gist id="96d1dd879b535c3c7ffe8f74065d4bc4"]

At least a few caveats surround what I did manage to get working, including but not limited to:
<ul>
 <li> I'm not sure how to put the x-axis title back in at the right position without padding it with a lot of linebreaks (<code>"\n\n\n\nX-AXIS TITLE"</code>).</li>
 <li> I'm not sure how to move the <code>caption</code> line from <code>labs()</code> (assuming you're using the development version of <code>ggplot2</code> on GitHub with @hrbrmstr's excellent annotation additions) so it potentially gets drawn over.</li>
 <li> The spacing below the graph is currently arbitrarily set to a few lines more than necessary, but it's a compromise in having an arbitrary number of images loaded at their correct sizes.</li>
 <li> Similarly, I've just expanded the plot range of the original graph by a seemingly okay amount which has worked for the few examples I've tried.</li>
 <li> Using a graph like this places the onus of domain knowledge onto the reader; if you don't know what those flags refer to then this graph is less useful than one with the countries labelled with words. Prettier though.</li>
</ul>
I've no doubt that there must be a better way to do this, but it's beyond my understanding of how <code>ggproto</code> works, and I can't seem to bypass <code>element_text</code>'s requirements with what I do know. If you would like to help develop this into something more robust then I'm most interested. Given that it's a single function I wasn't going to create a package just for this, but I'm willing to help incorporate it into someone's existing package. Hit the comments or ping me on Twitter (<a href="https://twitter.com/carroll_jono" target="_blank">@carroll_jono</a>)!