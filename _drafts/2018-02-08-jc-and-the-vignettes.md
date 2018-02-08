---
ID: 1127
post_title: JC and the Vignettes
author: Jonathan Carroll
post_date: 2018-02-08 21:21:24
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1127
published: false
---
If that's not a great band name then I don't know what is (hint: I don't know what is).

<!--more-->

At the start of the year I set out my 'goals for 2018' just like many of us do; an overly ambitious list of things we'd like to do to better ourselves. My list includes improving my French to better interact with a colleague I'll be cohabitating and working with (40 day streak on Duolingo so far... c'est un bon début); reading more books (two a month, so far so good); writing more blog posts (one a month, this one included); and interacting more with the R community. 

My original plan for the increased interaction was to pick a package a month. I'd pick a package which didn't already have a vignette; write it, submit it as a PR, and blog about the experience. This seemed straightforward enough. People have long complained about the lack of vignettes in R packages (LINK; Twitter?). I looked through my backlog of interesting packages I meant to look at more closely and checked to see if they already had vignettes... all of them did.

For those not familiar, vignettes in R packages are long-form documentation. Not just a listing of each function, but a good solid walkthrough of background, a use-case, examples, motivations, pitfalls, comparisons, performance metrics, and so on. Function documentation rarely provides sufficient detail like this, so vignettes are a convenient way to include some longer discussions about your package. The problem is that people either neglect to, forget to, or aren't aware that they can (and should!) write vignettes for their packages. How does one go about it? What tools are required? How do I include that in a package? I'm glad you asked.