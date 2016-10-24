---
published: false
layout: post
title:  "Create gif image for GitHub readme"
date:   2016-10-10 14:00:00 +0300
categories: android, github, gif, android-studio
---

Once you write an application or library. You want to share it with other people. The best way for demonstaration is gif animation. It's lightweight, save time and provide robust information about your project.

-Is it hard?
-No, it's requre few steps.

### AZ Screen Recorder - No Root

* Record video
* Can create Gif animation in pro version
Can create screenshots in free version
* [Google Play](https://play.google.com/store/apps/details?id=com.hecorat.screenrecorder.free> )

### Android Studio Record video from device

#### AS

* Start Android Studio and run your application
* Go to the Android Monitor at the bottom of Android Studio
* Start record video by click the Record Video button. Set up resolution and bitrate
* Close and save record then you done

#### FFmpeg

* Download FFmpeg. Select OS, download static version
* Unpack
* Go to the unpacked folder find bin folder inside
* Copy FFmpeg to the video directory
* Open comandline (power shell or terminal)
* Run one of the folowing command. It depends of what frame per second your want 

```bat
ffmpeg -i myvideo.avi -vf fps=1/60 img%03d.jpg // every 1 minute

ffmpeg -i "device-2016-04-24-003254 - Copy.mp4" -vf fps=1/1 img%03d.jpg // every 1 second
ffmpeg -i "device-2016-04-24-003254 - Copy.mp4" -vf fps=2/1 img%03d.jpg // every 1/2 second
```

Some details:

* *-i* - input video name
* *-vf* - set fps
* *img%03d.jpg* - pattern output image nameing

#### GIFCreator.me

GIFCreator.me is a free online gif maker and gif editor, with it you can make funny animated gifs from your photos or paintings, edit a gif with a few clicks, no ad watermarks, no need to register or download any software.
[GIFCreator.me](http://gifcreator.me/)

* Upload set of images to this site.
* Configure output gif image size, speed
* Download your gif image

It's Done! Hooray. 
