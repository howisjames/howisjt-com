---
title: Hugo Image Gallery
date: 2019-05-04T19:00:52-06:00
lastmod: 2019-05-26T19:00:52-06:00
cover: "/images/tech/foldergallery-example_640.jpg"
draft: false
categories: ["tech"]
tags: ["web design"]
description: Comparing a few options.
---
My new Hugo blog website wouldn't be complete without the ability to host and display photos in an efficient, quick loading and mobile friendly manner. I searched around a bit examining several options. Each has pros and cons in my opinion, yet none of the sources for this code seemed to acknowledge the existence of the others. I'm providing links to the source where I found each of these, although those developers may have pulled it from somewhere else. Please don't hold me responsible for their potential intellectual "borrowing."

## Attempt #1 - Hugo Easy Gallery
https://www.liwen.id.au/heg/

Code author Li-Wen Yip clearly has this implementation of photoswipe working on his site, but I've had trouble.\
Failed: presumably due to a conflict in the CSS somewhere. I searched and searched without finding it. I tried renaming variables in the CSS accompanying the script to no avail. The problem I encountered was that the gallery displayed little thumbnail versions of the image but only partially covering each of the larger images. It's as if the images were loaded twice, with the second covering just a portion of the intended space. (Note to self: a screen-shot here would better conveys the problem to readers.) Also, when I clicked on an image to view it in lightbox, controls and other features never worked properly. I think I had a script problem, a CSS problem, maybe both. (My theme utilizes the Semantic UI 2.4.2 CSS in addition to it's own "site.css" so it is fairly complex.) This experience with easy gallery and photoswipe was disappointing because, from what I saw on the  source site, this seemed the ideal solution for me. In the end, Easy Gallery wasn't so easy. Perhaps a Hugo user will pick it up and write a new tutorial from scratch so that I can discover my error. Alternately, I could try switching to a different Hugo theme. Naa.


## Attempt #2 - Goggle Photo Album
https://www.google.com/photos/about/

Failed: I couldn't find an open-source way to display the album contents as thumbnails. Sure, you can purchase a 3rd party tool [Galleria.io](https://galleria.io) to do this, or  just place a link to the Goggle album in your blog post, but simply displaying a link doesn't help the appearance of my page. I want some photos! Goggle Photos does of course have the benefit of handling the hosting of all of your images in an interface that allows you to easily create, rearrange, and append or delete images to the gallery with no other programming or image processing tools needed. And, my phone automatically uploads my pictures there anyway. So I am motivated to keep looking.\

One tool I'm watching is [publicalbum.org](https://www.publicalbum.org/blog/embedding-google-photos-albums). After creating an album within goggle photos, you copy the shared album link and then go over to publicalbum.org and paste it into a form which generates code which you then embed in your site. Problem #1 is that this would be pasting HTML code into my Hugo markdown file. I'm not sure it will work. Problem #2 is that this is mostly just another image carousel. The developer has been improving this though. It does not display thumbnails and the overall appearance rather poor. Some users report that subsequent additions, deletions or changes to photos within your Goggle photos album will not be properly reflected in this publicalbum iframe. You have to go back and regenerate the code every time you add photos to the Google album.


## Attempt #3 - Flickr Photo Album
Failed: Flickr shares benefits with Google Photos in that it handles the hosting of your images (but unlike Google there is a limit of 1,000 in free account), you don't have to resize them, and creating or modifying albums is easy. Also, Flickr allows you to embed an image gallery into your web page. But, it only offers a slideshow view where clicking advances to the next full image. There is no thumbnail gallery view. Also, inserting an iframe into a Hugo site is sort of like pouring orange juice into a glass of cold milk.\ Why...just, why?


## Attempt #4 - Folder Gallery, version 1
https://dev.to/sarmis/building-a-folder-based-gallery-for-hugo-4i8c

Another implementation:
https://greekdeveloper.com/2018/folder-based-gallery-for-hugo/

Failed: Wouldn't display images from the "static" folder where I intended to keep my images. Essentially, I found two versions of this Folder Gallery code. (And now I've got them confused so bear with me while I straighten this out and post the correct information.) This first one expects to pull images from a "content" folder associated with each of your blog posts, so every blog entry itself would have to be contained within a subdirectory bearing it's name. This may be ideal for some of you who set up your site with the folder-based blog post format. I can see how that makes sense to keep the visual content together with the narrative content for any particular post. If I were building a huge blog site with lots of posts which would inevitably require "retiring" older content, this is the preferred file management technique for Hugo. But I don't need that. I tried modifying this code to suite my needs without success - you may have the skills to accomplish this.\
**Follow-up**: I think my problem was following the directions on these and putting the calls to load the javascripts in the footer.html partial. Attempt #5 below is basically the same except I put the calls in the "init-head.html" partial of my Hugo theme. Also, don't try to use the newest jquery 3.4.x. I found the gallery is only formatted properly when using jquery version 3.3.1, including the display of controls, thumbnails button, etc.


## Attempt #5 - Folder Gallery, version 2
https://www.control-alt-del.org/posts/building-an-image-gallery-for-hugo/

Success! This version of the folder gallery script I found seeks images from the "static" folder in your Hugo directory. This jived with my file management technique, and it also worked immediately. It does require that you manually generate thumbnails of all images in the directory you wish to display. On linux, I use the command-line tool Imagemagic, like the author of the source blog. However, I did have to increase the thumbnail resolution from 100 x 100 (pixels) to 300 x 300. Otherwise, the tiny thumbnail images get stretched and look pixelated. The result was unprofessional. After regenerating new, larger thumbnails I found the resolution to be acceptable without too much of a performance hit. Also, the lightbox image viewer worked without a hitch.\
{{< foldergallery src="images/travel/dadeville/smith-mountain" >}}

### Pros
- Fast display of thumbnail images
- Clean layout so it looks like it belongs in my blog theme, not like an add-on
- Responsive so it is mobile friendly, controls work on mobile too

### Cons
- I'm self-hosting all my images from my virtual server
- No pulling from cloud-based image service
- It is tedious to collect, rename, resize and organize the images for each post (but is this a bad thing?)
- Changing album contents requires using WinSCP to add or remove images from my web server (not any more with Firebase hosting)

Solution #5 is not as simple as a GUI-based image manager such as a media library manager for Wordpress. There is no "drag-and-drop" nor automated scaling. But, then again, I'm implementing a very low overhead jamstack website solution. I've settled upon the idea that several of these solutions may be utilized together within the same website, if not on the same blog page. And they can also be co-mingled with hugo's [figure](https://gohugo.io/content-management/shortcodes/#figure) shortcode. After all, sometimes you just want a single image displayed but other times you want a gallery of the most appropriate images. Visitors who want to see even more pictures - including your "B"-roll - can click a link to the google album containing all images. This pushes the demand for media off the micro webserver instance and onto Google.

## Attempt #6 NanoGallery2
https://nanogallery2.nanostudio.org/

Failed: Nanogallery2 is a javascript extension which pulls images from a specific album of a Flickr or Google account. The code produced for embedding is HTML and it may very well work on a non-markdown site, but for me Hugo simply displays the HTML code when I generate the static site. It does not display the image gallery. This is a shame because the demo galleries on the project website are quite stunning. Loading of the nanogallery2 javascript also conflicted with my site's custom javascript, eliminating functionality until I figured out what had happened. Despite it's faults, this solution deserves further investigation.

## Possibility #7 Galleria
Not yet attempted: galleria.io offers a free JavaScript gallery framework released under the MIT license. This display is different in that it really appears like an image slider, showing one image at a time. But, controls are displayed in a bar at the bottom offering thumbnail view, play, count of images, pop-out, and full screen. An interesting possibility is that Galleria can connect to Flickr, Vimeo, Youtube and perhaps other online media repositories. Instructions for using this framework are all assuming you're coding in straight HTML, not markup; and I wasn't successful in finding any "hacks" to make it work for Hugo. But, this is worth pursuing because I suspect it might be possible. Galleria.io offers additional "fancy" themes for it's gallery for a fee.