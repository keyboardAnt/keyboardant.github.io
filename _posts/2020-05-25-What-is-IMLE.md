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

*IMLE* is a generative model that maximize likelihood. IMLE solves: ① the [*mode dropping* (*mode collapse*) problem in GANs](/mode-dropping-problem-in-gans); ② the [*vanishing gradient* problem in GANs](/vanishing-gradient-problem-in-gans); and ③ the [training instability problem in GANs](/training-instability-problem-in-gans). In practice IMLE synthesizes blurry images. Nevertheless, IMLE has its own strengths; it is utilised as a component of [a novel generative model that outperforms VAEs and GANs (named GLANN)](/what-is-glann).[^1]

IMLE stands for *Implicit Maximum Likelihood Estimation*, since it deals with *implicit* probabilistic models (like deep neural networks).

IMLE was proposed on 2018, by Ke Li and Jitendra Malik.[^2]

## Why maximizing likelihood is a great approach?

Maximizing [likelihood](https://en.wikipedia.org/wiki/Likelihood_function) in effect *minimize a divergence measure* between the *data* distribution and the *model* distribution.[^2]
The [maximum likelihood estimator (MLE)](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation) has a number of appealing properties: under mild regularity conditions, it is asymptotically [consistent](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation#Consistency), [efficient](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation#Efficiency) and [normal](https://en.wikipedia.org/wiki/Local_asymptotic_normality).[^2]

All of the above can explain why maximum likelihood is perhaps the standard method for estimating the parameters of a probabilistic model from observations.[^2]

## Likelihood maximization in deep generative models (like GANs)

### Why maximizing likelihood is not trivial for deep generative models (like GANs)?

Because deep neural networks (like GANs) are *implicit* probabilistic models. Their likelihood function considered to be too complicated to express/evaluate.

#### *Prescribed* vs *Implicit* models

Generative models can be classified into two (not disjoint*) categories:[^2]

##### *Prescribed* models

are defined by an explicit specification of the density. Therefore their unnormalized complete likelihood can be usually expressed in closed form. Examples include [mixture of Gaussians](https://en.wikipedia.org/wiki/Mixture_model#Gaussian_mixture_model), and [hidden Markov models](https://en.wikipedia.org/wiki/Hidden_Markov_model).

##### *Implicit* models

are defined most naturally in terms of a (simple) sampling procedure. Most models take the form of a deterministic parameterized transformation $T_θ(·)$ of an analytic distribution, like a Gaussian. The transformation $T_θ(·)$ often takes the form of a highly expressive function approximator, like a [neural network](https://machinelearningmastery.com/neural-networks-are-function-approximators/#:~:text=Training%20a%20neural%20network%20on,the%20intuitions%20for%20function%20approximation.). Examples include GANs.

  > Implicit models can be naturally viewed as the distribution induced by the following sampling procedure:[^2]
  >
  > 1. Sample $z ∼ N(0,I)$
  > 2. Return $x := T_θ(z)$ 

> *Some models admit both an explicit specification of the density and a simple sampling procedure and so can be considered as both prescribed and implicit. Examples include [variational autoencoders (VAE)](https://towardsdatascience.com/understanding-variational-autoencoders-vaes-f70510919f73).[^2]

###### Likelihood of an implicit model

According to Li and Malik, in general, attempting to reduce the marginal likelihood of an implicit model to a closed-form expression is hopeless. Evaluating it numerically is also challenging, since the domain of integration could consist of an exponential number of disjoint regions and numerical differentiation is ill-conditioned.[^2]

### GANs alternative learning approach: minimizing the objective will minimize an $f$-divergence between data and samples

Instead of maximizing likelihood, GANs took a different learning approach:

#### Learning goal

GANs are based on the idea of minimizing the distinguishability between data and samples.[^2]

#### Theoretical guarantees

It has been shown that when given access to an infinitely powerful discriminator, the GAN objective *minimizes* a few instances of [$f$-divergences](https://en.wikipedia.org/wiki/F-divergence).[^2]

#### Problems in practice

Despite the theoretical results, there are a number of challenges that arise in practice, such as ① [mode dropping/collapse](/mode-dropping-problem-in-gans), ② [vanishing gradients](vanishing-gradient-problem-in-gans) and ③ [training instability](/training-instability-problem-in-gans).[^2]

##### Why those problems occur in practice?

A number of explanations have been proposed to explain these phenomena and point out that many theoretical results rely on assumptions that does *not* holds in practice (for example, that the number of samples from the true data distribution must be infinite).[^2] For more details on those three problems, read my blogposts (link above).

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
