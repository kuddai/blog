---
layout: post
title: Automatic computational complexity
---

Can we automatically calculate/estimate/approximate the complexity of various algorithms?

Trivially, yes. We can just time the algorithm, we can track the amount of memory used, ...

But, that requires input from humans.
Also, it is not efficient.  

## Desiderdata

* Accurate:
  * Want the lowest upper bound. That might take some work to find!?
* Understandable:
  Want the bound to be expressed in an 'intuitive' way.
* Efficient:
  * must be more efficient than just running the program at various `n` (which would be the baseline). Is there any existing work on this?
  * must have low overhead so it can passively exist in the background
* General:
  * works on arbitrary programs
* ?

```python
import bound
from bound import complexity_measures as cplx

def sort_list(length):
  unsorted_list = random_list(length)
  sorted_list = []

  with bound.scope():
    for _ in range(length):
      x = min(unsorted_list)
      sorted_list.append(x)
      unsorted_list.remove(x)

    return sorted_list

>>> b = bound.upper(sort_list, measure=cplx.memory)
>>> print(b)
"O(n)"

>>> b = bound.upper(sort_list, measure=cplx.time)
>>> print(b)
"O(n**2)"
```

## Computational complexity

What is it complexity theorists do?
Some examples, calculated via proof, and empirically backed up.


## Implementation

I imagine it would work similar to how automatic differentiation works. Define a set of basis operations, where each one has its complexity defined (memory, time, parallel, energy, latency, ...). As these basis ops are composed we can propagate these complexities via a chain rule.

#### Efficient reverse-AD

AD is efficient because ? (is it? only reverse is - memory - efficient)
Reverse AD is efficient because ?

#### Efficient reverse-AB (automatic bounding)

Question. Does the complexity of one hyperparameters tells us something about others!?


Can we come up with some sort of chain rule here?
The theorem we are after is something like

__Conjecture__: Resource chain rule

$$
\begin{align}
if \quad z &= g \circ f \\
\mathcal B_{mem}(g) \circ \mathcal B_{mem}(f) &= \mathcal B_{mem}(g \circ f) \tag{!!!} \\
\end{align}
$$

Examples

$$
\begin{align}
f(n) &= m \\
g(m) &= z \\
h(n) &= g \circ f \;\;(n) \tag{chained functions} \\
\\
\mathcal B_{mem}(f) &= O(log(n)) \tag{CC of f}\\
\mathcal B_{mem}(g) &= O(m^2) \tag{CC of g}\\
&= O(log(n)^2) \\
\end{align}
$$
***
$$
\begin{align}
m_1 &= f_1(n_1) \\
m_2 &= f_2(n_2) \\
z &= g(m_1 + m_2) \\
\mathcal B_{mem}(f_1) &= O(log(n_1)) \\
\mathcal B_{mem}(f_2) &= O(1) \\
\mathcal B_{mem}(g) &= O(m^2) \\
\\
\mathcal B_{mem}(g \circ f_1) &= \\
&= O(log(n)^2) \\
\mathcal B_{mem}(g \circ f_2) &= O(1) \\
\end{align}
$$
$g \circ f_1$ doesnt work here!? it is more like $\mathcal B_{mem}(z \leftarrow n_1), z = g(m_1, m_2)$ the complexity of $z$ w.r.t $n_1$.

## How accurate?

But what about the compiler?! Different optimisations are possible depending on data type, size, ...? So the complexity changes based on how various hardware is targeted etc...

Worst case versus expected case versus best case versus !? case.

Extra compute could be spent to find tight(er) bounds!? Sounding like we would need an automated proof assistant?

## Use case?

If we have, say, 10 hyperparameters, we might care about how our algorithms scales each of them and with each other?!

Doesnt actually need to run the algorithm, only construct the computation graph and then !?!?

## Minimal proof of concept

Lets make some ops with their complexity defined and compose them together.

```python
class Operation(object):
  def __call__(self, *args, **kwargs):
    raise NotImplementedError

  @static_method
  def memory_complexity(self):
    """
    Do I want this to return a general fn for the complexity,
    or to simply return the value of this ops complexity!?
    """
    raise NotImplementedError

class Square(Operation):
  def __call__(self, x):
    self.x = x
    return np.pow(x, 2)

  @static_method
    def memory_complexity(self):
      return lambda n:
```

## Future work

* Use this to fill out Scott Aaronson's zoo of algols.
* What about using this to help you make tradeoffs? Needs access to alternatives?!?
* What about sample, accuracy, energy, parallel, latency, reversible, ... complexity?
