---
ID: 1142
post_title: Constricted development with reticulate
author: Jonathan Carroll
post_date: 2018-04-04 22:41:27
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1142
published: false
---
I've been using the reticulate package occasionally for a while now, so I was surprised to see that it had only just been officially released. It's a brilliant piece of work, allowing python and R to coexist in the same workflow. 

<!--more-->

Another opportunity came up today to use it so I thought it might be nice to do a very quick blog post to show just how easy it is to take external python code and have it callable directly from R. In this case, @coolbutuseless posed a challenge on Twitter to write a fast 'needle in a haystack' search of a small vector inside a larger one. I looked over the existing candidates and figured some sort of <a href="https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes" rel="noopener" target="_blank">Sieve of Eratosthenes</a>-esque algorithm might have a chance (though the name eluded me entirely at the time). 

My proposal was to search for the first digit using <code>which()</code>, and use this reduced vector of possible-matches in additional tests on the remaining parts of the 'needle'. @coolbutuseless refactored my attempt allowing for arbitrary length needles and found it to do quite well against the current offerings. What he still wanted though was a <a href="https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_string_search_algorithm" rel="noopener" target="_blank">Boyer–Moore string search algorithm</a> implementation. This is apparently what <a href="https://lists.freebsd.org/pipermail/freebsd-current/2010-August/019310.html" rel="noopener" target="_blank">GNU <code>grep</code> uses</a>, so it's probably pretty okay.

I wasn't about to write one of those myself in R, so naturally people think of C. There's a C implementation on the Wikipedia site, so that seems like a nice place to start. I <a href="https://gist.github.com/jonocarroll/d658b5ccf33aaef150b6b36f055d2d6d#file-boyermoore-c">saved the text</a> to a new <code>boyermoore.c</code> file and ran 

<code>
R CMD SHLIB boyermoore.c 
</code>

from a terminal to compile it into <code>boyermore.so</code>. This could then be loaded into R with <code>dyn.load("boyermore.so")</code> and in theory called with <code>.C("boyer_moore(<something>, <something>))</code>. I tried a <code><something></code> (which wasn't a pointer) and promptly crashed RStudio.

https://gist.github.com/jonocarroll/d658b5ccf33aaef150b6b36f055d2d6d#file-testbmpy-r