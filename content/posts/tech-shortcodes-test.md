---
title: Shortcodes Test
date: 2019-06-14T19:00:52-06:00
lastmod: 2019-07-14T19:00:52-06:00
cover: "/images/cards/shortcodes-640x420.jpg"
draft: false
categories: ["tech"]
tags: ["web design"]
description: Test of custom shortcodes for Hugo.
---

# Hugo Shortcodes
Shortcodes are little snippets of code that can be called from within a post to perform an action. Hugo comes with a few shortcodes baked in such as "figure", but others I've gleaned from internet searches and perhaps from my own tinkering.

## Folder-based Image Gallery
from a folder of pictures within "website/hugo/howisjt/static/". Don't put a slash in front of the "images" directory. This is different from all others.
{{< foldergallery src="images/travel/dadeville/house" >}}

## Youtube 
Just insert "youtube" with the unique video code. Here is the Baton Rouge High Symphony Orchestra.
{{< youtube hnQQDMK8WVw >}}

## Vimeo
{{< vimeo 146022717 >}}

## Figure
Figure is an extension of the image syntax in markdown.  You can use multiple arguments. Displays as a flat image with no shadow background.
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.\
{{< figure src="/images/cards/camping-clear-springs-640x420.jpg" title="Clear Springs Campground" >}}

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

{{< figure class="floatright" src="/images/cards/default2.jpg" title="Scaled down, float right." >}} Here is a same size image using the figure command with a floatright argument. It works nicely, scaling down the fullsize image (no thumbnail required) and provides a buffer from the text. Probably too much buffer space. Again, it is flat styled with no shadowing.\
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim est laborum.


## Regular image insert
The theme's CSS adds the shadow and centers the image.
![Woody the Dog](/images/woodyavatar.jpg "Woody is my silly puppy.")

## Insert an Instagram image
The Instagram shortcode is now broken as of 11/29/2020, and probably a while before that. It seems Instagram is blocking the downloading of images.


## audio file player
Be cautious using this because I fear I'd have to host the audio files on my virtual server which could consume valuable disk space. There must be a more efficient way to embed audio hosted elsewhere. Here is a 3MB Sky Tour podcast.
{{< audio mp3="/audio/SkyTour-February-2019.mp3" >}}

## Google Map
Below should be a single point google map iframe locating our house. It pulls my Google API key from the toml file. Woops, looks like the gmaps function has closed down. Thanks Google...\
{{< gmap height="300" location="4932 Front Royal Dr, Baton Rouge, LA" >}}


An embedded "Google My Map" - my Bucket List. I have to intentionally define the maps zoom by appending "&zoom=6" to the src= .\
<iframe src="https://www.google.com/maps/d/embed?mid=1UaY6uD_OlvffgJuvMOv0roz6N-s&zoom=6" width="100%" height="480"></iframe>

## Gallery Slider
An image slider with customizable features. See https://github.com/tbiering/hugo-slider-shortcode  It displays scaled images but cannot allow visitors to click to enlarge an image - such as with lightbox. Also, it is not mobile friendly; it doesn't scale to fit the width of small screens correctly.

Default use-case

{{< gallery-slider dir="/images/planning/recognition/gallery" >}}


Set width and height. This isn't working. It always displays the same size regardless of the values I feed it for width and height. 
{{< gallery-slider dir="/images/hobby/camping/chuckbox/mine" width="200px" height="150px" >}}


Set left and right icon. This example uses the double chevron icons. These are pulled from FontAwesome.
{{< gallery-slider dir="/images/hobby/camping/chuckbox/others" arrow-left="fa-angle-double-left" arrow-right="fa-angle-double-right" >}}


Set automatic sliding duration of 200ms. Doesn't work.
{{< gallery-slider dir="/images/hobby/camping/florida" auto-slide="200" >}}


## Slide
An image slider drawing from a directory of JPGs. There must be a CSS conflict because it's not displaying the images properly. It displays successive images below the previous, not over the top of the previous, replacing it. Weird.

{{< slide "/images/travel/batonrouge" >}}