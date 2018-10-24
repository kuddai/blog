---
layout: post
title: The advantages of abduction?
---

What can reasoning via abdction provide that deduction cannot?
(refering to abduction to mean reasoning from effects to causes)

$$
\begin{align}
???
\end{align}
$$

test

![]({{ site.baseurl }}/images/abduction-cup.png){: .center-image }

???


## Deduction + Abduction

Imagine you are an agent in a 2d environment. Lets discretise the space for simlicity, he grid graph in n dimensions.

However, rather than having access to the usual euclidean metric, you have nothing.
You are tasked with getting from A to B.

This is a common situation in the RL setting. The learner does not know how its actions move it around the space it is in, and it does not know which actions will lead to a reward.


![]({{ site.baseurl }}/images/abduction.png){: .center-image }


In this case, in the deduction only case, there are $2^6$ states that are searched. While in the adbuction and deduction search there are $2\times 2^3=2^4$ states searched.

![]({{ site.baseurl }}/images/abduction-tree.png){: .center-image }

## Questions/thoughts

- If you have many subgoals along the way.
- Requires that assumption of symmetry. All we are doing is exploiting the symmetry that the path from A to B is the same as the path from B to A. (when is this not the case?)
