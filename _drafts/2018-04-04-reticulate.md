---
ID: 1142
post_title: Constricted development with reticulate
author: Jonathan Carroll
post_date: 2018-04-04 22:30:50
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1142
published: false
---
I've been using the reticulate package occasionally for a while now, so I was surprised to see that it had only just been officially released. It's a brilliant piece of work, allowing python and R to coexist in the same workflow. 

<!--more-->

Another opportunity came up today to use it so I thought it might be nice to do a very quick blog post to show just how easy it is to take external python code and have it callable directly from R. In this case, @coolbutuseless posed a challenge on Twitter to write a fast 'needle in a haystack' search of a small vector inside a larger one. I looked over the existing candidates and figured some sort of <a href="https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes" rel="noopener" target="_blank">Sieve of Eratosthenes</a> might have a chance (though the name eluded me entirely at the time).


https://gist.github.com/jonocarroll/d658b5ccf33aaef150b6b36f055d2d6d#file-testbmpy-r