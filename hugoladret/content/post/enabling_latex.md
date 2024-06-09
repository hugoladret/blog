+++
author = "Hugo Ladret"
title = "[ephys] [biblio] SUA vs MUA"
date = "2024-06-09"
description = """ 'I see. Here is the corrected version:' > ChatGPT, upon realizing that I meant LaTeX and not latex.
"""
tags = [

]
+++

<!--more-->
# The problem
Enabling LaTeX equations on blog to make things beautiful.

Before:
\begin{aligned}
p(v|u) = \frac{p(v)p(u|v)}{p(u)} \\ &= \frac{\frac{1}{\sqrt{2\pi\Sigma_p}} \exp{\frac{(v-v_p)^2}{2\Sigma_p}} \frac{1}{\sqrt{2\pi\Sigma_u}} \exp{\frac{(u-g(v))^2}{2\Sigma_u}}}{\int p(v) p(u|v)dv}.
\end{aligned}
After :

$$
\begin{aligned}
p(v|u) = \frac{p(v)p(u|v)}{p(u)} \\ &= \frac{\frac{1}{\sqrt{2\pi\Sigma_p}} \exp{\frac{(v-v_p)^2}{2\Sigma_p}} \frac{1}{\sqrt{2\pi\Sigma_u}} \exp{\frac{(u-g(v))^2}{2\Sigma_u}}}{\int p(v) p(u|v)dv}.
\end{aligned}
$$

Useful ! Takes less than two minutes, for this GitHub-hosted Hugo-based blog.  
In my specific case : 
* Go to blog repository/static
* Create a folder js, if not present 
* Create a file mathjax-config.js with the contents 

> """
window.MathJax = {
  tex: {
    inlineMath: [['$', '$'], ['\\(', '\\)']],
    displayMath: [['$$', '$$'], ['\\[', '\\]']]
  },
  svg: {
    fontCache: 'global'
  }
};
"""

* Go to blog repository/layouts
* Create a folder partials, if not present 
* Create a file head.html, in which you copy your themes' head.html file (same file structure as your blog, most likely in its own directory). 
* At the end of the copy, append : 

> """
<!-- MathJax -->
<script type="text/javascript" src="/js/mathjax-config.js"></script>
<script type="text/javascript" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>
"""

Commit, push, done. 

Inline equations, single dollar sign, the rest, double dollar sign. 

# An era of asking ChatGPT instead of Google 
Good meta-argumentative point to be made here. Troubled by why LaTeX not enabled by default at first.  
Asked Google, read the Hugo documentation, GitHub issues, stackoverflow.  
Not too complex, not too simple either: language for someone who does Hugo/websites. Not language for someone with small brain like me. 

Asked ChatGPT, correct answer in 2 minutes, implementation in 3, writing this post in 5.  
Many such cases in recent debugging attempts in various settings. Thanks LLM.
