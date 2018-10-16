---
ID: 1203
post_title: Even more images as xaxis labels
author: Jonathan Carroll
post_date: 2018-10-16 22:38:48
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1203
published: false
---
This is the last update to this strange saga... I hope.

[caption]<img src="https://jcarroll.com.au/wp-content/uploads/2018/10/labels.jpg" />Image labels... Photo: http://www.premierpaper.com/shop/custom-labels/[/caption]

<!--more-->

Easily two of the most popular posts on my blog are <a href="https://jcarroll.com.au/2016/06/02/images-as-x-axis-labels/">this one</a> and <a href="https://jcarroll.com.au/2016/06/03/images-as-x-axis-labels-updated/">this one</a> describing a couple of ways in which I managed to hack together using an image as a category label in a ggplot. There are likely many people who believe one should _never_ do such a thing, but given the popularity, it seems a lot of people aren't listening to that. Good on you.

<div style="width:100%;height:0;padding-bottom:54%;position:relative;"><iframe src="https://giphy.com/embed/bqalUGFYfyHzW" width="100%" height="100%" style="position:absolute" frameBorder="0" class="giphy-embed" allowFullScreen></iframe></div><p><a href="https://giphy.com/gifs/good-hang-breastfeeding-bqalUGFYfyHzW">via GIPHY</a></p>

One of these posts was recently shared again by the amazing #rstats amplifier Mara Averick (if you're not following her on Twitter, you're missing out) and @baptiste_auguie (the saviour of the previous implementation) mentioned that he had seen a 'hack' to get chemical symbols as a categorical axis label using tikzDevice. That package leverages [latex]\LaTeX[/latex] (of which I am _very_ familiar, having written my PhD thesis entirely in [latex]\LaTeX[/latex]many moons ago) to treat all of the text in an image into rendered output, assuming that it contains valid [latex]\LaTeX[/latex] commands.

This got me curious, though -- if it can process $\LaTeX$, could it process a <code>\\includegraphics</code> call?

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Efficient! If it&#39;s arbitrary LaTeX, could the labels just be \includegraphics calls?</p>&mdash; Jonathan Carroll (@carroll_jono) <a href="https://twitter.com/carroll_jono/status/1050535371241476096?ref_src=twsrc%5Etfw">October 11, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Yes, as it turns out. 

<div style="width:100%;height:0;padding-bottom:75%;position:relative;"><iframe src="https://giphy.com/embed/XreQmk7ETCak0" width="100%" height="100%" style="position:absolute" frameBorder="0" class="giphy-embed" allowFullScreen></iframe></div><p><a href="https://giphy.com/gifs/retro-thumbs-up-XreQmk7ETCak0">via GIPHY</a></p>

A quick test showed that it was indeed possible, which only leaves re-implementing the previous posts' images using this method.

I've done so, and the code isn't particularly shorter than the other method.

[gist id="08a1ccff36be628430d768e5b9426e54"]

Producing nearly the same end result.

[caption align="center"]<img src="https://jcarroll.com.au/wp-content/uploads/2018/10/xaxis.png" />tikzDevice result[/caption]

There are a few differences with the previous version(s):

 - I had a request for rotating the additional text, which I actually <a href="https://gist.github.com/jonocarroll/2f9490f1f5e7c82ef8b791a4b91fc9ca#file-images_as_xaxis_labels_updated-r">also updated recently</a>, and it seemed to fit better, so I rotated the labels within the [latex]\LaTeX[/latex]command.
 - Since all of the text has been rendered via [latex]\LaTeX[/latex], the fonts are a bit different.
 - The rankings have since changed, so I've added an 11th to keep Australia in the list.

The [latex]\LaTeX[/latex] component of this also meant that a few changes were necessary in the other labels, such as the dollar sign in the y-axis label, and the underscores throughout (these are considered special characters in [latex]\LaTeX[/latex]. Lastly, the result of running the <code>tikz</code> command is that a <code>.tex</code> ([latex]\LaTeX[/latex]source code) file is produced. This isn't quite the plot image file we want. It _does_ however have the commands to generate one. The last steps in the above gist are to process this <code>.tex</code> file with [latex]\LaTeX[/latex] (here I used the <code>tools::texi2dvi</code> function, but one _could_ also use a <code>system</code> command to their [latex]\LaTeX[/latex] installation.