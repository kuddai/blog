---
layout: post
title:  First class loss functions
---

What is the right language for describing systems of loss functions? How should they be composed and decomposed?

Relatedly, is there some language that can take loss functions as [first class](https://en.wikipedia.org/wiki/First-class_function) objects which can be passed around, transformed, composed, … ? Thus allowing for [high order](https://en.wikipedia.org/wiki/Higher-order_function) loss functions. Much like functions can be in functional programming (interestingly, we could make a recursive loss functions).


Can we make this into a more general framework, where we can reason about how to compose and decompose parameterised (loss) functions?

<!-- We can do this with tf in some senses? Connecting nets together. We just dont have ideas about what the result will be-->

Problem. How the loss acts on a model is dependent on;

* the variables it is allowed to control,
* the optimiser used, learning rate, momentum, ...
* the data provided,
* ?

### Desierdata



##### Transformation

$$
f, g \in \mathcal L \\
\mathcal T: f \rightarrow g \\
$$

[PFC as meta-RL](https://deepmind.com/blog/prefrontal-cortex-meta-reinforcement-learning-system/). An expensive loss function is used to construct a heuristic version that has been fit to data. How does the parent loss fn relate to the child loss fn?

$$
\begin{align}
\mathcal A_{\mathcal D}(f) = g \tag{loss fn generates loss fn give a dataset}\\
f \sim g ??? \tag{how are they related}\\
\end{align}
$$


##### Composition

$$
f, g, h \in \mathcal L \\
\circ: f \times g \rightarrow h \\
$$

Maybe $y = P(cat)$? So we reverse the label for $f_{-1}$, thus training on both we would expect the gradients to cancel each other out.


$$
\begin{align}
f(y, t) &= -t \cdot log(y) - (1-t) \cdot log(1-y)  \\
f^{-1}(y, t) &= -t \cdot log(1-y) - (1-t) \cdot log(y)  \\
f \circ f^{-1} &= \mathbb 0  \tag{} \\
\end{align}
$$

* What do we mean when we say we want X and Y? Does that mean we can simply add the loss fns?
* What does the product of two loss fns mean? What if they are applied to different parameters?
* What we really want to know. How will my model/system evolve given the interaction of these loss fns?
* What guarantees are there for finding minima when composing loss fns? Do no harm to each other?!?


* Loss1 of Loss2 ( Loss1(Loss2) )
* Loss1 and Loss2 ( Loss1 + Loss2 )
* ?

### Related ideas and resources

* How are the layers in a neural net related to the tapes in a turing machine?
* [Compsing neural networks for QAs](https://arxiv.org/abs/1601.01705), [Predicting parameters](https://arxiv.org/abs/1306.0543)
* [Decoupled neural interfaces](http://arxiv.org/abs/1608.05343) decompose a global loss function into local loss functions (the functions learnt by the synthetic gradient predictors — the $M_i$s).
* Bootstrapping loss functions (term from [Integration of DL and NS](https://arxiv.org/abs/1606.03813)
* [Continuation optimisation](http://people.csail.mit.edu/hmobahi/pubs/aaai_2015.pdf)
* [Curriculum learning](http://ronan.collobert.com/pub/matos/2009_curriculum_icml.pdf)
* [Mollifying networks](http://arxiv.org/abs/1608.04980)
* What about parameterised loss functions?
