---
ID: 1237
post_title: forcats::fct_match
author: Jonathan Carroll
post_date: 2019-02-22 22:03:11
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1237
published: false
---
<!-- wp:paragraph -->
<p>This journey started almost a year ago, but it's finally been sufficiently worked through and merged! Yay, I've officially contributed to the <a href="https://www.tidyverse.org/">tidyverse</a>. </p>
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

<!-- wp:paragraph -->
<p>For those of you not so comfortable with pipes/<g class="gr_ gr_8 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling" id="8" data-gr-id="8">dplyr</g>, I was trying to subset a <code>data.frame</code> <g class="gr_ gr_76 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="76" data-gr-id="76">named </g><code>data</code><g class="gr_ gr_76 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="76" data-gr-id="76"> to</g> only those rows for which the <g class="gr_ gr_58 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="58" data-gr-id="58">column </g><code>g</code><g class="gr_ gr_58 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="58" data-gr-id="58"> had</g> value <g class="gr_ gr_48 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="48" data-gr-id="48">either </g><code>"X_Y"</code><g class="gr_ gr_48 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="48" data-gr-id="48"> </g><g class="gr_ gr_49 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="49" data-gr-id="49"><g class="gr_ gr_48 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="48" data-gr-id="48">or</g> </g><code>"Z"</code><g class="gr_ gr_49 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="49" data-gr-id="49">.</g> Another way to do this might simply be</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code</p>
<!-- /wp:paragraph -->