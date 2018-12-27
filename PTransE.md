# PTransE

https://arxiv.org/pdf/1506.00379.pdf

## Introduction

TransE model only using single-step relation to map knowledge graph to low dimension space. And TransE has issues when modeling 1-to-N, N-to-1, and N-to-N relations.

It is Known that there are also substantial multiple-step relation paths between entities indicating their semantic relationships.

For example, if I want know a language of a movie, In fact, the language of the film is derived from the language of the director(most of). so I can through the language of the director of movie infer the language of a movie.

 ## Model

### loss of TransE

There are relational tuple(h,r,t) in KG, where h is head entity, t is tail entity, r is relation.

$ E(h,r,t) = ||h+r-t||$ 

### loss of PTransE

$G(h,r,t)=E(h,r,t)+E(h,P,t)$

where

$E(h,P,t) = \frac{1}{Z}\sum_{p\in P(h,t)}R(p|h,t)E(h,p,t)$

where $R(p|h,t)$ indicates the reliability of the relation path $p$ given the entity pair $(h,t)$, and

$ Z=\sum_{p\in P(h,t)}R(p|h,t)$ 

is a normalization factor.

### path-constraint resource allocation (PCRA) algorithm

Set head entity as source node,  like flood flow in different path, the reliability of the path p from head h to tail t $R(p|h,t) = R_p (t)$ is how much water can be well translated.

### Relation Path Representation

####  ADD

$p = r_1 + ... + r_l$

#### MUL

$p = r_1 \cdot ... \cdot r_l$

#### RNN

$ci = f(W [c_{i-1}; ri]) $

and 

$E(h, p, t) = ||p-(t-h)|| = ||p-r|| = E(p, r) $

which is expected to be a low score when the
multiple-relation path p is consistent with the direct relation r, and high otherwise, without using
entity embeddings. 

### Optimization and Implementation Dentails

#### Reverse Relation Addition

there are BornInCity, so infer CityWhereBornIn, so add Reverse Relation to KG

#### Path Selection Limitation
We unable to make use of large amount of relations and facts about each entity pair. so, like n-gram, we only consider 2-step or 3-step paths.

## Task

### Knowledge base completion

KB completion aiming to predict the missing entities or relations in given triples only based on existing KBs.

### Relation extraction

This topic I don't care now.

