---
layout: post
title: "Neural Network Memorization"
permalink: neural-network-memorization
date: Jan 11, 2021
comments: true
typora-copy-images-to: ../assets
---

## 1. Abstract

It is well-known that a sufficiently large neural network can *memorize* (i.e., interpolate) an arbitrary finite dataset. However, current state-of-the-art network constructions are delicate and unlikely to be found by standard training methods. In contrast, guarantees for such methods require a network size much larger than what is information-theoretically needed. This blogpost proposes to study the gap between the two and understand memorization limitations using computationally efficient methods.

## 2. Introduction

Machine learning has become a pivotal component in a wide variety of fields, providing rich and powerful abilities that are changing the way we live, think and act. From controlling most of the trading in the world's capital markets, through advertising and content recommendation systems that affect our personal consciousness and social awareness. Autonomous vehicles that could potentially ease the physical distance barrier in commuting and delivering commodities, to groundbreaking advances in health which save lives. A notably valuable machine learning task is supervised learning, i.e., learning a function (a.k.a. predictor or hypothesis) that maps an input to an output based on example input-output pairs. A key question in supervised learning is that of *generalization*: how will a predictor $$\hat{h}$$ that was selected based on a given data set $$S = \left\{ \left( x_i, y_i \right) \right\}_{i=1}^{n}$$ perform on an unseen data? A well-known rule to select $\hat{h}$ is to use an *empirical risk minimization* (ERM) learning algorithm \[Vap95\]:

$$
\hat{h} = ERM_{\mathcal{H}} \left( S \right) \in \arg  \min_{h \in \mathcal{H}} L_{S}(h) = \arg \min_{h \in \mathcal{H}} \sum_{i = 1}^{n} L \left( h \left( x_i \right), y_i \right)
$$

Where $L$ is a loss function, and $\mathcal{H}$ is a set of functions (can be a function space). By restricting the learner to selecting a predictor from $\mathcal{H}$, we bias it toward a specific set of predictors. Such restrictions are often called an *inductive bias*. A classic example of an inductive bias is Occam's razor, prioritizing simpler, consistent hypotheses about the target function over more complex ones. Here consistent means that the learner’s hypothesis yields correct outputs for all of the examples given to the algorithm. The learner (i.e., the learning algorithm) receives the function class $\mathcal{H}$ before seeing the training data. Thus, how should we choose $\mathcal{H}$? Ideally, base on some prior knowledge about the problem to be learned (see, e.g., \[SS14\]). According to the *bias-variance tradeoff*, ideally, $\mathcal{H}$ should balances underfitting and overfitting [GBD92, HTF01]. Classical thinking is concerned with finding the “sweet spot” between underfitting and overfitting by controlling the capacity of $\mathcal{H}$ (e.g., limiting its VC dimension, covering number, fat-shattering dimension, Rademacher complexity, or other measures. See, for instance, [AB09, V’yu15, BHX20]). The control may be explicit, via the choice of $\mathcal{H}$ (e.g., picking the neural network architecture), or it may be implicit, using regularization (e.g., early stopping). Nevertheless, practitioners often use modern machine learning methods such as large neural networks and other non-linear predictors with zero (or negligible) empirical risk (i.e., training loss). Despite (i) the high capacity of the function class $\mathcal{H}$, and (ii) near-perfect fit to training data, these predictors typically give accurate predictions on new data [Bre95, LGT96, SFBL98, Bar98, NTS14, BFT17, ZBH+17, GRS18, DZPS18]. Consequently, a best practice in deep learning for choosing a neural network architecture is that the network should be large enough to allow effortless zero training loss, a.k.a. *memorization* or interpolation of the training data \[Sal17\]. Interestingly, experiments demonstrated that those networks generalize well even when memorizing a noisy training set [ZBH+17, BMM18, BHMM19].

When and why does interpolation imply generalization? It is yet another open question in the deep learning theory. One research direction that popped up was to analyze neural networks of infinite width (a.k.a. Neural Tangent) [JGH18, COB19]. Although negative results published in 2019 might end the hope of discovering a complete general answer to the interpolation–generalization question by studying those networks [YS19, GMMM19].

One of the questions people are interested in is: what are a network’s capabilities to memorize a data set? There are currently two kinds of results in the literature, answering the following: (i) what the smallest size of a network required to memorize a given training data set is? Moreover, (ii)—which is the same question as in (i)—but under the assumption of using a standard (i.e., computationally efficient) learning algorithm such as gradient descent (GD)? Our primary goal in this blogpost is to propose studying the current gap between (i) and (ii).

### The Expressive Power of a Single Hidden Layer ReLU Network (a.k.a. Information-Theoretic Bounds): When Is It Theoretically Possible to *Memorize*?

Positive results show that a sufficiently large neural network is expressive enough in order to ***memorize*** (i.e. interpolate) an arbitrary dataset [YSJ18, HM17, NH18, Ver20, KH19]. Formally, ***memorizing*** a dataset $$\left\{ \left( x_i, y_i \right) \right\}_{i=1}^{n}$$ (where no two $x_i$ are the same) by a neural network $$f_{w} : \mathbb{R}^{d} \to \mathbb{R}$$ (parameterized by $w$) means to satisfy $$f_{w} \left( x_j \right) = y_j$$ for all $$j \in \left\{ 1, 2, \ldots, n \right\}$$. Why is this not a surprise?

This phenomenon is closely related to the fact that a wide enough neural network is a universal approximator whenever its activation function is non-polynomial (as almost all activation functions are in the literature) [LLPS93, Pin99]. In other words (informally), it is possible to express a *continuous* function from $$\mathbb{R}^{d}$$ to $$\mathbb{R}$$ (i.e., *infinitely* many data points) via a neural network of sufficient width. Unlike those results, our blogpost deals with interpolating through *finitely* many data points, using the smallest possible width. How small exactly? Furthermore, more generally, what can we say where there is a bound on the network’s size?

Previous results indicated that a neural network (of any depth; and for various activation functions, including the ReLU) must have at least $n$ parameters (i.e., $n$ degrees of freedom) in order to memorize an arbitrary training set of size $n$ [BELM20, YSJ18M, MZ20, LPW+17, KL19, Hua03, HH91, HB98, Bau88, Sak92, Kow93, NH18, HM17, KH19].

Lately, a construction named the *Baum network* has been introduced: a feedforward fully-connected single hidden layer ReLU network of only $$\lceil 4n/d \rceil$$ hidden neurons (i.e. has slightly more than $n$ free parameters), that nevertheless can interpolate any given training set of size $n$, in ***general position*** \[BELM20\]. A ***general positioned*** dataset consists of $n$ distinct input points $$x_1, x_2, \ldots, x_n \in \mathbb{R}^{d}$$ such that $$\operatorname {span} \left( \left\{ x_1, x_2, \ldots, x_n \right\} \right) = \mathbb{R}^{d}$$, labeled correspondingly with a real value $$y_1, y_2, \ldots, y_n \in \mathbb{R}$$.

However, \[BELM20\] constructed the Baum network “by hand”: given a general positioned training set of size $n$, they built a network by carefully choosing its parameters. Those specific parameters are unlikely to be found by any known learning algorithm, e.g., GD, whenever the network initialization is random as in Xavier (namely, as in [GB10]). It is not yet clear whether a randomly initialized network of the same architecture that was trained by GD exhausts its own memorization capacity (i.e., will successfully memorize any general positioned training set of size $n$). It raises the open question: what is the smallest size of a network required to memorize a general data set?

### Learning to Memorize via gradient methods Over a *Randomly Initialized* Single Hidden Layer ReLU Network: When Is It Computationally Efficient?

Consider a *randomly initialized* (e.g., as in Xavier) neural network with non-polynomial activation function (e.g., a single hidden layer ReLU network). Can a gradient method (e.g., GD) reach a global minimum (in which the loss provably vanishes) in polynomial time complexity (w.r.t. $n$ and $d$, the number of samples in the training set and their dimension, respectively)?

A few results proved that as long as the network is sufficiently wide, namely, of width $$\widetilde{\Omega} \left( nd \right)$$, the answer to the previous question is positive for various settings [Sun19, DG19, Dan19, SY19, BELM20, MZ20, OS19, DZPS18, JGH18, BGW20, KH19].

Consequently, an open question is: will a gradient method (as GD) continue to efficiently memorize as the width decreases to its minimum, according to the information-theoretic bound, namely, $$\Theta{(n)}$$ hidden neurons?

Two recent papers revealed that GD over a single hidden layer ReLU network needs only $$\widetilde{O} \left( nd \right)$$ hidden neurons to efficiently memorizing a training set $$\left\{ \left( x_i, y_i \right) \right\}_{i=1}^{n}$$: both if (i) the inputs are one-dimensional real value $$x_1, \ldots, x_n \in \mathbb{R}$$ [SY19]; or if (ii) they are $d$-dimensional $$x_1, \ldots, x_n \in \mathbb{R^{d}}$$ in *isotropic position* [Dan20]. More precisely, in [Dan20] the inputs $$x_1, \ldots, x_n$$ were sampled i.i.d. from the standard multivariate normal distribution, i.e. $$x_1, \ldots, x_n \overset{\text{i.i.d.}}{\sim} \mathcal{N}{ \left( 0, I_d \right) }$$. Due to the *concentration of measure* phenomenon of the standard normal distribution $$\mathcal{N}{\left( 0, I_d \right)}$$ in high dimensions, the inputs $$x_1, \ldots, x_n$$ are concentrated in a thin spherical shell around the sphere of radius $$\sqrt{d}$$, a shell of width $$O \left( 1 \right)$$ [Ver18]. Thus the training set tends to be highly separable; intuitively making the learning easier [GD08].

This blogpost’s fundamental question is: can we relax the assumption that the training set is isotropic? That is to say, can a gradient method such as GD efficiently memorize an *arbitrary* training set of generally positioned inputs in $$\mathbb{R}^{d}$$?

## References

[Bau88]: E. B. Baum; "On the Capabilities of Multilayer Perceptrons";1988.

[HH91]: S. Huang and Y. Huang; “Bounds on the Number of Hidden Neurons in Multilayer Perceptrons”; 1991.

[GBD92]: S. Geman, E. Bienenstock, and R. Doursat; “Neural networks and the bias/variance dilemma”; 1992.

[Sak92]: A. Sakurai; "n-h-1 Networks Store No Less n*h+1 Examples, but Sometimes No More"; 1992.

[Kow93]: A. Kowalczyk; "Counting Function Theorem for Multi-Layer Networks"; 1993.

[LLPS93]: M. Leshno, V. Ya. Lin, A. Pinkus, and S. Schocken; “Multilayer Feedforward Networks With a Nonpolynomial Activation Function Can Approximate Any Function”; 1993.

[Bre95]: L. Breiman; “Reflections after refereeing papers for NIPS”; 1995.

[Vap95]: V. Vapnik; “The Nature of Statistical Learning Theory”; 1995.

[LGT96]: S. Lawrence, C. L. Giles, and A. C. Tsoi, “What size neural network gives optimal generalization? Convergence properties of backpropagation”; 1996.

[Bar98]: P. L. Bartlett; “The sample complexity of pattern classification with neural networks: The size of the weights is more important than the size of the network”; 1998.

[HB98]: G. Huang and H. A. Babri; “Upper Bounds on the Number of Hidden Neurons in Feedforward Networks With Arbitrary Bounded Nonlinear Activation Functions”; 1998.

[SFBL98]: R. E. Schapire, Y. Freund, P. L. Bartlett, and W. S. Lee; “Boosting the margin: A new explanation for the effectiveness of voting methods”; 1998.

[Pin99]: A. Pinkus; "Approximation Theory of the MLP Model in Neural Networks"; 1999.

[HTF01]: T. Hastie, R. Tibshirani, and J. Friedman; “The Elements of Statistical Learning”; 2001.

[Hua03]: G. Huang; “Learning Capability and Storage Capacity of Two- Hidden-Layer Feedforward Networks”; 2003.

[GD08]: M. Grochowski and W. Duch; "A Comparison of Methods for Learning of Highly Non-Separable Problems"; 2008.

[AB09]: M. Anthony and P. L. Bartlett; “Neural network learning: Theoretical foundations”; 2009.

[GB10]: X. Glorot and Y. Bengio; "Understanding the difficulty of training deep feedforward neural networks"; 2010.

[NTS14]: B. Neyshabur, R. Tomioka, and N. Srebro; "In search of the real inductive bias: On the role of implicit regularization in deep learning"; 2014.

[SS14]: S. Ben-David and S. Shalev-Shwartz; “Understanding Machine Learning: From Theory to Algorithms”; 2014.

[V’yu15]: V. V. V’yugin; “Measures of Complexity”; 2015.

[BFT17]: P. L. Bartlett, D. J. Foster, and M. J. Telgarsky; “Spectrally-normalized margin bounds for neural networks”; 2017.

[ZBH+17]: C. Zhang, S. Bengio, M. Hardt, B. Recht, and O. Vinyals; "Understanding deep learning requires rethinking generalization"; 2017.

[HM17]: M. Hardt and T. Ma; “Identity Matters in Deep Learning”; 2017.

[LPW+17]: Z. Lu, H. Pu, F. Wang, Z. Hu, L. Wang; "The Expressive Power of Neural Networks: A View from the Width"; 2017.

[Sal17]: R. Salakhutdinov; Deep learning tutorial at the Simons Institute, Berkeley; 2017.

[BMM18]: M. Belkin, S. Ma, and S. Mandal; "To understand deep learning we need to understand kernel learning"; 2018.

[DZPS18]: S. S. Du, X. Zhai, B. Poczos, A. Singh; "Gradient Descent Provably Optimizes Over-parameterized Neural Networks"; 2018.

[GRS18]: N. Golowich, A. Rakhlin, and O. Shamir; “Size-independent sample complexity of neural networks,”; 2018.

[JGH18]: A. Jacot, F. Gabriel, C. Hongler; "Neural Tangent Kernel: Convergence and Generalization in Neural Networks"; 2018.

[NBS18]: B. Neyshabur, S. Bhojanapalli, and N. Srebro; “A PAC-Bayesian approach to spectrally-normalized margin bounds for neural networks”; 2018.

[NH18]: Q. Nguyen and M. Hein; “Optimization Landscape and Expressivity of Deep CNNs”; 2018.

[Ver18]: R. Vershynin; "High-Dimensional Probability: An Introduction with Applications in Data Science"; 2018.

[YSJ18]: C. Yun, S. Sar, and A. Jadbabaie; “Small ReLU Networks Are Powerful Memorizers: A Tight Analysis of Memorization Capacity”; 2018.

[BHMM19]: M Belkin, D. Hsu, S. Ma, and Soumik Mandal; “Reconciling modern machine learning practice and the bias-variance trade-off”; 2019.

[COB19]: L. Chizat, E. Oyallon, and F. Bach; “On lazy training in differentiable programming”; 2019.

[Dan19]: A. Daniely; "Neural Networks Learning and Memorization With (Almost) No Over-Parameterization"; 2019.

[DG19]: B. Das and E. A. Golikov; "Quadratic Number of Nodes Is Sufficient to Learn a Dataset via Gradient Descent"; 2019.

[GMMM19]: B. Ghorbani, S. Mei, T. Misiakiewicz, and A. Montanari; “Linearized two-layers neural networks in high dimension”; 2019.

[KH19]: K. Kawaguchi and J. Huang; “Gradient Descent Finds Global Minima for Generalizable Deep Neural Networks of Practical Sizes”; 2019.

[KL19]: P. Kidger and T. Lyons; "Universal Approximation with Deep Narrow Networks"; 2019.

[OS19]: S. Oymak and M. Soltanolkotabi; "Towards Moderate Overparameterization: Global Convergence Guarantees for Training Shallow Neural Networks"; 2019.

[Sun19]: R. Sun; "Optimization for Deep Learning: Theory and Algorithms"; 2019.

[SY19]: L Su and P. Yang; "On Learning Over-Parameterized Neural Networks: A Functional Approximation Perspective"; 2019.

[YS19]: G. Yehudai and O. Shamir, “On the power and limitations of random features for understanding neural networks”; 2019.

[BELM20]: S. Bubeck, R. Eldan, Y. Tat Lee, D. Mikulincer; “Network Size and Weights Size for Memorization With Two-Layers Neural Networks”; 2020.

[BGW20]: S. Buchanan, D. Gilboa, and J. Wright; “Deep Networks and the Multiple Manifold Problem”; 2020.

[BHX20]: M. Belkin, D. Hsu, and J. Xu; "Two models of double descent for weak features"; 2020.

[Dan20]: A. Daniely; "Memorizing Gaussians With No Over-Parameterization via Gradient Descent on Neural Networks"; 2020.

[MZ20]: A. Montanari and Y. Zhong; "The Interpolation Phase Transition in Neural Networks- Memorization and Generalization under Lazy Training"; 2020.

[Ver20]: R. Vershynin; "Memory Capacity of Neural Networks With Threshold and ReLU Activations"; 2020.
