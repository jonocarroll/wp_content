---
ID: 1203
post_title: Even more images as xaxis labels
author: Jonathan Carroll
post_date: 2018-10-16 21:53:58
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1203
published: false
---
This is the last update to this... I hope.

<!--more-->

Easily one of the most popular posts on my blog is this one describing a couple of ways in which I managed to hack together using an image as a category label in a ggplot.

It was recently shared again by the amazing #rstats amplifier Mara Averick (if you're not following her on Twitter, you're missing out) and @baptiste_auguie (the saviour of the previous implementation) mentioned that he had seen a 'hack' to get chemical symbols as a categorical axis label using tikzDevice. That package leverages LaTeX (of which I am _very_ familiar, having written my PhD thesis entirely in LaTeX) to treat all of the text in an image into rendered output, assuming that it contains valid LaTeX commands.

This got me curious, though -- if it can process