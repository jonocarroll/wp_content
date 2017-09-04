---
ID: 1106
post_title: An integer by any other name
author: Jonathan Carroll
post_date: 2017-09-04 14:15:53
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1106
published: false
---
<p>This was just going to be a few Tweets but it ended up being a bit of a rollercoaster of learning for me, and I haven’t blogged in far too long, so I’m writing it up quickly as a ‘hey look at that’ example for newcomers.</p>
<p>I’ve been working on the ‘merging data’ part of my book and, as I do when I’m writing this stuff, I had a play around with some examples to see if there was anything funky going on if a reader was to try something slightly different. I’ve been using <code>dplyr</code> for the examples after being thoroughly convinced on Twitter to do so. It’s going well. Mostly.</p>
<pre class="r"><code>## if you haven't already done so, load dplyr
suppressPackageStartupMessages(library(dplyr))</code></pre>
<p>My example involved joining together two <code>tibble</code>s containing text values. Nothing too surprising. I wondered though; do numbers behave the way I expect?</p>
<p>If I had a <code>tibble</code> where the column I would use to <code>join</code> had integers</p>
<pre class="r"><code>dataA &lt;- tribble(
    ~X, ~Y,
    0L, 100L,
    1L, 101L,
    2L, 102L,
    3L, 103L
)
dataA</code></pre>
<pre><code>## # A tibble: 4 x 2
##       X     Y
##   &lt;int&gt; &lt;int&gt;
## 1     0   100
## 2     1   101
## 3     2   102
## 4     3   103</code></pre>
<p>and another <code>tibble</code> with <code>numeric</code> in that column</p>
<pre class="r"><code>dataB &lt;- tribble(
    ~X, ~Z,
    0, 1000L,
    1, 1001L,
    2, 1002L,
    3, 1003L
)
dataB</code></pre>
<pre><code>## # A tibble: 4 x 2
##       X     Z
##   &lt;dbl&gt; &lt;int&gt;
## 1     0  1000
## 2     1  1001
## 3     2  1002
## 4     3  1003</code></pre>
<p>would they still <code>join</code>?</p>
<pre class="r"><code>full_join(dataA, dataB)</code></pre>
<pre><code>## Joining, by = &quot;X&quot;</code></pre>
<pre><code>## # A tibble: 4 x 3
##       X     Y     Z
##   &lt;dbl&gt; &lt;int&gt; &lt;int&gt;
## 1     0   100  1000
## 2     1   101  1001
## 3     2   102  1002
## 4     3   103  1003</code></pre>
<p>Okay, sure. <code>R</code> treats these as close enough to join. I mean, maybe it shouldn’t, but we’ll work with what we have. <code>R</code> doesn’t always think these are equal</p>
<pre class="r"><code>identical(0L, 0)</code></pre>
<pre><code>## [1] FALSE</code></pre>
<pre class="r"><code>identical(2L, 2)</code></pre>
<pre><code>## [1] FALSE</code></pre>
<p>though sometimes it does</p>
<pre class="r"><code>0L == 0</code></pre>
<pre><code>## [1] TRUE</code></pre>
<pre class="r"><code>2L == 2</code></pre>
<pre><code>## [1] TRUE</code></pre>
<p>(<code>==</code> coerces types before comparing). Well, what if one of these just ‘looks like’ the other value (can be coerced to the same?)</p>
<pre class="r"><code>dataC &lt;- tribble(
    ~X, ~Z,
    &quot;0&quot;, 100L,
    &quot;1&quot;, 101L,
    &quot;2&quot;, 102L,
    &quot;3&quot;, 103L
)
dataC</code></pre>
<pre><code>## # A tibble: 4 x 2
##       X     Z
##   &lt;chr&gt; &lt;int&gt;
## 1     0   100
## 2     1   101
## 3     2   102
## 4     3   103</code></pre>
<pre class="r"><code>full_join(dataA, dataC) </code></pre>
<pre><code>## Joining, by = &quot;X&quot;</code></pre>
<pre><code>## Error in full_join_impl(x, y, by$x, by$y, suffix$x, suffix$y, check_na_matches(na_matches)): Can't join on 'X' x 'X' because of incompatible types (character / integer)</code></pre>
<p>That’s probably wise. Of course, <code>R</code> is perfectly happy with things like</p>
<pre class="r"><code>&quot;2&quot;:&quot;5&quot;</code></pre>
<pre><code>## [1] 2 3 4 5</code></pre>
<p>and <code>==</code> thinks that’s fine</p>
<pre class="r"><code>&quot;0&quot; == 0L</code></pre>
<pre><code>## [1] TRUE</code></pre>
<pre class="r"><code>&quot;2&quot; == 2L</code></pre>
<pre><code>## [1] TRUE</code></pre>
<p>but who am I to argue?</p>
<p>Anyway, how far apart can those integers and numerics be before they aren’t able to be joined? What if we shift the ‘numeric in name only’ values away from the integers just a teensy bit? <code>.Machine$double.eps</code> is the built-in value for ‘the tiniest number you can produce’. On this system it’s 2.22044610^{-16}.</p>
<pre class="r"><code>dataBeps &lt;- tribble(
    ~X, ~Z,
    0 + .Machine$double.eps, 1000L,
    1 + .Machine$double.eps, 1001L,
    2 + .Machine$double.eps, 1002L,
    3 + .Machine$double.eps, 1003L
)
dataBeps</code></pre>
<pre><code>## # A tibble: 4 x 2
##              X     Z
##          &lt;dbl&gt; &lt;int&gt;
## 1 2.220446e-16  1000
## 2 1.000000e+00  1001
## 3 2.000000e+00  1002
## 4 3.000000e+00  1003</code></pre>
<pre class="r"><code>full_join(dataA, dataBeps) </code></pre>
<pre><code>## Joining, by = &quot;X&quot;</code></pre>
<pre><code>## # A tibble: 6 x 3
##              X     Y     Z
##          &lt;dbl&gt; &lt;int&gt; &lt;int&gt;
## 1 0.000000e+00   100    NA
## 2 1.000000e+00   101    NA
## 3 2.000000e+00   102  1002
## 4 3.000000e+00   103  1003
## 5 2.220446e-16    NA  1000
## 6 1.000000e+00    NA  1001</code></pre>
<p>Well, that’s… weirder. The values offset from <code>2</code> and <code>3</code> joined fine, but the <code>0</code> and <code>1</code> each got multiple copies since <code>R</code> thinks they’re different. What if we offset a little further?</p>
<pre class="r"><code>dataB2eps &lt;- tribble(
    ~X, ~Z,
    0 + 2*.Machine$double.eps, 1000L,
    1 + 2*.Machine$double.eps, 1001L,
    2 + 2*.Machine$double.eps, 1002L,
    3 + 2*.Machine$double.eps, 1003L
)
dataB2eps</code></pre>
<pre><code>## # A tibble: 4 x 2
##              X     Z
##          &lt;dbl&gt; &lt;int&gt;
## 1 4.440892e-16  1000
## 2 1.000000e+00  1001
## 3 2.000000e+00  1002
## 4 3.000000e+00  1003</code></pre>
<pre class="r"><code>full_join(dataA, dataB2eps) </code></pre>
<pre><code>## Joining, by = &quot;X&quot;</code></pre>
<pre><code>## # A tibble: 8 x 3
##              X     Y     Z
##          &lt;dbl&gt; &lt;int&gt; &lt;int&gt;
## 1 0.000000e+00   100    NA
## 2 1.000000e+00   101    NA
## 3 2.000000e+00   102    NA
## 4 3.000000e+00   103    NA
## 5 4.440892e-16    NA  1000
## 6 1.000000e+00    NA  1001
## 7 2.000000e+00    NA  1002
## 8 3.000000e+00    NA  1003</code></pre>
<p>That’s what I’d expect. So, what’s going on? Why does <code>R</code> think those numbers are the same. Let’s check with a minimal example: For each of the values <code>0:4</code>, let’s compare that integer with the same offset by <code>.Machine$double.eps</code></p>
<pre class="r"><code>suppressPackageStartupMessages(library(purrr)) ## for the 'thou shalt not for-loop' crowd
map_lgl(0:4, ~ as.integer(.x) == as.integer(.x) + .Machine$double.eps)</code></pre>
<pre><code>## [1] FALSE FALSE  TRUE  TRUE  TRUE</code></pre>
<p>And there we have it. Some sort of relative difference tolerance I suspect. In any case, the general rule to live by is to <em>never</em> compare floats. Add this to the list of reasons why.</p>