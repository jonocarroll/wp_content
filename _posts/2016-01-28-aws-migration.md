---
ID: 624
post_title: AWS Migration
author: Jonathan Carroll
post_date: 2016-01-28 12:54:45
post_excerpt: ""
layout: post
permalink: >
  http://jcarroll.com.au/2016/01/28/aws-migration/
published: true
---
Given how terrible my internet connection has been of late, I decided to migrate my site over to Amazon Web Services (AWS) where it's now hosted for free with a reliable connection. <!--more-->

The migration itself was a bit of a headache but that was mainly due to attempting to perform it automatically. In the end zipping the directory plus MySQL tables up and sending them across manually was the best move. I have full ssh access to the AWS instance (Ubuntu 14.04 LTS) so it's still exactly what I wanted from a self-hosted site (I didn't go with a wordpress.com site because I wouldn't have control over the backend).

Hopefully this site becomes a little more stable now. I guess I could run another less mission-critical site over on my own server now.