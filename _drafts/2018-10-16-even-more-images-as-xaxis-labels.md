---
ID: 1203
post_title: Even more images as xaxis labels
author: Jonathan Carroll
post_date: 2018-10-16 21:56:52
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1203
published: false
---
This is the last update to this strange saga... I hope.

<!--more-->

Easily one of the most popular posts on my blog is this one describing a couple of ways in which I managed to hack together using an image as a category label in a ggplot. There are likely many people who believe one should _never_ do such a thing, but given the popularity, it seems a lot of people aren't listening to that. Good on you.

One of these posts was recently shared again by the amazing #rstats amplifier Mara Averick (if you're not following her on Twitter, you're missing out) and @baptiste_auguie (the saviour of the previous implementation) mentioned that he had seen a 'hack' to get chemical symbols as a categorical axis label using tikzDevice. That package leverages LaTeX (of which I am _very_ familiar, having written my PhD thesis entirely in LaTeX many moons ago) to treat all of the text in an image into rendered output, assuming that it contains valid LaTeX commands.

This got me curious, though -- if it can process LaTeX, could it process a <code>\\includegraphics</code> call?

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Efficient! If it&#39;s arbitrary LaTeX, could the labels just be \includegraphics calls?</p>&mdash; Jonathan Carroll (@carroll_jono) <a href="https://twitter.com/carroll_jono/status/1050535371241476096?ref_src=twsrc%5Etfw">October 11, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Yes, as it turns out. 

A quick test showed that it was indeed possible, which only leaves re-implementing the previous posts' images usign