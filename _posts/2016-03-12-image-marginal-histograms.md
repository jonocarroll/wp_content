---
ID: 655
post_title: Image marginal histograms
author: Jonathan Carroll
post_date: 2016-03-12 00:37:37
post_excerpt: ""
layout: post
permalink: >
  http://jcarroll.com.au/2016/03/12/image-marginal-histograms/
published: true
---
Another day, another interesting challenge. 

<!--more-->

I follow <a href="http://rud.is/b/" target="_blank">Bob Rudis' (a.k.a. hrbrmstr's) blog</a>, typically via <a href="http://www.r-bloggers.com/" target="_blank">R-bloggers</a>, and <a href="http://rud.is/b/2016/03/10/some-light-image-processing-creation-with-r/" target="_blank">this post</a> caught my eye. Partly because I thought I knew of an existing way to do this. As usual, actually getting that to work took a little longer than I might have hoped, but I think the end result is pretty neat.

His post describes the process of writing an R function to take an image file, for example this one

<a href="http://jcarroll.com.au/wp-content/uploads/2016/03/file10a566a2b4dc3.png" rel="attachment wp-att-656"><img src="http://jcarroll.com.au/wp-content/uploads/2016/03/file10a566a2b4dc3.png" alt="file10a566a2b4dc3" width="700" height="400" class="aligncenter size-full wp-image-656" /></a>

and producing a histogram along the sides of the number of pixels on a given row/column. This is what he created (a different image to the example, I believe)

<img src=http://i2.wp.com/rud.is/b/wp-content/uploads/2016/03/Rplot1.png?resize=940%2C512></img>

Something funny is going on with the right-hand histogram; it doesn't line up with the image.

Here's my approach. 

<script src="https://gist.github.com/JonoCarroll/7960dff5bf42e47423db.js"></script>

It leverages the <code>png</code> package to extract the channels into a matrix, converts those to <code>x,y,z data.frame</code>s, takes the median value, plots that with <code>ggplot2</code>, then leverages <code>ggExtra::ggMarginal</code> to add the marginal histograms. Note that the <code>ggExtra</code> package has some bugs (it hasn't been maintained in a while) in relation to more recent (possibly the dev branch) of <code>ggplot2</code>. I got it working on at least one of my machines. This is my result

<div align="center"><a href="http://jcarroll.com.au/wp-content/uploads/2016/03/marginal.png" rel="attachment wp-att-661"><img src="http://jcarroll.com.au/wp-content/uploads/2016/03/file10a566a2b4dc3.png" alt="file10a566a2b4dc3" width="700" height="400" class="aligncenter size-full wp-image-656" /> vs <img src="http://jcarroll.com.au/wp-content/uploads/2016/03/marginal.png" alt="marginal" width="800" height="500" class="aligncenter size-full wp-image-661" /></a></div>

I've had several uses for these types of marginal plots lately, so hopefully I can sort out the issues I've been getting in combination with <code>ggplot2</code>.