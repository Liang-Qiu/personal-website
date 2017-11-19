---
layout: post
title: "Gaussian Mixture Model"
---

{{ page.title }}
================

GMM is similar to K-means except that GMM gives the possibily of each sample assigned to each cluster.  
In GMM, it assumes that the samples of each cluster are generated following Gaussian Distribution(Normal Distribution). Suppose we have $$K$$ clusters then the GMM is composed by $$K$$ Gaussian distributions while

$$ 
\begin{align*}
	p(x) &= \sum_{k=1}^Kp(k)p(x|k) \\
		 &= \sum_{k=1}^K\pi_k N(x|\mu_k, \Sigma_k)
\end{align*}
$$ 

To train a GMM, it means that we need to find the optimal values of $$\pi_k, \mu_k, \Sigma_k$$ so that they can maximize the **likelihood function $$\prod_{i=1}^N p(x_i)$$**. And to avoid floating underflow, we uauslly use **log-likelyhood function $$\sum_{i=1}^N log[p(x_i)]$$**.
Specifically, for GMM, the log-likelyhood function is  

$$ \sum_{i=1}^N log\{\sum_{k=1}^K \pi_k N(x_i|\mu_k, \Sigma_k)\} $$  

**Step 1:** for sample $$x_i$$, the possibility of it generated from $$k$$th component is:

$$ \gamma(i, k) = \frac{\pi_k N(x_i|\mu_k, \Sigma_k)}{\sum_{j=1}^K \pi_jN(x_i|\mu_j, \Sigma_j)} $$  

**Step 2:** now according to the $$\gamma(i, k)$$ in step 1, we can update the values of $$\mu_k, \Sigma_k$$ by:

$$
\begin{align*}
	&\mu_k = \frac{1}{N_k}\Sigma_{i=1}^N \gamma(i,k)x_i \\
	&\Sigma_k = \frac{1}{N_k}\Sigma_{i=1}^N \gamma(i,k)(x_i - \mu_k)(x_i - \mu_k)^T
\end{align*}
$$

**Step 3:** iterate the two steps above until the log-likelyhood converges.  

**Note: GMM needs more computation than K-means, so a popular method is to firstly use K-means to get a rough result, then use the centroids in K-means as the initialization values of GMM.**
