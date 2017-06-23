---
ID: 1046
post_title: 'Data Munging with R Preview &#8211; Storing Values (Assigning)'
author: Jonathan Carroll
post_date: 2017-06-23 23:00:31
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1046
published: false
wpasciidoc_checkbox:
  - 'a:1:{i:0;s:1:"1";}'
---
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN"
    "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
<head>
<meta http-equiv="Content-Type" content="application/xhtml+xml; charset=UTF-8" />
<meta name="generator" content="AsciiDoc 8.6.9" />
<title></title>
<style type="text/css">
/* Shared CSS for AsciiDoc xhtml11 and html5 backends */

/* Default font. */
body {
  font-family: Georgia,serif;
}

/* Title font. */
h1, h2, h3, h4, h5, h6,
div.title, caption.title,
thead, p.table.header,
#toctitle,
#author, #revnumber, #revdate, #revremark,
#footer {
  font-family: Arial,Helvetica,sans-serif;
}

body {
  margin: 1em 5% 1em 5%;
}

a {
  color: blue;
  text-decoration: underline;
}
a:visited {
  color: fuchsia;
}

em {
  font-style: italic;
  color: navy;
}

strong {
  font-weight: bold;
  color: #083194;
}

h1, h2, h3, h4, h5, h6 {
  color: #527bbd;
  margin-top: 1.2em;
  margin-bottom: 0.5em;
  line-height: 1.3;
}

h1, h2, h3 {
  border-bottom: 2px solid silver;
}
h2 {
  padding-top: 0.5em;
}
h3 {
  float: left;
}
h3 + * {
  clear: left;
}
h5 {
  font-size: 1.0em;
}

div.sectionbody {
  margin-left: 0;
}

hr {
  border: 1px solid silver;
}

p {
  margin-top: 0.5em;
  margin-bottom: 0.5em;
}

ul, ol, li > p {
  margin-top: 0;
}
ul > li     { color: #aaa; }
ul > li > * { color: black; }

.monospaced, code, pre {
  font-family: "Courier New", Courier, monospace;
  font-size: inherit;
  color: navy;
  padding: 0;
  margin: 0;
}
pre {
  white-space: pre-wrap;
}

#author {
  color: #527bbd;
  font-weight: bold;
  font-size: 1.1em;
}
#email {
}
#revnumber, #revdate, #revremark {
}

#footer {
  font-size: small;
  border-top: 2px solid silver;
  padding-top: 0.5em;
  margin-top: 4.0em;
}
#footer-text {
  float: left;
  padding-bottom: 0.5em;
}
#footer-badges {
  float: right;
  padding-bottom: 0.5em;
}

#preamble {
  margin-top: 1.5em;
  margin-bottom: 1.5em;
}
div.imageblock, div.exampleblock, div.verseblock,
div.quoteblock, div.literalblock, div.listingblock, div.sidebarblock,
div.admonitionblock {
  margin-top: 1.0em;
  margin-bottom: 1.5em;
}
div.admonitionblock {
  margin-top: 2.0em;
  margin-bottom: 2.0em;
  margin-right: 10%;
  color: #606060;
}

div.content { /* Block element content. */
  padding: 0;
}

/* Block element titles. */
div.title, caption.title {
  color: #527bbd;
  font-weight: bold;
  text-align: left;
  margin-top: 1.0em;
  margin-bottom: 0.5em;
}
div.title + * {
  margin-top: 0;
}

td div.title:first-child {
  margin-top: 0.0em;
}
div.content div.title:first-child {
  margin-top: 0.0em;
}
div.content + div.title {
  margin-top: 0.0em;
}

div.sidebarblock > div.content {
  background: #ffffee;
  border: 1px solid #dddddd;
  border-left: 4px solid #f0f0f0;
  padding: 0.5em;
}

div.listingblock > div.content {
  border: 1px solid #dddddd;
  border-left: 5px solid #f0f0f0;
  background: #f8f8f8;
  padding: 0.5em;
}

div.quoteblock, div.verseblock {
  padding-left: 1.0em;
  margin-left: 1.0em;
  margin-right: 10%;
  border-left: 5px solid #f0f0f0;
  color: #888;
}

div.quoteblock > div.attribution {
  padding-top: 0.5em;
  text-align: right;
}

div.verseblock > pre.content {
  font-family: inherit;
  font-size: inherit;
}
div.verseblock > div.attribution {
  padding-top: 0.75em;
  text-align: left;
}
/* DEPRECATED: Pre version 8.2.7 verse style literal block. */
div.verseblock + div.attribution {
  text-align: left;
}

div.admonitionblock .icon {
  vertical-align: top;
  font-size: 1.1em;
  font-weight: bold;
  text-decoration: underline;
  color: #527bbd;
  padding-right: 0.5em;
}
div.admonitionblock td.content {
  padding-left: 0.5em;
  border-left: 3px solid #dddddd;
}

div.exampleblock > div.content {
  border-left: 3px solid #dddddd;
  padding-left: 0.5em;
}

div.imageblock div.content { padding-left: 0; }
span.image img { border-style: none; vertical-align: text-bottom; }
a.image:visited { color: white; }

dl {
  margin-top: 0.8em;
  margin-bottom: 0.8em;
}
dt {
  margin-top: 0.5em;
  margin-bottom: 0;
  font-style: normal;
  color: navy;
}
dd > *:first-child {
  margin-top: 0.1em;
}

ul, ol {
    list-style-position: outside;
}
ol.arabic {
  list-style-type: decimal;
}
ol.loweralpha {
  list-style-type: lower-alpha;
}
ol.upperalpha {
  list-style-type: upper-alpha;
}
ol.lowerroman {
  list-style-type: lower-roman;
}
ol.upperroman {
  list-style-type: upper-roman;
}

div.compact ul, div.compact ol,
div.compact p, div.compact p,
div.compact div, div.compact div {
  margin-top: 0.1em;
  margin-bottom: 0.1em;
}

tfoot {
  font-weight: bold;
}
td > div.verse {
  white-space: pre;
}

div.hdlist {
  margin-top: 0.8em;
  margin-bottom: 0.8em;
}
div.hdlist tr {
  padding-bottom: 15px;
}
dt.hdlist1.strong, td.hdlist1.strong {
  font-weight: bold;
}
td.hdlist1 {
  vertical-align: top;
  font-style: normal;
  padding-right: 0.8em;
  color: navy;
}
td.hdlist2 {
  vertical-align: top;
}
div.hdlist.compact tr {
  margin: 0;
  padding-bottom: 0;
}

.comment {
  background: yellow;
}

.footnote, .footnoteref {
  font-size: 0.8em;
}

span.footnote, span.footnoteref {
  vertical-align: super;
}

#footnotes {
  margin: 20px 0 20px 0;
  padding: 7px 0 0 0;
}

#footnotes div.footnote {
  margin: 0 0 5px 0;
}

#footnotes hr {
  border: none;
  border-top: 1px solid silver;
  height: 1px;
  text-align: left;
  margin-left: 0;
  width: 20%;
  min-width: 100px;
}

div.colist td {
  padding-right: 0.5em;
  padding-bottom: 0.3em;
  vertical-align: top;
}
div.colist td img {
  margin-top: 0.3em;
}

@media print {
  #footer-badges { display: none; }
}

#toc {
  margin-bottom: 2.5em;
}

#toctitle {
  color: #527bbd;
  font-size: 1.1em;
  font-weight: bold;
  margin-top: 1.0em;
  margin-bottom: 0.1em;
}

div.toclevel0, div.toclevel1, div.toclevel2, div.toclevel3, div.toclevel4 {
  margin-top: 0;
  margin-bottom: 0;
}
div.toclevel2 {
  margin-left: 2em;
  font-size: 0.9em;
}
div.toclevel3 {
  margin-left: 4em;
  font-size: 0.9em;
}
div.toclevel4 {
  margin-left: 6em;
  font-size: 0.9em;
}

span.aqua { color: aqua; }
span.black { color: black; }
span.blue { color: blue; }
span.fuchsia { color: fuchsia; }
span.gray { color: gray; }
span.green { color: green; }
span.lime { color: lime; }
span.maroon { color: maroon; }
span.navy { color: navy; }
span.olive { color: olive; }
span.purple { color: purple; }
span.red { color: red; }
span.silver { color: silver; }
span.teal { color: teal; }
span.white { color: white; }
span.yellow { color: yellow; }

span.aqua-background { background: aqua; }
span.black-background { background: black; }
span.blue-background { background: blue; }
span.fuchsia-background { background: fuchsia; }
span.gray-background { background: gray; }
span.green-background { background: green; }
span.lime-background { background: lime; }
span.maroon-background { background: maroon; }
span.navy-background { background: navy; }
span.olive-background { background: olive; }
span.purple-background { background: purple; }
span.red-background { background: red; }
span.silver-background { background: silver; }
span.teal-background { background: teal; }
span.white-background { background: white; }
span.yellow-background { background: yellow; }

span.big { font-size: 2em; }
span.small { font-size: 0.6em; }

span.underline { text-decoration: underline; }
span.overline { text-decoration: overline; }
span.line-through { text-decoration: line-through; }

div.unbreakable { page-break-inside: avoid; }


/*
 * xhtml11 specific
 *
 * */

div.tableblock {
  margin-top: 1.0em;
  margin-bottom: 1.5em;
}
div.tableblock > table {
  border: 3px solid #527bbd;
}
thead, p.table.header {
  font-weight: bold;
  color: #527bbd;
}
p.table {
  margin-top: 0;
}
/* Because the table frame attribute is overriden by CSS in most browsers. */
div.tableblock > table[frame="void"] {
  border-style: none;
}
div.tableblock > table[frame="hsides"] {
  border-left-style: none;
  border-right-style: none;
}
div.tableblock > table[frame="vsides"] {
  border-top-style: none;
  border-bottom-style: none;
}


/*
 * html5 specific
 *
 * */

table.tableblock {
  margin-top: 1.0em;
  margin-bottom: 1.5em;
}
thead, p.tableblock.header {
  font-weight: bold;
  color: #527bbd;
}
p.tableblock {
  margin-top: 0;
}
table.tableblock {
  border-width: 3px;
  border-spacing: 0px;
  border-style: solid;
  border-color: #527bbd;
  border-collapse: collapse;
}
th.tableblock, td.tableblock {
  border-width: 1px;
  padding: 4px;
  border-style: solid;
  border-color: #527bbd;
}

table.tableblock.frame-topbot {
  border-left-style: hidden;
  border-right-style: hidden;
}
table.tableblock.frame-sides {
  border-top-style: hidden;
  border-bottom-style: hidden;
}
table.tableblock.frame-none {
  border-style: hidden;
}

th.tableblock.halign-left, td.tableblock.halign-left {
  text-align: left;
}
th.tableblock.halign-center, td.tableblock.halign-center {
  text-align: center;
}
th.tableblock.halign-right, td.tableblock.halign-right {
  text-align: right;
}

th.tableblock.valign-top, td.tableblock.valign-top {
  vertical-align: top;
}
th.tableblock.valign-middle, td.tableblock.valign-middle {
  vertical-align: middle;
}
th.tableblock.valign-bottom, td.tableblock.valign-bottom {
  vertical-align: bottom;
}


/*
 * manpage specific
 *
 * */

body.manpage h1 {
  padding-top: 0.5em;
  padding-bottom: 0.5em;
  border-top: 2px solid silver;
  border-bottom: 2px solid silver;
}
body.manpage h2 {
  border-style: none;
}
body.manpage div.sectionbody {
  margin-left: 3em;
}

@media print {
  body.manpage div#toc { display: none; }
}
.highlight .hll { background-color: #ffffcc }
.highlight  { background: #f8f8f8; }
.highlight .c { color: #408080; font-style: italic } /* Comment */
.highlight .err { border: 1px solid #FF0000 } /* Error */
.highlight .k { color: #008000; font-weight: bold } /* Keyword */
.highlight .o { color: #666666 } /* Operator */
.highlight .cm { color: #408080; font-style: italic } /* Comment.Multiline */
.highlight .cp { color: #BC7A00 } /* Comment.Preproc */
.highlight .c1 { color: #408080; font-style: italic } /* Comment.Single */
.highlight .cs { color: #408080; font-style: italic } /* Comment.Special */
.highlight .gd { color: #A00000 } /* Generic.Deleted */
.highlight .ge { font-style: italic } /* Generic.Emph */
.highlight .gr { color: #FF0000 } /* Generic.Error */
.highlight .gh { color: #000080; font-weight: bold } /* Generic.Heading */
.highlight .gi { color: #00A000 } /* Generic.Inserted */
.highlight .go { color: #808080 } /* Generic.Output */
.highlight .gp { color: #000080; font-weight: bold } /* Generic.Prompt */
.highlight .gs { font-weight: bold } /* Generic.Strong */
.highlight .gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.highlight .gt { color: #0040D0 } /* Generic.Traceback */
.highlight .kc { color: #008000; font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: #008000; font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: #008000; font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: #008000 } /* Keyword.Pseudo */
.highlight .kr { color: #008000; font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: #B00040 } /* Keyword.Type */
.highlight .m { color: #666666 } /* Literal.Number */
.highlight .s { color: #BA2121 } /* Literal.String */
.highlight .na { color: #7D9029 } /* Name.Attribute */
.highlight .nb { color: #008000 } /* Name.Builtin */
.highlight .nc { color: #0000FF; font-weight: bold } /* Name.Class */
.highlight .no { color: #880000 } /* Name.Constant */
.highlight .nd { color: #AA22FF } /* Name.Decorator */
.highlight .ni { color: #999999; font-weight: bold } /* Name.Entity */
.highlight .ne { color: #D2413A; font-weight: bold } /* Name.Exception */
.highlight .nf { color: #0000FF } /* Name.Function */
.highlight .nl { color: #A0A000 } /* Name.Label */
.highlight .nn { color: #0000FF; font-weight: bold } /* Name.Namespace */
.highlight .nt { color: #008000; font-weight: bold } /* Name.Tag */
.highlight .nv { color: #19177C } /* Name.Variable */
.highlight .ow { color: #AA22FF; font-weight: bold } /* Operator.Word */
.highlight .w { color: #bbbbbb } /* Text.Whitespace */
.highlight .mf { color: #666666 } /* Literal.Number.Float */
.highlight .mh { color: #666666 } /* Literal.Number.Hex */
.highlight .mi { color: #666666 } /* Literal.Number.Integer */
.highlight .mo { color: #666666 } /* Literal.Number.Oct */
.highlight .sb { color: #BA2121 } /* Literal.String.Backtick */
.highlight .sc { color: #BA2121 } /* Literal.String.Char */
.highlight .sd { color: #BA2121; font-style: italic } /* Literal.String.Doc */
.highlight .s2 { color: #BA2121 } /* Literal.String.Double */
.highlight .se { color: #BB6622; font-weight: bold } /* Literal.String.Escape */
.highlight .sh { color: #BA2121 } /* Literal.String.Heredoc */
.highlight .si { color: #BB6688; font-weight: bold } /* Literal.String.Interpol */
.highlight .sx { color: #008000 } /* Literal.String.Other */
.highlight .sr { color: #BB6688 } /* Literal.String.Regex */
.highlight .s1 { color: #BA2121 } /* Literal.String.Single */
.highlight .ss { color: #19177C } /* Literal.String.Symbol */
.highlight .bp { color: #008000 } /* Name.Builtin.Pseudo */
.highlight .vc { color: #19177C } /* Name.Variable.Class */
.highlight .vg { color: #19177C } /* Name.Variable.Global */
.highlight .vi { color: #19177C } /* Name.Variable.Instance */
.highlight .il { color: #666666 } /* Literal.Number.Integer.Long */


</style>
<script type="text/javascript">
/*<![CDATA[*/
var asciidoc = {  // Namespace.

/////////////////////////////////////////////////////////////////////
// Table Of Contents generator
/////////////////////////////////////////////////////////////////////

/* Author: Mihai Bazon, September 2002
 * http://students.infoiasi.ro/~mishoo
 *
 * Table Of Content generator
 * Version: 0.4
 *
 * Feel free to use this script under the terms of the GNU General Public
 * License, as long as you do not remove or alter this notice.
 */

 /* modified by Troy D. Hanson, September 2006. License: GPL */
 /* modified by Stuart Rackham, 2006, 2009. License: GPL */

// toclevels = 1..4.
toc: function (toclevels) {

  function getText(el) {
    var text = "";
    for (var i = el.firstChild; i != null; i = i.nextSibling) {
      if (i.nodeType == 3 /* Node.TEXT_NODE */) // IE doesn't speak constants.
        text += i.data;
      else if (i.firstChild != null)
        text += getText(i);
    }
    return text;
  }

  function TocEntry(el, text, toclevel) {
    this.element = el;
    this.text = text;
    this.toclevel = toclevel;
  }

  function tocEntries(el, toclevels) {
    var result = new Array;
    var re = new RegExp('[hH]([1-'+(toclevels+1)+'])');
    // Function that scans the DOM tree for header elements (the DOM2
    // nodeIterator API would be a better technique but not supported by all
    // browsers).
    var iterate = function (el) {
      for (var i = el.firstChild; i != null; i = i.nextSibling) {
        if (i.nodeType == 1 /* Node.ELEMENT_NODE */) {
          var mo = re.exec(i.tagName);
          if (mo && (i.getAttribute("class") || i.getAttribute("className")) != "float") {
            result[result.length] = new TocEntry(i, getText(i), mo[1]-1);
          }
          iterate(i);
        }
      }
    }
    iterate(el);
    return result;
  }

  var toc = document.getElementById("toc");
  if (!toc) {
    return;
  }

  // Delete existing TOC entries in case we're reloading the TOC.
  var tocEntriesToRemove = [];
  var i;
  for (i = 0; i < toc.childNodes.length; i++) {
    var entry = toc.childNodes[i];
    if (entry.nodeName.toLowerCase() == 'div'
     && entry.getAttribute("class")
     && entry.getAttribute("class").match(/^toclevel/))
      tocEntriesToRemove.push(entry);
  }
  for (i = 0; i < tocEntriesToRemove.length; i++) {
    toc.removeChild(tocEntriesToRemove[i]);
  }

  // Rebuild TOC entries.
  var entries = tocEntries(document.getElementById("content"), toclevels);
  for (var i = 0; i < entries.length; ++i) {
    var entry = entries[i];
    if (entry.element.id == "")
      entry.element.id = "_toc_" + i;
    var a = document.createElement("a");
    a.href = "#" + entry.element.id;
    a.appendChild(document.createTextNode(entry.text));
    var div = document.createElement("div");
    div.appendChild(a);
    div.className = "toclevel" + entry.toclevel;
    toc.appendChild(div);
  }
  if (entries.length == 0)
    toc.parentNode.removeChild(toc);
},


/////////////////////////////////////////////////////////////////////
// Footnotes generator
/////////////////////////////////////////////////////////////////////

/* Based on footnote generation code from:
 * http://www.brandspankingnew.net/archive/2005/07/format_footnote.html
 */

footnotes: function () {
  // Delete existing footnote entries in case we're reloading the footnodes.
  var i;
  var noteholder = document.getElementById("footnotes");
  if (!noteholder) {
    return;
  }
  var entriesToRemove = [];
  for (i = 0; i < noteholder.childNodes.length; i++) {
    var entry = noteholder.childNodes[i];
    if (entry.nodeName.toLowerCase() == 'div' && entry.getAttribute("class") == "footnote")
      entriesToRemove.push(entry);
  }
  for (i = 0; i < entriesToRemove.length; i++) {
    noteholder.removeChild(entriesToRemove[i]);
  }

  // Rebuild footnote entries.
  var cont = document.getElementById("content");
  var spans = cont.getElementsByTagName("span");
  var refs = {};
  var n = 0;
  for (i=0; i<spans.length; i++) {
    if (spans[i].className == "footnote") {
      n++;
      var note = spans[i].getAttribute("data-note");
      if (!note) {
        // Use [\s\S] in place of . so multi-line matches work.
        // Because JavaScript has no s (dotall) regex flag.
        note = spans[i].innerHTML.match(/\s*\[([\s\S]*)]\s*/)[1];
        spans[i].innerHTML =
          "[<a id='_footnoteref_" + n + "' href='#_footnote_" + n +
          "' title='View footnote' class='footnote'>" + n + "</a>]";
        spans[i].setAttribute("data-note", note);
      }
      noteholder.innerHTML +=
        "<div class='footnote' id='_footnote_" + n + "'>" +
        "<a href='#_footnoteref_" + n + "' title='Return to text'>" +
        n + "</a>. " + note + "</div>";
      var id =spans[i].getAttribute("id");
      if (id != null) refs["#"+id] = n;
    }
  }
  if (n == 0)
    noteholder.parentNode.removeChild(noteholder);
  else {
    // Process footnoterefs.
    for (i=0; i<spans.length; i++) {
      if (spans[i].className == "footnoteref") {
        var href = spans[i].getElementsByTagName("a")[0].getAttribute("href");
        href = href.match(/#.*/)[0];  // Because IE return full URL.
        n = refs[href];
        spans[i].innerHTML =
          "[<a href='#_footnote_" + n +
          "' title='View footnote' class='footnote'>" + n + "</a>]";
      }
    }
  }
},

install: function(toclevels) {
  var timerId;

  function reinstall() {
    asciidoc.footnotes();
    if (toclevels) {
      asciidoc.toc(toclevels);
    }
  }

  function reinstallAndRemoveTimer() {
    clearInterval(timerId);
    reinstall();
  }

  timerId = setInterval(reinstall, 500);
  if (document.addEventListener)
    document.addEventListener("DOMContentLoaded", reinstallAndRemoveTimer, false);
  else
    window.onload = reinstallAndRemoveTimer;
}

}
asciidoc.install();
/*]]>*/
</script>
</head>
<body class="article">
<div id="header">
</div>
<div id="content">
<div class="paragraph"><p>Since about October last year, I&#8217;ve been writing an introduction to R book. It&#8217;s
been quite the experience. I&#8217;ve finally started making time to document some of
the interesting things I&#8217;ve learned (about R, about writing, about about how to
bring those two together) along the way.</p></div>
<div class="paragraph"><p>The book is aimed at proper beginners; people with absolutely no formal coding
experience. This tends to mean people coming from Excel who need to do more than
a spreadsheet can/should.</p></div>
<div class="imageblock" style="text-align:center;">
<div class="content">
<img src="tweet.png" alt="tweet.png" width="400" />
</div>
</div>
<div class="paragraph"><p>Most of the books I&#8217;ve looked at which claim to teach programming begin with
some strong assumptions about the reader already knowing how to program, and
teach the specific syntax of some language. That&#8217;s no good if this is your first
language, so I&#8217;m working towards teaching the concepts, the language, and the
syntax (warts and all).</p></div>
<div class="paragraph"><p>The book is currently available under the Manning Early Access Program (MEAP)
which means if you buy it you get the draft of the first three chapters right
now. If you find something you still don&#8217;t understand, or you don&#8217;t like how
I&#8217;ve written some/all of it, then jump onto the forum and let me know. I make
more edits and write more chapters, and you get updated versions. Lather, rinse,
repeat until the final version and you get a polished book which (if I&#8217;m any
good) contains what you want it to.</p></div>
<div class="paragraph"><p>I&#8217;m genuinely interested in getting this right; I want to help people learn R. I
contribute a bit of time on Stack Overflow answering people&#8217;s questions, and
it&#8217;s very common to see questions that shouldn&#8217;t need asking. I don&#8217;t blame the
user for not knowing something (a different answer for not searching, perhaps),
but I can help make the resource they need.</p></div>
<div class="paragraph"><p>To show that I really want people to contribute, here&#8217;s a discount code to
sweeten the deal: use <code>mlcarroll</code> for 50% off here:
<a href="https://www.manning.com/books/data-munging-with-r?a_aid=datamungingwithr&amp;a_bid=1dc44480">https://www.manning.com/books/data-munging-with-r?a_aid=datamungingwithr&amp;a_bid=1dc44480</a></p></div>
<div class="paragraph"><p>Chapter 1 is a free download, so please check that out too! At the moment the
MEAP covers the first three chapters, but the following four aren&#8217;t too far
behind.</p></div>
<div class="paragraph"><p>I&#8217;ll document some of the behind-the-scenes process shortly, but for now here&#8217;s
an excerpt from chapter 2:</p></div>
<div class="paragraph"><p>## Storing Values (Assigning)</p></div>
<div class="paragraph"><p>In order to do something with our data, we will need to tell <code>R</code> what to call
it, so that we can refer to it in our code. In programming in general, we
typically have <em>variables</em> (things that may vary) and <em>values</em> (our data). We&#8217;ve
already seen that different data <em>values</em> can have different <em>types</em>, but we
haven&#8217;t told <code>R</code> to store any of them yet. Next, we&#8217;ll create some <em>variables</em>
to store our data <em>values</em>.</p></div>
<div class="paragraph"><p># Data (Variables)</p></div>
<div class="paragraph"><p>If we have the values <code>4</code> and <code>8</code> and we want to do something with them, we can
use the values literally (say, add them together as <code>4 + 8</code>). You may be
familiar with this if you frequently use Excel; data values are stored in cells
(groups of which you can opt to name) and you tell the program which values you
wish to combine in some calculation by selecting the cells with the mouse or
keyboard. Alternatively, you can opt to refer to cells by their grid reference
(e.g. <code>A1</code>). Similarly to this second method, we can store values in <em>variables</em>
(things that may vary) and <em>abstract</em> away the values. In <code>R</code>, assigning of
values to variables takes the following form</p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span>variable <span class="o">&lt;-</span> value
</pre></div></div></div>
<div class="paragraph"><p>The <em>assignment operator</em> <code>\&lt;-</code> can be thought of as storing the value/thing on
the right hand side into the name/thing on the left hand side. For example, try
typing <code>x \&lt;- 4</code> into the <code>R</code> <code>*Console*</code> then press kbd:[Enter]:</p></div>
<div class="imageblock">
<div class="content">
<img src="variable_value.png" alt="Variable" />
</div>
</div>
<div class="paragraph"><p>You could just as easily use the equals sign to achieve this; <code>x = 4</code> but I
recommend you use <code>\&lt;-</code> for this for reasons that will become clear later.</p></div>
<div class="paragraph"><p>You&#8217;ll notice that the <code>*Environment*</code> tab of the <code>*Workspace*</code> pane now lists
<code>x</code> under <code>*Values*</code> and shows the number 4 next to it, as shown in <a href="#fig-x_eq_4">[fig-x_eq_4]</a></p></div>
<div class="imageblock" id="fig-x_eq_4" style="text-align:center;">
<div class="content">
<img src="fig-x_eq_4.png" alt="fig-x_eq_4.png" width="400" />
</div>
<div class="title">Figure 2. 1. The <em>variable</em> <code>x</code> has been assigned the <em>value</em> <code>4</code>.</div>
</div>
<div class="paragraph"><p>What happened behind the scenes was that when we pressed kbd:[Enter], <code>R</code> took
the entire expression that we entered (<code>x \&lt;- 4</code>) and evaluated it. Since we
told <code>R</code> to <em>assign</em> the value <code>4</code> to the variable <code>x</code>, <code>R</code> converted the value
<code>4</code> to binary and placed that in the computer&#8217;s memory. <code>R</code> then gives us a
reference to that place in the computer&#8217;s memory and labels it <code>x</code>. A diagram of
this process is shown in <a href="#fig-assign">[fig-assign]</a> Nothing else appeared in the
<code>*Console*</code> because the action of assigning a value doesn&#8217;t <em>return</em> anything
(we&#8217;ll cover this more in our section on functions).</p></div>
<div class="paragraph"><div class="title">Assigning a value to a variable. The value entered is converted to binary, then stored in memory, the reference to which is labelled by the variable.</div><p>![figures/assigning.png]</p></div>
<div class="paragraph"><p>This is overly simplified, of course. Technically speaking, in <code>R</code>, names have
objects rather than the other way around. This means that <code>R</code> can be quite
memory efficient since it doesn&#8217;t create a copy of anything it doesn&#8217;t need to.</p></div>
<div class="admonitionblock">
<table><tr>
<td class="icon">
<img src="./images/icons/caution.png" alt="Caution" />
</td>
<td class="content">
<div class="title">On <em>"hidden"</em> variables</div>
<div class="paragraph"><p>Variables which begin with a period (e.g. <code>.length</code>) are considered
<em>hidden</em> and do not appear in the <code>*Environment*</code> tab of the
<code>*Workspace*</code>. They otherwise behave exactly as any other variable; they can be
printed and manipulated. An example of one of these is the <code>.Last.value</code>
variable, which exists from the moment you load up <code>R</code> (with the value <code>TRUE</code>)&#8201;&#8212;&#8201;this contains the output value of the last statement executed (handy if you
forgot to assign it to something). There are very few reasons you&#8217;ll want to use
this feature (dot-prefixed hidden variables) on purpose at the moment, so for
now, avoid creating variable names with this pattern. The exception to the
<em>hidden</em> nature of these is again the <code>.Last.value</code> variable which you can
request to be visible in the <code>*Environment*</code> tab via
menu:Tools[Global Options&#8230; &gt; General &gt; Show .Last.value in environment listing].</p></div>
</td>
</tr></table>
</div>
<div class="paragraph"><p>We can retrieve the value assigned to the variable <code>x</code> by asking <code>R</code> to print
the value of <code>x</code></p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span><span class="kp">print</span><span class="p">(</span>x <span class="o">=</span> x<span class="p">)</span>
</pre></div></div></div>
<div class="listingblock">
<div class="content">
<pre><code>#&gt; [1] 4</code></pre>
</div></div>
<div class="paragraph"><p>for which we have a useful shortcut&#8201;&#8212;&#8201;if your entire expression is just a
variable, <code>R</code> will assume you mean to <code>print()</code> it, so</p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span>x
</pre></div></div></div>
<div class="listingblock">
<div class="content">
<pre><code>#&gt; [1] 4</code></pre>
</div></div>
<div class="paragraph"><p>works just the same.</p></div>
<div class="paragraph"><p>Now, about that <code>[1]</code>: it&#8217;s important to know that in <code>R</code>, there&#8217;s no such thing
as a single value; every value is actually a <em>vector</em> of values (we&#8217;ll cover
these properly in the next chapter, but think of these as collections of values
of the same type).<span class="footnote"><br />[In technical terms, <code>R</code> has no <em>scalar</em> types.]<br /></span>
Whenever <code>R</code> prints a value it allows for the case where the value contains more
than one number. To make this easier on the eye, it labels the first value
appearing on the line by it&#8217;s position in the collection. For collections
(vectors) with just a single value, this might appear strange, but this makes
more sense once our variables contain more values</p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span><span class="c1"># Print the column names of the mtcars dataset</span>
<span class="kp">names</span><span class="p">(</span>x <span class="o">=</span> mtcars<span class="p">)</span>
</pre></div></div></div>
<div class="listingblock">
<div class="content">
<pre><code>#&gt;  [1] "mpg"  "cyl"  "disp" "hp"   "drat" "wt"   "qsec" "vs"   "am"   "gear"
#&gt; [11] "carb"</code></pre>
</div></div>
<div class="paragraph"><p>We can assign another variable to another value</p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span>y <span class="o">&lt;-</span> <span class="m">8</span>
</pre></div></div></div>
<div class="paragraph"><p>There are few restrictions for what we can name our data <em>values</em>, but <code>R</code> will
complain if you try to break them. Variables should start with a letter, not a
number. Trying to create the variable <code>2b</code> will generate an error. Variables can
also start with a dot (<code>.</code>) as long as it&#8217;s not immediately followed by a
number, although you may wish to avoid doing so. The rest of the variable name
can consist of letters (upper and lower case) and numbers, but not punctutation
(except <code>.</code> or <code>_</code>) or other symbols (except the dot, though again, perferrably
not).</p></div>
<div class="paragraph"><p>There are also certain <em>reserved words</em> that you can&#8217;t name variables as. Some
are <em>reserved</em> for built-in functions or keywords</p></div>
<div class="paragraph"><p><code>if</code>, <code>else</code>, <code>repeat</code>, <code>while</code>, <code>function</code>, <code>for</code>, <code>in</code>, <code>next</code>, and <code>break</code>.</p></div>
<div class="paragraph"><p>Others are <em>reserved</em> for particular values</p></div>
<div class="paragraph"><p><code>TRUE</code>, <code>FALSE</code>, <code>NULL</code>, <code>Inf</code>, <code>NaN</code>, <code>NA</code>, <code>NA_integer_</code>, <code>NA_real_</code>,
<code>NA_complex_</code>, and <code>NA_character_</code>.</p></div>
<div class="paragraph"><p>We&#8217;ll come back to what each of these means, but for now you just need to know
that you can&#8217;t create a variable with one of those names.</p></div>
<div class="admonitionblock">
<table><tr>
<td class="icon">
<img src="./images/icons/caution.png" alt="Caution" />
</td>
<td class="content">
<div class="title">On overwriting names</div>
<div class="paragraph"><p>What you <strong>can</strong> do however, which you may wish to take care with, is <em>overwrite</em>
the in-built names of variables and functions. By default, the value <code>pi</code> is
available (&#960; = 3.141593).</p></div>
<div class="paragraph"><p>If you were translating an equation into code, and wanted to enter the value
<em>p<sub>i</sub></em> you might accidentally call it <code>pi</code> and in doing so change the default
value, causing all sorts of trouble when you next go to use it or call a
function you&#8217;ve written which expects it to still be the default.</p></div>
<div class="paragraph"><p>The default value can still be accessed by specifying the package in which it is
defined, separated by two colons (<code>::</code>). In the case of <code>pi</code>, this is the <code>base</code>
package.</p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span><span class="kc">pi</span> <span class="o">&lt;-</span> <span class="m">3L</span> <span class="c1">#<img src="./images/icons/callouts/1.png" alt="1" /></span>
base<span class="o">::</span><span class="kc">pi</span> <span class="c1">#<img src="./images/icons/callouts/2.png" alt="2" /></span>
</pre></div></div></div>
<div class="listingblock">
<div class="content">
<pre><code>#&gt; [1] 3.141593</code></pre>
</div></div>
<div class="colist arabic"><table>
<tr><td><img src="./images/icons/callouts/1.png" alt="1" /></td><td>
Re-defining <code>pi</code> to be equal to exactly <code>3</code>
</td></tr>
<tr><td><img src="./images/icons/callouts/2.png" alt="2" /></td><td>
The default, correct value is still available.
</td></tr>
</table></div>
<div class="paragraph"><p>This is also an issue for functions, with the same solution; specify the package
in which it is defined to use that definition. We&#8217;ll return to this in
<a href="#SS-Scope">Scope</a>.</p></div>
</td>
</tr></table>
</div>
<div class="paragraph"><p>We&#8217;ll cover how to do things to our variables in more detail in the next
section, but for now let&#8217;s see what happens if we add our variables <code>x</code> and <code>y</code>
in the same way as we did for our regular numbers</p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span>x <span class="o">+</span> y
</pre></div></div></div>
<div class="listingblock">
<div class="content">
<pre><code>#&gt; [1] 12</code></pre>
</div></div>
<div class="paragraph"><p>which is what we got when we added these numbers explicitly. Note that since our
expression produces just a number (no assigment), the value is printed. We&#8217;ll
cover how to add and subtract values in more depth in <a href="#SS-math">Basic Mathematics</a>.</p></div>
<div class="paragraph"><p><code>R</code> has no problems with overwriting these values, and it doesn&#8217;t mind what data
you overwrite these with.<span class="footnote"><br />[This is where the distinction of <em>weakly
typed</em> becomes important - in a <em>strongly typed</em> language you would not be able
to arbitrarily change the type of a variable.]<br /></span></p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span>y <span class="o">&lt;-</span> <span class="s">&#39;banana&#39;</span>
y
</pre></div></div></div>
<div class="listingblock">
<div class="content">
<pre><code>#&gt; [1] "banana"</code></pre>
</div></div>
<div class="paragraph"><p><code>R</code> is <em>case-sensitive</em>, which means that it treats <code>a</code> and <code>A</code> as distinct
names. You can have a variable named <code>myVariable</code> and another named <code>MYvariable</code>
and another named <code>myVARIABLE</code> and <code>R</code> will hold the value assigned to each
independently.</p></div>
<div class="quoteblock">
<div class="title">On variable names</div>
<div class="content">There are only two hard things in Computer Science: cache invalidation and naming things.</div>
<div class="attribution">
<em>Principal Curmudgeon Netscape Communications Corporation</em><br />
&#8212; Phil Karlton
</div></div>
<div class="paragraph"><p>I said earlier that <code>R</code> won&#8217;t keep track of your units so it&#8217;s a good idea to
name your variables in a way that makes logical sense, is meaningful, and will
help you remember what it represents. Variables <code>x</code> and <code>y</code> are fine for playing
around with values, but aren&#8217;t particularly meaningful if your data represents
speeds, where you may want to use something like <code>speed_kmph</code> for speeds in
kilometers per hour. Underscores (<code>_</code>) are allowed in variable names, but
whether or not you use them is up to you. Some programmers prefer to name
variables in this way (sometimes referred to as <em>snake_case</em>), others prefer
<em>CamelCase</em>. The use of periods (dots, <code>.</code>) to separate words is discouraged for
reasons beyond the scope of this book.<span class="footnote"><br />[This syntax is already used
within <code>R</code> to denote functions acting on a specific class, such as
<code>print.Date()</code>.]<br /></span></p></div>
<div class="admonitionblock">
<table><tr>
<td class="icon">
<img src="./images/icons/important.png" alt="Important" />
</td>
<td class="content">
<div class="title">Naming things</div>
<div class="paragraph"><p>Be careful when naming your variables. Make them meaningful and
concise. In six months from now, will you remember what <code>data_17</code> corresponds
to? Tomorrow, will you remember that <code>newdata</code> was updated twice?</p></div>
</td>
</tr></table>
</div>
<div class="paragraph"><p># Unchanging Data</p></div>
<div class="paragraph"><p>If you&#8217;re familiar with working with data in a spreadsheet program (such as
Excel), you may expect your variables to behave in a way that they
won&#8217;t. Automatic recalculation is a very useful feature of spreadsheet programs,
but it&#8217;s not how <code>R</code> behaves.</p></div>
<div class="paragraph"><p>If we assign our two variables, then add them, we can save that result to
another variable</p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span>a <span class="o">&lt;-</span> <span class="m">4</span>
b <span class="o">&lt;-</span> <span class="m">8</span>
sum_of_a_and_b <span class="o">&lt;-</span> a <span class="o">+</span> b
</pre></div></div></div>
<div class="paragraph"><p>This has the value we expect</p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span><span class="kp">print</span><span class="p">(</span>x <span class="o">=</span> sum_of_a_and_b<span class="p">)</span>
</pre></div></div></div>
<div class="listingblock">
<div class="content">
<pre><code>#&gt; [1] 12</code></pre>
</div></div>
<div class="paragraph"><p>Now, if we <em>change</em> one of these values</p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span>b <span class="o">&lt;-</span> <span class="m">2</span>
</pre></div></div></div>
<div class="paragraph"><p>this has <strong>no impact</strong> on the value of the variable we created to hold the sum
earlier</p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span><span class="kp">print</span><span class="p">(</span>x <span class="o">=</span> sum_of_a_and_b<span class="p">)</span>
</pre></div></div></div>
<div class="listingblock">
<div class="content">
<pre><code>#&gt; [1] 12</code></pre>
</div></div>
<div class="paragraph"><p>Once the sum was calculated, and that value stored in a variable, the connection
to the original values was lost. This makes things <em>reliable</em> because you know
for sure what value a variable will have at any point in your calculation by
following the steps that lead to it, whereas a spreadsheet depends much more on
its current overall <em>state</em>.</p></div>
<div class="paragraph"><p># Assigmnent Operators (<code>\&lt;-</code> vs <code>=</code>)</p></div>
<div class="paragraph"><p>If you&#8217;ve read some <code>R</code> code already, you&#8217;ve possibly seen that both <code>\&lt;-</code> and
<code>=</code> are used to assign values to objects, and this tends to cause some
confusion. Technically, <code>R</code> will accept either when assigning variables, so in
that respect it comes down to a matter of style (I still highly reccomend
assigning with <code>\&lt;-</code>). The big difference comes when using functions that take
<em>arguments</em>&#8201;&#8212;&#8201;there you should only use <code>=</code> to specify what the <em>value</em> of the
<em>argument</em>. For example, when we inspected the <code>mtcars</code> data, we could
specify a string with which to indent the output</p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span>str<span class="p">(</span>object <span class="o">=</span> mtcars<span class="p">,</span> indent.str <span class="o">=</span> <span class="s">&#39;&gt;&gt;  &#39;</span><span class="p">)</span>
</pre></div></div></div>
<div class="listingblock">
<div class="content">
<pre><code>#&gt; 'data.frame':        32 obs. of  11 variables:
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
#&gt; &gt;&gt;  $ carb: num  4 4 1 1 2 1 4 2 2 4 ...</code></pre>
</div></div>
<div class="paragraph"><p>If we had used <code>\&lt;-</code> instead of <code>=</code> for either argument, then <code>R</code> would treat
that as creating a new variable <code>object</code> or <code>indent.str</code> with value <code>mtcars</code> or
<code>'&gt;&gt; '</code> respectively, which isn&#8217;t what we want.</p></div>
<div class="admonitionblock">
<table><tr>
<td class="icon">
<img src="./images/icons/warning.png" alt="Warning" />
</td>
<td class="content">
<div class="title">Assigning to variables.</div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span>score <span class="o">&lt;-</span> <span class="m">4.8</span>
score
</pre></div></div></div>
<div class="listingblock">
<div class="content">
<pre><code>#&gt; [1] 4.8</code></pre>
</div></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span>str<span class="p">(</span>object <span class="o">=</span> score<span class="p">)</span>
</pre></div></div></div>
<div class="listingblock">
<div class="content">
<pre><code>#&gt;  num 4.8</code></pre>
</div></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span>fruit <span class="o">&lt;-</span> <span class="s">&#39;banana&#39;</span>
fruit
</pre></div></div></div>
<div class="listingblock">
<div class="content">
<pre><code>#&gt; [1] "banana"</code></pre>
</div></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span>str<span class="p">(</span>object <span class="o">=</span> fruit<span class="p">)</span>
</pre></div></div></div>
<div class="listingblock">
<div class="content">
<pre><code>#&gt;  chr "banana"</code></pre>
</div></div>
</td>
</tr></table>
</div>
<div class="paragraph"><p>Note that we didn&#8217;t need to tell <code>R</code> that one of these was a number and one was
a string, it figured that out itself. It&#8217;s good practice (and easier to read) to
make your <code>\&lt;-</code> line up vertically when defining several variables:</p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span>first_name <span class="o">&lt;-</span> <span class="s">&#39;John&#39;</span>
last_name  <span class="o">&lt;-</span> <span class="s">&#39;Smith&#39;</span>
top_points <span class="o">&lt;-</span> <span class="m">23</span>
</pre></div></div></div>
<div class="paragraph"><p>but only if this can be achieved without adding too many spaces (exactly how
many is too many is up to you).</p></div>
<div class="admonitionblock">
<table><tr>
<td class="icon">
<img src="./images/icons/caution.png" alt="Caution" />
</td>
<td class="content">
<div class="paragraph"><div class="title">Watch this space!</div><p>An extra space can make a big difference to the syntax. Compare:</p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span>a <span class="o">&lt;-</span> <span class="m">3</span>
</pre></div></div></div>
<div class="paragraph"><p>with</p></div>
<div class="listingblock">
<div class="content"><div class="highlight"><pre><span></span>a <span class="o">&lt;</span> <span class="o">-</span> <span class="m">3</span>
</pre></div></div></div>
<div class="listingblock">
<div class="content">
<pre><code>#&gt; [1] FALSE</code></pre>
</div></div>
<div class="paragraph"><p>In the first case we assigned the value <code>3</code> to the variable <code>a</code> (which returns
nothing). In the second case, with a wayward space, we <em>compared</em> <code>a</code> to the
value <code>-3</code> which returns <code>FALSE</code> (I&#8217;ll explain why that works at all, later).</p></div>
</td>
</tr></table>
</div>
<div class="paragraph"><p>Now that we know how to provide some data to <code>R</code>, what if we want to explicitly
tell <code>R</code> that our data should be of a specific type, or we want to convert our
data to a different type? That&#8217;s an article for another day.</p></div>
<div class="paragraph"><p>If you&#8217;re interested in seeing more, and hopefully providing feedback on what
you do/don&#8217;t like about it, then use the discount code <code>mlcarroll</code> here
<a href="https://www.manning.com/books/data-munging-with-r?a_aid=datamungingwithr&amp;a_bid=1dc44480">https://www.manning.com/books/data-munging-with-r?a_aid=datamungingwithr&amp;a_bid=1dc44480</a>
for 50% off and get reading!</p></div>
</div>
<div id="footnotes"><hr /></div>
<div id="footer">
<div id="footer-text">
Last updated
 2017-06-23 00:02:51 ACST
</div>
</div>
</body>
</html>