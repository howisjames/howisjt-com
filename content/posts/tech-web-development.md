---
title: Web Development Projects
date: 2019-01-04T19:00:52-06:00
lastmod: 2019-06-11T19:00:52-06:00
cover: "/images/cards/web-code-640x420.jpg"
draft: false
categories:
- tech
tags:
- web design
description: I've been tinkering with websites since the 1990s. Here is a selection of my experience.
---
My earliest website development began with static sites hosted at GeoCities and other no-cost hosting providers. Each never amounted to more than a dozen or so pages each, but I learned the basics of HTML and CSS. Future employment led me to WordPress and then to Drupal frameworks. Each presented benefits, challenges, and learning opportunities.

## Twitter Bootstrap
Site content development with WordPress  - specifically custom coding certain pages to achieve desired effects - led me back to hard-coding. The explosion of cell phone use drove home the necessity that all website *must* be mobile friendly, if not mobile-native. Soon I discovered Twitter's Bootstrap and began developing single or few-page sites for small projects. This was the perfect solution and I still use these in combination with Github sites to deploy micro sites of project-specific information.

## WordPress Site Development
Franklinassoc.com was built from scratch by me... Like all of the wordpress sites I've built, it got slow and clunky as more and more content was added. Some have suffered from security issues, though I've tried to keep their core up to date. I built my early WP sites from scratch on bare hosting, so the responsibility of periodically checking and applying updates fell to me. I've now learned to deploy WordPress (and Drupal) through GoDaddy's cPanel Installatron, which applies significant, vetted updates automatically. I've not had problems with hacking since implementing this process.
But this doesn't solve the sluggishness problem. Sure, WordPress-optimized hosting is available and perhaps I need to try that, but I'm also intrigued by the low overhead approach of JamStacks. That's why I deployed this blog site you're reading now with Hugo.

## Drupal 7
![Drupal 7](/images/tech/Drupal_logo-175px.jpg#floatright)Another work opportunity put me in charge of replacing a public agency's proprietary website with a "modern", content-rich and mobile-friendly site. The site development was outsourced to a specialist who built it with Drupal 7. The developer's task performance waned as the basic site was deployed, so I as prime consultant was tasked with content management. I learned enough Drupal to fully populate and then manage the site. While there were a few calls for help from the developer as new features were requested, I was able to handle all of the content posting and maintenance. I learned a lot about Drupal, site hosting, Google SEO, and more. Regrettably, the site succumbed to "drupalgeddon 2015" and it had to be restored by the developer from backups. This taught me a great deal about the seriousness of website and webserver security, and the need to maintain vigilance. Vigilance is time consuming and costly.

![Drupal 7 site hacked!](/images/tech/2015-06-13_brcats_hacked.jpg "Site hacked! - Drupalgeddon")

The experience gained with the agency site led me to replace my professional association's website [louisianaplanning.org] with a new Drupal 7 site. This has been a labor of love, as all time spent is voluntary. The new site has been a big improvement over the previous "Google Sites" deployment, as I've been able to add custom content types and features unique to our professional organization. The issue I'm now facing is "how do I turn it over to another member?" This is a state association of urban planners, not IT professionals. Many would be challenged to post to a WordPress site, and finding a member interested in learning how to maintain a Drupal site will be a challenge. At the national level, a whole new web-presence framework based on Joomla is being rolled out. The national association's site has now been running for about two years, and "chapter sites" are now being rolled out to organization chapters in each of the states. Still, this will be a daunting migration process with high likelihood of lost information - content and features presently offered in our custom Drupal site which won't be offered in the future site. Still, the long-term goal of enabling non-technical members to take on the role of communications officer is more easily reached with support of the national organization, so I'll assist with the migration.

![Louisiana Planning drupal site](/images/tech/louisianaplanning_screencap2014-10-20.jpg "louisianaplanning.com")

## Cloud Instances
![Google Compute Engine](/images/tech/Google_Compute_Engine_logo-100px.jpg#floatright)Desiring to deploy a personal website without recurring hosting fees - and not satisfied with the SAAS services such as WordPress.com, Wix, Weebly, Google Sites or Zoho Sites - I became interested in deploying a virtual server in the cloud. I first experimented with Amazon Web Services but, after a year, your free trial does expire. Google Cloud Platform I learned offers a minimal free level of cloud services - a "micro instance" - which persists even after the one-year $300 value trial period ends.
 
I attempted deployment of a personal site with drupal 8. I succeeded with getting it up and running on GCP with a theme installed, but before I could add any content my Micro instance was groaning from insufficient resources. Enlarging it to "Small" or larger would push my hosting costs much higher than a managed shared hosting provider. That defeated my purpose of developing a no-cost personal site, so I nixed the instance.

## Firebase Hosting
*Update July 2019*  After several months of hosting this site on a Debian virtual machine at Google Compute Engine's free tier, I decided to migrate it over to Google's Firebase hosting. The numerous reason are:

1. I can use Firebase CLI tools from both Windows and my LINUX PCs to upload new and sync modified content to the host. Previously, I could only do this on Windows using WinSCP linking by private keys.
2. There is no virtual machine for me to manage. I don't have to periodically SSH in and apply updates. I also don't have to worry about it crashing.
3. No VM means no backup snapshots consuming disk space at GCP and me getting charged a few pennies per month - which was only going to grow as more snapshot backups were made.
4. I get to use the full 10GB of no cost firebase storage for my static website(s) content.
5. Firebase applies SSL (HTTPS) automatically, so I don't have to use the let's encrypt bot.
6. Firebase hosting provides CDNs to distribute content globally.
7. It's still free, provided I shut down my GCP instance and purge the snapshots on this particular Google account.
8. Google Page Speed Insights show no loss in page loading performance compared to my GCP micro instance.

## JamStack / Flatfile
![Debian 9 server](/images/tech/Debian_9_logo-100px.jpg#floatright)Recognizing the complexity and vulnerability of the MySQL-backed CMS frameworks has led me to seek simplification in website development. I've had a Drupal 7 site hacked (pictured above) because the developer didn't promptly apply core updates. I've had a Wordpress site outgrow it's virtual server, crashing the server while attempting a code update. Data loss ensued and so did frustration. I tried playing with several flat-file CMSs including Gatsby and Grav. My repeated attempts to install and configure a site on a GCP virtual server with Grav failed. I know I had problems with linux file permissions on my VM host, and not being an expert I followed several "recipes" on the web. None worked for me, and eventually I had a convoluted mess so I purged it all. I finally realized there were complexities with PHP versions, extensions and other server settings that I found too frustrating.
Then I discovered Hugo. Woah. I relaunched a basic Debian 9 virtual server with apache at GCP and it's been running ever since. 

>JAMstack: noun \’jam-stak’\ 
>Modern web development architecture based on client-side **J**avaScript, reusable **A**PIs, and prebuilt **M**arkup.
>jamstack.org

## Hugo
![Hugo CMS](/images/tech/hugo-logo-wide-275px.gif#floatright)With Hugo, all of the inputs are either simple text code, (usually) stock javascript, or the images. A hugo site will run from the simplest of webservers, so my GCP "micro" debian VM was no longer a problem. And I can draft and manage content on my old personal computers or even from my android phone. The catch is I've not yet implemented a "continuous deployment" solution. As I create content, I upload it to my VM host using WinSCP. "Cons" of my setup include:

1. Site content additions or deletions are only achieved by WinSCP from a Windows computer. (Not anymore! see #1 above.)
2. Learning "MarkDown" language syntax. (not very difficult)
3. Image processing is necessary to "right size" the full resolution images, as well as batch generating thumbnails for image galleries.
4. I can't modify my published website from my linux computer, although I can draft new or revise existing content, preparing it for upload.(Not anymore! see #1 under Firebase above.)
5. I can't actually post from my phone. I've never done this anyway, but I can rough-out new content with a text editor and a bluetooth keyboard.

I anticipate that numbers 1 and 4 above are the dealbreakers for most readers. For you, the Netlify, Firebase and other hosting solutions are well documented on the goHugo.io site. I brought these constraints upon myself because I wanted to use a free tier Google Compute Engine virtual machine. Some of you linux people will be comfortable connecting to your VM by terminal and transferring files using command line tools such as rsync. Cool for you! That's not me.
I've always used PhotoShop or similar image editing software to prepare images intended for my WordPress or Drupal sites, so this is normal to me. I like them appropriately cropped and "right-sized" for their intended display resolution, minimizing any excessive download burdens.

## Text editing tools
Different computer platforms often require different tools, and I can appreciate how this may itself add a layer of complexity and cause concern for those considering Hugo CMS. While you can use a basic text editor on any and all platforms, this requires that you're already familiar with the Markdown language and don't need a preview. I'll share my tools:

1. On Windows I use **Notepad++**. This allows me to generate the markdown code for my post. Adding the extension MarkdownViewer++ to Notepad++ offers a nice preview pane so I can admire my work as I type or revise.
2. On Linux (xubuntu) I use **ReText**. Notepad++ wasn't able to install the MarkdownViewer++ extension for ubuntu, so I had to find an alternative. ReText works fine and includes the side-pane preview, plus menu-based formatting choices for GUI-dependent losers like myself. 
3. On my android phone I use the __Turbo Editor__ app. It has a dark theme, and offers colorized code highlighting (but sometimes highlights things it shouldn't - such as between single apostrophes. There is a "View markdown result" choice which previews your work within Turbo Editor. There is no side-by-side preview pane, but it's a phone screen. Do you really have room for that?

Of these, I think I like ReText the best so far, though the preview isn't perfect. For instance, it ignores ordered (numbered) lists.

## Content Management
I store my Hugo website development directory and associated "raw files" or "working" folders in Dropbox. This folder gets synchronized between my personal windows laptop, my windows PC at work, and my linux box. It is also on my android phone. So, I can access my content to write new posts or edit existing content from any device and it all gets synced via DropBox. Note that it does not "go live" to the web until I upload it to the virtual host using WinSCP. Obviously, if you're considering Hugo or any JamStack solution you should carefully consider using one of the continuous deployment solutions such as with Netlify, GitHub, Forestry.io, or similar.

## Markdown Syntax
It is really simple to learn MarkDown once you start using it. I feel it's easier than HTML, though it's purpose is more limited. Numerous "cheat sheets" exist for markdown syntax on line, and my technique was to develop a template "template_post.md" file in my posts directory. To this file I added example markdown syntax to the bottom, providing examples of numbered lists, links, embedded images, and tables. Whenever I create a new post, I simply duplicate this file and rename it with the post name, then start writing. All of my syntax tips are just a mouse scroll away, and I delete this before I finalize and post the content, changing "draft: false" to "draft: true" for publication. 

Here's a convenient, printable markdown syntax guide: https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf

One limitation I've discovered with MarkDown is that there is no way to insert an image or external link set to open in a new tab or window. Most solutions suggest just using the HTML `<a hrefs target='blank'` code. I'd rather not mix HTML with markdown if I can help it. I have seen references to certain flavors of markdown, or certain markdown renderers, which can overcome this limitation, but my understanding is that the current version of Hugo does not.
