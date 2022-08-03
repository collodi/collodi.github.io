---
layout: post
title: Initial Discussion on Climber Localization
topic: Climber Localization
---

Thankfully, climber localization is a much easier topic than global localization, so we don’t have to shoot any satellites up into space.
A climbing wall is a 2D manifold in a 3D space and does not change shape.
This makes our job easier if we have the structure of the climbing wall.

Initially, we will mostly assume that the climbing wall does not change in angle.
This will simplify the problem and give us a solid understanding of the topic before we move on to harder techniques.

Over the article, we’ll talk about possible methods to localize a climber, different levels of climber localization, discuss use cases, and what the future might hold for the technology.

**Different Methods For Localization**

There can be multiple different ways to localize a climber.
The 2 most obvious ways that I can think of are visual and auditory.
You can see their examples in BelayVision and BelaySound, respectively.
You may also be able to use the vibration of the wall when the climber makes contact with the wall or holds.

The most efficient and general way would be visual in my opinion.
However, you might be able to achieve extra accuracy with other mediums depending on the use case.
Also, the cost of hardware can be a factor for using different mediums for localization.

**Levels Of Localization**

Not all localization techniques are equal.
Some are much harder to achieve than others.

Here are the levels that outline the difficulty of each technique (in my opinion).

Level 1: Approximate location of the climber on the wall
Level 2: Location of the enclosing box of the climber
Level 3: Location of specific body parts (hands, feet, arms, legs, hips, head, etc.)
Level 4: Orientation of body parts

The accuracy of approximation in level 1 can range widely.
The lowest accuracy would be to detect if the climber is on the wall or on the ground.
Whereas the highest accuracy can be within inches of the actual climber.

Obviously, the list is still in its infancy, and we’ll see how it changes once throughout different projects.

**Use Cases**

The use cases for climber localization can be categorized into 3 different buckets.
The first is when we use the location or orientation data given by the localization technique mentioned above.
The second is when we calculate new features from the spatial domain (images) using the given information.
For example, we can have a use case that calculates the center of gravity of a climber given the locations of their body parts.
The third is when we calculate features from the time domain (videos).
This can include instances where we utilize the velocity and trajectory of a climber in a dynamic coordination move.

I already have a couple of projects that utilize climber localization: BelaySound (Level 1) and BelayVision (Level 2).
Other examples would be to analyze popular routes, pinpoint cruxes, and analyze climber density on each part of the gym.

**Over And Beyond**

A technology that we can make a good use of with localization is identification.
If we have the identity of the climber, we can automatically log and analyze their progress: what they have sent, what their projects are, and even what their strengths and weaknesses are (we can calculate this by looking at which cruxes they stick and fall on).

An unusual use case of climber localization would be elbow tracking.
With elbow tracking, we may also be able to tell how pumped a specific climber is.
Since the correlation of elbow angle and the pumped-ness depends on each individual, we must utilize identification.

I feel super excited about this topic.
If I can meet my own expectations on the topic, I will be a happy man.
