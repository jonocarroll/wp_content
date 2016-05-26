---
ID: 835
post_title: 'De-brief: #auunconf 2016'
author: Jonathan Carroll
post_date: 2016-05-26 13:34:37
post_excerpt: ""
layout: post
permalink: http://jcarroll.com.au/?p=835
published: false
---
###IMAGE OF ROPENSCI LOGO###

<h1>The #auunconf</h1> 

The 2016 ROpenSci #auunconf was held in Brisbane, Queensland, Australia on 21/22
April, hosted at the Microsoft Innovation Centre in central Brisbane, 30 or so R
enthusiasts met to share knowledge, discuss ideas, and build something awesome
using R. From varied backgrounds we came, we drank, we coded. It was, in a word,
awesome. I had heard a little about ROpenSci before this, but not a lot. I knew
that an <a href="http://unconf16.ropensci.org/#participants">unconf had been
held in San Francisco not long before this one, featuring a who's-who of R and
data science</a> and the reports coming out of that were very positive. When I
first saw the announcement for one happening in my own country (I'm Australian;
we don't travel far without paying a *lot*) I couldn't resist filling in an
application on the spot.

Fast forward a month or so and I'm on a flight to Brisbane to meet up with a
bunch of strangers and write some R code. Discussions of potential projects had
been flowing via <a href="https://github.com/ropensci/auunconf/issues">GitHub
issues</a>, banter exchanged over slack (a new experience for me, but a tool
I've come to really cherish), packages updated, and laptops readied.

The event involved a welcome BBQ the night before the actual unconf which was a
great ice-breaker (for those not familiar with the local custom, Brisbane
riverbank + BBQ + beer + people = good times(TM)). The combination of people
coming from across the country from a wide range of backgrounds mixed with a few
decent beers made for great conversations both on and off the topic of R
programming. As fantastic as that was, the true highlight of the night would
have to go to the export-quality cross-bred Wagyu steak provided
by <a href="http://www.aaco.com.au/operations/branded-beef/">the Australian
Agricultural Company (AACo)</a> who, as it turns out, dabble in performance
metrics using R. Now, I don't want to downplay the incredible networking
discussions that were had under the stars in the amazingly beautiful Brisbane
Southbank Parklands, but that steak was utterly, mouthwateringly delicious. I
digress.

###IMAGE OF LANTERN WALKWAY###

(steak: not pictured; devoured before one could be taken)

The next morning we were welcomed into the upper levels of the Microsoft
Innovation Centre, overlooking the Brisbane River and city. ROpenSci hexbin
stickers were applied to laptop lids and votes cast for projects to focus on (my
suggestion of [code language="r"]split(ninjas, sample(Ngroups, length(ninjas),
replace=TRUE))[/code] wasn't deemed "_productive_"). Once a good number of
projects had been chosen by popular vote we gathered within the groups we felt
most strongly about and got to work. GitHub repos were created on
the <a href="https://github.com/ropenscilabs">ROpenSciLabs</a> account and the
beginnings of packages formed quickly.

Within the team I aligned best to (<code>snowball</code>) there were already a
wide variety of skills on offer and rather usefully, an existing
proof-of-concept, so we got to work quickly bringing everyone up to speed on
integrating GitHub with RStudio, Amazon Web Services terminology and structure,
installing and running the <code>aws-cli</code>, and mapping out ideas of what
the framework might look like. 

This project involved sending data and an R analysis script to an AWS S3 storage
bucket, launching an AWS instance (computing in the cloud) which knows to look
for code and data in said bucket, having the code process the data and write the
results back to the AWS bucket. Sounds easy enough, until you (a) don't want to
have to manually do *anything* on the remote machine including key exchange or
authentication; (b) realise that implies you can't log in to the instance to
tell it anything, start the analysis, write out the results, or handle failures;
and (c) you want to do it for parallel or multiple jobs, and as such need to
keep track of which machines you have running. 

###IMAGE OF COW PRESENTING###

###IMAGE OF MAP ON WINDOW###

Cue plentiful coffee, commits, and consults. The time went by disturbingly fast,
but by the end of the day we had the beginnings of a working product. People
moved freely between groups to get a taste of what else was being developed and
offer their insights where they could help. Dinner offered more casual
conversation without the temptation of bashing out a few lines of code, and
drinks afterwards didn't exactly deviate from that.

Coffees in hand the next morning we re-assessed our roadmap with fresh ideas and
got to work bringing together a fully working product. By the time presentations
came around at the end of the day, we were able to demonstrate a successful
launch of an instance running code obtained automatically from an AWS S3
bucket. Our eventual solution to the problems highlighted above involves
deploying a payload with the instance launch, a lot of <code>tryCatch</code>
or <code>safely</code> calls, and a process scheduler. It's still a work in
progress but it has good potential.

The primary projects worked on during the #auunconf are detailed below:

<h2><a href="https://github.com/ropenscilabs/snowball" target="_blank">snowball</a></h2>

<a href="http://jcarroll.com.au/wp-content/uploads/2016/05/CHsnowballs.gif"><img src="http://jcarroll.com.au/wp-content/uploads/2016/05/CHsnowballs-300x173.gif" alt="CHsnowballs" width="300" height="173" class="alignnone size-medium wp-image-845" /></a>

the <code>snowball</code> team
<table width="100%">
   <tr>
      <td><a href="https://github.com/dpagendam" target="_blank">Dan Pagendam</a></td>
      <td><a href="https://github.com/jonocarroll" target="_blank">Jonathan Carroll</a></td>
      <td><a href="https://github.com/daniel-t" target="_blank">Daniel Thomas</a></td>
   </tr>
   <tr>
      <td><a href="https://github.com/zoevanhavre/" target="_blank">Zoé van Havre</a></td>
      <td><a href="https://github.com/camroach87/" target="_blank">Cameron Roach</a></td>
      <td><a href="https://github.com/felixleungsc" target="_blank">Felix Leung</a></td>
   </tr>
      <td>Suren Rathnayake</td>
      <td><a href="https://github.com/MilesMcBain" target="_blank">Miles McBain</a></td>
      <td><a href="https://github.com/mattyjkelly" target="_blank">Matt Kelly</a></td>
   </tr>
</table>

I'm best able to discuss this project as it's the one I worked on. Dan had a
working script that he uses which already does the basics of this project;
launches an instance and runs some analyses. His issue with it was that he
needed to authenticate with the instance and have it communicate back to him
over ports he may not have full access to in the future, so a more general
solution was required.

We played with the idea of launching a head node to spawn the worker nodes but
came ot the conclusion that between using the authenticated payload and using S3
for storage, we could bypass that and have the user's machine act as the
once-off head node.


<h2><a href="https://github.com/ropenscilabs/leafier" target="_blank">leafier</a></h2>
the <code>leafier</code> team:
<table width="100%">
   <tr>
      <td><a href="https://github.com/paleo13" target="_blank">Jeffrey Hanson</a></td>
      <td><a href="https://github.com/michaelcheng429" target="_blank">Michael Cheng</a></td>
      <td><a href="https://github.com/CourtneyCampany" target="_blank">Courtney Campany</a></td>
   </tr>
   <tr>
      <td><a href="https://github.com/mattwatts" target="_blank">Matt Watts</a></td>
      <td>Amy Cook</td>
      <td>Sam Rathmanner</td>
   </tr>
   <tr>
      <td>Ruth Luscombe</td>
      <td></td>
      <td></td>
   </tr>
</table>

<h2><a href="https://github.com/ropenscilabs/eechidna" target="_blank">eechidna</a></h2>
the <code>eechidna</code> team
<table>                                                                                                                                                                          
   <tr>                                                                                                                                                                             
      <td><a href="https://github.com/dicook" target="_blank">Di Cook</a></td>                                                                                                       
      <td><a href="https://github.com/heike" target="_blank">Heike Hofmann</a></td>                                                                                                  
      <td><a href="https://github.com/robjhyndman" target="_blank">Rob Hyndman</a></td>                                                                                              
   </tr>                                                                                                                                                                            
   <tr>                                                                                                                                                                             
      <td><a href="https://github.com/tslumley" target="_blank">Thomas Lumley</a></td>                                                                                               
      <td><a href="https://github.com/benmarwick" target="_blank">Ben Marwick</a></td>                                                                                               
      <td><a href="https://github.com/cpsievert" target="_blank">Carson Sievert</a></td>                                                                                             
   </tr>                                                                                                                                                                            
   <tr>                                                                                                                                                                             
      <td><a href="https://github.com/njtierney" target="_blank">Nicholas Tierney</a></td>                                                                                           
      <td>Nathaniel Tomasetti</td>                                                                                                                                                   
      <td>Fang Zhou</td>                                                                                                                                                             
   </tr>                                                                                                                                                                            
</table>        

<h2><a href="https://github.com/saundersk1/auunconf16/blob/master/Vignette%20BoM.Rmd" target="_blank">BOM</a></h2>
the <code>BOM</code> team
<table>
   <tr>
      <td><a href="https://github.com/saundersk1" target="_blank">Kate Saunders</a></td>
      <td><a href="https://github.com/adamhsparks/" target="_blank">Adam Sparks</a></td>
   </tr>
</table>

<h2><a href="https://github.com/ropenscilabs/uncertVis" target="_blank">uncertVis</a></h2>
the <code>uncertVis</code> team
<table>
   <tr>
      <td><a href="https://github.com/petrakuhnert" target="_blank">Petra Kuhnert</a></td>
      <td><a href="https://github.com/cofiem" target="_blank">Mark Cottman-Fields</a></td>
      <td><a href="https://github.com/mattyjkelly" target="_blank">Matt Kelly</a></td>
   </tr>
   <tr>
      <td><a href="https://github.com/jesse-jesse" target="_blank">Jessie Roberts</a></td>
      <td></td>
      <td></td>
   </tr>
</table>

<table>
   <tr>
      <td></td>
      <td></td>
      <td></td>
   </tr>
</table>



<h2>Final Thoughts</h2>
conf was awesome!

[wpghs]

.

[wpghs target="view" text="This links to the view"]

.

[wpghs target="edit" text="This links to the edit"]

.

[wpghs text="Here's the post on GitHub. Feel free to submit a pull request if you find an error."]

That link should work.