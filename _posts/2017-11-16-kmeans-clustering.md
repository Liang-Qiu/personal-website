---
layout: post
title: "K-means Clustering"
---

{{ page.title }}
================

$$ J = \sum_{n=1}^{N}\sum_{k=1}^{K}r_{nk}\|x_{n} - \mu_{k}\|^2, \quad r_{nk} = \{0, 1\} $$  

First, fix $$\mu_{k}$$, then the optimal $$r_{nk}$$ choices would be putting $$x_{n}$$ in the clusters whose centers are the nearest to $$\mu_{k}$$;  
Second, calculate the partial gradient and update $$\mu_{k}$$:

$$
\begin{align*}
   \frac{\partial J}{\partial \mu_{k}} &= -2\sum_{k=1}^{K}\sum_{n=1}^{N}r_{nk}(x_{n} - \mu_{k}) \\ &= 
  -2\sum_{k=1}^{K}[(\sum_{n=1}^{N}r_{nk}x_{n}) - (\sum_{n=1}^N r_{nk}) \mu_{k}] \\
   \mu_{k} &= \frac{\sum_n r_{nk}x_{n}}{\sum_n r_{nk}}
\end{align*}
$$

Third，iterate the two steps above until it reaches a predefined maximum step or the difference beween two succesive $$J$$s is smaller than a threshold.   
**Note: The initialization of $$\mu_{k}$$ maters so we usually do initialization for sevaral times and choose the best one.**