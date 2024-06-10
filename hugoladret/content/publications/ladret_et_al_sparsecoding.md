+++
author = "Hugo Ladret, Christian Casanova, Laurent Perrinet"
title = "[2024] [model] -- Kernel heterogeneity improves sparseness of natural images representations"
date = "2024-01-01"
journal = "ArXiv preprint"
description = "Ladret et al. 2024"
tags = [

]
+++

 - [<i class="fa-solid fa-file-pdf"></i>](https://hugoladret.github.io/publications/ladret_et_al_sparsecoding.pdf) - [<i class="fa-solid fa-globe"></i>](https://arxiv.org/abs/2312.14685)

<!--more-->
# TL;DR
How to sample variance ? Same as with mean, sample it heterogeneously = better deep neural networks for free.

# Context
Learning representations of the world is learning about a continuum of values on an arbitrary space.

Learning images = learning representations of light (spaces = luminosity, contrast, colors, ...)
Learning sound = learning representation of air compression (spaces = frequency, amplitude, ...)

If learning how to represent MNIST images, sampling every luminosity point is OK. Low number of pixels, low complexity problem.  
This is sampling mean of distribution.

If learning how to representation real images, sampling mean of distribution not possible.  
Complex distributions, mean is meaningless.

Solution one (top image below) : sample lots of mean. Precise but costly.  
If representations ends up being same size as input, process useless.

![Sampling of natural images](https://hugoladret.github.io/publications/imgs/ladret_et_al_sparsecoding_1.png)

Solution two (bottom image above) : sample mean, describe succintly variance around it. Approximative, but efficient.  
Useful, also gives idea of how much one bit of information varies with respect to others.


# Natural images 
For the problem of natural images, sampling variance very useful. Stereotypical pattern of distribution of orientations.

![Sampling of natural images](https://hugoladret.github.io/publications/imgs/ladret_et_al_sparsecoding_2.png)


# Learning from this 
If one tries to make models of these images (here, sparse coding), good models also get this distribution of orientations. 

![Sampling of natural images](https://hugoladret.github.io/publications/imgs/ladret_et_al_sparsecoding_3.png)

Logical step : already give this distribution to the models. Save them time from figuring it out.  
5 scenarii :
* green = sample only mean (same uncertainty/variance sampling in the model)
* blue = sample mean and variance (heterogeneous variance sampling)
* orange = green + fine tuning on dataset 
* purple = blue + fine tuning on dataset 
* black = let the model learn everything (fine tuning on the dataset, without any intervention) 

![Sampling of natural images](https://hugoladret.github.io/publications/imgs/ladret_et_al_sparsecoding_4.png)

Learning always gives best representation quality (Peak Signal to Noise Ratio, PSNR) and efficiency (sparseness).  
Without learning, sampling variance massively boosts sparseness. Slight cost in quality. 

Learning = finding the best of both worlds ! Simple task of reconstruction, no big difference. 

Complex task ? Put that into a deep neural network that classifies images. 

![Sampling of natural images](https://hugoladret.github.io/publications/imgs/ladret_et_al_sparsecoding_5.png)

Sampling variance (last row, first column) much better for representations.  

Sampling variance (last row, second and third column) also much, much better than others methods when facing noise.   
Here, cutting off a fraction of the coefficients (25% or 50%) does not significantly hinder the model. Performance collapses for other.


# Relevance
In previous paper ([Cortical recurrence something something sensory variance](https://hugoladret.github.io/publications/ladret_et_al_variance_V1/)), showed that neurons in actual brain compute variance.  
Here, showed that this computation is very useful. Namely, prevents models from failing when facing noise. Important for brain, noisy machines !

Full code in PyTorch - seamlessly integrate this into any deep neural network ! 


# On a personal note
Talked myself into buying a new GPU for this paper.  
Now mostly used for Cyberpunk 2077, rather than PyTorch. 