---
ID: 1237
post_title: forcats::fct_match
author: Jonathan Carroll
post_date: 2019-02-22 22:41:51
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
<p> For those of you not so comfortable with pipes/<g class="gr_ gr_8 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling" id="8" data-gr-id="8">dplyr</g>, I was trying to subset a <code>data.frame</code> named <code>data</code> (with a <g class="gr_ gr_291 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="291" data-gr-id="291">column </g><code>g</code><g class="gr_ gr_291 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="291" data-gr-id="291"> having</g> <g class="gr_ gr_294 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="294" data-gr-id="294">values </g><code>"W"</code><g class="gr_ gr_294 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="294" data-gr-id="294"><g class="gr_ gr_239 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Punctuation only-del replaceWithoutSep" id="239" data-gr-id="239">,</g></g><g class="gr_ gr_239 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Punctuation only-del replaceWithoutSep" id="239" data-gr-id="239"> </g><code>"X_Y"</code><g class="gr_ gr_239 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Punctuation only-del replaceWithoutSep" id="239" data-gr-id="239">,</g> and <code>"Z"</code>) to only those rows for which the <g class="gr_ gr_58 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="58" data-gr-id="58">column </g><code>g</code><g class="gr_ gr_58 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="58" data-gr-id="58"> had</g> the value <g class="gr_ gr_48 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="48" data-gr-id="48">either </g><code>"X_Y"</code><g class="gr_ gr_48 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="48" data-gr-id="48"> </g><g class="gr_ gr_49 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="49" data-gr-id="49"><g class="gr_ gr_48 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="48" data-gr-id="48">or</g> </g><code>"Z"</code><g class="gr_ gr_49 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="49" data-gr-id="49">.</g> In base <g class="gr_ gr_126 gr-alert gr_gramm gr_inline_cards gr_run_anim Punctuation only-ins replaceWithoutSep" id="126" data-gr-id="126">code</g> this might simply be</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code language="r" light="true"]data[data$g %in% c("X Y", "Z"), ][/code]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>To make that more concrete, let's actually show it in action</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code language="r" light="true"]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>data &lt;- data.frame(a = 1:5, g = c("X_Y", "W", "Z", "Z", "W"))<br>data<br>#>   a   g<br>#> 1 1 X_Y<br>#> 2 2   W<br>#> 3 3   Z<br>#> 4 4   Z<br>#> 5 5   W<br><br>data %>% filter(g %in% c("X Y", "Z"))<br>#>   a g<br>#> 1 3 Z<br>#> 2 4 Z</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><code>filter</code> isn't at fault here -- the same issue would arise with <code>[</code> -- I have <g class="gr_ gr_5 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling" id="5" data-gr-id="5">mis-specified</g> the values I wish to match, so I am returned only the matching values. <code>%in%</code> is also performing its job - it returns a logical vector; the result of comparing the values in the <g class="gr_ gr_165 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling ins-del multiReplace" id="165" data-gr-id="165">column</g><code>g</code><g class="gr_ gr_165 gr-alert gr_spell gr_inline_cards gr_disable_anim_appear ContextualSpelling ins-del multiReplace" id="165" data-gr-id="165">to</g> the <g class="gr_ gr_205 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="205" data-gr-id="205">vector </g><code>c("X Y", "Z")</code><g class="gr_ gr_205 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="205" data-gr-id="205">.</g> Both of these functions are behaving as they should, but the logic of what I was trying to achieve (subset to only these values) was lost.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Now, in some instances, that is exactly the behaviour you want -- subset this vector to <em>any</em> of these values... where those values may not be present in the vector <g class="gr_ gr_98 gr-alert gr_gramm gr_inline_cards gr_run_anim Punctuation only-ins replaceWithoutSep" id="98" data-gr-id="98">to</g> begin with</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code language="r" light="true"]data %>% filter(values %in% known_values)[/code]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The problem, for me, is that there isn't a way to say "all of these should be there". The lack of matching happens silently. If you make a typo, you don't get that level, and you aren't told that it's been skipped</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code language="r" light="true"]simpsons_characters %>% filter(first_name %in% c("Homer", "Marge", "Bert", "Lisa", "Maggie")[/code]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Technically this is a double-post because I also want to sidenote this with something I am amazed I have not known about yet (I was approximately today years old when I learned about this)... I've used <code>regex</code>matching for a while, and have been surprised at <a href="https://twitter.com/carroll_jono/status/908186714350403584">how well I've been able to make it work</a> occasionally. I'm familiar with counting patterns (<code>(A){2}</code> to match two occurrences of <code>A</code>) and ranges of counts (<code>(A){2,4}</code> to match between two and four occurrences of <code>A</code>) but I was not aware that you can specify <g class="gr_ gr_1434 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Grammar multiReplace" id="1434" data-gr-id="1434">a number</g> of <em><strong>mistakes</strong></em> that can be included to still make a match... </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code language="r" light="true"]grep("Bart", c("Bart", "Bort"), value = TRUE)<br>#> [1] "Bart"<br>grep("(Bart){~1}", c("Bart", "Bort"), value = TRUE)<br>#> [1] "Bart" "Bort"[/code]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Use the <g class="gr_ gr_4 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="4" data-gr-id="4">syntax </g><code>(pattern){~n}</code><g class="gr_ gr_4 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="4" data-gr-id="4"> to</g> allow up to <code>n</code>substitutions in the pattern matching. Refer <a href="https://twitter.com/klmr/status/1098238987968438273?s=20">here</a> and <a href="https://laurikari.net/tre/documentation/regex-syntax/">here</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Back to the original problem -- <code>filter</code>and <code>%in%</code>are doing their jobs, but we aren't getting the result we want because we made a typo, and we aren't told that we've done so.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Enter a <a href="https://github.com/tidyverse/forcats/pull/127">new PR</a> to <code>forcats</code>(originally to <code>dplyr</code>, but <code>forcats</code>does make more sense) which implements <code>fct_match(f, lvls)</code>. This checks that all of the values in <code>lvls</code>are actually present in <code>f</code>before returning the logical vector of which entries they correspond to. With this, the pattern becomes</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code language="r" light="true"]data %>% filter(fct_match(g, c("X Y", "Z")))<br>> Error in filter_impl(.data, quo): Evaluation error: Levels not present in factor: "X Y".[/code]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Yay! We're notified that we've made an error. <code>"X Y"</code>isn't actually in our column <code>g</code>. If we don't make the error, we get the result we actually wanted in the first place. After loading the development version of <code>forcats</code>from <g class="gr_ gr_81 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling ins-del multiReplace" id="81" data-gr-id="81">github</g> we can now use</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code language="r" light="true"]data %>% filter(fct_match(g, c("X_Y", "Z")))<br>#>   a   g<br>#> 1 1 X_Y<br>#> 2 3   Z<br>#> 3 4 Z[/code]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>It took a while for the PR to be addressed (the tidyverse crew have plenty of backlog, no doubt) but after some minor requested changes and a very neat cleanup by Hadley himself, it's been merged.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>My original version had a few bells and whistles that the current implementation has put aside, such as inverting the matching with <code>fct_exclude</code>to make it easier to negate the matching without having to create a new anonymous function, i.e. <code>~!fct_match(.x)</code>and specifying whether or not to include missing levels when considering if <code>lvls</code> is a valid value in <code>f</code> since <code>unique(f)</code>and <code>levels(f)</code>give different answers.</p>
<!-- /wp:paragraph -->