---
title: Pi Zero Cam Upgrade
date: 2024-02-26T19:00:52-06:00
lastmod: 2024-02-28T19:00:52-06:00
cover: "/images/cards/pi-cam-640-425.jpg"
draft: false
categories: ["tech"]
tags: ["hardware", "open source"]
description: 16 MP Arducam on a Pi Zero W.
---
I bought my first (and so far only) [Raspberry Pi computer](https://www.raspberrypi.com/) in 2021 with the 5 MP "Pi cam 1" and set it up to capture time lapse images of a woodworking project. It worked pretty well, capturing images every 15 minutes while I worked on my project over an 18-month period. The result is a [2-minute time lapse movie](https://www.youtube.com/watch?v=Z3MccWJDgww). In late 2022 I participated in a Kickstarter campaign for Arducam's new 16 MP autofocus camera for Raspberry Pi, and ended up receiving one a few months later. 

## The Backstory

My newly acquired high resolution Arducam sat on a shelf for over a year for several reasons. First, my Pi computer is one of the lowest power models - the Pi Zero W - and I read it was underpowered to handle the high resolution video. Second, I learned the Arducam brand camera was not compatible with the open source software - MotionOS - which I installed on the Pi to run the camera. And lastly, I finished my woodworking project and hadn't started anything new. Things changed when I decided to start a new woodworking project and wanted to create another timelapse video to document the process. 

## Arducam Upgrade for Raspberry Pi

I wanted to use the new camera to take advantage of higher resolution images so that the video would be clearer and more detailed. But the aforementioned problems remained.

### Solutions

- I found an alternative to the MotionOS - just the Pi OS with libcamera extensions installed;
- I didn't need to capture images at 16 MP to create the time lapse video, lessening stress on the computer;
- I used spare "go pro" style camera mounts to build a better Pi cam mount.

## Libcamera

[Libcamera](https://libcamera.org/) is software. As the developers say it is "An open source camera stack and framework for Linux, Android, and ChromeOS." After installing the base Raspian (Linux) operating system, libcamera is installed to provide a means of controlling the camera hardware. Raspian includes software to control the native Raspberry brand camera hardware, but it does not work (as I understand at the time of this writing) with [Arducam](https://www.arducam.com/) hardware. 

The software allows one to control the camera via code instructions. I was hoping to find what I considered to be thorough documentation and "recipies" of appropriate code snippets for various photographic situations. So far I haven't found much other than code snippets and resulting photos from the efforts of a few hobbiests. If you know of more, I'd love to hear about it! Below is a list of the resources I've found so far:

Num.    | Site
--------|------
1       | [Waveshare.com](https://www.waveshare.com/wiki/Template:RPi_Camera_Libcamera_Guide#libcamera-still)
2       | [Arducam commands](https://docs.arducam.com/Raspberry-Pi-Camera/Native-camera/Libcamera-User-Guide/)
3       | [python script](https://picamera.readthedocs.io/en/release-1.13/recipes1.html#capturing-consistent-images)

### Overnight Timelapse

My first test of the camera was to capture a sequence of images overnight with the Pi camera pointed a Polaris, the north star. The result will be a "star trails" image which is a composite of all images. But I made a mistake and didn't sufficiently tighten the camera mount. Overnight it slowly, very slowly, drooped. The video below shows this error as the image seems to pan down towards the ground. But if you look close (in a dark room), really closely, you can see the apparent movement of the stars around Polaris. (Yea, yea astrophysicists - I'm well aware that it is our earth that is rotating and that, comparatively, the stars are stationary.)

{{< youtube NmnWbQiTu-8 >}}

Thankfully, Photoshop has a command to [auto-align](https://helpx.adobe.com/photoshop/using/aligning-layers.html#automatically_align_image_layers) a stacked layer. This allowed me to "undo" the drooping camera mount problem, and this brought the stars much closer to being in alignment. After applying other filters I stacked the images resulting in the following image. Not too bad for a first effort with just eyeballing the aiming of the device at Polaris.

	out = os.system("/usr/bin/libcamera-still --autofocus-range full --denoise off --sharpness 1.75 
	--shutter 10000000 --gain 2 --awbgains 2.2,2.3 --immediate -o /home/admin/shared/"+date+"_"+time+".jpg >>
	test.txt")

</br>

![Star Trails Image](/images/tech/pi-cam/star-trails_20240219.jpg)

### Daylight Timelapse

Test number two was a daylight time lapse sequence at comparatively close distance observing the bluebirds nesting in my new bluebird house. No motion detection was involved. The camera simply captured a full 16MP image once every 5 minutes. That night I visually scanned through the photos and discarded all without a bird in the frame. I batch renamed the images with sequential numbers, and then Photoshop was used to process the sequence into a very short video shown below.

{{< youtube LuZukTHq7KY >}}

	out = os.system("/usr/bin/libcamera-still --vflip --autofocus-range macro --autofocus-mode default
	--autofocus-window 0.25,0.25,0.5,0.5 --awb daylight --immediate -o /home/admin/shared/"+date+"_"+time+".jpg >>
	test.txt")

</br>
Now I'll try to explain what I understand of the libcamera instruction code...

yea. blank space.

---

### Gallery

{{< foldergallery src="images/tech/pi-cam" >}}

</br>

## Future Improvements

I'd like to get one of the new Raspberry Pi 5 computers to pair with my 16 MP Arducam. This would have plenty of processing power, allowing me to capture full resolution video. I'm certain there are other things I could do with it that I presently can't even imagine.