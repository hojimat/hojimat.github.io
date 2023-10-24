---
layout: post
title: Global maxima in fitness landscapes
lang: english
categ: blog
description: Simple models in complexity science. We can't even do them. 
keywords: statistical consulting, economic consulting, data analytics, econometrics
image: /assets/img/landscape/maxima.jpg
---

<figure class="text-center">
<img class="w-75" src="/assets/img/landscape/maxima.jpg"/>
</figure>

This blog post states a problem, does not provide any solutions. This is a high form of whining.

### Background

Here I present Kauffman's NK model. Let agents face a complex decision _x_, i.e. a decision that consists of _N_ interacting sub-decisions: _x = (x<sub>1</sub>,x<sub>2</sub>,...,x<sub>N</sub>)_. For simplicity, assume that decisions are binary (either _0_ or _1_). Let every sub-decision be "coupled" with _K_ other decisions, i.e. the performance _f<sub>i</sub> (x<sub>i</sub>) = f<sub>i</sub> (x<sub>i</sub>,x<sub>i<sub>1</sub></sub>, ..., x<sub>i<sub>K</sub></sub>)_. Finally, for simplicity, assume that the performances _f(.)_ are uniform random.

### Problem statement
There are two ways to model a search process --- (a) generate the reference landscape of size _(N_ x _2<sup>1+K</sup>)_ and calculate values according to it, and (b) generate performance values on-the-fly. The advantage of the former is that you can always know what the global maximum of the landscape is, and you can normalize your results accordingly. The disadvantage is that to store landsape for _N = 28_ and _K = 27_ you need 56 GB of RAM and lots of CPU time. Don't even dream of parallelizing or running 100 repetitions.

We have the simplest model you can imagine and can't even get to 30 decisions --- if you allocate 4 decisions to 7 people... ummm, well you can't do that apparently.

### Why (b) won't work
OK, so let's say we have decided to generate values on the fly and estimate the global maximum. What is wrong with that? The problem is that the higher the value of _K_, the closer is the maximum to _1_ (tail probabilities), but at the same time, the higher is the _N_, the lower is the maximum of a sum (multiple columns can't be high at the same time). The answer probably lies somewhere in the ratio _K/N_, like it was mentioned in Kauffman's 1991 avalanches paper. But I can't tell, to be honest.

### Conclusion
Life is difficult. 

**Update** I have made some sensitivities on _K/N_, here are the results:

<figure class="text-center">
<img class="w-100" src="/assets/img/landscape/globalmax.png"/>
</figure>

So, ... kinda proves my point: there is a pattern, but too risky to straight out assume. ikr: if I solved this, then I would solve _P vs. NP problem_.

A new conclusion: pick your battles!

