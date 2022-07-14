---
layout: post
title: Introducing BelaySound
topic: Safer Autobelay
---

In my last semester of school, I had to do a project that utilized different sensors on a smart device.
I wanted a project that I would be psyched to work on, so I decided to bring climbing into it.

At the time, we had a couple incidents where the climber completely forgot to clip into the auto belay at our local gym.
I decided that this is a worthwhile problem to tackle.
To make it a little more interesting for the class, I decided to use the audio signals in my solution.

The project is called BelaySound. The proof of concept can be found on my [repo](https://github.com/collodi/belaysound).
A detailed write up can be downloaded [here](https://github.com/collodi/belaysound/raw/main/BelaySound.pdf).

Using the audio signal over vision has many caveats.
One of the biggest disadvantages is that the machine learning network must be trained separately for every line.
This is because the sound propagation heavily depends on the shape of the wall and the room.
So, a recording of the exact same behavior can sound very different depending on the location on the wall.
In extreme cases, we may need new training data for newly set routes or even different climbers.

On the other hand, one of the advantages is that it’s very hard to mask the sound of a climber on an auto belay.
Even with some background noise, the sound of the auto belay will still be present.
This is not the case for vision where the auto belay can be blocked by an obstacle.

The next step for this project is to see how the visual system performs.
Stay tuned!
