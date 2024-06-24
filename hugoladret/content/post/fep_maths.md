+++
author = "Hugo Ladret"
title = "[model] Some maths behind PC under FEP"
date = "2024-06-24"
description = """ 
"""
tags = [

]
+++

<!--more-->
# The problem
Need to explain Predictive Coding (PC) to someone ?  
Usually, have to scroll between Rafal Bogacz's excellent [Tutorial on the Free Energy Principle](https://www.sciencedirect.com/science/article/pii/S0022249615000759), Beren Millidge's papers on classification 
using [relaxed PC](https://arxiv.org/pdf/2010.01047), and a couple more.   
Better to have the main maths regrouped here !

# A toy example of perception
Overly simplified, PC-based networks are an ensemble of computational units. They evaluate the posterior probabilities of the environment $p(v|u)$ (i.e. what's actually going on now/next)
based on a (top-down) prior $p(v)$ and a (bottom-up) likelihood $p(u|v)$.  
We can assume Gaussian distributions here (central limit theorem + [this paper](https://hugoladret.github.io/publications/ladret_et_al_sparsecoding/), but also wrong, see [this](https://www.2kmm.pl/blog/On-the-ubiquity-of-skewness-in-nature/)). 
Bayes' theorem frames this as:
$$
p(v|u) = \frac{p(v)p(u|v)}{p(u)} = \frac{\frac{1}{\sqrt{2\pi\Sigma_p}} \exp{\frac{(v-v_p)^2}{2\Sigma_p}} \frac{1}{\sqrt{2\pi\Sigma_u}} \exp{\frac{(u-g(v))^2}{2\Sigma_u}}}{\int p(v) p(u|v)dv}.
$$
$v$ is an actual scalar value of the environment,described by $v_p$ and $\Sigma_p$, respectively, the mean and variance of its Gaussian distribution of probabilities.  
$p(u|v)$ is the likelihood, in which the scalar $u$ is the product of an transforming function $g(v)$ (ex the reflection of light on a surface) with a variance $\Sigma_u$.

Denominator problematic. Normalization term, computationally intractable for a biological neural network, because of required sampling of every possible permutations of $p(v)$ and $p(u|v)$.   

# Simplification through MLE 
First solution to denominator problem : maximum likelihood estimation. MLE tries to find the value of $v$ that maximizes $p(v|u)$.  
This value is written as $\Phi$, whose probability $p(\Phi)$ replaces $p(v)$ in an MLE approach. That term is absent from the denominator in the left-hand side of equation above: remove the denominator, write the logarithm of the numerator as $F$:  
$$
     F = \ln  \left( p(\Phi) p(u|\Phi) \right) = \ln p(\Phi) + \ln p(u|\Phi)
$$

We get:
$$
\begin{align}
F &= \ln p(\Phi) + \ln p(u|\Phi) \\ 
  &=\ln \left( \frac{1}{\sqrt{2\pi\Sigma_p}} \exp{-\frac{(\Phi-v_p)^2}{2\Sigma_p}}\right) + \ln \left( \frac{1}{\sqrt{2\pi\Sigma_u}} \exp{-\frac{(u-g(\Phi))^2}{2\Sigma_u}} \right) \\
  &= \ln \left( \frac{1}{\sqrt{2\pi\Sigma_p}} \right) + \ln \left(\exp{-\frac{(\Phi-v_p)^2}{2\Sigma_p}} \right) + 
        \ln \left( \frac{1}{\sqrt{2\pi\Sigma_u}} \right) + \ln \left(\exp{-\frac{(u-g(\Phi))^2}{2\Sigma_u}} \right) \\
  &= \ln \left( \frac{1}{\sqrt{2\pi}} \right) - \frac{1}{2} \ln \Sigma_p- \frac{(\Phi-v_p)^2}{2\Sigma_p} + 
        \ln \left( \frac{1}{\sqrt{2\pi}} \right) - \frac{1}{2} \ln \Sigma_u -  \frac{(u-g(\Phi))^2}{2\Sigma_u} \\ 
  &=  \frac{1}{2} \left( - \ln \Sigma_p - \frac{(\Phi - v_p)^2}{\Sigma_p}  - \ln \Sigma_u - \frac{(u - g(\Phi))^2}{\Sigma_u}\right) + C
\end{align}
$$

We now seek the maximum likelihood - we compute the derivative of $F$ over the surrogate value $\Phi$:
$$
    \begin{align}
        \frac{\delta F}{\delta \Phi} &= 
\frac{1}{2} \left(
\frac{\delta}{\delta \Phi}     \left(-\frac{(u - g(\Phi))^2}{\Sigma_u}\right) +
\frac{\delta}{\delta \Phi}     \left(-\frac{(\Phi - v_p)^2}{\Sigma_p}\right) + 
\frac{\delta}{\delta \Phi}      \left( -\ln\Sigma_u \right) + 
\frac{\delta}{\delta \Phi}      \left( -\ln\Sigma_p \right) + 
\frac{\delta}{\delta \Phi}      C
\right) \\
&= \frac{1}{2} \left(
\left( -\frac{1}{\Sigma_u} \frac{\delta}{\delta \Phi} (u-g(\Phi))^2) \right) +
\left( -\frac{1}{\Sigma_p} \frac{\delta}{\delta \Phi} (\Phi-v_p)^2 \right)
\right)
    \end{align}
$$

Applying the power rule $(f(x)^n)' = n f(x)^{n-1} f'(x)$:
$$
    \begin{align}
        \frac{\delta F}{\delta \Phi} &= \frac{1}{2} \left(
\left( -\frac{1}{\Sigma_u} 2(u-g(\Phi))\frac{\delta}{\delta \Phi} (u-g(\Phi)) \right) +
\left( -\frac{1}{\Sigma_p} 2(\Phi-v_p) \frac{\delta}{\delta \Phi} (\Phi-v_p) \right)
\right) \\
&= \frac{1}{2} \left(
\left( -\frac{1}{\Sigma_u} 2(u-g(\Phi)) \left(\frac{\delta}{\delta \Phi} u - \frac{\delta}{\delta \Phi} g(\Phi)\right) \right) +
\left( -\frac{1}{\Sigma_p} 2(\Phi-v_p) \left(\frac{\delta}{\delta \Phi} \Phi - \frac{\delta}{\delta \Phi} v_p \right)\right)
\right) \\
&= \frac{1}{2} \left(
\left( -\frac{1}{\Sigma_u} 2(u-g(\Phi))(-g'(\Phi)) \right) +
\left( -\frac{1}{\Sigma_p} 2(\Phi-v_p) \right)
\right) \\
&= \left( \frac{1}{\Sigma_u} (u-g(\Phi))(g'(\Phi)) \right) +
\left( -\frac{1}{\Sigma_p} (\Phi-v_p) \right) \\
&= \frac{(u-g(\Phi))}{\Sigma_u} g'(\Phi)  + \frac{(v_p-\Phi)}{\Sigma_p}  
    \end{align}
$$

We can rewrite this as:
$$
\begin{align}
    \epsilon_p &= \frac{(v_p-\Phi)}{\Sigma_p} \\
    \epsilon_u &= \frac{(u - g(\Phi))}{\Sigma_u}
\end{align}
$$

such that the derivative becomes:
$$
\frac{\delta F}{\delta \Phi} = \epsilon_u  g'(\Phi)   + \epsilon_p 
$$

We reformulate the gradient of $F$ w.r.t $\Phi$ as a learning rule:
$$
    \dot{\Phi} = \epsilon_u  g'(\Phi) - \epsilon_p
$$

$\epsilon_p$ is the prediction error on the causes.  
$\epsilon_u$ is the prediction error on the states (see Friston [2005](link)).  
$\epsilon_p$ measures the difference between the inferred observation and the model's prior expectations.  
$\epsilon_u$ measures the difference between the true external value and the predicted value, i.e. prediction error on the causes represents errors at higher level representations, while prediction error on the states represents raw differences between inferred and real states. 

Rewriting everything as $F$ is useful. 
$F$ is the variational free energy, and relates to certain useful information theoretical metrics, forming a lower bound of the model's surprise.

PC seeks to maximize prediction efficiency by minimizing prediction errors. When minimal, they are at a stable point of $\epsilon_p$ and $\epsilon_u$ defined as:
$$
    \begin{align}
        \epsilon_p &= \frac{\Phi - v_p}{\Sigma_p} \\
        \Sigma_p\epsilon_p &= \Phi - v_p \\
        \Phi - v_p - \Sigma_p\epsilon_p &= 0 
    \end{align}
$$

$$
    \begin{align}
        \epsilon_u &= \frac{u - g(\Phi)}{\Sigma_u} \\
        \Sigma_u\epsilon_u &= u - g(\Phi)\\
         u - g(\Phi) - \varSigma_u \varepsilon_u &= 0
    \end{align}
$$

And thus, minimizing prediction errors to infer the most likely value of $\Phi$ in an MLE approach is: 
$$
\begin{align}
\dot{\varepsilon_p} &= \Phi - v_p - \varSigma_p \varepsilon_p  \\
\dot{\varepsilon_u} &= u - g(\Phi) - \varSigma_u \varepsilon_u  \\
\end{align}
$$

Both $\varSigma_p$ and $\varSigma_u$ parametrize the uncertainty of the model. 
In this MLE approach, which ideally should converge onto the most likely value of the input, any model or input-bound uncertainties are discarded.
This transforms an information-rich, distribution-based computation into a point estimate, which is a shame.

# Better than MLE
MLE that conserves distribution computations is something called variational inference.  
Instead of facing computationally untractable normalization terms, or arbitrarily complex input distributions, variational inference uses a new distribution $q(v)$. This possesses a standard form described by its mean and variance. 

We thus change from MLE to approximating posterior $p(v|u)$ using $q(v)$. This requires a metric of difference, or divergence, between the two distributions. For instance, the Kullback-Leibler divergence:
$$
\begin{align}
    KL(q(v), p(v|u)) &= \int{q(v) \ln \frac{q(v)}{p(v|u)} dv}
\end{align}
$$

Still, implausible for a biological network to measure this difference due to the same issue of computational intractability of $p(v|u)$ that led us to MLE. Indeed: 
$$
\begin{align}
    p(v|u) = \frac{p(u, v)}{p(u)} = \frac{p(u, v)}{\int p(v) p(u|v)dv}
\end{align}
$$

Expanding the KL divergence using the above, we see:
$$
    \begin{align}
        KL(q(v), p(v|u)) & = \int{q(v) \ln \frac{q(v)}{p(v|u)} dv} \\ 
                        &= \int{q(v) \ln \frac{q(v)p(u)}{p(u,v)} dv} \\
                        &= \int{q(v) \ln \frac{q(v)}{p(u,v)} dv} + \int{q(v) \ln p(u) dv} \\
    \end{align}
$$

given that the surrogate $q(v)$ is a probability distribution which sums up to $1$, we get:
$$
    \begin{align}
        KL(q(v), p(v|u)) = \int{q(v) \ln \frac{q(v)}{p(u,v)} dv} + \ln p(u) \
    \end{align}
$$

We can then define a term that simplifies everything, once again called $F$, defined as:
$$
    \begin{align}
        F &= \int q(v) \ln \frac{q(v)}{p(u,v)} dv \\
        KL (q(v), p(v|u)) &= F + \ln p(u)
    \end{align}
$$

since $F$ depends on the surrogate distribution $q(v)$, the parameters which minimize the distance between the surrogate $q(v)$ and the posterior $p(v|u)$ are identical to those which maximize $F$.  
This removes the computation of the normalization term. With $F$, we define the right-hand term as:
$$
    \ln p(u) = -F+ KL (q(v), p(v|u)) 
$$

$\ln p(u)$ directly relates to the information "surprise" of the estimate $p(u)$ of the actual value $v$. Thus, directly to its uncertainty.  
Since KL divergence is strictly positive, $F$ is a lower bound of the surprise $\ln p(u)$.  
Then, maximizing $F$ minimizes surprise or uncertainty of $\ln p(u)$ improving the approximation of the surrogate $q(v)$.

This allows to update the uncertainty parameters - we can now rewrite:
$$
\begin{align}
    \ln p(u) & = F+ KL (q(v), p(v|u)) \\
            & = \frac{1}{2} \left[ - \ln \Sigma_p - \frac{(\Phi - v_p)^2}{\Sigma_p}  - \ln \Sigma_u - \frac{(u - g(\Phi))^2}{\Sigma_u}\right] + C + KL (q(v), p(v|u))
\end{align}
$$

as the KL divergence is a strictly positive term that forms a lower bound on surprise, it can be included in the constant term $C$ for simplicity's sake.

Starting from this definition, we can now derive $F$ to optimize $v_p$:
$$
\begin{align}
\frac{\delta F}{\delta v_p} &=
\frac{1}{2} \left(
\frac{\delta}{\delta v_p} \left( - \frac{(\Phi - v_p)^2}{\Sigma_p} \right) +
\frac{\delta}{\delta v_p} \left( - \frac{(u - g(\Phi))^2}{\Sigma_u} \right) +
\frac{\delta}{\delta v_p} \left( - \ln \Sigma_u  \right) + 
\frac{\delta}{\delta v_p} \left( - \ln \Sigma_p  \right) + 
\right)
\frac{\delta}{\delta v_p} C \\
 &= \frac{1}{2} \left(
\frac{\delta}{\delta v_p} \left( - \frac{(\Phi - v_p)^2}{\Sigma_p} \right) 
\right) \\
& = \frac{1}{2} \left(
\frac{1}{-\Sigma_p}
\frac{\delta}{\delta v_p} (\Phi - v_p)^2
\right) \\
&= 
\frac{1}{-\Sigma_p}
(\Phi - v_p)
\frac{\delta}{\delta v_p} (\Phi - v_p) \\
&= 
\frac{1}{-\Sigma_p}
(\Phi - v_p)
\left(\frac{\delta}{\delta v_p} \Phi -
\frac{\delta}{\delta v_p} v_p\right) \\
&= \frac{\Phi - v_p}{\Sigma_p}
\end{align}
$$

The same can be done for $\Sigma_p$:
$$
\begin{align}
\frac{\delta F }{\delta \Sigma_p} &= 
\frac{1}{2} \left(
\frac{\delta}{\delta \Sigma_p} \left( - \frac{(\Phi - v_p)^2}{\Sigma_p} \right) +
\frac{\delta}{\delta \Sigma_p} \left( - \frac{(u - g(\Phi))^2}{\Sigma_u} \right) +
\frac{\delta}{\delta \Sigma_p} \left( - \ln \Sigma_u  \right) + 
\frac{\delta}{\delta \Sigma_p} \left( - \ln \Sigma_p  \right)  
\right) +
\frac{\delta}{\delta \Sigma_p} C \\
&= 
\frac{1}{2} \left(
- \frac{\delta}{\delta \Sigma_p} \ln \Sigma_p +
\left( - (\Phi - v_p)^2
\frac{\delta}{\delta \Sigma_p} \frac{1}{\Sigma_p} \right) 
\right) \\
&= 
\frac{1}{2} \left(
- \frac{1}{\Sigma_p} +
\left(  (\Phi - v_p)^2
\frac{\frac{\delta}{\delta \Sigma_p} \Sigma_p}{\Sigma_p^2} \right) 
\right) \\
&= 
\frac{1}{2} \left(
(\Phi - v_p)^2
\frac{\frac{\delta}{\delta \Sigma_p} \Sigma_p}{\Sigma_p^2} 
- \frac{1}{\Sigma_p}
\right) \\
&= 
\frac{1}{2} \left(
\frac{(\Phi - v_p)^2}{\Sigma_p^2} 
- \frac{1}{\Sigma_p}
\right)
\end{align}
$$

Likewise, for $\Sigma_u$:
$$
\begin{align}
\frac{\delta F }{\delta \Sigma_u} &=
\frac{1}{2} \left(
\frac{\delta}{\delta \Sigma_u} \left( - \frac{(\Phi - v_p)^2}{\Sigma_p} \right) +
\frac{\delta}{\delta \Sigma_u} \left( - \frac{(u - g(\Phi))^2}{\Sigma_u} \right) +
\frac{\delta}{\delta \Sigma_u} \left( - \ln \Sigma_u \right) +
\frac{\delta}{\delta \Sigma_u} \left( - \ln \Sigma_p \right)
\right) +
\frac{\delta}{\delta \Sigma_u} C\\
&=
\frac{1}{2} \left(
\frac{\delta}{\delta \Sigma_u} \left( - \frac{(u - g(\Phi))^2}{\Sigma_u} \right) -
\frac{\delta}{\delta \Sigma_u} \ln \Sigma_u
\right)\\
&=
\frac{1}{2} \left(
-(u - g(\Phi))^2 \frac{\delta}{\delta \Sigma_u} \frac{1}{\Sigma_u} -
\frac{\delta}{\delta \Sigma_u} \ln \Sigma_u
\right)\\
&=
\frac{1}{2} \left(
-(u - g(\Phi))^2 \frac{\delta}{\delta \Sigma_u} \frac{1}{\Sigma_u} -
\frac{1}{\Sigma_u}
\right)\\
&=
\frac{1}{2} \left(
\frac{(u - g(\Phi))^2}{\Sigma_u^2} -
\frac{1}{\Sigma_u}
\right)\\
\end{align}
$$

Yielding the learned parameters of a predictive coding network:
$$
    \begin{align}
    \frac{\delta F}{\delta v_p} &= \frac{\Phi - v_p}{{\Sigma_p}} = \epsilon_p \\
    \frac{\delta F}{\delta \Sigma_p} &= \frac{1}{2} \left[ \frac{(\Phi - v_p)^2}{{\Sigma_p^2}} - \frac{1}{{\Sigma_p}} \right]  = \frac{1}{2} \left(\epsilon_p^2 - {\Sigma_p^{-1}} \right) \\
    \frac{\delta F}{\delta \Sigma_u} &=  \frac{1}{2} \left[ \frac{(u - g(\Phi))^2}{{\Sigma_u^2}} - \frac{1}{{\Sigma_u}} \right] = \frac{1}{2} \left(\epsilon_u^2 - {\Sigma_u^{-1}} \right)
    \end{align}
$$

# Matrix form
Straightforward from the vector (current) form. Bogacz even formulates the addition of an inhibitory neuron to make everything biological more plausible.  
Also fits the idea from [this paper](https://hugoladret.github.io/publications/ladret_et_al_variance_v1/) that inhibition shapes uncertainty weighting.