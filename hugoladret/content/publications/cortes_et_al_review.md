+++
author = "Nelson Cortes, Reza Abbas Farishta, Hugo Ladret, Christian Casanova"
title = "[2021] [model] -- Corticothalamic Projections Gate Alpha Rhythms in the Pulvinar"
date = "2021-12-06"
journal = "published in Frontiers in Cellular Neuroscience"
description = "Cortes et al. 2021"
tags = [

]
+++

[<i class="fa-solid fa-book"></i>](https://www.frontiersin.org/articles/10.3389/fncel.2021.787170/full) - [<i class="fa-solid fa-file-pdf"></i>](https://hugoladret.github.io/publications/cortes_et_al_pulvinar.pdf) - [<i class="fa-solid fa-quote-left"></i>](https://scholar.googleusercontent.com/scholar.bib?q=info:2rWuhDabRecJ:scholar.google.com/&output=citation&scisdr=CgUKAuoEEOK9kuLcTUA:AAGBfm0AAAAAZBnZVUBkRbCvg2xAo80_7651biNTTXmq&scisig=AAGBfm0AAAAAZBnZVWxcvy0mz_lUiJM_cNQ6rhQTTgEy&scisf=4&ct=citation&cd=-1&hl=fr) - [<i class="ai ai-biorxiv"></i>](https://www.biorxiv.org/content/10.1101/2021.09.10.459796v1)

<!--more-->
# TL;DR
Distinct synaptic connections cortex->pulvinar = distinct oscillatory patterns. Significant implications for visual processing in the cortex, especially for attention.

# Context
The pulvinar, thalamic nucleus, is right next to the lateral geniculate nucleus (LGN). Size of the pulvinar correlates with neocortex expansion throughout mammalian evolution [1]. Hence, pulvinar being the largest nucleus of primates' thalamus. Unique extensive (and reciprocal) synaptic connections with all visual cortical areas.

![Pulvinar connectivity](https://hugoladret.github.io/publications/imgs/cortes_et_al_pulvinar_1.png)

Synaptic connections from cortex to pulvinar not uniform. Differ by cortical origin. Low-level areas (e.g., V1) cause post-synaptic depression; higher-level areas (e.g., V4) cause post-synaptic facilitation [2].

![Synaptic types](https://hugoladret.github.io/publications/imgs/cortes_et_al_pulvinar_2.png)

# Takeaways
We created a spiking neural network model of the pulvinar. Studied effects of varying synapse types on pulvinar activity.

![Model](https://hugoladret.github.io/publications/imgs/cortes_et_al_pulvinar_3.png)

Model showed V4 and V1 projections have opposing effects on the pulvinar's state. Alpha oscillatory state from V1 input shifts to non-oscillatory spiking activity with V4 input, and vice versa.

With direct cortical connectivity in the model, V1-generated alpha oscillations in the pulvinar propagate to V4. V4 synaptic activity transitions system to non-oscillatory state, closing the oscillation loop.

# Relevance
Canonical view: visual processing in the cortex as hierarchical communication. Our paper: alpha oscillations - typically seen as high-to-low level feedback/attention can travel opposite direction through the pulvinar.

![Message passing](https://hugoladret.github.io/publications/imgs/cortes_et_al_pulvinar_4.png)

# References
[1] Hutchins, B., & Updyke, B. V. (1989). Retinotopic organization within the lateral posterior complex of the cat. Journal of Comparative Neurology, 285(3), 350-398.

[2] Abbas Farishta, R., Boire, D., & Casanova, C. (2020). Hierarchical organization of corticothalamic projections to the pulvinar. Cerebral Cortex Communications, 1(1).

# On a personal note