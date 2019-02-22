---
ID: 1237
post_title: forcats::fct_match
author: Jonathan Carroll
post_date: 2019-02-22 21:55:00
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1237
published: false
---
<!-- wp:paragraph -->
<p>This journey started almost a year ago, but it's finally been sufficiently worked through and merged! Yay, I've officially contributed to the tidyverse. </p>
<!-- /wp:paragraph -->

<!-- wp:more -->
<!--more-->
<!-- /wp:more -->

<!-- wp:paragraph -->
<p>It began with a tweet, recalling a surprise I encountered that day during some routine data processing</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>Source of today's mild heart-attack: I have categories W, X_Y, and Z in some data. Intending to keep only the second two:<br><br>data %&gt;% filter(g %in% c("X Y", "Z")<br><br>Did you spot that I used a space instead of an underscore? I sure as heck didn't, and filtered excessively to just Z.— Jonathan Carroll (@carroll_jono) <a href="https://twitter.com/carroll_jono/status/971093803099541504?ref_src=twsrc%5Etfw">March 6, 2018</a></p></blockquote>
<!-- /wp:quote -->