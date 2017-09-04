---
ID: 1106
post_title: An integer by any other name
author: Jonathan Carroll
post_date: 2017-09-04 14:26:18
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1106
published: false
---
<p>This was just going to be a few Tweets but it ended up being a bit of a rollercoaster of learning for me, and I haven’t blogged in far too long, so I’m writing it up quickly as a ‘hey look at that’ example for newcomers.</p>
<p>I’ve been working on the ‘merging data’ part of my book and, as I do when I’m writing this stuff, I had a play around with some examples to see if there was anything funky going on if a reader was to try something slightly different. I’ve been using <code>dplyr</code> for the examples after being thoroughly convinced on Twitter to do so. It’s going well. Mostly.</p>

[code language="r"]## if you haven't already done so, load dplyr
suppressPackageStartupMessages(library(dplyr))[/code]

<p>My example involved joining together two <code>tibble</code>s containing text values. Nothing too surprising. I wondered though; do numbers behave the way I expect?</p>
<p>If I had a <code>tibble</code> where the column I would use to <code>join</code> had integers</p>
[code language="r"]dataA &amp;lt;- tribble(
    ~X, ~Y,
    0L, 100L,
    1L, 101L,
    2L, 102L,
    3L, 103L
)
dataA[/code]
[code language="r"]## # A tibble: 4 x 2
##       X     Y
##   &amp;lt;int&amp;gt; &amp;lt;int&amp;gt;
## 1     0   100
## 2     1   101
## 3     2   102
## 4     3   103[/code]
<p>and another <code>tibble</code> with <code>numeric</code> in that column</p>
[code language="r"]dataB &amp;lt;- tribble(
    ~X, ~Z,
    0, 1000L,
    1, 1001L,
    2, 1002L,
    3, 1003L
)
dataB[/code]
[code language="r"]## # A tibble: 4 x 2
##       X     Z
##   &amp;lt;dbl&amp;gt; &amp;lt;int&amp;gt;
## 1     0  1000
## 2     1  1001
## 3     2  1002
## 4     3  1003[/code]
<p>would they still <code>join</code>?</p>
[code language="r"]full_join(dataA, dataB)[/code]
[code language="r"]## Joining, by = &amp;quot;X&amp;quot;[/code]
[code language="r"]## # A tibble: 4 x 3
##       X     Y     Z
##   &amp;lt;dbl&amp;gt; &amp;lt;int&amp;gt; &amp;lt;int&amp;gt;
## 1     0   100  1000
## 2     1   101  1001
## 3     2   102  1002
## 4     3   103  1003[/code]
<p>Okay, sure. <code>R</code> treats these as close enough to join. I mean, maybe it shouldn’t, but we’ll work with what we have. <code>R</code> doesn’t always think these are equal</p>
[code language="r"]identical(0L, 0)[/code]
[code language="r"]## [1] FALSE[/code]
[code language="r"]identical(2L, 2)[/code]
[code language="r"]## [1] FALSE[/code]
<p>though sometimes it does</p>
[code language="r"]0L == 0[/code]
[code language="r"]## [1] TRUE[/code]
[code language="r"]2L == 2[/code]
[code language="r"]## [1] TRUE[/code]
<p>([code language="r"]==[/code] coerces types before comparing). Well, what if one of these just ‘looks like’ the other value (can be coerced to the same?)</p>
[code language="r"]dataC &amp;lt;- tribble(
    ~X, ~Z,
    &amp;quot;0&amp;quot;, 100L,
    &amp;quot;1&amp;quot;, 101L,
    &amp;quot;2&amp;quot;, 102L,
    &amp;quot;3&amp;quot;, 103L
)
dataC[/code]
[code language="r"]## # A tibble: 4 x 2
##       X     Z
##   &amp;lt;chr&amp;gt; &amp;lt;int&amp;gt;
## 1     0   100
## 2     1   101
## 3     2   102
## 4     3   103[/code]
[code language="r"]full_join(dataA, dataC) [/code]
[code language="r"]## Joining, by = &amp;quot;X&amp;quot;[/code]
[code language="r"]## Error in full_join_impl(x, y, by$x, by$y, suffix$x, suffix$y, check_na_matches(na_matches)): Can't join on 'X' x 'X' because of incompatible types (character / integer)[/code]
<p>That’s probably wise. Of course, <code>R</code> is perfectly happy with things like</p>
[code language="r"]&amp;quot;2&amp;quot;:&amp;quot;5&amp;quot;[/code]
[code language="r"]## [1] 2 3 4 5[/code]
<p>and <code>==</code> thinks that’s fine</p>
[code language="r"]&amp;quot;0&amp;quot; == 0L[/code]
[code language="r"]## [1] TRUE[/code]
[code language="r"]&amp;quot;2&amp;quot; == 2L[/code]
[code language="r"]## [1] TRUE[/code]
<p>but who am I to argue?</p>
<p>Anyway, how far apart can those integers and numerics be before they aren’t able to be joined? What if we shift the ‘numeric in name only’ values away from the integers just a teensy bit? <code>.Machine$double.eps</code> is the built-in value for ‘the tiniest number you can produce’. On this system it’s 2.22044610^{-16}.</p>
[code language="r"]dataBeps &amp;lt;- tribble(
    ~X, ~Z,
    0 + .Machine$double.eps, 1000L,
    1 + .Machine$double.eps, 1001L,
    2 + .Machine$double.eps, 1002L,
    3 + .Machine$double.eps, 1003L
)
dataBeps[/code]
[code language="r"]## # A tibble: 4 x 2
##              X     Z
##          &amp;lt;dbl&amp;gt; &amp;lt;int&amp;gt;
## 1 2.220446e-16  1000
## 2 1.000000e+00  1001
## 3 2.000000e+00  1002
## 4 3.000000e+00  1003[/code]
[code language="r"]full_join(dataA, dataBeps) [/code]
[code language="r"]## Joining, by = &amp;quot;X&amp;quot;[/code]
[code language="r"]## # A tibble: 6 x 3
##              X     Y     Z
##          &amp;lt;dbl&amp;gt; &amp;lt;int&amp;gt; &amp;lt;int&amp;gt;
## 1 0.000000e+00   100    NA
## 2 1.000000e+00   101    NA
## 3 2.000000e+00   102  1002
## 4 3.000000e+00   103  1003
## 5 2.220446e-16    NA  1000
## 6 1.000000e+00    NA  1001[/code]
<p>Well, that’s… weirder. The values offset from <code>2</code> and <code>3</code> joined fine, but the <code>0</code> and <code>1</code> each got multiple copies since <code>R</code> thinks they’re different. What if we offset a little further?</p>
[code language="r"]dataB2eps &amp;lt;- tribble(
    ~X, ~Z,
    0 + 2*.Machine$double.eps, 1000L,
    1 + 2*.Machine$double.eps, 1001L,
    2 + 2*.Machine$double.eps, 1002L,
    3 + 2*.Machine$double.eps, 1003L
)
dataB2eps[/code]
[code language="r"]## # A tibble: 4 x 2
##              X     Z
##          &amp;lt;dbl&amp;gt; &amp;lt;int&amp;gt;
## 1 4.440892e-16  1000
## 2 1.000000e+00  1001
## 3 2.000000e+00  1002
## 4 3.000000e+00  1003[/code]
[code language="r"]full_join(dataA, dataB2eps)[/code]
[code language="r"]## Joining, by = &amp;quot;X&amp;quot;[/code]
[code language="r"]## # A tibble: 8 x 3
##              X     Y     Z
##          &amp;lt;dbl&amp;gt; &amp;lt;int&amp;gt; &amp;lt;int&amp;gt;
## 1 0.000000e+00   100    NA
## 2 1.000000e+00   101    NA
## 3 2.000000e+00   102    NA
## 4 3.000000e+00   103    NA
## 5 4.440892e-16    NA  1000
## 6 1.000000e+00    NA  1001
## 7 2.000000e+00    NA  1002
## 8 3.000000e+00    NA  1003[/code]
<p>That’s what I’d expect. So, what’s going on? Why does <code>R</code> think those numbers are the same. Let’s check with a minimal example: For each of the values <code>0:4</code>, let’s compare that integer with the same offset by <code>.Machine$double.eps</code></p>
[code language="r"]suppressPackageStartupMessages(library(purrr)) ## for the 'thou shalt not for-loop' crowd
map_lgl(0:4, ~ as.integer(.x) == as.integer(.x) + .Machine$double.eps)[/code]
[code language="r"]## [1] FALSE FALSE  TRUE  TRUE  TRUE[/code]
<p>And there we have it. Some sort of relative difference tolerance I suspect. In any case, the general rule to live by is to <em>never</em> compare floats. Add this to the list of reasons why.</p>