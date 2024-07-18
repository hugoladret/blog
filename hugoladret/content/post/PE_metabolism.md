+++
author = "Hugo Ladret"
title = "[model] Information cost of two prediction error streams"
date = "2024-07-18"
description = """ 
"""
tags = [

]
+++

<!--more-->
# The problem
Two types of neuronal responses to error in the cortex. Positive and negative prediction error neurons. 

Why ? Could also have one single neuron and have excitation be positive errors and inhibition be negative errors.

# Some context 
On any arbitrary dimension (light intensity, sound frequency, size of a dog), one can only be wrong in two possible directions. In the case of the dog: one sees it from afar, and either think the dog is too big, or the dog is too small, compared to what it actually is.
In the first case, the prediction is larger than the reality - so a negative prediction error should "decrease" the magnitude of new predictions to be more accurate about the world.   
In the second case, the prediction is smaller than the reality - so a positive prediction error should "increase" the magnitude of new predictions to be more accurate about the world.  

Both positive and negative response type to mismatch exist in the cortex and can be assigned to molecular signatures ([O'Toole 2023](https://pubmed.ncbi.nlm.nih.gov/37708892/)). 

Yet, neural activity is expensive, so why have double the amount of neurons if the goal is to reduce the cost of neural activity ?

# Some concepts 
Neurons in the cortex have non-zero baselines. This is important for a whole host of functions - and also means that they can, on average, deviate from baseline both by firing more or less. Physical bound on less (cant have negative firing rate), energetic bound on more (cant spike at 3000Hz).

Information theory tells that information content is related to its probability - or inverse surprise. Information of these prediction errors are thus related to a probability of change in firing rate. 
Let's assume $\Delta_R$ a change in firing rate around baseline $R$ is Gaussian (not true but still) with standard deviation $\sigma_R$. Information is then 
$$
I = \log_2(1+|\Delta_R| / \sigma_R) 
$$

Suppose a semi-arbitrary baseline $R$ of approx. $5 spike/s$ in mouse V1. Then two deviations possible
Positive prediction error: $\Delta R_+ = +2$ spikes/s
Negative prediction error: $\Delta R_- = -2$ spikes/s

Bits per spike are defined as:
$$
E(\Delta R, R, \sigma, t) = \frac{\log_2(1 + |\Delta R|/\sigma)}{(R + \Delta R)t}
$$

For $\Delta R_+ = +2$, within a time window of $1s$ and an std of $1 spike/s$:
$$
\begin{align}
E_+ &= \frac{\log_2(1 + |\Delta R_+|/\sigma)}{(R + \Delta R_+)t} 
    &= \frac{\log_2(1 + 2/1)}{(5 + 2) \cdot 1}
    &= \frac{\log_2(3)}{7}
    &\approx 0.229 \text{ bits/spike}
\end{align}
$$

For $\Delta R_- = -2$:
$$
\begin{align}
E_- &= \frac{\log_2(1 + |\Delta R_-|/\sigma)}{(R + \Delta R_-)t}
    &= \frac{\log_2(1 + 2/1)}{(5 - 2) \cdot 1
    &= \frac{\log_2(3)}{3}
    &\approx 0.528 \text{ bits/spike}
\end{align}
$$

This scales - meaning that negative deviations are always more efficient. This would encourage the system to overpredict, but is also inefficient.

# Zero-baseline concepts 

For a hypothetical two-neuron type system with near zero baselines:
$$
\begin{align}
E &= \frac{\log_2(1 + 2/1)}{2 \cdot 1}
  &= \frac{\log_2(3)}{2}
  &\approx 0.792 \text{ bits/spike}
\end{align}
$$

Four times better than positive prediction error, and better than negative prediction error too. Two times better than average efficiency of $\approx 0.379 \text{ bits/spike}$.
Also more costly - need to have two populations of neurons. This also means two separate prediction errors pathways that can be individually controlled - might improve information.

# Some remarks
Given how, from a conditional perspective, the mutual information is:
$$
\begin{equation}
I(S;R) = 1 + p \log_2 p + (1-p) \log_2 (1-p)
\end{equation}
$$

and is maximized by 
$$
\begin{equation}
\frac{dI(S;R)}{dp} = \log_2 \frac{p}{1-p} = 0
\end{equation}
$$

This means that for two deviations in a single neural pathway we have $p=0.5$ and the maximum mutual information is 
$$
\begin{equation}
C = 1 + 0.5 \log_2 0.5 + 0.5 \log_2 0.5 = 0.5 \text{ bits}
\end{equation}
$$

Hence a single neural pathway with + and - deviation is already efficient. So either the two type of response are there because they are both non-zero baseline and can each deviate in two directions (over-over shooting and over-under shooting for instance).
Or, it is simply better for control's sake and/or downstream readibility to have two separate pathways.

In conclusion - no clear conclusion (:.