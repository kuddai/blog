---
layout: post
title: An adversarial game with taxes
category: main
---

I came across a new adversarial setting (at least new to me...) while getting curious about how to apply AI/ML to complete tax law and how to regulate tax optimisation (aka avoidance in my mind, see [this post - TODO](?)).

Imagine a game between taxation law(yers) (or IRD) and corporations

<side>What about retrospective application of the law? Need to investigate</side>
(from the perspective of the IRD)  

1. You reveal your move (write and pass some taxation legislation).
2. Your adversary (a corporation) organises its finances to minimise tax paid.
3. The loss is revealed to the adversary (they avoided $$ of tax). You must choose whether to query an expensive oracle (go to court and get a ruling from the law) to check whether you adversary has made a legal move. If qeried the oracle returns the loss. Otherwise you must use your approximation of the law to estimate the loss.

(_The loss should really the sum of avoided tax over all iterations? Or not? What difference does this make? Cumulative versus absolute versus differential?_)

What makes this setting hard?
- __Information asymmetry__. The adversary always gets access to the current loss (with respect to their moves, kinda, the multi-agent setting complicates this). While we don't get any info about the loss unless we query an expensive oracle (prosecution). (false positives are costly, although not as costly as false negatives. This also needs to be learned.
- __Computation asymmetry__. The adversary needs to find a single strategy to minimise tax. You need to find and subvert all potential strategies to avoid tax.
<side>Tracking changes in a corporations finances my be indicative of avoidance</side>
- __Memory asymmetry__. In the multiplayer setting (many adversaries), it is easy(er) for each adversary to model and track changes in tax law (maybe they even collaborate...). But it is hard(er) for us to model and track changes to thousands, or more, adversaries.

Effectively there is a true loss function (judges and the high court). We are just trying to approximate it with few samples. But, as we change our strategy (the law), our adversaries (corporations) adapt their strategies.

Extensions
* What if we cannot accurately model the true loss function (because of its expense and complexity, small numbers of samples compared to the complexity of the fn to be learned). It would be impossible to achieve zero loss, so how should we proceed?
* want to minimise cumulative loss, so we should learn to adapt quickly to our adversaries new strategies, or even predict them before they occur.

_Huh, a property of the minima (wrt to IRDs actions) would be that dLoss/dAdversary would also = 0. It doesnt matter what the adversary does, our loss remains the same, tax cant be avoided (although maybe they could pay more than necessary). Is that because it is a zero-sum game?_

## Related work

<side>TODO Need to investigate other work using these asymmetries. Also what examples are there of problems that share these asymmetries?</side>
Aside from the asymmetries, this setting is similar to;

Adversarial examples. They are typically framed as black box problems (at least as far as I have seen), but what if you know that your adversary is going to be given the model, how would you design the model given that? Design a model so that it is stable under an informed adversarial attack. TODO need an examle of an application of this.

<side>Do any connections to mechanism design come to mind? I imagine there must be some previous work on this question.</side>
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

***
Questions raised;

* How can we design an un-gameable model, or what might be called a complete set of laws?
* How much harder is it to design un-gameable systems than to game that system?
* How would you even prove a strategy it is un-gameable?
* Is there a measure of gameability? The ability to __easily__ find hacks/strategies?
