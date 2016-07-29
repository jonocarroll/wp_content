---
ID: 964
post_title: 2016 Australian Election Flexdashboard
author: Jonathan Carroll
post_date: 2016-07-29 22:39:47
post_excerpt: ""
layout: post
permalink: http://jcarroll.com.au/?p=964
published: false
---
Here in the land down under we've finally completed our Federal election. We complain that it seems to go on for too long, but it's a flash in the pan compared to the USA electoral process. 
<!--more-->

<a href="http://jcarroll.com.au/wp-content/uploads/2016/07/voting.jpg"><img src="http://jcarroll.com.au/wp-content/uploads/2016/07/voting.jpg" alt="voting" width="624" height="351" class="alignnone size-full wp-image-970" /></a>

This year turned out to be quite eventful (when aren't they these days?) with what might appear to an outside observer to be a conspired attempt at a perfect split vote (a hung parliament). In the end, it seems the incumbent Liberal/National Coalition managed to form government in their own right by the slimmest of margins, with one electorate triggering a recount when the margin dropped to a single vote. 

Things run a little more smoothly here because we (functionally) follow the <a href="https://en.wikipedia.org/wiki/Westminster_system" target="_blank">Westminster system</a> for electing a party rather than a specific leader, a fact that has resulted in our having 5 Prime Ministers (4 unique) in the last 6 years, despite elections being held every 4 years. Structurally, we are similar to the United States Congress in that we have a House of Representatives elected from single-member constituencies of approximately equal population, and a Senate consisting of an equal number of Senators from each state, regardless of population. The election is decided based on how many electorates each party can win such that they can form a majority government. There are currently 150 electorates, so a party requires 76 to gain full control without having to go into talks with the minor parties.

This year, with voting completed and counted (eventually) the Liberal/National Coalition held 76 seats and can govern in their own right. Given that electorates are defined to be of <a href="https://en.wikipedia.org/wiki/Redistribution_(election)#Australia" target="_blank">approximately equal population sizes</a>, this means that the majority of people voted for that party, right? Right? Let's see.

In terms of open data, Australia doesn't do too bad. We have a few underutilised resources, such as <a href="http://data.gov.au" target="_blank">data.gov.au</a> (building an R interface to that site is on my to-do list), <a href="http://www.ands.org.au/" target="_blank">the Australian National Data Service</a>, <a href="https://researchdata.ands.org.au/" target="_blank">Research Data Australia</a>, and <a href="http://www.govpond.org/index.php" target="_blank">GovPond</a> and the <a href="http://www.aec.gov.au/" target="_blank">Australian Electoral Commission</a> (via the <a href="http://vtr.aec.gov.au/HouseDefault-20499.htm" target="_blank">Virtual Tally Room</a>) is one of the better agencies in terms of data availability.

When I visited the <a href="http://vtr.aec.gov.au/HouseDefault-20499.htm" target="_blank">Virtual Tally Room</a> to find out what level of data was available, I was rather impressed to find that the results weren't only available at the electorate level, but the polling place ('booth') level even! Not the individual voters of course, that would be a bit much, but the 7741 polling places around the country with their latitudes/longitudes and votes per party. Not too bad, and certainly an opportunity to look more closely.

This seemed like a good opportunity to try out a <a href="https://github.com/rstudio/flexdashboard/" target="_blank">flexdashboard</a> and the new <a href="https://github.com/rstudio/crosstalk" target="_blank">crosstalk</a> feature. I'll skip the minor details here and disappoint you early in that I didn't end up using crosstalk (properly, it's still in there); it turns out it's great for subsetting a data set, not so great for performing further aggregations on the data after subsetting. Not to worry.

I managed to grab a <a href="http://www.aec.gov.au/Electorates/gis/gis_datadownload.htm" target="_blank">shapefile of the electorates</a> from the AEC and merged the polling data with these to produce a map of each state with electorates colored by winning party and polling places colored by the party with the most votes. 

There's two caveats to this. Firstly, while we're required to vote within our electorates (compulsory voting, or at least getting your name ticked off as present) it's an assumption that people vote at the closest polling place to where they live or work, in which case the distribution of people isn't biasing the result at each polling place. That might not necessarily be true - perhaps people who vote for a particular party tend towards the city center on election day.

Secondly, there's no requirement on polling places that they each cater for the same number of people. Electorates are population-balanced, but a polling place could have anywhere from 0 to all of the voters for that electorate show up on that day (we tend to run BBQs at polling places serving up <a href="http://democracysausage.org" target="_blank">democracy sausages</a>, so people do move around to find the best one). I did try scaling the polling place markers by the number of votes at each but something screwy was going on with the markers disappearing on zoom-changes so I've left them all the same.

[caption id="attachment_968" align="alignnone" width="300"]<a href="http://jcarroll.com.au/wp-content/uploads/2016/07/democracysausage.jpg"><img src="http://jcarroll.com.au/wp-content/uploads/2016/07/democracysausage-300x300.jpg" alt="democracysausage.org" width="300" height="300" class="size-medium wp-image-968" /></a> democracysausage.org[/caption]

With those in mind, we can now have a look at how polarised each electorate is and compare it to the overall winner. <a href="https://jcarroll.shinyapps.io/AUelection2016/" target="_blank">Here's the result</a>, hosted over at <a href="http://shinyapps.io" target="_blank">shinyapps.io</a>. I've added a tab for both the first preference votes and two-party preferred (this data isn't completely available at the time of writing, but I'll keep updating it).

In my home state of South Australia it's clear that there's a big geographical split between the northern and central/southern suburbs

<a href="http://jcarroll.com.au/wp-content/uploads/2016/07/elec1.png"><img src="http://jcarroll.com.au/wp-content/uploads/2016/07/elec1.png" alt="elec1" width="618" height="511" class="alignnone size-full wp-image-972" /></a>

as well as a clear preference away from the two major parties in the country areas to the East.

In Tasmania, in the electorate that contains the state capital of Hobart, most polling places appear to be overwhelmingly supportive of an independent candidate. Looking at the number of polling places w