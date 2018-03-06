---
ID: 1127
post_title: JC and the Vignettes
author: Jonathan Carroll
post_date: 2018-03-06 15:16:58
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1127
published: false
---
If that's not a great band name then I don't know what is (hint: I don't know what is).

<!--more-->

At the start of the year I set out my 'goals for 2018' just like many of us do; an overly ambitious list of things we'd like to do to better ourselves. My list includes improving my French to better interact with a colleague I cohabitate and work with while onsite (my 48 day streak on Duolingo was interrupted by travel... c'est un bon début); reading more books (two a month, so far so good); writing more blog posts (one a month, this one included); and interacting more with the R community. 

My original plan for the increased interaction was to pick an R package a month. I'd pick a package which didn't already have a vignette, learn the package, write a vignette, submit it as a PR, and blog about the experience. This seemed straightforward enough. There's a long-standing feeling that R too many R packages lack vignettes (note: https://juliasilge.com/blog/mining-cran-description/ -- an analysis I intend to reproduce/update). I looked through my backlog of interesting packages I meant to look at more closely and checked to see if they already had vignettes... all of them did (womp womp).

For those not familiar, vignettes in R packages are long-form documentation. Not just a listing of each function, but a good solid walkthrough of background, a use-case, examples, motivations, pitfalls, comparisons, performance metrics, and so on. Function documentation rarely provides sufficient detail like this, so vignettes are a convenient way to include some longer discussions about your package. The problem is that people either neglect to, forget to, or aren't aware that they can (and should!) write vignettes for their packages. 

Rather than admit defeat and throw another resolution on the ever-growing pile of failures, I decided to take a different approach. I sent out a request on Twitter: suggest a package which needs a vignette. It seemed to be a popular invite

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">The old argument was that <a href="https://twitter.com/hashtag/rstats?src=hash&amp;ref_src=twsrc%5Etfw">#rstats</a> packages generally lack vignettes. Someone scraped CRAN and found &#39;most&#39; (lots of?) packages don&#39;t have them.<br><br>With my book now with the copyeditors, I finally have some time to get/give back to this awesome community...</p>&mdash; Jonathan Carroll (@carroll_jono) <a href="https://twitter.com/carroll_jono/status/961139524901527552?ref_src=twsrc%5Etfw">February 7, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">So, my offer: point me towards a new(ish) package on GitHub that (a) does something cool, and (b) doesn&#39;t have a vignette. I&#39;ll learn the package inside-out, write a vignette, submit it as a PR, and blog about it. Your package, someone else&#39;s which you use, I don&#39;t mind...</p>&mdash; Jonathan Carroll (@carroll_jono) <a href="https://twitter.com/carroll_jono/status/961139533701054464?ref_src=twsrc%5Etfw">February 7, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Thus began the 'Volunteer Vignettes' program. 



How does one go about it? What tools are required? How do I include that in a package? I'm glad you asked. Over the next few months I'll be blogging about vignettes; how they're currently used, how they might be more useful, and how we might be able to get people to use them more.

For now, stay tuned!