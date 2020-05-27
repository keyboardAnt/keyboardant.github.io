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

*IMLE* is a generative model that maximise likelihood. IMLE solves: ① the [*mode dropping* (*mode collapse*) problem in GANs](/mode-dropping-problem-in-gans); ② the [vanishing gradient problem in GANs](/vanishing-gradient-problem-in-gans); and ③ the [training instability problem in GANs](/training-instability-problem-in-gans). In practice IMLE synthesises blurry images. Nevertheless, IMLE has its own strengths; it is utilised as a component of [a novel generative model that outperforms VAEs and GANs (named GLANN)](/what-is-glann).

IMLE stands for *Implicit Maximum Likelihood Estimation*, since it deals with *implicit* probabilistic models (like deep neural networks).

It was proposed on 2018, by Ke Li and Jitendra Malik.

## How IMLE works?



## IMLE drawbacks

Unfortunately in practice synthesises blurry images[^9].

## Improvements that outperform GANs

Can be combined with other methods to outperform GANs (GLANN)

> <img src="../assets/image-20200527131940130.png" alt="image-20200527131940130" style="zoom:25%;" />

## References
* "On the Implicit Assumptions of GANs", Ke Li and Jitendra Malik, 2018, [https://arxiv.org/abs/1811.12402](https://arxiv.org/abs/1811.12402)
* "Implicit Maximum Likelihood Estimation", Ke Li and Jitendra Malik, 2018, https://arxiv.org/abs/1809.09087

[^1]: "On the Implicit Assumptions of GANs", Ke Li and Jitendra Malik, 2018, [https://arxiv.org/abs/1811.12402](https://arxiv.org/abs/1811.12402)
[^2]: "Overcoming Mode Collapse and the Curse of Dimensionality" IAS Workshop, Ke Li, 2019, [https://drive.google.com/file/d/1PV4YN3OQprww4BCDwB9XWMUIz_mbdDab/view](https://drive.google.com/file/d/1PV4YN3OQprww4BCDwB9XWMUIz_mbdDab/view)
[^3]:"Unrolled Generative Adversarial Networks", Luke Metz, Ben Poole and David Pfau, 2017, [https://arxiv.org/pdf/1611.02163.pdf](https://arxiv.org/pdf/1611.02163.pdf)

[^4]: "Implicit Maximum Likelihood Estimation", Ke Li and Jitendra Malik, 2018, https://arxiv.org/abs/1809.09087

