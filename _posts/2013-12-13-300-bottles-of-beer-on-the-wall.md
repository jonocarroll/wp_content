---
ID: 342
post_title: 300 Bottles of Beer on the Wall...
author: Jonathan Carroll
post_date: 2013-12-13 19:30:05
post_excerpt: ""
layout: post
permalink: >
  http://jcarroll.com.au/2013/12/13/300-bottles-of-beer-on-the-wall/
published: true
tc-thumb-fld:
  - 'a:2:{s:9:"_thumb_id";s:3:"344";s:11:"_thumb_type";s:5:"thumb";}'
---
It's known to some that I've been keeping a beer log for -- I'm not exactly sure how long, maybe a couple of years. I wanted to know how many unique beers I was going through over time. I know certain people that do this, and who have long-since crossed the 600 mark. I've most likely done that myself over the many years that I've been tasting beer, but without the records to back that up, it's a guess.

<!--more-->

I've made a bit of a habit of trying to only purchase beers that I haven't yet tried. Surprisingly, the available pool of such hasn't dried up in poor little Adelaide just yet. I have of course supplemented the local availability with beers from my travels around the world in the last two years, including Paris, London, Germany, and Italy.

I started by writing a list of each and every commercial (available in either bottles, cans, or on tap, through the exchange of currency) beer I tasted. To be fair, these aren't all beers that I've paid full price for and consumed in their entirety; a sip counts if I tasted it, even if someone else bought it. Under this definition, I'm also excluding home brews. For the sake of simplicity, I'm also excluding most things that I personally don't count as "beer" (don't get me started on the difficulties of pigeonholing that definition) such as ginger beer and the like. There's also no need to point out some of the lower-quality beers (typically American mainstream lagers) on the list that I would gladly refrain from calling "beer". For the purposes of this list, they count.

I'm still debating whether or not to go through my many beer texts and add the beers that I 100% recall tasting. I may get around to doing that in the future.

The list on its own would be a little unweildy - not only is it by definition compiled under the influence of alcohol, but it lacks most of the useful information such as 'is this beer unique on the list' and in several cases, either the brewery or beer name itself, or in some cases is simply a shorthand designation such as 'LCPA' which I instantly recognise as Little Creatures Pale Ale. I very quickly gave up on the idea of keeping tasting notes, simply because I know that almost any beer I get to at the end of a large session will be completely biased in judgement of its finer qualities.

As I was beginning to re-learn MySQL at the time of starting the list, I decided to put some of my programming skills and the availability of my self-hosted website to good use. Given that my iPhone was also jailbroken at the time, the extraction process was able to be contained nicely in a shell script that was run (via crontab) every night at midnight, which:
<ul>
	<li>Checked to see if my iPhone responded to pings on my wifi network (DHCP controlled, designated IP)</li>
	<li>If so, opened an ssh tunnel to my iPhone, and rsync'd my Notes to a backup directory</li>
	<li>Scanned the Notes SQLlite file for a Note beginning with the tag 'BEERLIST'</li>
	<li>If found, extracted the body of the note into a CSV (under the vague assumption that I'd entered data in a usable format)</li>
</ul>
At this point, a little human intervention was required, in which I fixed up the CSV list of beers/breweries by hand. From there, I re-exported to a CSV file. I had MySQL create a database table, read in the CSV, remove duplicate beers, order by brewery, and generate linked tables of breweries and beers. It also counts the number of occurances of each beer, though I'm not currently leveraging that functionality. The less of that code anyone sees, the better. It's a mess, and I won't be posting it here.

That's all well and good if I wanted everyone to come over and <code>SELECT DISTINCT(BREWERY) FROM BEERLIST</code> from within the database. The next step was to get it visible. A little PHP was all I needed to query the database on each page load (with the login details nicely hidden by the HTML-spitting script) and a tiny bit more HTML/css/PHP to get it neatly presented in a clean table containing appropriate links to each alphabetical category of brewery. I've tilted the formatting towards my own iPhone screen, since that's mainly where I want to view the site.

The entire page is dynamic based on what the current state of the database is. The code is provided in case anyone's interested.

[php]
&amp;lt;html&amp;gt;
&amp;lt;head&amp;gt;
&lt;title&gt;Jono's Beer List&lt;/title&gt;
&amp;lt;style type=&amp;quot;text/css&amp;quot;&amp;gt;

@media screen {

body {
width: 640px;
font: 12pt Helvetica, sans-serif;
} 

img, table {
max-width: 640px;
} 

}

&amp;lt;/style&amp;gt;

&amp;lt;/head&amp;gt;
&amp;lt;meta name=&amp;quot;viewport&amp;quot; content=&amp;quot;width=300;&amp;quot; /&amp;gt;
&amp;lt;body bgcolor=&amp;quot;#FFFF66&amp;quot;&amp;gt;

&amp;lt;div class=&amp;quot;content_letters&amp;quot;&amp;gt;
&lt;a id=&quot;top&quot;&gt;&amp;nbsp;&lt;/a&gt;&lt;br /&gt;
      &lt;?php
      $array_letter = array(&amp;quot;A&amp;quot;,&amp;quot;B&amp;quot;,&amp;quot;C&amp;quot;,&amp;quot;D&amp;quot;,&amp;quot;E&amp;quot;,&amp;quot;F&amp;quot;,&amp;quot;G&amp;quot;,&amp;quot;H&amp;quot;,&amp;quot;I&amp;quot;,&amp;quot;J&amp;quot;,
	                    &amp;quot;K&amp;quot;,&amp;quot;L&amp;quot;,&amp;quot;M&amp;quot;,&amp;quot;N&amp;quot;,&amp;quot;O&amp;quot;,&amp;quot;P&amp;quot;,&amp;quot;Q&amp;quot;,&amp;quot;R&amp;quot;,&amp;quot;S&amp;quot;,&amp;quot;T&amp;quot;,
                            &amp;quot;U&amp;quot;,&amp;quot;V&amp;quot;,&amp;quot;W&amp;quot;,&amp;quot;X&amp;quot;,&amp;quot;Y&amp;quot;,&amp;quot;Z&amp;quot;,&amp;quot;#&amp;quot;,&amp;quot;END&amp;quot;);

      for ($i=0;$i&lt;9;$i++) {
        echo &quot;&lt;a href='#{$array_letter[$i]}'&gt;{$array_letter[$i]}  |    &quot;;
      }
      echo &amp;quot;&amp;lt;br /&amp;gt;&amp;quot;;
      for ($i=10;$i&lt;19;$i++) {
        echo &quot;&lt;a href='#{$array_letter[$i]}'&gt;{$array_letter[$i]}  |    &quot;;
      }
      echo &amp;quot;&amp;lt;br /&amp;gt;&amp;quot;;
      for ($i=20;$i&lt;25;$i++) {
        echo &quot;&lt;a href='#{$array_letter[$i]}'&gt;{$array_letter[$i]}  |    &quot;;
      }
      echo &amp;quot;&amp;lt;a href='#1'&amp;gt;#  |  &amp;lt;/a&amp;gt;&amp;quot;;
      echo &amp;quot;&amp;lt;a href='#bottom'&amp;gt;END&amp;lt;/a&amp;gt;&amp;quot;;
    ?&amp;gt;
&amp;lt;br /&amp;gt;&amp;lt;br /&amp;gt;
&amp;lt;/div&amp;gt;

&amp;lt;div id=&amp;quot;container&amp;quot; align=&amp;quot;center&amp;quot;&amp;gt;
&lt;?php
$con=mysqli_connect(&amp;quot;localhost&amp;quot;,&amp;quot;jono&amp;quot;,&amp;quot;password&amp;quot;,&amp;quot;beerlog&amp;quot;);
// Check connection
if (mysqli_connect_errno())
  {
  echo &amp;quot;Failed to connect to MySQL: &amp;quot; . mysqli_connect_error();
  }

$result = mysqli_query($con,&amp;quot;SELECT beer, brewery FROM beers ORDER BY brewery, beer&amp;quot;);

echo &amp;quot;&amp;lt;table border='0' width='95%'&amp;gt;
&amp;lt;tr align=\&amp;quot;left\&amp;quot;&amp;gt;
&amp;lt;th height='20px'&amp;gt;#&amp;lt;/th&amp;gt;
&amp;lt;th&amp;gt;Brewery&amp;lt;/th&amp;gt;
&amp;lt;th&amp;gt;Beer&amp;lt;/th&amp;gt;
&amp;lt;td&amp;gt;&amp;lt;/th&amp;gt;
&amp;lt;/tr&amp;gt;&amp;quot;;

$j = 1;
$prev = &amp;quot;&amp;quot;;
while($row = mysqli_fetch_array($result))
  {
  $newbrewery = ($row['brewery'][0] &gt; $prev[0]);
  echo &amp;quot;&amp;lt;tr&amp;gt;&amp;quot;;
  if ($newbrewery) {
    echo &amp;quot;&amp;lt;tr&amp;gt;&amp;lt;td colspan=\&amp;quot;4\&amp;quot;&amp;gt;&amp;lt;hr&amp;gt;&amp;lt;/td&amp;gt;&amp;lt;/tr&amp;gt;&amp;quot;;
  }
  echo &amp;quot;&amp;lt;td&amp;gt;&amp;quot; . $j . &amp;quot;&amp;lt;/td&amp;gt;&amp;quot;;
  if ($newbrewery) {
    echo &amp;quot;&amp;lt;td id=\&amp;quot;&amp;quot; . $row['brewery'][0] . &amp;quot;\&amp;quot;&amp;gt;&amp;quot; . $row['brewery'] . &amp;quot;&amp;lt;/td&amp;gt;&amp;quot;;
  /*  echo &amp;quot;&amp;lt;td&amp;gt;&amp;quot; . $row['brewery'][0] . &amp;quot;&amp;lt;/td&amp;gt;&amp;quot;; */
  } else {
    echo &amp;quot;&amp;lt;td&amp;gt;&amp;quot; . $row['brewery'] . &amp;quot;&amp;lt;/td&amp;gt;&amp;quot;;
  /*  echo &quot;&lt;td&gt; &amp;nbsp; &lt;/td&gt;&quot;; */
  }
  echo &amp;quot;&amp;lt;td&amp;gt;&amp;quot; . $row['beer'] . &amp;quot;&amp;lt;/td&amp;gt;&amp;quot;;
  if ($newbrewery) {
    echo &quot;&lt;td&gt; &lt;a href=#top style=\&quot;text-decoration: none\&quot;&gt;&amp;uarr;&lt;/a&gt; &lt;/td&gt;&quot;;
  } else {
    echo &quot;&lt;td&gt; &amp;nbsp; &lt;/td&gt;&quot;;
  }
  echo &amp;quot;&amp;lt;/tr&amp;gt;\n&amp;quot;;
  $j = $j + 1;
  $prev = $row['brewery'][0];
  }
echo &amp;quot;&amp;lt;/table&amp;gt;&amp;quot;;

mysqli_close($con);
?&amp;gt;
&amp;lt;/div&amp;gt;

&amp;lt;div class=&amp;quot;content_letters&amp;quot;&amp;gt;
&lt;a id=&quot;bottom&quot;&gt;&amp;nbsp;&lt;/a&gt;&lt;br /&gt;
      &lt;?php
      $array_letter = array(&amp;quot;A&amp;quot;,&amp;quot;B&amp;quot;,&amp;quot;C&amp;quot;,&amp;quot;D&amp;quot;,&amp;quot;E&amp;quot;,&amp;quot;F&amp;quot;,&amp;quot;G&amp;quot;,&amp;quot;H&amp;quot;,&amp;quot;I&amp;quot;,&amp;quot;J&amp;quot;,
	                    &amp;quot;K&amp;quot;,&amp;quot;L&amp;quot;,&amp;quot;M&amp;quot;,&amp;quot;N&amp;quot;,&amp;quot;O&amp;quot;,&amp;quot;P&amp;quot;,&amp;quot;Q&amp;quot;,&amp;quot;R&amp;quot;,&amp;quot;S&amp;quot;,&amp;quot;T&amp;quot;,
                            &amp;quot;U&amp;quot;,&amp;quot;V&amp;quot;,&amp;quot;W&amp;quot;,&amp;quot;X&amp;quot;,&amp;quot;Y&amp;quot;,&amp;quot;Z&amp;quot;,&amp;quot;#&amp;quot;);

      for ($i=0;$i&lt;9;$i++) {
        echo &amp;quot;&amp;lt;a href='#{$array_letter[$i]}'&amp;gt;{$array_letter[$i]}  |  &amp;lt;/a&amp;gt;  &amp;quot;;
      }
      echo &amp;quot;&amp;lt;br /&amp;gt;&amp;quot;;
      for ($i=10;$i&amp;lt;19;$i++) {
        echo &amp;quot;&amp;lt;a href='#{$array_letter[$i]}'&amp;gt;{$array_letter[$i]}  |  &amp;lt;/a&amp;gt;  &amp;quot;;
      }
      echo &amp;quot;&amp;lt;br /&amp;gt;&amp;quot;;
      for ($i=20;$i&amp;lt;25;$i++) {
        echo &amp;quot;&amp;lt;a href='#{$array_letter[$i]}'&amp;gt;{$array_letter[$i]}  |  &amp;lt;/a&amp;gt;  &amp;quot;;
      }
      echo &amp;quot;&amp;lt;a href='#1'&amp;gt;#  |  &amp;lt;/a&amp;gt;&amp;quot;;
      echo &amp;quot;&amp;lt;a href='#top'&amp;gt;TOP&amp;lt;/a&amp;gt;&amp;quot;;
    ?&amp;gt;
&amp;lt;br /&amp;gt;&amp;lt;br /&amp;gt;
&amp;lt;/div&amp;gt;

&amp;lt;/body&amp;gt;
&amp;lt;/html&amp;gt;
[/php]

Last but not least, an update to the A records on the DNS host I use allowed me to use <a title="beer.jcarroll.com.au" href="http://beer.jcarroll.com.au" target="_blank">beer.jcarroll.com.au</a> as a sub-domain (separate to this site) for free. It's not the prettiest site, but it's quite functional now for what I'm after. The important fact being that the index of unique beers (keeping in mind the possibility of a few undetected duplicates) has crossed 300. Woo!

The (duplicate-filtered, alphabetical, searchable) list itself has been quite useful in situations where I'm asked the "have you tried X?" question. There's still plenty to add to the list, and a stack of new breweries coming on line regularly means there's no better time for us to catch up for a drink sometime.

The site: <a title="beer.jcarroll.com.au" href="http://beer.jcarroll.com.au" target="_blank">beer.jcarroll.com.au</a> -- why not share a beer that's not on the list with me?

Cheers!