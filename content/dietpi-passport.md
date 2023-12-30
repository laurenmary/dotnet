---
title: "connecting 2TB passport to apple TV vis-à-vis dietpi"
date: 2023-11-04
draft: true
tags:
  - pi
  - bash
---
## what

## why

## how

### notes
#### bash
##### escaping characters
I'm spoiled by [ohmyzsh](https://ohmyz.sh)

thank you chatgpt

first I tried: ```mv "~/passport/watch/Serial Experiments Lain" "~/passport/watch/TV Shows/"``` which didn't work because

> the ~ tilde for the home directory doesn't expand to your home directory when it's inside single quotes. You need to keep the ~ outside of the quotes so that the shell can interpret it correctly.

so `mv ~/passport/watch/"Serial Experiments Lain" ~/passport/watch/"TV Shows"/` works

Of course, [Infuse](http://firecore.com/infuse) still didn't recognize the episodes after this, so I asked how to change `/Serial Experiments Lain` to `/Serial Experiments Lain (1998)`

Easy! keep using `mv`: `mv ~/passport/watch/"TV Shows"/"Serial Experiments Lain" ~/passport/watch/"TV Shows"/"Serial Experiments Lain (1998)"`

#### batch rename files

Adding the date *still* did not work, so I asked chatgpt:

> Inside the directory ~/passport/watch/TV Shows/Serial Experiments Lain (1998) there are 13 .mp4 files named 01.mp4, 02.mp4, 03.mp4 and so on. How would I rename those 13 files to be "Serial Experiments Lain S01 E01.mp4", "Serial Experiments Lain S01 E02.mp4", "Serial Experiments Lain S01 E03.mp4" and so on?

It gave me a shell script, but it didn't work when I pasted it in, and I figured it was the formatting. I asked how to run it inline (which I think is the correct term?)

Apparently I

> need to use semicolons to separate the commands when running it as a one-liner.

`for i in {01..13}.mp4; do mv "$i" "Serial Experiments Lain S01 E$i"; done` 👍
