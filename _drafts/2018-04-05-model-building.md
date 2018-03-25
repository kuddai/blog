---
layout: post
title: Automated model building
category: main
---

The models I currently care about;

* of the brain (why? -- another post?)
* tax (see [this post]({{site.baseurl}}) for some motivation)
* knowledge/wikipedia (dbpedia)
* ?

all share a similar problem. We want a working model of X so we can test various interventions. A computational model allows us to do this ethically and quickly.

Most of the time we have two types of data that we want to use to construct the model;

* examples in the form of measurements
* structured data in databases (gene interactions) that needs to be parsed
* existing knowledge in academic papers, ...

Cannot always trust any of the sources; experimental negilgence, wishful thinking, ...



Automatic differentiation. Allows us to tune model/parameters using the examples.
