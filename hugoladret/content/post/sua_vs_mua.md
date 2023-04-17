+++
author = "Hugo Ladret"
title = "SUA vs MUA #ephys #bibliography"
date = "2023-04-14"
description = """ 'We should all do what, in the long run, gives us joy, even if it is only picking grapes or sorting the spikes.' > E. B. White, 1989 (approximative quote)
"""
tags = [

]
+++

<!--more-->
# The problem
Extracellular electrophysiology can be about :
* Recording Single Unit Activity (SUA), i.e. the potentials from one single neuron in the brain, with a small-ish electrode nearby.
* Recording multiple of those simultaneously and in a mixed manner, i.e. a pool of potentials from multiple closeby cells, called Multi Unit Activity (MUA).
* Scaling up even higher in space and time, recording the transient potential of many neurons, in the form of Local Field Potentials (LFP).

What is recorded depends on many factors, amongst which the impedance of the electrode and the filtering frequencies are key. In terms of SUA vs MUA, it is mostly about impedance, or put more simply the size of a "listening sphere" around the tip of the electrode.

I've been personally dealing entirely with SUA in my career so far, but they have recently used datasets [in which they are not necessarily accessible](https://hugoladret.github.io/post/sua_ks3/). Wishing to know more about how a mixed bag of SUA compares to a "pure" SUA, I started browsing the relevant literature. This post will be updated regularly to reflect new findings.

# Solution(s)
## [ 2023-04-14 ]
It is not uncommon to mix SUA and MUA in publications, which reflects their shared origin and function. Recently, I've read two articles [here](https://www.nature.com/articles/s41593-018-0089-1) and [there](https://www.science.org/doi/10.1126/science.aao0284?url_ver=Z39.88-2003&rfr_id=ori:rid:crossref.org&rfr_dat=cr_pub%20%200pubmed) in which authors were mixing both signals in V1 electrophysiology.

I found these paper through a [third one](https://pubmed.ncbi.nlm.nih.gov/36947884/) in which the authors went so far as to claim that :
> No spike sorting was performed, as previous studies similar to ours have reported no significant difference between single- and multi-unit results.

which, when reading all three articles, seems quite true.
