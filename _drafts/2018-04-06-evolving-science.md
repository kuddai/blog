---
layout: post
title: Evolving scientific models
---
<!--
The relationship of emergence the scientific process.
-->

In the past science has made progress by reducing phenomena down to its atomic parts, the irreducible bases that are composed to the given phenomena.
<!-- Would prefer not to lecture... -->
Imagine we want to understand {insert reduction example}.

This method works well. But, what about the converse problem. Rather than going from complex phenomena to

<side>Recently this method has been recieving criticism.</side>


> Science by first principles.

What is the goal of science? Generate accurate explanations for phenomena we observe. It isnt enough to just fit a model to the observed data, because we almost always do not have access to all of the information and thus we are solvig an underconstrained problem. There are many models that fit the data.

So the question becomes; which model is the best one?


Assumption 1: Reducability
If components of a model can independently explain some of the observed phenomena then the composition of those components makes a likely model.
Assumption 2: Generality (it this different to simplicity? the assumption of an integrated representation of everything)

Assumption 3: Simplicity (is this equivalent to reducability?)
<!-- Assumption 4: Induction !? -->
Assumptin 5: Smoothness
Assumption 6: Necessity implies causality (is that an assumption?!)

***


Show that: optimising a reward, in different environments (aka under different constraints/assumptions) various strategies (memory, safe trade, ...) emerge naturally.

Other ways of stating the same thing;
- Show which environments provide advantages to different strategies when optimising for the same goal.
- Show what is necessary/sufficient for a certain phenomena to emerge


### What does it mean to understand?

Heirarchy of explanation;

1. Generative (association. could just fit a fn)
- Disentanglement and reductionism. (this `fn` is sufficient to generate Z from X and Z)
- Counterfactuals (via ablation) -- can give us necessity (given other assumptions). (X is necessary for Z)
- Advantages given by bounds on the complexities of resources. (why is X necessary for Z?)
- A single simple fn being optimised.


Process;

- generate various emergent behaviours.
- study them and find patterns?
- ...?

Questions to answer;

- What is the problem being solved by X?
- And why is X necessary? (comprared to potential alternatives it ...?)
- What can inaccurate models tell us? The models half way along the trajectory?

## In practice

Imagine we have a model of the brain. Questions we might like to ask would be;

- how much does assumption A effect the accuracy of our model?
- ?


## Problems with this approach;

- a trajectory/generative reward only proves sufficiency (or conditional necessity).
- ?

What is necessary to build an explanation?
Generative. Each part is necessary.

This is just the same as all science? Build a model!?! But the how is the important part.
- Reduce to simple testable cases.
- Build up complexity
- Figure out which assumptions are necessary and cut others. Compress!!

# Examples

I see some similarities in the methodology (I would want to use) to understand cooperation/trading/specialisation and to understand the brains structure.

## Explaining the evolution of XXX

For each arrow we want;
- proof that the step provides an advantage
- the step to be possible via a 'smooth' trajectory
- ?

### The evolution of collaboration
> Reputation -> Money -> Markets.
<!-- Repuation (as a signal for estimating trust) doesn't scale well ($n^{\mathcal O(1)}$) with larger numbers of traders. Money ... scales -->

### The evolution of language
> Planning -> Merge -> Language.

### The evolution of life

> Membrane potentials -> ? -> ?

<!-- Need to re-read the vital question. -->

### The evolution of the brain

> Learning -> ? -> ?

The main question I would want to answer is; what advantage does X brain structure provide? If we are going to include bounary/goal/time cells, or some alternative neural topology between CA1 and grid cells, what advantage do they provide our agent/organism? Can it learn faster? Can it generalise better? ... etc Does the change help make more babies?

So, what I really want to understand is what needs to be done computationally to solve a problem, aka its complexity, and what structures in the brain are necessary/sufficient.

### The construction of the brain

Given a value fn (maybe many?), construct a new loss fn tailored to the environment.

## What about other theories?


What about if we viewed the evolution of theories of gravity in a similar way?!? Always optimising accuracy.

### Relativity

> Classical mechanics -> Relativity -> ?

First the easily solutions are found and constrained by data.
- Speed of light is necessary for relativity.
- ?


***

Not only does a model have to be as simple as possible, but it also needs a simple process by which the model can arise. (is that the same as just having a model that is as simple as possible?)

Many models might fit the data. Only consider "constructible" (aka learnable?) models.


Just give the process some names to make things clear.
$$
Data \math_op{\rightarrow}_{} Model \math_op{\rightarrow}_{Compression} Axioms \\
Data \math_op{\leftarrow}_{Generation} Model \math_op{\leftarrow}_{Construction} Axioms \\
$$


```python
construct: Axioms -> Model
generate: Model -> Data
compress: Data -> Model
formalise: Model -> Axioms
```

The axioms, given a ???, can construct the model.
The model, given an init, can generate the data.

Ahh, but when we are searching for the right axioms, we still use the data to constrain the space of models.

How can we formalise?
Imagine we have a model of particle physics. How can we find the minimal set of assumptions that (approximately) generate our model?

Nah, formalisation and compression are really the same thing? Take an explicit construction of something (a dataset or a model) and compress it.
