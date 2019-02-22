---
ID: 1237
post_title: forcats::fct_match
author: Jonathan Carroll
post_date: 2019-02-22 22:11:51
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1237
published: false
---
<!-- wp:paragraph -->
<p>This journey started almost a year ago, but it's finally been sufficiently worked through and merged! Yay, I've officially contributed to the <a href="https://www.tidyverse.org/">tidyverse</a>. </p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1243,"align":"center"} -->
<div class="wp-block-image"><figure class="aligncenter"><img src="https://jcarroll.com.au/wp-content/uploads/2019/02/zoidberg_helping.jpeg" alt="" class="wp-image-1243"/></figure></div>
<!-- /wp:image -->

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
<p>For those of you not so comfortable with pipes/<g class="gr_ gr_8 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling" id="8" data-gr-id="8">dplyr</g>, I was trying to subset a <code>data.frame</code> <g class="gr_ gr_76 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="76" data-gr-id="76">named </g><code>data</code><g class="gr_ gr_76 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="76" data-gr-id="76"> to</g> only those rows for which the <g class="gr_ gr_58 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="58" data-gr-id="58">column </g><code>g</code><g class="gr_ gr_58 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="58" data-gr-id="58"> had</g> value <g class="gr_ gr_48 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="48" data-gr-id="48">either </g><code>"X_Y"</code><g class="gr_ gr_48 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="48" data-gr-id="48"> </g><g class="gr_ gr_49 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="49" data-gr-id="49"><g class="gr_ gr_48 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="48" data-gr-id="48">or</g> </g><code>"Z"</code><g class="gr_ gr_49 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="49" data-gr-id="49">.</g> In base code this might simply be</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code language="r" light="true"]<br>data[data$g %in% c("X Y", "Z"), ]<br>[/code]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><code>filter</code>isn't at fault here -- the same issue would arise with <code>[</code> -- I have <g class="gr_ gr_5 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling" id="5" data-gr-id="5">mis-specified</g> the values I wish to match, so I am returned only the matching values. <code>%in%</code> is also performing its job - it returns a logical vector; the result of comparing the values in the <g class="gr_ gr_165 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling ins-del multiReplace" id="165" data-gr-id="165">column</g><code>g</code><g class="gr_ gr_165 gr-alert gr_spell gr_inline_cards gr_disable_anim_appear ContextualSpelling ins-del multiReplace" id="165" data-gr-id="165">to</g> the <g class="gr_ gr_205 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="205" data-gr-id="205">vector </g><code>c("X Y", "Z")</code><g class="gr_ gr_205 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="205" data-gr-id="205">.</g> Both of these functions are behaving as they should, but the logic of what I was trying to achieve (subset to only these values) was lost.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Now, in some instances, that is exactly the behaviour you want -- subset this vector to <em>any</em> of these values... where those values may not be present in the vector to begin with.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The problem, for me, is that there isn't a way to say "all of these should be there". The lack of matching happens silently.</p>
<!-- /wp:paragraph -->