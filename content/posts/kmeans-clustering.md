---
title: "K-means Clustering"
date: 2017-11-16
---

================

$$ J = \sum_{n=1}^N \sum_{k=1}^Kr_{nk}\|x_n - \mu_k\|^2, \quad r_{nk} = \{0, 1\} $$  

First, fix $$\mu_k$$, then the optimal $$r_{nk}$$ choice would be putting $$x_n$$ in the cluster whose center $$\mu_k$$ is the nearest to $$x_n$$;  
Second, calculate the partial gradient and update $$\mu_k$$:

$$
\begin{align*}
   \frac{\partial J}{\partial \mu_k} &= -2\sum_{k=1}^K\sum_{n=1}^Nr_{nk}(x_n - \mu_k) \\ &= 
  -2\sum_{k=1}^K[(\sum_{n=1}^Nr_{nk}x_n) - (\sum_{n=1}^N r_{nk}) \mu_k] \\
   \mu_k &= \frac{\sum_n r_{nk}x_n}{\sum_n r_{nk}}
\end{align*}
$$

Third，iterate the two steps above until it reaches a predefined maximum step or the difference beween two succesive $$J$$s is smaller than a threshold.   
**Note: The initialization of $$\mu_k$$ maters so we usually do initialization for sevaral times and choose the one which gives us the best results.**