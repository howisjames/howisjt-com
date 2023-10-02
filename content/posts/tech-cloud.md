---
title: Experiences with Google Compute Engine
date: 2019-01-04T19:00:52-06:00
lastmod: 2020-06-28T11:00:52-06:00
cover: "/images/cards/cloud-dev-640x420.jpg"
draft: false
categories:
- tech
tags:
- cloud
description: Narrative about my one-year trial with Google Compute Engine.
---
 ![Google Compute Engine](/images/tech/Google_Compute_Engine_logo-100px.jpg#floatright)I was excited about the possibility of deploying "micro" webservers hosting sites which cost nothing - due to their tiny resource requirements and ability to fit within Google's "always free" thresholds. This experimentation, and failures, led me to static site generators.

## WordPress Won't Run Free
Initially, I was trying to deploy full-blown SQL-driven CMS sites using WordPress and Drupal. While some of my sites functioned for a while, eventually they all failed as I added content because the load just became overwhelming for GCE's "Micro" instance. And, really, I didn't have to add very much. Often simply applying a WordPress or extension update would break the VM. 

## Flat File CMS
Next I looked into Flat File CMS frameworks and settled on Grav. Frustration set in quickly - mostly due to my lack of expertise working with file and directory permissions in LINUX. I got really close - following a recipe that allowed me to get Grav installed, but I was never successful in getting the Grav admin panel to display. Following one Google recommendation after another resulted in a confused mess, so I purged the instance. 

## Static Site Generator
Further research led me to the concept of automated "generators" which produce static sites from raw content. I'd coded static sites before so I'm comfortable with that concept, but these new projects showed me how a static site could still host a blog. This is interesting. More reading and testing led me to Hugo, which is what I've used to deploy this site. I've written more about this on [this post]({{< relref "tech-web-development.md" >}}).

## Google App Engine
A downside with the Google Compute Engine is that I'm also responsible for maintaining the headless Debian server. By using App Engine, or Cloud Buckets I could deploy this Hugo-generated static site with zero infrastructure overhead. But, the cost goes up for those amenities. For this reason I'm stuck with the virtual machine for about a year. Then I made a discovery...

## Firebase
If one huge benefit of static websites is that they are hack proof and maintenance free, wouldn't it be great if the hosting environment was also maintenance free? And, it also cost nothing? Heck yes! I abandoned the Google Compute Engine service in favor of Google's Firebase hosting service. I develop my Go Hugo websites on my local machine, stored in a DropBox folder so that I can work on them from home, work, even my phone, and the content is both backed-up and synced. After running the hugo command to generate the static site, I use Firebase command line tools to deploy the site - or modifications to the site - to that particular Google  account's Firebase hosting. As long as I reduce the number of backed-up images of previous deployments down to 3, I've found I don't get billed. My only cost for hosting these websites is the $12 per year domain.

