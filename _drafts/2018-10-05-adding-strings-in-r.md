---
ID: 1165
post_title: Adding strings in R
author: Jonathan Carroll
post_date: 2018-10-05 21:29:06
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
  fmt.Println(&quot;go &quot; + &quot;adds &quot; + &quot;strings&quot;)
}
&gt; &quot;go adds strings&quot;
[/code]

but this is not something natively available in R. 

[code language="r"]
&quot;this doesn't&quot; + &quot;work&quot;
#&gt; Error in &quot;this doesn't&quot; + &quot;work&quot; : 
#&gt;  non-numeric argument to binary operator
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

what's inter