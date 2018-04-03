---
layout: post
title: Tax optimisation as an adversarial game
---

I came across a new adversarial setting (at least new to me...) while getting curious about how to apply AI/ML to complete tax law and how to regulate tax optimisation (aka avoidance in my mind, see [this post - TODO](?)).

TODO Some background.
NZ uses a GAAR. In practice this means judiciaries end up making the law. Aka, there doesnt exist a set of well-specified laws, so judges must interpret the GAAR (expensive calls to the oracle). The rulings are then used as precedent for the future.

Two parts.
- Classifying avoidance. (precedent and judges interpretation)
- Completing tax law. (a formal set of rules)

_(but if we could classify all types of avoidance then tax law would be complete??? kinda? ...)_

# Completing tax law

Current tax law is incomplete, we have an inaccurate approximation of some complete set of tax laws. We use judges to ...?

## An adversary

Imagine a game between IRD and a taxpayer

<side>What about retrospective application of the law? Need to investigate</side>
(from the perspective of IRD)  

1. You reveal your move (write and pass some taxation legislation).
2. Your adversary (a tawpayer) organises its finances to minimise tax paid.
3. The loss is revealed to the adversary (they avoided $$ of tax). You must choose whether to query an expensive oracle (go to court and get a ruling from the law) to check whether you adversary has made a legal move. If qeried the oracle returns the loss. Otherwise you must use your approximation of the law to estimate the loss.

(_The loss should really the sum of avoided tax over all iterations? Or not? What difference does this make? Cumulative versus absolute versus differential?_)

What makes this setting hard?
- __Information asymmetry__. The adversary always gets access to the current loss (they know how much tax they avoided) (with respect to their moves, kinda, the multi-agent setting complicates this). While we don't get any info about the loss unless we query an expensive oracle (judges). (false positives are costly, although not as costly as false negatives. This also needs to be learned.
- __Computation asymmetry__. The adversary needs to find a single strategy to minimise tax (that is also legal). You need to find and subvert all potential strategies to avoid tax.
- __Memory asymmetry__. In the multiplayer setting (many adversaries), it is easy(er) for each adversary to model and track changes in tax law (maybe they even collaborate...). But it is hard(er) for us to model and track changes to thousands, or more, adversaries (changes in a corporations finances my be indicative of avoidance).

_Huh, a property of the minima (wrt to IRDs actions) would be that dLoss/dAdversary would also = 0. It doesnt matter what the adversary does, our loss remains the same, tax cant be avoided (although maybe they could pay more than necessary). Is that because it is a zero-sum game?_

## Adversarial examples

Adversarial examples are typically framed as black box problems (at least as far as I have seen), but what if you know that your adversary is going to be given your current model? How would you design your model given that information? Design a model so that it is stable under an informed adversarial attack. TODO need an examle of an application of this.

<side>Robustness to adversarial pertubations during training?!?</side>
There is a target function (implicitly known by judges and the high court), which captures tax avoidance. We are trying to approximate that implicit knowledge with few samples. But, as we learn our approximation (the law -- no? and yes!?), our adversaries (taxpayers) adapt their strategies. So, while learning to approximate the target function we want to minimise taxpayers ability to game our approximation.
<side>dL/dadv = 0. Dont want taxpayers to be able to change outcomes!?</side>
Note: We may be learning this target function for a while due to changes in the environment (which we need to adapt to) ...?

***

Extensions
* What if we cannot accurately model the true loss function (because of its expense and complexity, small numbers of samples compared to the complexity of the fn to be learned). It would be impossible to achieve zero loss, so how should we proceed?
* want to minimise cumulative loss, so we should learn to adapt quickly to our adversaries new strategies, or even predict them before they occur.

# Classifying tax avoidance

Defined as; set of actions that are legal, but when viewed from a global perspective, their only (\*) purpose is to avoid tax.

## Credit assignment

So if we have a set of loss function that capture the tax payers goals, ... and tax minimisation.

Can we assign credit to certain actions? WANT: this (set of) action(s) minimised tax paid, and did little else. (in fact, it made the company have a more complex structure and harder to run everyday.)

# Related work

<side>TODO Need to investigate other work using these asymmetries. Also what examples are there of problems that share these asymmetries?</side>
Aside from the asymmetries, this setting is similar to;

(Do any connections to mechanism design come to mind? I imagine there must be some previous work on this question.)
Learning a loss function. Which GANs are a good example of.
The key here us that we (the loss learner) have some finite capacity to check whether agents are exploiting our incomplete loss fn. How do you choose to spend your resources?


What would it look like if GANs shared these asymmetries?
```python
for _ in range(iterations):
    # player one makes its move
    discriminator = discriminator.update(loss)
    discrim = discriminator.freeze()

    # player two recieves the discriminator and
    # uses it to search for a low loss strategy
    generator = generator.train(discrim, iters=N)

    # the change in loss from generator at
    # step=0 to step=N is the loss
    loss = generator.loss(t=N) - generator.loss(t=0)
    dparams = generator.params(t=N) - generator.params(t=0)

    # maybe check the legality of the generators move
    # the loss is only revealed to the discriminator if
    # the oracle is queried. returns None if is not checked
    loss = maybe_check(loss, dparams)  
```

TODO. Relationship to reinforcement learning and reward hacking? And some of the safety research?
https://worldmodels.github.io/
Overfitting to approximate models, can do well in the virtual world, but poorly in the real world.

```python
# build an approximate model of the true dynamics
# aka construct some tax law to match intuition about right/wrong
for _ in range(iterations):

    o = env.step(a)

    # fit your model of tax law to observations
    # might not get these very often
    h = V(o)
    z_ = M(h, z)
    o_ = V_(z_)
    loss = d(o, o_)

# use the virtual/approximate model to
# learn a policy given some reward fn.
for _ in range(iterations):
  o = M.step(a)

  h = V(o)
  z_ = M(h, z)

  a = C(z_)
  r = R(z_)  
  # this issue is avoided in the paper.
  # how do we know R in the virtual environment?!?
```

We have a model. The set of laws.
And a loss function. How much the laws are gamed (aka unexpected use of the model?). Under the model, is a set of actions avoidance?


***
Questions raised;

* How can we design an un-gameable model, or what might be called a complete set of laws?
* How much harder is it to design un-gameable systems than to game that system?
* How would you even prove that a strategy is un-gameable?
* Is there a measure of gameability? The ability to __easily__ find hacks/strategies?

Legal questions

* What if I am overpaying my tax and then reorganise my finances so that I now pay as much as I 'should' be.
* The law seems to be two things? Specifies (some of) the allowable moves, a classifier of avoidance.
