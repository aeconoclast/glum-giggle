---
layout: page
title: "Free Mouse Clicks"
permalink: /free-mouse-clicks
---
# Free Mouse Clicks

After I installed Ubuntu on the PC that I built, I found myself clicking on the mouse more often.
I didn't know many hotkeys, and the PC didn't register all the clicks I made with my wireless mouse.
I couldn't use a wired mouse due to space constraints.

Looking for a way to automate mouse clicks, I landed on [ydotool](https://github.com/ReimuNotMoe/ydotool). 
[ydotool](https://github.com/ReimuNotMoe/ydotool) allows keyboard and other hardware inputs to be automated. But it had limitations.
One of them was that the press and release of the click button were separately timed.

The press and release routine in [ydotool](https://github.com/ReimuNotMoe/ydotool) was painfully slow. There would be a press, and after a delay, there would be a release. That made all mouse clicks, mouse drags. No option in _ydotool_ eliminated that delay.

## Issue, Work
This [issue](https://github.com/ReimuNotMoe/ydotool/issues/199) also talked about the same problem. I used that issue to create a pull request.

I decided to work on removing the delay. After looking through the code, and figuring out how it ran, I made the changes.
I added an option "-P" which did a rapid press and release.
After building those changes, I ran them myself for more than 2 months.

They are now part of this [release](https://github.com/aeconoclast/ydotool/releases/tag/1.0.5), and in this [repository](https://github.com/aeconoclast/ydotool). 

## Using ydotool with the changes
A few points on how to use this part of the tool are below.

1. Download the code ([zip file](https://github.com/aeconoclast/ydotool/archive/refs/tags/1.0.5.zip), or [tar archive](https://github.com/aeconoclast/ydotool/archive/refs/tags/1.0.5.tar.gz)), build it using the instructions in the [Notes](https://github.com/ReimuNotMoe/ydotool?tab=readme-ov-file#notes)
   - Instructions also given in [this askubuntu answer](https://askubuntu.com/a/1413830).
3. Run _ydotoold_ daemon. This is required to create the virtual devices for processing the input.
4. Then run ydotool client. For automated mouse clicks occurring every 2 seconds (or 2000 milliseconds) this is the command:
   - ``ydotool click -P 0xc0 -D 2000 -r 10000``
   - 10000 in the above command is the number of clicks.
5. The daemon and the client need _sudo_ permissions. Without those permissions, the tool does not work.

For certain tasks, you might not want the automated clicks. I workaround this by finding the ydotool process, and sending SIGSTOP like this:
``sudo kill -STOP <pid>``
To continue the process, send SIGCONT:
``sudo kill -CONT <pid>``

I found that 10000 clicks lasts about 6 hours. Change this number as you wish.
   
## Background

When I was asked to work from home in 2020 indefinitely/as much as possible, I started working from home with whatever setup I had.
But I didn't have to time to check if my home office setup was ergonomic. There were other concerns at that time needing my attention.
Ergonomics of my home setup was the last of my worries then.

Building a PC during the time spent not working from home, was a rewarding task. PCs act as a platform.
One of the tasks my PC let me do was the automation of the mouse click. There are many others, and I hope to talk about them in the future.
 
## 22-12-2025 Update
My additions have been [merged](https://github.com/ReimuNotMoe/ydotool/commit/708e96ff27e381a8c549418a9d34cdde12305317), and are now part of the [ydotool package](https://github.com/ReimuNotMoe/ydotool). Download and use ydotool from its original repository to enjoy rapid clicking!
