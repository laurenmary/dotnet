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
    + I wasn't sure if I would be using USB or 3.5 mm to connect my microphone - I ultimately chose the retailer I did because they sell this cheap sound card #notsponsored
+ A microSD card
+ USB extension cable
    + I believe I got the suggestion from someone in [this GitHub discussion about microphones for BirdNET-Pi](https://github.com/mcguirepr89/BirdNET-Pi/discussions/39) to not plug a USB microphone directly into the pi due to noise

Since I'm #blessed to work at a university library that has a relatively robust collection of media production equipment, I checked out 3 different types of microphones for testing:
+ [Blue Snowball USB mic](http://recordinghacks.com/microphones/Blue-Microphones/Snowball)
+ [RØDE VideoMicro](https://www.bhphotovideo.com/c/product/1183909-REG/rode_videomicro_compact_on_camera.html)
+ [RØDE VideoMic](http://recordinghacks.com/microphones/Rode/VideoMic)

"Testing" makes it sound a bit more involved than it actually was - I ended up not even trying the RØDE VideoMic because, once I got the software up and running, I didn't want to fall in love with a $250 mic that I would ultimately have to purchase.
