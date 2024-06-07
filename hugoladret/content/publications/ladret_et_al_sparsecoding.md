+++
author = "Hugo Ladret, Christian Casanova, Laurent Perrinet"
title = "[2024] [model] -- Kernel Heterogeneity Improves Sparseness of Natural Images Representations
"
date = "2024-01-01"
journal = "ArXiv preprint"
description = "Ladret et al. 2024"
tags = [

]
+++

 - [<i class="fa-solid fa-file-pdf"></i>](https://hugoladret.github.io/publications/ladret_et_al_sparsecoding.pdf) - [<i class="fa-solid fa-globe"></i>](https://laurentperrinet.github.io/publication/ladret-23/) - [<i class="ai ai-arxiv"></i>](https://www.biorxiv.org/content/10.1101/2021.03.30.437692v5)

<!--more-->
# TL;DR
Connections between neighboring cortical neurons allow neural networks to compute variance of sensory input. \
Crucial for Bayesian computations in the brain. 

# Context
Imagine hiking through a forest. Wind rustles leaves. Strange noise catches your attention. Squirrel ? Bird ? Lion ? Wait for instagram picture, or flee for survival ? Daily problem: making sense of unreliable sensory input.

This unreliability: inverse of information variance. Constant problem in vision. Images: numerous lines, "edges," like puzzle pieces.

![Decomposition of natural images](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_1.png)

Puzzle pieces vary. Problem for the primary visual cortex. Human behavior known to take uncertainty as a decision factor [1,2].

Recent research: showed uncertainty-dependent activity in macaque primary visual cortex. Complex responses, mirroring human decision-making [3]. \
Why and how responses exists ? Only theories until this paper.

# Method
Our research: examine neurons in primary visual cortex. Construct comprehensive interaction model. Visual stimuli: Motion Clouds, mimic natural image complexity [4].

![Article Figure 1](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_2.png)

# Results: single neurons
Discovered phenomenon: neurons in primary visual cortex respond distinctly to image uncertainty. Two main types: "flat" (unchanged by increased variance), "non-linear" (response quickly destroyed by increased variance).

![Article Figure 2](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_3.png)

Different timings: "flat" neurons respond slowly, "non-linear" neurons respond quickly.

![Article Figure 3](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_4.png)

Labeled groups: "flat = "resilient" as opposed to "non-linear" = "vulnerable," clustered based on neural metrics.

# Results: population of neurons
Next question: what do these neurons do? Used neural decoding: guess neurons' "seeing" based on responses.

![Neural Decoding](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_6.png)

Both resilient and vulnerable neurons guessed average orientation well.

![Article Figure 5](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_7.png)

Resilient neurons excelled in guessing both average orientation and complexity. Not vulnerable.

![Article Figure 6](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_8.png)

Specific neurons found in different cortex layers, connecting differently. Provided anatomical basis for two neuron groups.

![Cortical Anatomy](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_9.png)

# Results: model
Simulated differential anatomical basis using a computer model. Tweaking "recurrence" mimicked behavior of resilient and vulnerable neurons.

![Article Figure 7](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_10.png)

# Overall
Recurrence explains how neurons encode (or not) input variance. Findings support understanding of brain encoding complexity, not just average features, thanks to neuronal connectivity.

![Article Figure 8](https://hugoladret.github.io/publications/imgs/ladret_et_al_variance_V1_11.png)

# Relevance
Crucial step in understanding how cortex handles "visual puzzles." Allows brain to perform complex probabilistic computations. Model gaining popularity in neuroscience [5].

# References
[1] Von Helmholtz, H. (1925). Helmholtz's treatise on physiological optics (Vol. 3). Optical Society of America.

[2] Barthelmé, S., & Mamassian, P. (2009). Evaluation of objective uncertainty in the visual system. PLoS computational biology, 5(9), e1000504.

[3] Hénaff, O. J., Boundy-Singer, Z. M., Meding, K., Ziemba, C. M., & Goris, R. L. (2020). Representation of visual uncertainty through neural gain variability. Nature communications, 11(1), 2513.

[4] Leon, P. S., Vanzetta, I., Masson, G. S., & Perrinet, L. U. (2012). Motion clouds: model-based stimulus synthesis of natural-like random textures for the study of motion perception. Journal of neurophysiology, 107(11), 3217-3226.

[5] Spratling, M. W. (2016). A neural implementation of Bayesian inference based on predictive coding. Connection Science, 28(4), 346-383.

# On a personal note
Submitted this one on ArXiv right while shopping for christmas groceries !