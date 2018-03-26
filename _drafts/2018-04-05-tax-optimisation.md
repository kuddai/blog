---
layout: post
title: Tax optimisation
category: main
---

In NZ there is an anti-avoidance law stating;

> Quote of the law.

Want to minimise tax paid with legal strategies.
Aka constrainted optimisation? (but if we have a model, then)


<!-- ### Inequality

The rich can afford to pay lawyers and ...?
`Smart` allocations of their finances.

### Large companies paying low tax

Is this a bad thing?
Will need to look into how imports/exports are taxed.
Often the value has been created in another country so it feels weird to tax them for it?!
Income tax on any company that makes money from NZers, or any company that operates in NZ? -->

## Proposal

Rather than attempting to catch organisations that avoid paying tax (maybe I should look into this more. how easy is it?).
Want to make the tax system un-gameable.


More generally, how to write complete law. Tax law is more specified than most and more easily parsed by computers (?!?!? need to verify this claim). Making it a good candidate for it being the first body of law to apply ML.

Two parts.
Building a simulator.
Building un-gameable systems.

$f: allocation -> total_tax$
$g: allocation -> is_legal$ (by using the tax law model we are ensured that it is legal according to a narrow definition, but still could lose in court bc of the anti-avoidance law?!) Would like $h: allocation -> is_avoidance$

## Main barriers

What are the main dependencies? What can we do to quickly show that this idea will not work?

* Parsing the laws into computational model. Will need some new NLP tools? Is there anything fundmentally  hard/new? What are we even building? What are the inputs to tax law?
* Getting access to past cases. (are these necessary? probably, we will need to know how various inputs are classified!? and how laws are interpreted)
* ?
