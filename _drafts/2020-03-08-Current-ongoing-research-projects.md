---
layout: post
title: "Current ongoing research projects"
permalink: current-ongoing-research-projects
date: Mar 8, 2021
comments: true
typora-copy-images-to: ../assets
---

I am working with [Prof. Ohad Shamir](http://www.wisdom.weizmann.ac.il/~shamiro/) on two theoretical research projects. In both, we are studying the dynamics (and limitations) of Gradient Descent over neural nets.

The first project is a collaboration with [Dr. Gal Vardi](https://dblp.org/pid/167/9638.html), extending Vardi and Shamir’s [paper](https://arxiv.org/pdf/2012.05156.pdf) on GD’s implicit regularization to more general cases, contradicting the common conjecture that GD biases into minimizing [rank](https://papers.nips.cc/paper/2020/file/f21e255f89e0f258accbe4e984eef486-Paper.pdf) (of the net’s hidden weights matrix).

The second is a collaboration with [Dr. Dan Mikulincer](http://www.wisdom.weizmann.ac.il/~danmi/). Our goal is to extend Daniely’s memorization [guarantee](https://proceedings.neurips.cc/paper/2020/file/662a2e96162905620397b19c9d249781-Paper.pdf) for GD over an isotropic dataset to arbitrary datasets, or proving that a gap exists. We are analyzing whether GD could interpolate a dataset created by high-dimensional random walks on spheres, as it violates one of Daniely’s assumptions.