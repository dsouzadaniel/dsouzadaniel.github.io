---
layout: post
comments: true
title:  "The Hidden Connection between Dropout Regularization and Sexual Reproduction"
categories : machine-learning
---
**Note:** This will not be a mathematical treatment of Dropout. It is meant to be a more intuitive way of approaching this topic.

![alt text][dropout_header]

Alright. Let’s address the elephant in the room. There’s a decent chance you clicked this post thinking “CLICK BAIT”. _Well, it’s not._

What if I told you that the team who invented “dropout regularization” for neural networks actually state “the role of sex in evolution” as the motivation behind the whole thing?

Now that I’ve got your attention, let’s dive right in! 😄 

Sexual reproduction essentially boils down to taking half the genes from one parent and half from the other and combining them in a random way to create a unique offspring. Consider the random part again. Notice how kids sometimes have very specific characteristics either from their dad or their mom? Sometimes they get dealt a good hand, and sometimes it’s the worst characteristics from the two. I digress.

Anyway, if we were supposedly carrying out this “offspring creation” in a lab somewhere and we wanted to win out on Darwin’s Law of Evolution, it would make sense to take the best genes from the dad and the best genes from the mom to create one “gene jackpot” of a baby, right? However, if you look back about 4,000,000 years, you’ll notice that this “chance” or “random” pairing that occurs in sexual reproduction has in fact led to the evolution of many advanced organisms! Natural Selection, anyone?

What does this tell you? Well, one possible explanation to this whole thing could be that maybe it’s not the “gene jackpot” that eventually wins out. Maybe, just maybe its the random pairing that causes genes to not rely on fixed partners to create a “winning formula”, but to constantly be forced to evolve to either be useful by itself or in conjunction with many different partner genes.

All this gene knowledge I’m dropping may seem a little hand wavy, but just bear with me. It should all make sense toward the end of the post 😄  

Now let’s get back to Neural Networks! 

What’s the first thing you do when your neural network fails terribly at learning a task? Well, you try fiddling with the parameters, right? You try experimenting with different linear/convolutional/pooling layer sizes until you get your scores up. What you unknowingly end up doing, is trying to find different “architectures” that you hope can help solve your problem better than the base architecture you started out with.

**`Enter Dropout`**. It is defined as “a technique for randomly dropping out units/neurons( and their connections) during training to make learning robust". It works beautifully and here’s why:
![alt text][dropout_diagram]
What happens when you randomly drop neurons ( say with a probability p = 0.5; so essentially half the neurons are randomly “switched off” during training ), you end up creating these new architectures within your model during the forward pass. Since along with the neurons, the connections are also switched off, you only back-propagate through this temporary new network that’s created randomly (still inside of your main network ). Let that sink in. For every single sample of your training data, for every epoch, you randomly switch on and off neurons, essentially creating an exponential number of these new networks that then force every neuron to learn to be useful by itself, and not just rely on another neuron to get by.

Some questions that may immediately follow :

* **But wait, if my original model by itself with all its power and glory and neurons can’t learn the task, what makes you think a subset of it will learn anything?** 😅
            Well, general practice when applying dropout is to make sure your model is sufficiently big enough to overfit, so that you know that sub-networks will be robust enough to learn important features. Also, you have an exponential number of different architecture combinations to utilize. You can try thinking of it, as combining a bunch of weak learners and averaging out their results multiple times over several epochs. 

* **Is there any proof this works from an obvious sense?** 🤔
            Dropout is a very commonly used regularization technique that’s bound to boost scores on almost any task. But just for discussion’s sake, in the task of identifying numbers (MNIST), here are features before and after dropout. Notice just how clearly each neuron now concentrates on some part of the image, providing some useful knowledge on identifying the number.
![alt text][dropout_features]
* **"Dropout does nothing for me!" or “Help! It actually lowers my scores"** 😞
Well, you gotta learn to use it the right way. Maybe your net isn’t big enough. Maybe your learning rate is too low. Maybe your dataset isn’t good enough to drop 50% of the neurons at each stage. Common practice while using dropout is to use p=0.2 for the input layer and p=0.5 for subsequent layers.

* **Is it all good news?** 🤑
            Well, yes and no. What happens here is that because you essentially train new architectures on each pass, training the actual neural network takes much longer( depending on the architecture, sometimes even 4X as long!) . There are also a bunch of other fine little details you have to take care off like increasing the learning rate and momentum to help learn from this inherent stochastic process you have now induced. But Hey! Anything for higher scores, right? 😉  

I hope that this beautifully hidden connection between Sexual Reproduction and Dropout Regularization has now become apparent. You should now be able to justify why “Dropout” a.k.a dropping out neurons works in Deep Learning! 😄 

See you in the next one! 😄 

``
All my images are courtesy of the original Dropout paper by Srivastava et al. which I highly recommend reading to truly appreciate Dropout. You can find it here : `http://jmlr.org/papers/volume15/srivastava14a/srivastava14a.pdf`
``

[dropout_header] : https://github.com/dsouzadaniel/dsouzadaniel.github.io/raw/master/images/dropout_0.jpg "Elephants are awesome ^_^ "


[dropout_diagram] : https://github.com/dsouzadaniel/dsouzadaniel.github.io/raw/master/images/dropout_1.jpg "How to use Dropout in Neural Networks "


[dropout_features] : https://github.com/dsouzadaniel/dsouzadaniel.github.io/raw/master/images/dropout_2.jpg "How Features look after Dropout"