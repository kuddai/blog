---
layout: post
title: Automatic complexity bounds
---

```python
import bound
from bound import complexity_measures as cplx

def sort_list(length):

  unsorted_list = random_list(length)
  sorted_list = unsorted_list[0]
  with bound.scope():
    for i, elem in enumerate(unsorted_list):
      if

  return sorted(x)

b = bound.upper(sort_list, measure=cplx.memory)
print(b)
>>> "O(n)"

b = bound.upper(sort_list, measure=cplx.time)
print(b)
>>> "O(n**2)"
```

Can we automatically calculate/estimate/approximate the complexity of various algorithms?

I imagine it would work similar to how automatic differentiation works. Define a set of basis operations, where each one has its complexity defined (memory, time, parallel, energy, latency, ...). As these basis ops are composed we can easily ...?

## Desiderdata

* Want the lowest upper bound. That might take some work to find!?
* Want the bound to be expressed in an 'intuitive' way
* must be more efficient than just running the program at various `n` (which would be the baseline). Is there any existing work on this?

### How accurate?

But what about the compiler?! Different optimisations are possible depending on data type, size, ...?

Worst case versus average case versus ?

Extra compute could be spent to find tight(er) bounds!? Sounding like we would need an automated proof assistant?


## Use case?

If we have, say, 10 hyperparameters, we might care about how our algorithms scales each of them and with each other?!

Question. Does the complexity of one hyperparameters tells us something about others!?

Can we come up with some sort of chain rule here?

$$
m = f(n) \\
z = g(m) \\
z = g \cdot f (n) = h(n) \\
bound(f, cplx.memory) = O(log(n)) \\
bound(g, cplx.memory) = O(m^2) \\
B(g) \cdot B(f) = O(log(n)^2) \\
$$


Doesnt actually need to run the algorithm, only construct the computation graph and then !?!?


## Other questions

* What about accuracy bounds?
* What about sample complexity?
* ?
