+++
author = ">Hugo Ladret<, Nelson Cortes, Lamyae Ikan, Frederic Chavane, Christian Casanova, Laurent U Perrinet"
title = "Cortical recurrence supports resilience to sensory variance in the primary visual cortex"
date = "2023-06-01"
journal = "Nature Communications Biology"
description = "Ladret et al. 2023"
+++

[<i class="fa-solid fa-newspaper"></i>](https://www.nature.com/articles/s42003-023-05042-3) - [<i class="fa-solid fa-file-pdf"></i>](https://hugoladret.github.io/publications/ladret_et_al_variance_V1.pdf) - [<i class="fa-solid fa-quote-left"></i>](https://scholar.google.com/citations?view_op=view_citation&hl=en&user=n6dvyjwAAAAJ&citation_for_view=n6dvyjwAAAAJ:Tyk-4Ss8FVUC) - [<i class="fa-solid fa-globe"></i>](https://laurentperrinet.github.io/publication/ladret-23/) - [<i class="ai ai-biorxiv"></i>](https://www.biorxiv.org/content/10.1101/2021.03.30.437692v5)

<!--more-->
<!--more-->
# TL;DR
Connections between neighbouring cortical neurons endows neural networks with the ability to compute the variance of a sensory input. This is crucial to support Bayesian computations in the brain.


# Context
Imagine yourself hiking through a forest. The wind rustles through the leaves, when suddenly a strange noise catches your attention. Did it come from a squirrel scurrying along the path in plain sight ? Or perhaps a bird nestling behind the bushes, hidden behind foilage ? In the latter case, do you take the extra time to see the bird, or infer that the rustling is rather that of a lion, and run away as fast as possible ?

This simple and rather silly scenario showcases a daily problem that we as human are facing: how can our brain make sense of the world, when our senses are bombarded with unreliable information ?

This unreliability - the inverse of the variance of an information - is constant when it comes to vision. Indeed, an image can be broken down into numerous lines or "edges" that form its structure, similar to how a puzzle is made up of many different pieces.

![Decomposition of natural images](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_1.png)

However, not all pieces of the puzzles are cut equal, and some have more variables edges than others. This is a problem for the very first area of our brain that starts to make sense of these visual "puzzle pieces", the primary visual cortex. Until recently, our understanding of how the brain handles these complex visual inputs was largely based on observing human behavior [1,2].

In recent years, however, researchers began probing the primary visual cortex of macaques, discovering that this area of the brain exhibits complex behaviors that mirror the intricate decision-making processes we humans undertake [3].


# Method
For our current research, we decided to dive deep into this "visual puzzle" by examining neurons in the primary visual cortex and constructing a comprehensive model of how they interact. We used a type of visual stimuli, Motion Clouds, which nicely imitates the complexity of natural images [4].

![Article Figure 1](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_2.png)


# Results : single neurons
We discovered an interesting phenomenon: the neurons in our primary visual cortex have distinct responses to the complexity of images. We identified two main types of neurons based on their responses: some were fairly unmoved by increased variance (flat), while others showed quick decay in face of it (non-linear).

![Article Figure 2](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_3.png)

Moreover, these two groups of neurons exhibited different timings. The "flat" neurons took more time to respond, while the "non-linear" neurons responded more quickly.

![Article Figure 3](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_4.png)

We labeled these two groups as "resilient" and "vulnerable", and clustered them based on a range of different neural metrics.


# Results : population of neurons
The next question was: what exactly do these different neurons do? To figure this out, we used a method called neural decoding, which tries to guess what the neurons are "seeing" based on their responses.

![Neural Decoding](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_6.png)

Interestingly, both resilient and vulnerable neurons did a good job at guessing the average orientation of the visual input.

![Article Figure 5](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_7.png)

However, when it came to both the average orientation and complexity of the image, the resilient neurons performed much better than their vulnerable counterpart.

![Article Figure 6](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_8.png)

These specific neurons were found in different layers of the cortex, which connect to other parts of the cortex in different ways. This provided an anatomical basis for the existence of the two groups of neurons.

![Cortical Anatomy](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_9.png)


# Results : model
We simulated this differential anatomical basis phenomenon using a computer model and found that by tweaking the amount of "recurrence" (the way neurons connect and influence each other), we could mimic the behavior of both resilient and vulnerable neurons.

![Article Figure 7](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_10.png)


# Overall
Overall, recurrence can explain how different neurons encode (or not) the variance of their input. Our findings support a more complete understanding of the brain, which doesn't just encode average features, like previous models suggested, but also takes into account the complexity of the inputs, thanks to the connectivity between neurons.

![Article Figure 8](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_11.png)


# Relevance

This is a crucial step in understanding how our cortex manages the "visual puzzles" we encounter every day, allowing the brain to perform complex calculations on probabilistic distributions - a model that's gaining more popularity in neuroscience [5].



# References

[1] Von Helmholtz, H. (1925). Helmholtz's treatise on physiological optics (Vol. 3). Optical Society of America.

[2] Barthelmé, S., & Mamassian, P. (2009). Evaluation of objective uncertainty in the visual system. PLoS computational biology, 5(9), e1000504.

[3] Hénaff, O. J., Boundy-Singer, Z. M., Meding, K., Ziemba, C. M., & Goris, R. L. (2020). Representation of visual uncertainty through neural gain variability. Nature communications, 11(1), 2513.

[4] Leon, P. S., Vanzetta, I., Masson, G. S., & Perrinet, L. U. (2012). Motion clouds: model-based stimulus synthesis of natural-like random textures for the study of motion perception. Journal of neurophysiology, 107(11), 3217-3226.

[5] Spratling, M. W. (2016). A neural implementation of Bayesian inference based on predictive coding. Connection Science, 28(4), 346-383.


# On a personal note
This was my very first first-authored peer-reviewed paper ! It was one very long adventure - I started doing recordings back in 2020, before COVID-19 was even a thing - and wrote 4 versions of the paper from scratch. I'm very grateful to the reviewers and the editors at Nat. Com. Bio. for having given us the chance to publish with them.
