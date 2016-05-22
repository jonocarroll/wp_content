---
ID: 628
post_title: 'Adelaide Traffic - Part I'
author: Jonathan Carroll
post_date: 2016-01-28 22:45:11
post_excerpt: ""
layout: post
permalink: >
  http://jcarroll.com.au/2016/01/28/adelaide-traffic-part-i/
published: true
---
Have you seen the little <a href="http://ecx.images-amazon.com/images/I/417WkHpGffL._SY300_.jpg">shark-fins on top of some traffic light control boxes</a>? Have you seen the new '<a href="http://www.adelaidenow.com.au/news/south-australia/interactive-signs-to-measure-travelling-times-across-metropolitan-adelaide/news-story/36c23ebc19bec61856b0df600c644eec" target="_blank">x minutes to y road</a>' signs? Did you know they're connected? <!--more-->

<a href="http://www.dpti.sa.gov.au/movingtraffic" target="_blank">DPTI installed a heap of bluetooth sensors around Adelaide</a> and they capture mobile phone signals when you're stopped at traffic lights; correlate them in real-time; and figure out actual travel times between various points. I requested some of the data and <a href="http://data.sa.gov.au/data/organization/department-of-planning-transport-and-infrastructure">DPTI</a> kindly shared a 6-hour database dump under CC-BY... only a million or so unique captures. I'm still trying to figure out exactly what I can do with that but I have some neat ideas. For now I've built a nice interactive map using R (shiny+leaflet) to display the bluetooth sensor locations. There's several hundred of them around town, so the coverage isn't half bad. 

Check it out (interactive site after the jump):

<a href="http://traffic.jcarroll.com.au" rel="attachment wp-att-633"><img src="http://jcarroll.com.au/wp-content/uploads/2016/01/Screenshot-280116-224242.png" alt="Screenshot - 280116 - 22:42:42" width="834" height="446" class="aligncenter size-full wp-image-633" /></a>

<a href="http://traffic.jcarroll.com.au/" target="_blank">http://traffic.jcarroll.com.au/</a>