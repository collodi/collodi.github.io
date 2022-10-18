---
layout: post
title: First Thoughts on BelayVision
topic: Safer Autobelay
featured: True
---

Before I begin, I’d like to say that this post is a jumble of all my ideas relating to BelayVision.
Don’t expect too much structure or clear thoughts on this one.

Goal
---

The goal of BelayVision is to design and implement a system that can detect dangerous behaviors while using an autobelay.
The system must be easy to use for end users and avoid utilizing extra hardware other than those already commonly found in climbing gyms.

How does it work?
---

The ideal implementation of the system would be to track all humans and autobelay lines in a video.
However, detecting the autobelay lines with high accuracy in different scenarios requires a moderate amount of training data that I don’t have.
So, we make some assumptions to make the problem easier to solve, and leave the harder problem for the future.

Our problem consists of 2 smaller subproblems.
First is to detect the altitude of every person (relative to the gym floor).
An object detection network can easily output an enclosing box for every human, so this problem is pretty straightforward.

The trickier problem is to detect if an autobelay is in use or not.
For the initial design, we make use of the autobelay manufacturers’ triangle at the bottom.
If the triangle is in its upright position, we assume that the autobelay is not in use.

The assumption we made here is that if an autobelay is either clipped into the triangle or a climber.
This assumption is not always true, and we’ll talk about that later in discussions.

Also, we’ll start with image processing, but ideally we’ll progress to process video inputs.

To summarize, each autobelay lane is tagged with the autobelay use flag and a climber present above the threshold height flag.
If a climber is present and the autobelay is not in use in the same lane, we must sound the alarm.

Assumptions
---

Because the project aims to introduce no extra hardware, we assume that there are security cameras pointed at autobelay walls in most gyms.
I would guess this is a pretty safe assumption for most climbing gyms around the U.S. for insurance reasons.

We also assume that all autobelays have the triangles from the manufacturers of the autobelays to hold them down when not being used.
I’ve been to some other gyms that didn’t use the official triangles from the manufacturers, and I hope to relax this assumption in the future as mentioned above.

Another assumption that makes the system more robust is having the camera fixed at one angle.
This creates a stationary box where the triangle would be in the image, and triangle detection becomes much easier.
We haven’t talked about it much, but this also helps with establishing lane boundaries.

Also for now, we assume there are no objects blocking the vision of the camera to the autobelay wall. This assumption will hopefully be relaxed to temporary obstacles in the future.

Discussions
---

There are a few scenarios that can trigger false positives and false negatives for the current design.

The most obvious one is when a climber is free soloing on a runaway autobelay (clip is dangling at the top).
In this case, the system would see the triangle is down and not sound the alarm even when the climber is not clipped in.

The second case is when a climber (clipped in) goes out of their lane into another autobelay lane.
The system would see a triangle (from the other lane) directly below the climber and sound the alarm.
This is not necessarily a false positive because it’s generally against the rules to go out of the designated lane, but I’m not sure if an alarm is necessary.
Maybe a more soft alarm (alert the staff) is appropriate if we can detect this scenario.

The third case is when there are two climbers (one clipped in and one not) in one lane.
Without any modifications, the system would not sound the alarm for the climber who is not clipped in because the triangle is down.
To prevent this, we can implement a simple policy to sound the alarm when there are multiple climbers above the threshold height in one lane.

I think we are at a good starting point, and I’ll try to come up with a proof-of-concept next.
My hope is that we can collect enough training data for our ideal design with this version of the system.

Thanks for reading, and hope you enjoyed it!
