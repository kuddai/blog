---
layout: post
title: Causal calculus
---

I recently read Judea's [book](https://www.goodreads.com/book/show/36204378-the-book-of-why
) on Causal Inference (you should to). I noticed an intriguing generalisation of a couple of the formulas.


## Causal inference

<side>This section is largely taken from Chapter 7. in The book of Why
</side>

What we care about is the ability to estimate causal relationships from data. Here we consider two methods to estimate a causal relationship using observed data; the front and back door adjustments.

Causal relationships can sometimes be estimated from the data's correlation, but if a confounder is present it complicates the analysis.

![pic]({{site.baseurl}}\images/smoking.png)


$X$ stands for Smoking, $Y$ stands for Cancer, $Z$ stands for Tar and $U$ stands for Smoking gene.

Difference in P(Y \mid do(Z)) - P(Y \mid do(-Z)) = average causal effect.




#### The back door adjustment

If we are able to close all the back doors (control/remove all paths into $X$ that connect to $Y$) then the causal relationship between $X$ and $Y$ is simply their correlation.

$$
\begin{align}
P(Y \mid do(X)) &= \sum_U P(Y \mid X, U=u) P(U=u) \tag{iff all back doors are shut} \\
Y &= aX + bU + c \tag{assume linear and independent} \\
a &= \frac{\mathbb E [(X -\mu_X)(Y-\mu_Y - U + mu_U)]}{\sigma_X}  \tag{$X\cdot U = 0 \mid Y$} \\
&= \frac{\mathbb E [(X -\mu_X)(Y-\mu_Y)]}{\sigma_X}  \tag{correlation coefficient} \\
\end{align}
$$

THIS IS WRONG!!?!?


#### The front door adjustment

Now, lets consider the case where we do not have measurements on the confounder, $U$ but still want to estimate $P(Y \mid do(X))$. Is it still possible? Surprisingly, yes.

We can simply estimate the effect of smoking on tar from their correlation as there are no confounders.
And we can estimate the effecto for tar on cancer by blocking the backdoor, through controlling for smoking.

Or as eqns;

$$
\begin{align}
P(Z \mid do(X)) &= P(Z, X) \tag{no back doors to close}\\
P(Y \mid do(Z)) &= \sum_X P(Y, Z, X=x) P(X=x) \tag{close backdoor $Z \to X\to U\to Y$}\\
P(Y \mid do(X)) &= \sum_Z P(Z=z, X) \sum_X P(Y\mid X=x, Z=z) P(X=x) \\
\end{align}
$$

## Expected gradients

Cool, now here is the nice part. It all started from the realisation that the correlation coefficient can be rewritten as the expected gradient. I think this generalisation gives the ability to think about causal relationships between cts non-linear relationships between random variables (?).


$$
c_{x}(y) = \mathbb E [\parallel \frac{\partial y}{\partial x} \parallel_1]
$$

__Intuition:__

1. If changes in X almost always cause large changes Y this should yield high measure of a causal relationship
2. If there exists a value of X that cause large changes Y but it almost never occurs, then X is not a 'cause' of Y (at least most of the time...).


#### The backdoor adjustment

$$
\begin{align}
c_x(y) &= \mathbb E [\parallel\frac{\partial y}{\partial x}\parallel_1]  \\
&= \frac{\mathbb E[(X -\mu_X)(Y-\mu_Y)]}{\sigma_X}  \tag{from above -- backdoor adjustment} \\
&= \mathbb E\frac{[(X -\mu_X)(Y-\mu_Y)]}{(X -\mu_X)(X -\mu_X)} \\
&= \mathbb E\frac{[(Y-\mu_Y)]}{(X -\mu_X)} \\
&= \mathbb E\frac{\Delta Y}{\Delta X} \tag{expectation of gradient}\\
\end{align}
$$


#### The front door adjustment: Chain rule

$$
\begin{align}
c_{x_i}(y) &= \mathbb E [\parallel\frac{\partial Y}{\partial Z}\frac{\partial Z}{\partial X}\parallel_1] \\
\text{from frontdoor adjustment}\\
P(Z \mid do(X)) &= \frac{\mathbb E [(X -\mu_X)(Z-\mu_Z)]}{\sigma_X}  \tag{correlation} \\
P(Y \mid do(Z)) &= \\
\end{align}
$$

## Experiments

Lets test this out with some simple non-linear fns.

$f(x) = x^2$

$f(x) = sin(x)$

$f(\bar x, \bar y) = \bar x^T A \bar y$


## Thoughts

* Feels similar to https://arxiv.org/abs/1703.01365
* This captures the notion of sufficient causation? What about higher order gradients? $\frac{\partial f^2}{\partial x \partial y}$ to given necessary causes?
* ?

Desiderata.

Would like a measure of causal effect to;
- be between 0-1. Does not cause vs totally determined by.
- the direction of the gradient doest matter, only the magnitude (l1 or l2? or lp?)
- deterministic fns only (otherwise the grads dont make sense?) noise must be an argument.
