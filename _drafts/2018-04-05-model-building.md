---
layout: post
title: Automated model building
category: main
---

The models I currently care about (only the important things);

* tax (actually tho, see [this post]({{site.baseurl}}) for some motivation)
* knowledge/wikipedia (dbpedia)
* logic (already built) -- see Coq or similar
* physics for;
  * computer design
  * semi-conductors
  * the universe
* biochemsitry for;
  * genetic engineering/organism design/process design
  * human physiology for drug design and gene therapy
  * the brain (why? -- another post? [this post]({{site.baseurl}}/)
* environmental
  * uhh, climate change...
* economic
  *

## Why do we care?

all share a similar problem. We want a working model of X so we can test various interventions to optimise something we care about. A computational model allows us to do this (mostly) ethically and quickly.

Parallel computing. We can run 10,000 simulations in parallel. So rather than having to wait

Costs a lot of energy, but time is more important to us.

## Model design constraints

Need to achieve right trade-off. Efficient to run. But accurate.

At what level should these systems be modeled? And how should that be decided. Want the ability to smoothly abstract or reduce.

* If we are simulating economies, do we need to model the biochemistry of people brains?

How do we know it is accurate?

## Model construction


Most of the time we have two types of data that we want to use to construct the model;

* examples in the form of measurements
* existing model stored in schemas and databases
* existing knowledge in academic papers, ?, ...

Cannot always trust any of the sources; experimental negilgence, wishful thinking, ...

##### Examples

Example often dont measure all the variables.
Automatic differentiation. Allows us to tune model/parameters using the examples.
But how much tuning is reasonable?
And what should be tuneable?

I like the idea of having priors on the structure and value of parameters. We want to take the minimum sized step away from the priors to increase the fit to the data.
Ideally the init is the final model.

##### Existing model




## Advanced use

Model aided exploration!
Once we have a model we can; search for new ?? run experiments. BUT, how can thus be done efficiently/effectively?

What if we have priors about likely minimisers?  

What are we eploring for?
Given some measure;
* damage due to climate change,
* likelihood of getting alzheimers,
* energy cost of storing a bit,

search for minimisers (a series of actions/interventions/a path). And rank them according to some complexity measure (or should that be part of the search?).   
