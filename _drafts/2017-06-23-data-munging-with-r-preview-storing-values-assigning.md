---
ID: 1046
post_title: 'Data Munging with R Preview &#8211; Storing Values (Assigning)'
author: Jonathan Carroll
post_date: 2017-06-23 23:03:54
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1046
published: false
wpasciidoc_checkbox:
  - 'a:1:{i:0;s:1:"1";}'
---
<p>Since about October last year, I&#8217;ve been writing an introduction to R book. It&#8217;s
been quite the experience. I&#8217;ve finally started making time to document some of
the interesting things I&#8217;ve learned (about R, about writing, about about how to
bring those two together) along the way.</p>
<p>The book is aimed at proper beginners; people with absolutely no formal coding
experience. This tends to mean people coming from Excel who need to do more than
a spreadsheet can/should.</p>
<div align="center">
<img src="tweet.png" style="border-width: 0;" alt="tweet.png" width="400">
</div>
<p>Most of the books I&#8217;ve looked at which claim to teach programming begin with
some strong assumptions about the reader already knowing how to program, and
teach the specific syntax of some language. That&#8217;s no good if this is your first
language, so I&#8217;m working towards teaching the concepts, the language, and the
syntax (warts and all).</p>
<p>The book is currently available under the Manning Early Access Program (MEAP)
which means if you buy it you get the draft of the first three chapters right
now. If you find something you still don&#8217;t understand, or you don&#8217;t like how
I&#8217;ve written some/all of it, then jump onto the forum and let me know. I make
more edits and write more chapters, and you get updated versions. Lather, rinse,
repeat until the final version and you get a polished book which (if I&#8217;m any
good) contains what you want it to.</p>
<p>I&#8217;m genuinely interested in getting this right; I want to help people learn R. I
contribute a bit of time on Stack Overflow answering people&#8217;s questions, and
it&#8217;s very common to see questions that shouldn&#8217;t need asking. I don&#8217;t blame the
user for not knowing something (a different answer for not searching, perhaps),
but I can help make the resource they need.</p>
<p>To show that I really want people to contribute, here&#8217;s a discount code to
sweeten the deal: use <code>mlcarroll</code> for 50% off here:
<a href="https://www.manning.com/books/data-munging-with-r?a_aid=datamungingwithr&amp;a_bid=1dc44480">https://www.manning.com/books/data-munging-with-r?a_aid=datamungingwithr&amp;a_bid=1dc44480</a></p>
<p>Chapter 1 is a free download, so please check that out too! At the moment the
MEAP covers the first three chapters, but the following four aren&#8217;t too far
behind.</p>
<p>I&#8217;ll document some of the behind-the-scenes process shortly, but for now here&#8217;s
an excerpt from chapter 2:</p>
<p>## Storing Values (Assigning)</p>
<p>In order to do something with our data, we will need to tell <code>R</code> what to call
it, so that we can refer to it in our code. In programming in general, we
typically have <em>variables</em> (things that may vary) and <em>values</em> (our data). We&#8217;ve
already seen that different data <em>values</em> can have different <em>types</em>, but we
haven&#8217;t told <code>R</code> to store any of them yet. Next, we&#8217;ll create some <em>variables</em>
to store our data <em>values</em>.</p>
<p># Data (Variables)</p>
<p>If we have the values <code>4</code> and <code>8</code> and we want to do something with them, we can
use the values literally (say, add them together as <code>4 + 8</code>). You may be
familiar with this if you frequently use Excel; data values are stored in cells
(groups of which you can opt to name) and you tell the program which values you
wish to combine in some calculation by selecting the cells with the mouse or
keyboard. Alternatively, you can opt to refer to cells by their grid reference
(e.g. <code>A1</code>). Similarly to this second method, we can store values in <em>variables</em>
(things that may vary) and <em>abstract</em> away the values. In <code>R</code>, assigning of
values to variables takes the following form</p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">variable &lt;- value</pre>
</td></tr>
</table>
<p>The <em>assignment operator</em> <code>\&lt;-</code> can be thought of as storing the value/thing on
the right hand side into the name/thing on the left hand side. For example, try
typing <code>x \&lt;- 4</code> into the <code>R</code> <code>*Console*</code> then press kbd:[Enter]:</p>
<div>
<img src="variable_value.png" style="border-width: 0;" alt="Variable">
</div>
<p>You could just as easily use the equals sign to achieve this; <code>x = 4</code> but I
recommend you use <code>\&lt;-</code> for this for reasons that will become clear later.</p>
<p>You&#8217;ll notice that the <code>*Environment*</code> tab of the <code>*Workspace*</code> pane now lists
<code>x</code> under <code>*Values*</code> and shows the number 4 next to it, as shown in <a href="#fig-x_eq_4">[fig-x_eq_4]</a></p>
<div align="center">
<a name="fig-x_eq_4"></a>
<img src="fig-x_eq_4.png" style="border-width: 0;" alt="fig-x_eq_4.png" width="400">
<p><b>Figure 2. 1. </b>The <em>variable</em> <code>x</code> has been assigned the <em>value</em> <code>4</code>.</p>
</div>
<p>What happened behind the scenes was that when we pressed kbd:[Enter], <code>R</code> took
the entire expression that we entered (<code>x \&lt;- 4</code>) and evaluated it. Since we
told <code>R</code> to <em>assign</em> the value <code>4</code> to the variable <code>x</code>, <code>R</code> converted the value
<code>4</code> to binary and placed that in the computer&#8217;s memory. <code>R</code> then gives us a
reference to that place in the computer&#8217;s memory and labels it <code>x</code>. A diagram of
this process is shown in <a href="#fig-assign">[fig-assign]</a> Nothing else appeared in the
<code>*Console*</code> because the action of assigning a value doesn&#8217;t <em>return</em> anything
(we&#8217;ll cover this more in our section on functions).</p>
<p><b>Assigning a value to a variable. The value entered is converted to binary, then stored in memory, the reference to which is labelled by the variable.</b><br>![figures/assigning.png]</p>
<p>This is overly simplified, of course. Technically speaking, in <code>R</code>, names have
objects rather than the other way around. This means that <code>R</code> can be quite
memory efficient since it doesn&#8217;t create a copy of anything it doesn&#8217;t need to.</p>
<table frame="void" style="margin:0.2em 0;">
<tr valign="top">
<td style="padding:0.5em;">
<img src="./images/icons/caution.png" alt="Caution">
</td>
<td style="border-left:3px solid #e8e8e8; padding:0.5em;">
<p><b>On <em>"hidden"</em> variables</b></p>
<p>Variables which begin with a period (e.g. <code>.length</code>) are considered
<em>hidden</em> and do not appear in the <code>*Environment*</code> tab of the
<code>*Workspace*</code>. They otherwise behave exactly as any other variable; they can be
printed and manipulated. An example of one of these is the <code>.Last.value</code>
variable, which exists from the moment you load up <code>R</code> (with the value <code>TRUE</code>)&#8201;&#8212;&#8201;this contains the output value of the last statement executed (handy if you
forgot to assign it to something). There are very few reasons you&#8217;ll want to use
this feature (dot-prefixed hidden variables) on purpose at the moment, so for
now, avoid creating variable names with this pattern. The exception to the
<em>hidden</em> nature of these is again the <code>.Last.value</code> variable which you can
request to be visible in the <code>*Environment*</code> tab via
menu:Tools[Global Options&#8230; &gt; General &gt; Show .Last.value in environment listing].</p>
</td></tr></table>
<p>We can retrieve the value assigned to the variable <code>x</code> by asking <code>R</code> to print
the value of <code>x</code></p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">print(x = x)</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">#&gt; [1] 4</pre>
</td></tr>
</table>
<p>for which we have a useful shortcut&#8201;&#8212;&#8201;if your entire expression is just a
variable, <code>R</code> will assume you mean to <code>print()</code> it, so</p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">x</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">#&gt; [1] 4</pre>
</td></tr>
</table>
<p>works just the same.</p>
<p>Now, about that <code>[1]</code>: it&#8217;s important to know that in <code>R</code>, there&#8217;s no such thing
as a single value; every value is actually a <em>vector</em> of values (we&#8217;ll cover
these properly in the next chapter, but think of these as collections of values
of the same type).<br><i>[In technical terms, <code>R</code> has no <em>scalar</em> types.]</i><br>
Whenever <code>R</code> prints a value it allows for the case where the value contains more
than one number. To make this easier on the eye, it labels the first value
appearing on the line by it&#8217;s position in the collection. For collections
(vectors) with just a single value, this might appear strange, but this makes
more sense once our variables contain more values</p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;"># Print the column names of the mtcars dataset
names(x = mtcars)</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">#&gt;  [1] "mpg"  "cyl"  "disp" "hp"   "drat" "wt"   "qsec" "vs"   "am"   "gear"
#&gt; [11] "carb"</pre>
</td></tr>
</table>
<p>We can assign another variable to another value</p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">y &lt;- 8</pre>
</td></tr>
</table>
<p>There are few restrictions for what we can name our data <em>values</em>, but <code>R</code> will
complain if you try to break them. Variables should start with a letter, not a
number. Trying to create the variable <code>2b</code> will generate an error. Variables can
also start with a dot (<code>.</code>) as long as it&#8217;s not immediately followed by a
number, although you may wish to avoid doing so. The rest of the variable name
can consist of letters (upper and lower case) and numbers, but not punctutation
(except <code>.</code> or <code>_</code>) or other symbols (except the dot, though again, perferrably
not).</p>
<p>There are also certain <em>reserved words</em> that you can&#8217;t name variables as. Some
are <em>reserved</em> for built-in functions or keywords</p>
<p><code>if</code>, <code>else</code>, <code>repeat</code>, <code>while</code>, <code>function</code>, <code>for</code>, <code>in</code>, <code>next</code>, and <code>break</code>.</p>
<p>Others are <em>reserved</em> for particular values</p>
<p><code>TRUE</code>, <code>FALSE</code>, <code>NULL</code>, <code>Inf</code>, <code>NaN</code>, <code>NA</code>, <code>NA_integer_</code>, <code>NA_real_</code>,
<code>NA_complex_</code>, and <code>NA_character_</code>.</p>
<p>We&#8217;ll come back to what each of these means, but for now you just need to know
that you can&#8217;t create a variable with one of those names.</p>
<table frame="void" style="margin:0.2em 0;">
<tr valign="top">
<td style="padding:0.5em;">
<img src="./images/icons/caution.png" alt="Caution">
</td>
<td style="border-left:3px solid #e8e8e8; padding:0.5em;">
<p><b>On overwriting names</b></p>
<p>What you <strong>can</strong> do however, which you may wish to take care with, is <em>overwrite</em>
the in-built names of variables and functions. By default, the value <code>pi</code> is
available (&#960; = 3.141593).</p>
<p>If you were translating an equation into code, and wanted to enter the value
<em>p<sub>i</sub></em> you might accidentally call it <code>pi</code> and in doing so change the default
value, causing all sorts of trouble when you next go to use it or call a
function you&#8217;ve written which expects it to still be the default.</p>
<p>The default value can still be accessed by specifying the package in which it is
defined, separated by two colons (<code>::</code>). In the case of <code>pi</code>, this is the <code>base</code>
package.</p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">pi &lt;- 3L #<b>&lt;1&gt;</b>
base::pi #<b>&lt;2&gt;</b></pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">#&gt; [1] 3.141593</pre>
</td></tr>
</table>
<ol>
<li>
Re-defining <code>pi</code> to be equal to exactly <code>3</code>
</li>
<li>
The default, correct value is still available.
</li>
</ol>
<p>This is also an issue for functions, with the same solution; specify the package
in which it is defined to use that definition. We&#8217;ll return to this in
<a href="#SS-Scope">Scope</a>.</p>
</td></tr></table>
<p>We&#8217;ll cover how to do things to our variables in more detail in the next
section, but for now let&#8217;s see what happens if we add our variables <code>x</code> and <code>y</code>
in the same way as we did for our regular numbers</p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">x + y</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">#&gt; [1] 12</pre>
</td></tr>
</table>
<p>which is what we got when we added these numbers explicitly. Note that since our
expression produces just a number (no assigment), the value is printed. We&#8217;ll
cover how to add and subtract values in more depth in <a href="#SS-math">Basic Mathematics</a>.</p>
<p><code>R</code> has no problems with overwriting these values, and it doesn&#8217;t mind what data
you overwrite these with.<br><i>[This is where the distinction of <em>weakly
typed</em> becomes important - in a <em>strongly typed</em> language you would not be able
to arbitrarily change the type of a variable.]</i><br></p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">y &lt;- 'banana'
y</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">#&gt; [1] "banana"</pre>
</td></tr>
</table>
<p><code>R</code> is <em>case-sensitive</em>, which means that it treats <code>a</code> and <code>A</code> as distinct
names. You can have a variable named <code>myVariable</code> and another named <code>MYvariable</code>
and another named <code>myVARIABLE</code> and <code>R</code> will hold the value assigned to each
independently.</p>
<blockquote>
<p><b>On variable names</b></p>There are only two hard things in Computer Science: cache invalidation and naming things.<p align="right">
<em>Principal Curmudgeon Netscape Communications Corporation</em><br>
&#8212; Phil Karlton
</p>
</blockquote>
<p>I said earlier that <code>R</code> won&#8217;t keep track of your units so it&#8217;s a good idea to
name your variables in a way that makes logical sense, is meaningful, and will
help you remember what it represents. Variables <code>x</code> and <code>y</code> are fine for playing
around with values, but aren&#8217;t particularly meaningful if your data represents
speeds, where you may want to use something like <code>speed_kmph</code> for speeds in
kilometers per hour. Underscores (<code>_</code>) are allowed in variable names, but
whether or not you use them is up to you. Some programmers prefer to name
variables in this way (sometimes referred to as <em>snake_case</em>), others prefer
<em>CamelCase</em>. The use of periods (dots, <code>.</code>) to separate words is discouraged for
reasons beyond the scope of this book.<br><i>[This syntax is already used
within <code>R</code> to denote functions acting on a specific class, such as
<code>print.Date()</code>.]</i><br></p>
<table frame="void" style="margin:0.2em 0;">
<tr valign="top">
<td style="padding:0.5em;">
<img src="./images/icons/important.png" alt="Important">
</td>
<td style="border-left:3px solid #e8e8e8; padding:0.5em;">
<p><b>Naming things</b></p>
<p>Be careful when naming your variables. Make them meaningful and
concise. In six months from now, will you remember what <code>data_17</code> corresponds
to? Tomorrow, will you remember that <code>newdata</code> was updated twice?</p>
</td></tr></table>
<p># Unchanging Data</p>
<p>If you&#8217;re familiar with working with data in a spreadsheet program (such as
Excel), you may expect your variables to behave in a way that they
won&#8217;t. Automatic recalculation is a very useful feature of spreadsheet programs,
but it&#8217;s not how <code>R</code> behaves.</p>
<p>If we assign our two variables, then add them, we can save that result to
another variable</p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">a &lt;- 4
b &lt;- 8
sum_of_a_and_b &lt;- a + b</pre>
</td></tr>
</table>
<p>This has the value we expect</p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">print(x = sum_of_a_and_b)</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">#&gt; [1] 12</pre>
</td></tr>
</table>
<p>Now, if we <em>change</em> one of these values</p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">b &lt;- 2</pre>
</td></tr>
</table>
<p>this has <strong>no impact</strong> on the value of the variable we created to hold the sum
earlier</p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">print(x = sum_of_a_and_b)</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">#&gt; [1] 12</pre>
</td></tr>
</table>
<p>Once the sum was calculated, and that value stored in a variable, the connection
to the original values was lost. This makes things <em>reliable</em> because you know
for sure what value a variable will have at any point in your calculation by
following the steps that lead to it, whereas a spreadsheet depends much more on
its current overall <em>state</em>.</p>
<p># Assigmnent Operators (<code>\&lt;-</code> vs <code>=</code>)</p>
<p>If you&#8217;ve read some <code>R</code> code already, you&#8217;ve possibly seen that both <code>\&lt;-</code> and
<code>=</code> are used to assign values to objects, and this tends to cause some
confusion. Technically, <code>R</code> will accept either when assigning variables, so in
that respect it comes down to a matter of style (I still highly reccomend
assigning with <code>\&lt;-</code>). The big difference comes when using functions that take
<em>arguments</em>&#8201;&#8212;&#8201;there you should only use <code>=</code> to specify what the <em>value</em> of the
<em>argument</em>. For example, when we inspected the <code>mtcars</code> data, we could
specify a string with which to indent the output</p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">str(object = mtcars, indent.str = '&gt;&gt;  ')</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">#&gt; 'data.frame':        32 obs. of  11 variables:
#&gt; &gt;&gt;  $ mpg : num  21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
#&gt; &gt;&gt;  $ cyl : num  6 6 4 6 8 6 8 4 4 6 ...
#&gt; &gt;&gt;  $ disp: num  160 160 108 258 360 ...
#&gt; &gt;&gt;  $ hp  : num  110 110 93 110 175 105 245 62 95 123 ...
#&gt; &gt;&gt;  $ drat: num  3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
#&gt; &gt;&gt;  $ wt  : num  2.62 2.88 2.32 3.21 3.44 ...
#&gt; &gt;&gt;  $ qsec: num  16.5 17 18.6 19.4 17 ...
#&gt; &gt;&gt;  $ vs  : num  0 0 1 1 0 1 0 1 1 1 ...
#&gt; &gt;&gt;  $ am  : num  1 1 1 0 0 0 0 0 0 0 ...
#&gt; &gt;&gt;  $ gear: num  4 4 4 3 3 3 3 4 4 4 ...
#&gt; &gt;&gt;  $ carb: num  4 4 1 1 2 1 4 2 2 4 ...</pre>
</td></tr>
</table>
<p>If we had used <code>\&lt;-</code> instead of <code>=</code> for either argument, then <code>R</code> would treat
that as creating a new variable <code>object</code> or <code>indent.str</code> with value <code>mtcars</code> or
<code>'&gt;&gt; '</code> respectively, which isn&#8217;t what we want.</p>
<table frame="void" style="margin:0.2em 0;">
<tr valign="top">
<td style="padding:0.5em;">
<img src="./images/icons/warning.png" alt="Warning">
</td>
<td style="border-left:3px solid #e8e8e8; padding:0.5em;">
<p><b>Assigning to variables.</b></p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">score &lt;- 4.8
score</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">#&gt; [1] 4.8</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">str(object = score)</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">#&gt;  num 4.8</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">fruit &lt;- 'banana'
fruit</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">#&gt; [1] "banana"</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">str(object = fruit)</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">#&gt;  chr "banana"</pre>
</td></tr>
</table>
</td></tr></table>
<p>Note that we didn&#8217;t need to tell <code>R</code> that one of these was a number and one was
a string, it figured that out itself. It&#8217;s good practice (and easier to read) to
make your <code>\&lt;-</code> line up vertically when defining several variables:</p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">first_name &lt;- 'John'
last_name  &lt;- 'Smith'
top_points &lt;- 23</pre>
</td></tr>
</table>
<p>but only if this can be achieved without adding too many spaces (exactly how
many is too many is up to you).</p>
<table frame="void" style="margin:0.2em 0;">
<tr valign="top">
<td style="padding:0.5em;">
<img src="./images/icons/caution.png" alt="Caution">
</td>
<td style="border-left:3px solid #e8e8e8; padding:0.5em;">
<p><b>Watch this space!</b><br>An extra space can make a big difference to the syntax. Compare:</p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">a &lt;- 3</pre>
</td></tr>
</table>
<p>with</p>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">a &lt; - 3</pre>
</td></tr>
</table>
<table border="0" bgcolor="#e8e8e8" width="100%" style="margin:0.2em 0;">
<tr><td style="padding:0.5em;">
<pre style="margin:0; padding:0;">#&gt; [1] FALSE</pre>
</td></tr>
</table>
<p>In the first case we assigned the value <code>3</code> to the variable <code>a</code> (which returns
nothing). In the second case, with a wayward space, we <em>compared</em> <code>a</code> to the
value <code>-3</code> which returns <code>FALSE</code> (I&#8217;ll explain why that works at all, later).</p>
</td></tr></table>
<p>Now that we know how to provide some data to <code>R</code>, what if we want to explicitly
tell <code>R</code> that our data should be of a specific type, or we want to convert our
data to a different type? That&#8217;s an article for another day.</p>
<p>If you&#8217;re interested in seeing more, and hopefully providing feedback on what
you do/don&#8217;t like about it, then use the discount code <code>mlcarroll</code> here
<a href="https://www.manning.com/books/data-munging-with-r?a_aid=datamungingwithr&amp;a_bid=1dc44480">https://www.manning.com/books/data-munging-with-r?a_aid=datamungingwithr&amp;a_bid=1dc44480</a>
for 50% off and get reading!</p>