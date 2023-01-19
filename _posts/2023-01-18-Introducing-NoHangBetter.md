---
layout: post
title: Introducing NoHangBetter
topic: Better Hangboard
featured: True
---

The app is here! It’s called NoHangBetter, and it should be available for Android soon.
The bad news is that I don’t have a Mac, and I can’t develop or test the iPhone version.
Hopefully, this will happen in the future.

The app’s normal flow will be to connect to the scale through bluetooth first, pin your weight, set up your timer, and work.
There may be bugs with permissions and bluetooth features.
Please open an issue on github if you find any.

The timer flow goes prepare, work, rest, work, rest, …, work.
Note it always starts with prepare and the last rest is skipped.
If one arm mode is on, the flow is a little different.
For 2 sets, it goes prepare, work (left), prepare, work (right), rest, work (left), prepare, work (right).
Of course, you can choose which side you do first. 
It sounds complicated, but it should be quite straightforward once you try it on the app.

There are some bugs and caveats to this system.
The first is that the weight scale used does not update the weight through bluetooth when the user steps down.
So, you’ll see the app get stuck at some number when you step down from the scale.
This is possible to solve through the app, but it actually doesn’t present any problem when you’re actively using the scale, so we may never address it.

The second caveat is that the weight scale freezes when the weight doesn’t change for a time.
This is a problem because during this freeze time, the scale doesn’t update the weight through bluetooth.
It’s easily mitigated by stepping down from the scale for a short time.
The only way to fix this is building your own scale (since most scales freeze), but this would drive up the cost way too high.

The last one is something we mentioned last time.
The scale doesn’t operate to our desire when it’s on a soft surface (like a gym mat) because physics.
The errors on percentage seems to be low, but I was still getting about 5% difference, so I’m not sure if it’s usable for most people.

Considering the simplicity and the cost of the system, I think these disadvantages are quite bearable.
I believe there is a company that makes hangboards that can measure the hanging load.
They have their own system, so I would guess it’s much fancier and less buggy.
However, I’m pretty sure they are quite expensive (in the hundreds of dollars) whereas our app is free and it costs $20 to buy the scale.
Another advantage of our system is that you can use any hangboard you like.

The scale is the Xiaomi Mi 2, and you can buy it on Amazon.
The link is [here](https://a.co/d/dXOVuXT).

This project is open-source, and you can find the source [here](https://github.com/collodi/nohangbetter) on github.
For any feature requests or bug reports, please open an issue with an appropriate label.


This was a simple and fun project for me, and I hope you guys enjoy it!
