---
ID: 1165
post_title: Adding strings in R
author: Jonathan Carroll
post_date: 2018-10-05 21:15:18
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1165
published: false
---
This started out as a "hey, I wonder" sort of thing, but as usual, they tend to end up as interesting voyages into the deepest depths of code.

<!--more-->

<a href="http://www.happylittlescripts.com/2018/09/make-your-r-code-nicer-with-roperators.html">This post</a> came across my feed last week, referring to the <a href="https://cran.r-project.org/package=roperators">roperators package on CRAN</a>. In that post, the author introduces an infix operator from that package which 'adds' (concatenates) strings in a very Python/Javascript way

[code brush="R"]
&quot;using infix (%) operators&quot; %+% &quot;R can do simple string addition&quot;
#&gt; &quot;using infix (%) operators R can do simple string addition&quot;
[/code]