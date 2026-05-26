---
layout: post
title: Modeling organizations
lang: english
categories: [ blog ]
description: Justifying the use of ABM for organizational research and economics in general. 
tags: economics 
image: assets/img/orgtheory/tools.jpg
---


Herbert Simon famously wrote that if a visitor came from Mars they would call our economy an "organization economy," not a "market economy," because most economic activity happens inside firms, not between them. And inside those firms, price no longer works as a coordinating mechanism, making most economic models irrelevant.

To be fair, some organizational behavior fits neatly into existing economics, albeit, with some additional behavioral assumptions. For example, hidden-action problem works if agent wants to work less, as long as principal cannot observe it. This comes with a bunch of implicit assumptions (e.g. effort is costly, work is undesirable, agent is willing to gamble, prncipal is risk-neutral, etc.) but it is still not too far-fetched, while also being possible to model analytically. Another example is a vertical integration problem (make-or-buy decision) which can be modeled as a coordination game. This, in turn, assumes transaction costs, which are hard to operationalize, and already stretches the limits of what can be modeled analytically.

But a lot of day-to-day organizational behavior is hard to model. Take, for example, knowledge diffusion, e.g. something as simple as two individuals talking to each other and one of them sharing a piece of information that the other then uses to make decisions. Modeling this requires determining who talks to whom, what information they share, why they want to share it, how do they process received information, etc.    

<figure>
  <img src="/assets/img/orgtheory/knowledge-diffusion.png" alt="Knowledge diffusion demo">
  <figcaption>Simplest case of knowledge sharing in organizations.</figcaption>
</figure>

Again, you can technically replace networks with multipliers (similar to _SIR_ models from epidemiology) and sequential learning with Markov chains, but this forces you to think in aggregates, which is a valid, yet incomplete, approach. Brian Arthur wrote that math makes you think of economics in _"nouns"_ (and relationships between nouns given by equations) and miss out on the _"verbs"_ (i.e. processes), which are much easier modeled with algorithms (i.e. computer simulations).

Algorithms are so natural for modeling economic processes in organizations that it is almost too easy to code up in a day any scenario that you would struggle with for weeks if you were to use math. In fact, this is one of the [criticisms of _agent-based models_](https://economistwritingeveryday.com/2022/03/14/why-agent-based-modeling-never-happened-in-economics/) --- that they remove intelligence filter (that is advanced math) and allow anyone (arguably, not bright enough) to create an economic model.

Of course, this argument is nothing but gatekeeping, but I am not getting into this debate here, as it has been discussed a million times already. What I can say is that agent-based models have long grown beyond _cellular automata_ on 2D grids written in _NetLogo_ (e.g. Schelling's segregation model). Modern ABMs are large-scale, increasingly data-driven, and feature smart agents with complex decision rules (e.g. reinforcement learning, behavioral trees, etc.). Also, recently we saw a rise of models that set up a bunch of LLM agents and see them interact, trying to catch insights, although, I am skeptical about this because they have two degrees of separation from reality, i.e. data on which the LLMs were trained would be more useful to study directly.

On this note, it is worth mentioning that the micro-data revolution in economics didn't pass by organizational research. Data about edits in Google Docs, committed lines of code in GitHub, unique identifiers of online customers, etc. are all being actively studied. But there is a limit to what you can do with data without any model. Recalling the knowledge diffusion example, it is incredibly hard to identify whether an employee used a piece of information they received from a colleague or not when making a final decision, and it is even harder to get data on informal communications where information was shared, unless you go full surveillance mode, that is.

One possible way to control for all of the above is to gamify the organizational environment where different managers are shown different dashboard versions and all communication happens within organizational software. These are known as _serious games_, but this reminds me more of an old game _Football manager_, where you had your football club and you had to make decisions about training, transfers, etc. based on the information you got. In any case, this is nothing but an agent-based model with humans in the loop and less robustness.

In conclusion, a whole body of interesting research is happening at the intersection of organizational theory and operations research, using a combination of data and computer simulations. The expected democratization of economics that they are supposed to bring is still yet to be seen, because the rise of these tools coincided with the science funding cuts, but we can hope for the best.
