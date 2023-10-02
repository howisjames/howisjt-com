---
title: Multi-Theme Site
date: 2021-01-03T01:00:52.000Z
lastmod: 2022-01-6T01:00:52.000Z
cover: /images/cards/multitheme-card_640x420.jpg
draft: false
categories:
    - tech
tags:
    - hugo
    - themes
description: Use an alternate theme for a section of a Hugo site.
---
Website themes are great, providing a consistent appearance and layout of all pages in your website. Occasionally the need arises to format a particular section of your webite uniquely. Here I will describe how I've achieved this using two different themes in this website. I learned about this technique on this [Discourse thread](https://discourse.gohugo.io/t/two-themes-as-separate-hugo-directories-deployed-to-the-same-website/27899/4) As I began implementing this I ran into a few challenges that took me a bit of time to figure out. I'm providing a detailed account of my solution in hopes of assisting others.

>This broke (as of 12/2021) when I noticed that when I build my main site Hugo does not ignore the content of the secondary blog. Specifically, the ignoreFiles setting in the config.toml of the main site simply does not ignore the content within "stitchnglue", which is my subdirectory of posts within "content". The problem is that Hugo pulls all of the tags and categories specific to my sub-blog about kayak building and includes them with those of the main blog site where they are not applicable. It doesn't seem to build the sub-blog pages, however, as the links to them don't work. Refer to step #3 below...and to the [GoHugo.io documentation](https://gohugo.io/getting-started/configuration/#ignore-content-and-data-files-when-rendering).  For now, my work-around is to temporarily move the "stitchnglue" content directory containing my markdown and jpg files outside of the "content" directory when regenerating my main site. Perhaps the issue is that Hugo [cannot ignoreFiles recursively](https://github.com/gohugoio/hugo/issues/7748).

## Use Case

I'm about to begin a boat building project and I want to document it. I anticipate it will be a fairly lengthy and complex process with lots of descriptive details and photos. I could just write it all out on a few really long blog posts within my existing website as I've seen others do, but this is such a unique and content-rich topic I felt it deserved its own section. Perhaps it deserves its own website domain, but I'm too cheap for that. I wanted this content to be in a documentation blog style, and taxonomies had to be implemented to allow the filtered viewing of posts by category or keyword tag. These categories and tags were totally different from the posts in my main website, which was another reason to set this up as a separate entity. 

**See the demo!** The blog post you're reading now is within my main website, but I've created a second blog inside a subdirectory to host unique content as pictured below. [Click this link](https://howisjt.com/stitchnglue/) to see the unique style and content of the subsection within the main site.\
Below is a screenshot of what my modified version of the Hugo Creative Portfolio theme. I added the categories and tags features.

![screen capture of uniquely styled section](/img/screenshot-tn.jpg)


## Overview

Essentially, you include two Hugo themes and your post content for both website sections into the one build codebase and use two config.toml files to generate the two parts of the site. In this solution I have to run the hugo command twice to build both sets of content which are then uploaded to my webhost simultaneously.

### Terminology

The following terms have these meanings in my instructions below.

Term    | Definition
--------|------
main    | My main Hugo website at the bare domain, utilizing the main theme.
section | The subset of content to which a unique theme is applied.
root    | The base or "home" folder of my website's domain.
theme1  | The theme applied to the main Hugo website.
theme2  | The theme applied to the subsection only.


## Process

### 1. Set up both themes in the root/themes folder.
One theme is applied to your site as a whole. The second will be applied only to content within a specific section (directory or folder) within your website. 

### 2. Organize your content

#### Posts

The textual content displayed via the second theme will appear in a specific section of the website, in its own folder. Decide what this folder will be named, understanding it will be in the path of your URL. No spaces in the folder name. 
Content for the theme2 section must be stored in a single folder within root/content. The  [Discourse thread](https://discourse.gohugo.io/t/two-themes-as-separate-hugo-directories-deployed-to-the-same-website/27899/4) referenced above provides terrific directory structure diagrams which clarify this.

#### Static files

Content from either theme can reference anything stored in your site's root/static folder. But, I discovered that Hugo will pull all content from the static folder into both destinations, whether it is referenced or not. This creates extra bulk in your webhost, but otherwise no big deal.

One way to avoid this is to segregate static content into two separate folders within static. 

~~~

├── public
└── static
    ├── main
    │   ├── images
    │   ├── css
    │   └── ...
    └── section2
        ├── images
        ├── css
        └── ...
		
~~~

Then, in each config file you can define the path to the appropriate static files subdirectory.

~~~

staticDir = "static/main"
   or
staticDir = "static/section2"

~~~

You'll do this in the next step. It would be really beneficial in allowing you to not co-mingle custom CSS, JS or image files between two themes.

### 3. Set up the config.toml files

The main site will continue to use your original config.toml file. Add a line to instruct Hugo to exclude content within the special section content during site generation. Example below, the section folder to be ignored is "section2".

~~~

ignoreFiles = ["content/404.md", "content/about.md", "content/section2/\\.*"]

~~~

The second config file must have a unique name such as config-section2.toml.  You'll have to run Hugo separately on this second file by defining it's name as such:

~~~

hugo --config=config-section2.toml

~~~

In this second toml file you must specify the location of the source markdown files, the theme to apply, and the destination directory for the generated content.

~~~

theme = "theme2-name"
contentDir = "content/section2"
publishDir = "public/section2"
staticDir = "static/section2"

~~~


### 4. No Overrides

*This is a concern not mentioned in the Discourse post.* 
I may be a little slow, so it took me a while to realize what was causing style errors in my build.

Have you customized any of the css, html, partials, shortcodes or js of the site's main theme? If so you can't store them in root/static or root/layouts because they will override corresponding files of *both* themes.

All of these changes or additions must be made to files in the theme's corresponding static or layouts folders. This may create issues if you attempt to update a theme from the git repository source, because you risk overwriting your changes if you pull in new files from the theme source.

As stated above, static content can also be kept separate by defining the staticDir in the config.toml file for each theme.

~~~

staticDir = "static/main"`  - put all static files for the main site here
staticDir = "static/section2"  - put only static files for the subsection here

~~~

And, place no files in the root level of static.

You'll issue hugo commands to generate the main site and then again - specifying the second .toml file - to generate the section2 content. Then, all files are stored in the public directory.

