+++
author = "Hugo Ladret"
title = "[ephys] [biblio] SUA vs MUA"
date = "2023-04-14"
description = """ 'We should all do what, in the long run, gives us joy, even if it is only picking grapes or sorting the spikes.' > E. B. White, 1989 (approximative quote)
"""
tags = [

]
+++

<!--more-->
# The problem
Extracellular electrophysiology can involve:
* Recording Single Unit Activity (SUA), capturing activity from a single neuron in the brain with a nearby electrode.
* Recording multiple neurons simultaneously, resulting in a mixed signal from nearby cells, called Multi Unit Activity (MUA).
* Scaling up further, recording transient potentials from many neurons, known as Local Field Potentials (LFP).

What is recorded depends on various factors, with electrode impedance and filtering frequencies being crucial. For SUA vs MUA, it's primarily about impedance, essentially the size of the "listening sphere" around the electrode tip.

I've worked exclusively with SUA before this post. Recently encountered datasets where SUA is not necessarily accessible. \ 
Curious about how a mix of SUA compares to pure SUA - started exploring relevant literature. 

# Solution(s)
## [2023-04-14]
Mixing SUA and MUA in publications is not uncommon - reflecting their shared origins and functions ? \
Recently, read two articles [here](https://www.nature.com/articles/s41593-018-0089-1) and [there](https://www.science.org/doi/10.1126/science.aao0284?url_ver=Z39.88-2003&rfr_id=ori:rid:crossref.org&rfr_dat=cr_pub%20%200pubmed) which mixed both in V1.

Discovered these papers through a [third one](https://pubmed.ncbi.nlm.nih.gov/36947884/) - authors claimed:
> No spike sorting was performed, as previous studies similar to ours have reported no significant difference between single- and multi-unit results.

Reading all three articles, claim appears quite accurate.
