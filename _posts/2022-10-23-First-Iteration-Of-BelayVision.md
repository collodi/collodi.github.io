This article details my first implementation of BelayVision.
There are many aspects of the project that require huge improvements, but overall, I think we have a good start.
The source for this project can be found [here](https://github.com/collodi/belayvision) on my github.

I’d like to start with some assumptions that simplified the scope of the project for this iteration.
We first assume that there is only one autobelay lane in the input image.
This is definitely not a realistic assumption, but lane detection is a tricky subject, so I decided to leave it out for future iterations.
Second, we assume that the entire autobelay lane is not blocked by any obstacles.
Remember that these assumptions are laid on top of the ones we discussed previously in [this post]({% post_url 2022-07-24-First-Thoughts-on-BelayVision %}).

Now, we can go into system design.
The first step is to define the locations of all the static objects of interest.
Namely, the altitude threshold and the autobelay triangle.
These are static because we assume that the camera does not move.

For more flexibility, we define the altitude threshold with a polygon that encloses the “safe” area.
Safe here just simply means a relatively low risk of serious injuries without an autobelay.
In the same way, the location of the autobelay triangle is defined by a 3-point polygon.

Next step, we must detect all humans in the image.
We use PyTorch’s pretrained YOLOv5m model and filter out results with confidence lower than 60%.
Then, we tag each human outside of the “safe” polygon as “climbing”.

Now, we can introduce the alarm logic.
If there are no climbers, no alarms will sound.
If there are multiple climbers, we automatically sound the alarm since this means there are multiple climbers on one autobelay (for this iteration).
If there is only one climber, we can further perform triangle detection, and if the triangle is up, we sound the alarm.

The triangle detection can be done in many different ways depending on the resources you have.
As for this implementation, the algorithm is deterministic.
We randomly picked a frame out of the video and extracted the autobelay triangle.
This image only contains the area defined by the triangle polygon, and it serves as the model image.
Here, it is important that we store this model image in a lossless format.

The detection algorithm works by measuring the distance between the model image and the test image in the L*a*b* colorspace.
We empirically pick an arbitrary similarity threshold of this measurement.

As you may imagine, this method for triangle detection is far from perfect.
There are a few different approaches that may perform better.
One idea is to use the nearest neighbor with a pretrained encoder network.

![A snippet of the algorithm visualization](/public/assets/it1.gif)

You can see the full video [here](https://photos.app.goo.gl/Bk69SvL7W2xayRfBA).
The red horizontal line is the height threshold.
The first video is 4 fps, while the second video is 29 fps.
The first video is what the algorithm actually processes in real time.

This sums up the first implementation of BelayVision, and I’d like to talk a little more about possible future improvements.

One of the big disadvantages of the triangle detection approach over the autobelay line detection was that we wouldn’t be able to detect a runaway autobelay.
Thinking about it again, the solution is quite simple.
We can simply detect a runaway autobelay just like we detect the autobelay triangle because the location of the autobelay is fixed.
The accuracy may suffer just like in the case of the triangle detection, but it’s better than nothing.

Another important topic is lane detection.
As you might remember, this is only required in the case of the triangle detection approach.
Until we have a reliable way to detect autobelay lines on climbers, we must come up with a different approach to pair an autobelay to a climber.
Simply having vertical lines to segment a climber’s lane should cover most use cases.
I’m guessing there will be unforeseen edge cases that we must tackle in the future.

A lot of our problems stem from not having a dataset to train our own neural networks.
Going through the first iteration, we realized the greater importance of having a climbing specific dataset.
One instance that surprised me was how many times YOLOv5 failed to detect a climber as a person.
I’m speculating that this is because climbers’ body positions on the wall are rarely found in the normal object detection dataset.

—

The following is a side note on deterministic approach to autobelay line detection.

I wanted to see how a deterministic line detection algorithm would perform in our autobelay line detection approach, namely the HoughLinesP() function in OpenCV.

The conclusion was that this deterministic method would have to be really really complicated to have a desired accuracy.
One of the interesting facts I found was that the HoughLinesP() actually detects the shadow of the autobelay line.
This may come as an important insight for any future line detection algorithms.

—

This post took me a long time to publish even though the implementation was quite fast.
Sorry for the delay, and I will try to post a little more frequently.

Lastly, I’d like to thank [ABC Climbing](https://www.abckidsboulder.com) for letting me use their facility for this project.
