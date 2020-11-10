# mids-w251-fa2020-hw11

This repository is my homework #11 for MIDS W251 (FA2020).

### The links to videos are here:

* [First episode](https://mids-w251-jtrobec.s3.us-east-2.amazonaws.com/episode0.mp4)
* [Episode 1000 - middle](https://mids-w251-jtrobec.s3.us-east-2.amazonaws.com/episode1000.mp4)
* [Episode 1950 - end](https://mids-w251-jtrobec.s3.us-east-2.amazonaws.com/episode1950.mp4)

Note: I cannot play these directly in my browser, but if I download and open them, they play fine. Must be some unusual codec.

### Questions:

> What parameters did you change, and what values did you use?

I changed the number of neurons in the layers. My best run was 150/120. I also changed the learning rate to 0.0005 (cut it in half, basically). Another thing I tried was increasing the epsilon decay to 0.997. Finally, I increased the number of epochs to 10.

> Whhy did you change these parameters?

I changed the number of neurons because the original network seemed very small, and not capable of learning very much. I reduced the learning rate, because when I watched the training process, I got the sense that it would over-correct for things. Could have been my imagination, but it seemed to help. Increasing the epochs I hoped would mean that it would learn more from each episode, but I'm not sure if it did anything. Increasing the decay rate meant that it would do more random actions, which I guessed would mean that it would learn more at the expense of taking longer to converge.

> Did you try any other changes (like adding layers or changing the epsilon value) that made things better or worse?

I tried a few other things too: I added a third layer to the network, I added a new feature (sqrt(x-pos^2 + y-pos^2), or the total distance to the goal), and I also modified gamma. The new feature didn't hurt, but it didn't help as much as I had hoped. The other values got me further away, and sometimes didn't converge. Probably the most important change didn't really have anything to do with the newtork: I moved the generation of the video to every 20th episode. This actually dramatically sped up the execution of each episode, and allowed me to iterate faster and try more experimentation with the parameters.

> Did your changes improve or degrade the model? How close did you get to a test run with 100% of the scores above 200?

![Scores for my best model](ll-dqn-2layer.png?raw=true "Scores for my best model")

I got pretty close to 100%, at 98%. I tried a bunch of different changes (as described for previous questions) but I really was not able to improve on my best run.

> Based on what you observed, what conclusions can you draw about the different parameters and their values?

* Epsilon has a narrow useful range. Make it too small, and training will take ages, too big and you don't learn as much.
* Innitial settings for number of neurons in the layers were too small by a good bit. On the otherhand, making them 100x bigger doesn't actually help that much, all other things being equal.
* Adding a bunch of epochs doesn't really seem to do much.

> What is the purpose of the epsilon value?

The epsilon value dictates how much the learning process will explore new (random) approaches to solving the problem. More specifically, epsilon represents the probability that the agent will try something random. 1-epsilon then is the probability that the agent will use it's best available information to figure out what the next action should be. We start out relatively high, because the agent hasn't learned much and needs to explore to figure things out. We decay it over time, because as the agent learns, we want it to rely more and more on the best available information, reinforcing what it has learned.

> Describe "Q-Learning".

Q-learning is the process we use to train a neural network to figure out what the 'best' action is given the current state of a problem. It trains the network to do so by governing how the network explores possible options versus reinforces existing learning over time.
