---
ID: 94
post_title: >
  Display current time in requested time
  zones
author: Jonathan Carroll
post_date: 2012-11-19 12:18:19
post_excerpt: ""
layout: post
permalink: >
  http://jcarroll.com.au/2012/11/19/display-current-time-in-requested-time-zones/
published: true
---
From <a href="http://www.commandlinefu.com" target="_blank">commandlinefu.com</a>:

Display current time in requested time zones.<!--more-->

[sourcecode language="bash"]
$ zdump Japan America/New_York
Japan             Mon Nov 19 10:43:35 2012 JST
America/New_York  Sun Nov 18 20:43:35 2012 EST
[/sourcecode]

The time zone names come from the tz database which is usually found at <code>/usr/share/zoneinfo</code>.

Particularly useful for figuring out collaboration meetings.

via <a href="http://www.commandlinefu.com/commands/view/11537/display-current-time-in-requested-time-zones.">Display current time in requested time zones. | commandlinefu.com</a>.