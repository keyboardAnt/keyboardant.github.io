---
layout: post
title: "What is IMLE?"
permalink: what-is-imle
date: May 25, 2020
comments: true
typora-copy-images-to: ../assets
---

Why do we care?

## What is IMLE?

*IMLE* is a generative model that maximize likelihood. IMLE solves: ① the [*mode dropping* (*mode collapse*) problem in GANs](/mode-dropping-problem-in-gans); ② the [vanishing gradient problem in GANs](/vanishing-gradient-problem-in-gans); and ③ the [training instability problem in GANs](/training-instability-problem-in-gans). In practice IMLE synthesizes blurry images. Nevertheless, IMLE has its own strengths; it is utilised as a component of [a novel generative model that outperforms VAEs and GANs (named GLANN)](/what-is-glann).[^1]

IMLE stands for *Implicit Maximum Likelihood Estimation*, since it deals with *implicit* probabilistic models (like deep neural networks).

IMLE was proposed on 2018, by Ke Li and Jitendra Malik.[^2]

## Why maximizing likelihood is a great approach?

Maximizing [likelihood](https://en.wikipedia.org/wiki/Likelihood_function) in effect *minimize a divergence measure* between the *data* distribution and the *model* distribution.[^2]
The [maximum likelihood estimator (MLE)](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation) has a number of appealing properties: under mild regularity conditions, it is asymptotically [consistent](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation#Consistency), [efficient](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation#Efficiency) and [normal](https://en.wikipedia.org/wiki/Local_asymptotic_normality).[^2]

All of the above can explain why maximum [likelihood](https://en.wikipedia.org/wiki/Likelihood_function) is perhaps the standard method for estimating the parameters of a probabilistic model from observations.[^2]

### GANs approach: to minimize an  *f* -divergences

GANs are based on the idea of minimizing the distinguishability between data and samples (Tu, 2007; Gutmann & Hyvärinen, 2010). It has been shown that when given access to an infinitely powerful discriminator, the original GAN objective minimizes the Jensen-Shannon divergence, the − log D variant of the objective minimizes the reverse KL-divergence minus a bounded quantity (Arjovsky & Bottou, 2017), and later extensions (Nowozin et al., 2016) minimize arbitrary *f* -divergences.

In the case of GANs, despite the theoretical results, there are a number of challenges that arise in practice, such as mode dropping/collapse (Goodfellow et al., 2014; Arora & Zhang, 2017), vanishing gradients (Arjovsky & Bottou, 2017; Sinn & Rawat, 2017) and training instability (Goodfellow et al., 2014; Arora et al., 2017). A number of explanations have been proposed to explain these phenomena and point out that many theoretical results rely on three assumptions: the discriminator must have infinite modelling capacity (Goodfellow et al., 2014; Arora et al., 2017), the number of samples from the true data distribution must be infinite (Arora et al., 2017; Sinn & Rawat, 2017) and the gradient ascent-descent procedure (Arrow et al., 1958; Schmidhuber, 1992) can converge to a global pure-strategy Nash equilibrium (Goodfellow et al., 2014; Arora et al., 2017).

## How IMLE works?



## IMLE drawbacks

Unfortunately in practice synthesizes blurry images[^9].

## Improvements that outperform GANs

Can be combined with other methods to outperform GANs (GLANN)

> <img src="../assets/image-20200527131940130.png" alt="image-20200527131940130" style="zoom:25%;" />

## References
* "On the Implicit Assumptions of GANs", Ke Li and Jitendra Malik, 2018, [https://arxiv.org/abs/1811.12402](https://arxiv.org/abs/1811.12402)
* "Implicit Maximum Likelihood Estimation", Ke Li and Jitendra Malik, 2018, https://arxiv.org/abs/1809.09087

[^1]: "Overcoming Mode Collapse and the Curse of Dimensionality" IAS Workshop, Ke Li, 2019, [https://drive.google.com/file/d/1PV4YN3OQprww4BCDwB9XWMUIz_mbdDab/view](https://drive.google.com/file/d/1PV4YN3OQprww4BCDwB9XWMUIz_mbdDab/view)
[^2]: "Implicit Maximum Likelihood Estimation", Ke Li and Jitendra Malik, 2018, [https://arxiv.org/abs/1809.09087](https://arxiv.org/abs/1809.09087)
[^3]: "On the Implicit Assumptions of GANs", Ke Li and Jitendra Malik, 2018, [https://arxiv.org/abs/1811.12402](https://arxiv.org/abs/1811.12402)
