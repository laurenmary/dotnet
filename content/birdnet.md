---
title: "identifying birds by sound using birdnet-pi"
date: 2023-12-22
draft: false
tags:
  - pi
  - birds
---

Recently, in the [comments of a Hacker News post](https://news.ycombinator.com/item?id=38553291) about the [Sound ID feature in the Merlin Bird ID app](https://www.macaulaylibrary.org/2021/06/22/behind-the-scenes-of-sound-id-in-merlin/), I learned about [BirdNET-Pi](https://github.com/mcguirepr89/BirdNET-Pi) and [BirdWeather](https://app.birdweather.com/). As both a half-assed birder and a half-assed home server admin, I couldn't wait to try setting it up myself.

## supplies
After a couple of days of research and shopping around, I purchased the following:
+ [Raspberry Pi 4B, 4 GB memory kit](https://www.pishop.us/product/raspberry-pi-4b-budget-kit/)
    + Includes a case, power supply, and heatsinks
+ [This cheapie USB sound card dongle](https://www.pishop.us/product/usb-audio-adapter-works-with-raspberry-pi/)
    + I wasn't sure if I would be using USB or 3.5 mm to connect my microphone - I ultimately chose the retailer I did because they sell this cheap sound card `#notsponsored`
+ A microSD card
+ USB extension cable
    + I believe I got the suggestion from someone in [this GitHub discussion about microphones for BirdNET-Pi](https://github.com/mcguirepr89/BirdNET-Pi/discussions/39) to not plug a USB microphone directly into the pi due to noise

Since I'm `#blessed` to work at a university library that has a relatively robust collection of media production equipment, I checked out 3 different types of microphones for testing:
+ [Blue Snowball USB mic](http://recordinghacks.com/microphones/Blue-Microphones/Snowball)
+ [RØDE VideoMicro](https://www.bhphotovideo.com/c/product/1183909-REG/rode_videomicro_compact_on_camera.html)
+ [RØDE VideoMic](http://recordinghacks.com/microphones/Rode/VideoMic)

"Testing" makes it sound a bit more involved than it actually was - I ended up not even trying the RØDE VideoMic because, once I got the software up and running, I didn't want to fall in love with a $250 mic that I would ultimately have to purchase.

## setup
[The installation guide for BirdNET-Pi](https://github.com/mcguirepr89/BirdNET-Pi/wiki/Installation-Guide) is very helpful, although a little outdated. Since the release of Debian Bookworm and the update to Raspberry Pi OS, the requisite operating system for BirdNET-Pi has been buried a little bit in the Raspberry Pi Imager.

I originally imaged my SD card with Raspberry Pi OS Lite (64-bit), the newer, Bookworm-based image. When installing BirdNET-Pi, this caused the installation to fail, resulting in this error:

```
ERROR: tflite_runtime-2.6.0-cp39-none-linux_aarch64.whl is not a supported wheel on this platform.
The installation exited unsuccessfully.
```

Thankfully it was easy to re-image the OS the correct Debian Bullseye image, now titled Raspberry Pi OS (Legacy, 64-bit) Lite.

After that, I added a local DNS record for `birdnet.local` using [Pi-hole](https://pi-hole.net), which we have running on another raspberry pi.

That was really it! I was surprised at how easy it was to get up and running. I put the Snowball mic out on our porch, ran the cable under a french door, and plugged the pi into a nearby outlet in our living room.

## birds from Cuba and beyond
When the first detections started coming in, they were incorrect. I don't remember all the birds, but there were a handful from Sub-Saharan Africa and a [Cuban Pewee](https://ebird.org/species/cubpew1).

Thankfully, I was able to find [an issue](https://github.com/mcguirepr89/BirdNET-Pi/issues/988) that helped me fix it. I just had to change the BirdNET model from the installed default of `BirdNET_6K_GLOBAL_MODEL (2020)` to `BirdNET_GLOBAL_6K_V2.4_Model_FP16 (2023)` which was easy to do in the settings of the web interface.

## listening to peeps
Of course, I got this all set up right before I needed to start getting ready for a family gathering. I took these two screenshots so I could better explain the whole thing to my mom. Click to enlarge.

[![[firstbirds.png|350]]](/firstbirds.png)
[![[firstrecent.png|350]]](/firstrecent.png)

I brought in the Snowball that night, since the wind started to pick up and a bunch of rain was forecasted. Over the next week, I moved the pi to another spot and tried out the Snowball and the RØDE VideoMicro microphones.

As I reviewed the detections and their recordings, honestly, I couldn't tell much of a difference. The number of detections per day was similar with each mic. The recordings also sounded similar. I decided to purchase a Snowball mic of my own to use with the system, mostly because of how inexpensive it was with holiday sales. The attached stand is nice, too.

## notifications
My non-library-property mic arrived in the mail and I got the pi set up in its more permanent location, with the USB cord running through a window this time.

During my last few days of work before the holiday break, I spent a good amount of time daydreaming about all the birds it was hearing and wishing I could access the dashboard while away from home.

From my understanding, the safest way of doing this would be through some sort of VPN instead of exposing it to the web. Could/should I use WayVNC built into Raspberry Pi OS? Wireguard? Headscale? I guess I'm just not motivated enough right now to figure it out, so I used the lovely, integrated [Apprise](https://github.com/caronc/apprise) notifications from the settings of the BirdNET-Pi web interface.

I set up both a weekly summary and "uncommon birds" (detected ≤5 times in the last 7 days) notification that gets sent to my email. Hopefully this is enough to sate my curiosity while I'm at work, longing for home. 
