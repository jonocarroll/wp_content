---
ID: 1165
post_title: Adding strings in R
author: Jonathan Carroll
post_date: 2018-10-05 21:40:58
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1165
published: false
---
This started out as a "hey, I wonder" sort of thing, but as usual, they tend to end up as interesting voyages into the deepest depths of code.

<!--more-->

<a href="http://www.happylittlescripts.com/2018/09/make-your-r-code-nicer-with-roperators.html">This post</a> came across my feed last week, referring to the <a href="https://cran.r-project.org/package=roperators">roperators package on CRAN</a>. In that post, the author introduces an infix operator from that package which 'adds' (concatenates) strings

[code language="r"]
&quot;using infix (%) operators&quot; %+% &quot;R can do simple string addition&quot;
#&gt; [1] &quot;using infix (%) operators R can do simple string addition&quot;
[/code]

This might be familiar if you use python

[code language="python"]
&gt;&gt;&gt; &quot;python &quot; + &quot;adds &quot; + &quot;strings&quot;
'python adds strings'
[/code] 

or javascript

[code language="javascript"]
&quot;javascript &quot; + &quot;also adds &quot; + &quot;strings&quot;
&quot;javascript also adds strings&quot;
[/code] 

or perhaps even go

[code language="go"]
package main

import &quot;fmt&quot;

func main() {
  fmt.Println(&quot;go &quot; + &quot;even adds &quot; + &quot;strings&quot;)
}
&gt; &quot;go even adds strings&quot;
[/code]

but this is not something natively available in R. 

[code language="r"]
&quot;this doesn't&quot; + &quot;work&quot;
#&gt; Error in &quot;this doesn't&quot; + &quot;work&quot; : 
#&gt;  non-numeric argument to binary operator
[/code]

Could it be, though? That got me wondering. My first guess was to just create a new [code]+[/code] function which <i>does</i> allow for this. The problem there is that it doesn't seem to work. The normal addition operator is

[code language="r"]
`+`
#&gt; function (e1, e2)  .Primitive(&quot;+&quot;)
[/code]

so a first attempt might be

[code language="r"]
`+` &lt;- function(e1, e2) {
  if (is.character(e1) | is.character(e2)) {
    paste0(e1, e2)
  } else {
    base::`+`(e1, e2)
  }
}
[/code]

This checks to see if the left or right side of the operator is a character-classed object, and if either is, it pastes the two together. Otherwise it just uses the 'regular' addition operator between the two arguments. This works for simple cases, e.g.

[code language="r"]
&quot;a&quot; + &quot;b&quot;
#&gt; [1] &quot;ab&quot;
&quot;a&quot; + 2
#&gt; [1] &quot;a2&quot;
2 + 2
#&gt; [1] 4
2 + &quot;a&quot;
#&gt; [1] &quot;2a&quot;
[/code]

But we hit an important snag if we try to add to character-represented numbers

[code language="r"]
&quot;200&quot; + &quot;200&quot;
#&gt; &quot;200200&quot;
[/code]

That's probably going to be an issue if we read in unformatted data (e.g. from a CSV) as characters and try to treat it like numbers. Normally this would throw the above error about not being numeric, but now we get a silent weird number-character. That's no good.

An extension to this checks whether or not we have the number-as-a-character situation and falls back to the correct interpretation in that case

[code language="r"]
`+` &lt;- function(e1, e2) {
  ## unary
  if (missing(e2)) return(e1)
  if (!is.na(suppressWarnings(as.numeric(e1))) &amp; !is.na(suppressWarnings(as.numeric(e2)))) {
    ## both arguments numeric-like but characters
    return(base::`+`(as.numeric(e1), as.numeric(e2)))
  } else if ((is.character(e1) &amp; is.na(suppressWarnings(as.numeric(e1)))) | 
             (is.character(e2) &amp; is.na(suppressWarnings(as.numeric(e2))))) {
    ## at least one true character 
    return(paste0(e1, e2))
  } else {
    ## both numeric
    return(base::`+`(e1, e2))
  }
}

&quot;a&quot; + &quot;b&quot;
#&gt; [1] &quot;ab&quot;
&quot;a&quot; + 2
#&gt; [1] &quot;a2&quot;
  2 + 2
#&gt; [1] 4
  2 + &quot;a&quot;
#&gt; [1] &quot;2a&quot;
  &quot;2&quot; + &quot;2&quot;
#&gt; [1] 4
&quot;butter&quot; + &quot;fly&quot;
#&gt; [1] &quot;butterfly&quot;
2 + &quot;edgy&quot; + 4 + &quot;me&quot;
#&gt; [1] &quot;2edgy4me&quot;
[/code] 

In R, addition is limited to particular classes of objects, defined by the Ops groups. The methods for the Ops groups describe which classes can be involved in operations involving any of the Ops group members:

"+", "-", "*", "/", "^", "%%", "%/%"

"&", "|", "!"

"==", "!=", "<", "<=", ">=", ">"

These methods are:

[code language="r"]
methods(&quot;Ops&quot;)
 [1] Ops,array,array-method               Ops,array,structure-method          
 [3] Ops,nonStructure,nonStructure-method Ops,nonStructure,vector-method      
 [5] Ops,structure,array-method           Ops,structure,structure-method      
 [7] Ops,structure,vector-method          Ops,vector,nonStructure-method      
 [9] Ops,vector,structure-method          Ops.data.frame                      
[11] Ops.data.table*                      Ops.Date                            
[13] Ops.difftime                         Ops.factor                          
[15] Ops.numeric_version                  Ops.ordered                         
[17] Ops.POSIXt                           Ops.raster*                         
[19] Ops.roman*                           Ops.ts*                             
[21] Ops.unit*   
[/code]

What's missing from this list, in order for us to be able to just use "string" + "string" is a character method.