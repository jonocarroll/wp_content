---
ID: 225
post_title: Notepad in a browser
author: Jonathan Carroll
post_date: 2013-04-11 09:55:47
post_excerpt: ""
layout: post
permalink: >
  http://jcarroll.com.au/2013/04/11/notepad-in-a-browser/
published: true
---
Type the following into the address bar of your browser to get a scratchpad. <!--more-->

[sourcecode lang="bash"]data:text/html, &lt;html contenteditable&gt;[/sourcecode]

It won't save your notes, but when you need to jot something down and you have a browser open, this is pretty useful. Note: adding that tag into your page source makes things unclickable, but editable. Take care.

From: <a href="http://www.commandlinefu.com/commands/view/12161/notepad-in-a-browser-type-this-in-the-url-bar" title="commandlinefu.com" target="_blank">commandlinefu.com</a>

Update: Better versions exist <a href="https://coderwall.com/p/lhsrcq">elsewhere</a>. For example, I now have this one bookmarked instead, which uses a better font size, pads the scratchpad over to the right, and adds a title bar. Neat!

[code lang="html"]data:text/html, &lt;title&gt;Text Editor&lt;/title&gt;&lt;body contenteditable style=&quot;font-size:2rem;line-height:1.4;max-width:100rem;margin:0 auto;padding:2rem;&quot;&gt;[/code]