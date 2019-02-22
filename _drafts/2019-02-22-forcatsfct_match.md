---
ID: 1237
post_title: forcats::fct_match
author: Jonathan Carroll
post_date: 2019-02-22 23:07:12
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1237
published: false
---
<p>This journey started almost a year ago, but it's finally been sufficiently worked through and merged! Yay, I've officially contributed to the <a href="https://www.tidyverse.org/">tidyverse</a>.&nbsp;</p>

<div class="wp-block-image"><figure class="aligncenter"><img src="https://jcarroll.com.au/wp-content/uploads/2019/02/zoidberg_helping.jpeg" alt="" class="wp-image-1243"/></figure></div>

<!--more-->

<p>It began with <a href="https://twitter.com/carroll_jono/status/971093803099541504?ref_src=twsrc%5Etfw">a tweet</a>, recalling a surprise I encountered that day during some routine data processing</p>

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Source of today&#39;s mild heart-attack: I have categories W, X_Y, and Z in some data. Intending to keep only the second two:<br><br>data %&gt;% filter(g %in% c(&quot;X Y&quot;, &quot;Z&quot;)<br><br>Did you spot that I used a space instead of an underscore? I sure as heck didn&#39;t, and filtered excessively to just Z.</p>&mdash; Jonathan Carroll (@carroll_jono) <a href="https://twitter.com/carroll_jono/status/971093803099541504?ref_src=twsrc%5Etfw">March 6, 2018</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

For those of you not so comfortable with pipes `dplyr`, I was trying to subset a <code>data.frame</code>&nbsp;named&nbsp;<code>data</code>&nbsp;(with a <g class="gr_ gr_291 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="291" data-gr-id="291">column </g><code>g</code><g class="gr_ gr_291 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="291" data-gr-id="291">&nbsp;having</g>&nbsp;<g class="gr_ gr_294 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="294" data-gr-id="294">values </g><code>"W"</code><g class="gr_ gr_294 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="294" data-gr-id="294"><g class="gr_ gr_239 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Punctuation only-del replaceWithoutSep" id="239" data-gr-id="239">,</g></g><g class="gr_ gr_239 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Punctuation only-del replaceWithoutSep" id="239" data-gr-id="239"> </g><code>"X_Y"</code><g class="gr_ gr_239 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Punctuation only-del replaceWithoutSep" id="239" data-gr-id="239">,</g> and <code>"Z"</code>) to only those rows for which the <g class="gr_ gr_58 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="58" data-gr-id="58">column </g><code>g</code><g class="gr_ gr_58 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="58" data-gr-id="58"> had</g>&nbsp;the value <g class="gr_ gr_48 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="48" data-gr-id="48">either </g><code>"X_Y"</code><g class="gr_ gr_48 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="48" data-gr-id="48"> </g><g class="gr_ gr_49 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="49" data-gr-id="49"><g class="gr_ gr_48 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="48" data-gr-id="48">or</g> </g><code>"Z"</code><g class="gr_ gr_49 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="49" data-gr-id="49">.</g>&nbsp;In base <g class="gr_ gr_126 gr-alert gr_gramm gr_inline_cards gr_run_anim Punctuation only-ins replaceWithoutSep" id="126" data-gr-id="126">code</g> this might simply be

[code language="r" light="true"]data[data$g %in% c(&quot;X Y&quot;, &quot;Z&quot;), ][/code]

To make that more concrete, let's actually show it in action

[code language="r" light="true"]
data &lt;- data.frame(a = 1:5, g = c(&quot;X_Y&quot;, &quot;W&quot;, &quot;Z&quot;, &quot;Z&quot;, &quot;W&quot;))
data
#&gt;   a   g
#&gt; 1 1 X_Y
#&gt; 2 2   W
#&gt; 3 3   Z
#&gt; 4 4   Z
#&gt; 5 5   W

data %&gt;% filter(g %in% c(&quot;X Y&quot;, &quot;Z&quot;))
#&gt;   a g
#&gt; 1 3 Z
#&gt; 2 4 Z
[/code]
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><code>filter</code> isn't at fault here -- the same issue would arise with <code>[</code>&nbsp;-- I have <g class="gr_ gr_5 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling" id="5" data-gr-id="5">mis-specified</g> the values I wish to match, so I am returned only the matching values. <code>%in%</code>&nbsp;is also performing its job - it returns a logical vector; the result of comparing the values in the <g class="gr_ gr_165 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling ins-del multiReplace" id="165" data-gr-id="165">column</g><code>g</code><g class="gr_ gr_165 gr-alert gr_spell gr_inline_cards gr_disable_anim_appear ContextualSpelling ins-del multiReplace" id="165" data-gr-id="165">to</g>&nbsp;the <g class="gr_ gr_205 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="205" data-gr-id="205">vector </g><code>c("X Y", "Z")</code><g class="gr_ gr_205 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="205" data-gr-id="205">.</g>&nbsp;Both of these functions are behaving as they should, but the logic of what I was trying to achieve (subset to only these values) was lost.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Now, in some instances, that is exactly the behaviour you want -- subset this vector to <em>any</em> of these values... where those values may not be present in the vector <g class="gr_ gr_98 gr-alert gr_gramm gr_inline_cards gr_run_anim Punctuation only-ins replaceWithoutSep" id="98" data-gr-id="98">to</g> begin with</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code language="r" light="true"]data %&amp;gt;% filter(values %in% known_values)[/code]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The problem, for me, is that there isn't a way to say "all of these should be there". The lack of matching happens silently. If you make a typo, you don't get that level, and you aren't told that it's been skipped</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code language="r" light="true"]simpsons_characters %&amp;gt;% filter(first_name %in% c(&quot;Homer&quot;, &quot;Marge&quot;, &quot;Bert&quot;, &quot;Lisa&quot;, &quot;Maggie&quot;)[/code]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Technically this is a double-post because I also want to sidenote this with something I am amazed I have not known about yet (I was approximately today years old when I learned about this)... I've used <code>regex</code>matching for a while, and have been surprised at <a href="https://twitter.com/carroll_jono/status/908186714350403584">how well I've been able to make it work</a> occasionally. I'm familiar with counting patterns (<code>(A){2}</code>&nbsp;to match two occurrences of <code>A</code>) and ranges of counts (<code>(A){2,4}</code>&nbsp;to match between two and four occurrences of <code>A</code>) but I was not aware that you can specify <g class="gr_ gr_1434 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Grammar multiReplace" id="1434" data-gr-id="1434">a number</g> of <em><strong>mistakes</strong></em> that can be included to still make a match...&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code language="r" light="true"]grep(&quot;Bart&quot;, c(&quot;Bart&quot;, &quot;Bort&quot;), value = TRUE)&lt;br&gt;#&amp;gt; [1] &quot;Bart&quot;&lt;br&gt;grep(&quot;(Bart){~1}&quot;, c(&quot;Bart&quot;, &quot;Bort&quot;), value = TRUE)&lt;br&gt;#&amp;gt; [1] &quot;Bart&quot; &quot;Bort&quot;[/code]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Use the <g class="gr_ gr_4 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="4" data-gr-id="4">syntax </g><code>(pattern){~n}</code><g class="gr_ gr_4 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="4" data-gr-id="4">&nbsp;to</g> allow up to <code>n</code>substitutions in the pattern matching. Refer <a href="https://twitter.com/klmr/status/1098238987968438273?s=20">here</a> and <a href="https://laurikari.net/tre/documentation/regex-syntax/">here</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Back to the original problem -- <code>filter</code>and <code>%in%</code>are doing their jobs, but we aren't getting the result we want because we made a typo, and we aren't told that we've done so.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Enter a <a href="https://github.com/tidyverse/forcats/pull/127">new PR</a> to <code>forcats</code>(originally to <code>dplyr</code>, but <code>forcats</code>does make more sense) which implements <code>fct_match(f, lvls)</code>. This checks that all of the values in <code>lvls</code>are actually present in <code>f</code>before returning the logical vector of which entries they correspond to. With this, the pattern becomes</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code light="true" language="r"]data %&amp;gt;% filter(fct_match(g, c(&quot;X Y&quot;, &quot;Z&quot;)))&lt;br&gt;&amp;gt; Error in filter_impl(.data, quo): Evaluation error: Levels not present in factor: &quot;X Y&quot;.[/code]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Yay! We're notified that we've made an error. <code>"X Y"</code>isn't actually in our column <code>g</code>. If we don't make the error, we get the result we actually wanted in the first place. After loading the development version of <code>forcats</code>from <g class="gr_ gr_81 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling ins-del multiReplace" id="81" data-gr-id="81">github</g> we can now use</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code language="r" light="true"]data %&amp;gt;% filter(fct_match(g, c(&quot;X_Y&quot;, &quot;Z&quot;)))&lt;br&gt;#&amp;gt;   a   g&lt;br&gt;#&amp;gt; 1 1 X_Y&lt;br&gt;#&amp;gt; 2 3   Z&lt;br&gt;#&amp;gt; 3 4 Z[/code]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>It took a while for the PR to be addressed (the tidyverse crew have plenty of backlog, no doubt) but after some minor requested changes and a very neat cleanup by Hadley himself, it's been merged.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>My original version had a few bells and whistles that the current implementation has put aside. The first was inverting the matching with&nbsp;<code>fct_exclude</code>to make it easier to negate the matching without having to create a new anonymous function, i.e. <code>~!fct_match(.x)</code>. I find this particularly useful since a pipe expects a call/named function, not a lambda/anonymous function, which is actually quite painful to construct</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code language="r" light="true"]data$g %&amp;gt;% &lt;br&gt;&amp;nbsp; &amp;nbsp;(function(x) !fct_match(x, c(&quot;X_Y&quot;, &quot;Z&quot;)))[/code]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>whereas if we defined</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code language="r" light="true"]fct_exclude &amp;lt;- function(f, lvls, …) !fct_match(f, lvls, …)[/code]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>we can use</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>[code language="r" light="true"]data$g %&amp;gt;% &lt;br&gt;&amp;nbsp; &amp;nbsp;fct_exclude(c(&quot;X_Y&quot;, &quot;Z&quot;))[/code]</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> The other was specifying whether or not to include missing levels when considering <g class="gr_ gr_21 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="21" data-gr-id="21"><g class="gr_ gr_15 gr-alert gr_spell gr_inline_cards gr_run_anim ContextualSpelling ins-del" id="15" data-gr-id="15">if</g> </g><code>lvls</code><g class="gr_ gr_21 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="21" data-gr-id="21">&nbsp;is</g> a valid value <g class="gr_ gr_22 gr-alert gr_gramm gr_inline_cards gr_run_anim Style multiReplace" id="22" data-gr-id="22">in </g><code>f</code><g class="gr_ gr_22 gr-alert gr_gramm gr_inline_cards gr_disable_anim_appear Style multiReplace" id="22" data-gr-id="22">&nbsp;since</g> <code>unique(f)</code>and <code>levels(f)</code>can return different answers.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Hopefully this pattern of <code>filter(fct_match(f, lvls))</code> is useful to others. It's certainly going to save me overlooking some typos.</p>
<!-- /wp:paragraph -->