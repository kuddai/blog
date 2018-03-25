---
layout: post
title: Databases, arguments and models
category: main
---

Let $K$ be a <u>relational knowledgebase</u>, represented as a graph, $G(v, e)$.

Now, imagine we want to get from $a\rightarrow b$ ($a,b \in V$). We need to find a path (a series of edges in, $e \in E$) that connect $a$ and $b$.

***

Let $C$ be a set of concepts, and $R$ be a set of reasons that allow you to get from one concept to another, $r(x) = y: r\in R, x,y \in C$.

Now, imagine that we form an argument about why $b$ is true, based on the assumption of $a$. An argument is a chain of reason, $r \in R$, such that they take

***

Let $M$ be a <u>transitional model</u> that takes a state, $s_t$ to the next state given some action, $s_{t+1} = M(s_t, a_t)$.

Now imagine

### Multiple paths

What does connectedness imply?

Does having two paths ($p_1, p_2$) from $a\rightarrow b$ imply that $p_1$ is equivalent to $p_2$?
If we have two models, $m_1$ and $m_2$ that explain (a, b), which one is right?

They are equivalent w.r.t the data we have, need to collect more data, use another measure to compare them, such as the `simplicity` of each model/path.

##### Contradictions

<side>This means $a$ may not imply $b$, but isn't that what we just showed by finding a path from $a\rightarrow b$?</side>
What if we can use the database to also find a path from $\not a\rightarrow b$? How do we resolve this? Should this sort of behaviour even be allowed?

### Incomplete knowledge: Copression for efficient reasoning

What happens when the database is incomplete, or we are reuired to trade-off accuracy for reduced latency, lower computation, ...

##### Sketched nodes.

Rather than storing all $N$ nodes. Factorise them into a hierarchy of basis nodes and
Some may not be able to be `reduced` into the basis, so must be memorised, for now.

##### High-level linkages.

A path is more likely to be true if it is more specific. (aka not high level)
Specificity is measured by ???.
The length of the path?
How close the nodes visited are to being basis nodes.

##### Factored links.


##### Exploration

What about exploring new parts of the graph? May still have ???


***
All result in a type of <u>approximate reasoning</u>???

### (In)Coherence

Humans tend to have incoherent beliefs. We will reason about why X implies Y and about how Y implies Z, but disagree that X implies Z. (TODO want a beter example)

This is not possible in a relational database (assuming?). But if we consider the case of an incomplete database then the tradeoff for incoherency can buy some

This points at an unsupervised loss for compressing a database? Compress it coherently...

Paper title: Approximate reasoning with incomplete models.
