---
layout: post
title: A Note on Quantum Approximate Counting and Random Musings
date: 2020-07-17
description: 
tags: quantum-computing quantum
categories: math
giscus_comments: false
related_posts: false
featured: true
toc:
    sidebar: left
---

## Introduction

Ok, today we'll tackle something that I've never talked about in my blog before:Quantum computing.There might be a few more quantum computing posts in the future if I am in the mood for it.

The problem at hand is simple: There is an unordered list of  $$ N $$ items of which  $$ K $$ are marked;Approximate the value of  $$ K $$. Throughout, we'll represent the  $$ N $$ items by  $$ [N] $$ and the  $$ K items $$ by  $$ [K] $$. 

This is actually a rather old problem which has been tackled before, and is deeply connected to amplitude estimation(see [1]) which uses uses the Quantum Fourier transform. Recently though, a simpler proof which uses only Grover-like techniques was published by Scott Aaronson, a professor at UT Austin(Hook em' Horns!). Note that the algorithm is probabilistic with no bounds. 

The heart of the technique is Grover's algorithm so perhaps I should spend a few words on that. Consider an unordered list of size  $$ N $$ where you want to find a particular element which can be checked to be a solution in constant time, then this can be found in  $$ O(\sqrt{N}) $$.

In the classical case, one is forced to do this(both the above problem and QAC) in  $$ O(n) $$ time. The full strength of Grover's algorithm is that one can actually find the pre-image  $$ f^{-1}(b) $$ for  $$ f:[N] \to \{0,1\} $$ where  $$ f $$ maps  $$ x $$ to  $$ 1 $$ if and only if  $$ x $$ is a solution to the given problem. This is all encoded as a quantum black-box unitary operator  $$ U $$ defined by  $$ U\vert x \rangle =\vert x \rangle $$ if  $$ f(x)=0 $$ and  $$ U\vert x \rangle=-\vert x \rangle $$ if  $$ f(x)=1 $$.

The idea of the algorithm is that we spit out the the superposition of all states:

 $$ \vert s \rangle =\frac{1}{\sqrt{N}} \sum\limits_{i=1}^{N} \vert x \rangle $$

followed by applying the operator  $$ U $$ above which selects the marked item by flipping it.

and then apply the diffusion operator :

 $$ D=2 \vert s \rangle \langle s \vert-I $$. This, in effect, flips the marked qubit around the mean, selectively increasing its relative amplitude.

Explicitly, the mapping of the diffusion gate is:

 $$ \sum\limits_{x \in \{0,1\}^{n}}\alpha_{x}\vert x \rangle  \mapsto \sum\limits_{x \in \{0,1\}^{n}}(2\mu-\alpha_{x}) $$ where  $$ \mu $$ is the mean of the  $$ \vert x \rangle $$.

One repeats this a certain number of times(specifically  $$ O(\sqrt{N}) $$ and then measures, obtaining the corresponding eigenvalue with high probability.

## A Random Aside?

In the case of a non-local hidden-variable quantum computer, one can actually do this in atmost  $$ O(\sqrt[3]{N}) $$ time. I'm not really going to talk about this. However, this spawned a simple question:What if you could perform it in  $$ O(log(N)) $$ time? What would that actually imply?

Consider the SAT problem: There are variables  $$ x_{1},\cdots,x_{n} $$ and expressions in these variables  $$l_{1},\cdots,l_{k} $$. Find an assignment of either true/false to each  $$ x_{i} $$ such that all the expressions  $$ l_{p} $$ evaluate to true.,i.e  $$ l_{1} \land l_{2} \land \cdots \land l_{k} $$ is true.

Anyways, we can store all  $$ O(2^{n}) $$ possibilities and search through them in  $$ O(log(2^{n}))=O(n) $$ time in our hypothetical case, which is linear. This would mean that confirmed NP decision problems like  $$ SAT $$, Hamiltonian path problem can be solved in polynomial time which implies  $$ P=NP $$. So, it is unlikely that this is the case. 

I'll get back to the these things in the end of this post.

## Quantum Approximate Counting

Consider an unordered collection of size  $$ N $$ where  $$ K $$ of them is marked. Estimate the value of  $$ K $$. This is the problem at hand.

Firstly, let's clarify the exact problem statement. We wish to find an approxiamte solution, so that means we select multiplicative error  $$ \epsilon $$, i.e find  $$\tilde{K} $$ such that 

 $$ 1-\epsilon \leq \frac{\tilde{K}}{K} \leq 1+\epsilon $$

Moreover, the algorithm is supposed to be probabilistic so we also select a small probability of failure  $$\delta $$.

Let's first review some obvious solutions before getting to the actual algorithm. One must note that in the case of a quantum solution, we only care about how many query calls we make,i.e the query call complexity. The real difference in these cases is that in a quantum computer, we can measure observables and get a probability distribution of measurements, so we want to make clever choices for the observables that we measure to extract useful information, the same philosophy behind Grover's algorithm. As such, it seems reasonable that in a good solution, the query call complexity depends somehow on the value  $$ K $$ itself.

## Classical solution

To exactly find  $$ K $$, the only choice is a linear search which is  $$ O(n) $$. Actually, the approximate case(deterministic) could be done in  $$ O(\frac{1}{\epsilon^{2}}\frac{N}{K}) $$.

## 'Easy' quantum solution

Use Grover's algorithm where  $$ f $$ maps the input to  $$ 1 $$ if and only if it is marked, this would be  $$ O(\sqrt{N}) $$.

Query call complexity of the ideal solution

Perhaps, it is best if I reveal the complexity before moving on. The ideal ideal query call complexity to obtain  $$ \tilde{K} $$ which  $$ \epsilon-approximates $$  $$ K $$ with high probability of success  $$ 1-\delta $$ is  $$ O(\frac{1}{\epsilon} \sqrt{\frac{N}{K}} log(\frac{1}{\delta})) $$.

## Initial steps

Instead of approximating  $$ K $$, we equivalently approxiamte  $$ \theta = arcsin(\frac{N}{K}) $$.

There are really two steps:

First, we find a good constant-factor approximation to  $$ K $$ and then we cleverly shave off the bounds to get an  $$ \epsilon -approximation $$.

So, first we obtain some interval  $$ [\theta_{min}^{t+1},\theta_{max}^{t-1}] $$ containing  $$ \theta $$.

This is explained in part 1 of Aaronson's overview of the algorithm:

Here , $$ \phi $$ is the uniform superposition of all states and  $$ G $$ is the diffusion operator

Note that :

 $$ G^{\frac{r-1}{2}}\vert \psi \rangle=\frac{sin(r\theta)}{\sqrt{K}} \sum\limits_{x \in [K] } \vert x \rangle +\frac{cos(r\theta)}{\sqrt{K}} \sum\limits_{x \not\in [K]} \vert x \rangle $$. In the computational basis, the probability of measuring a marked item is  $$ sin^{2}(r\theta) $$. Step 1 essentially returns a constant factor approxiamtion to  $$ \theta $$ withhigh probability. This can be proven using Chernoff bounds which I'll omit from the discussion. 

It is also proven in page 5 that with high probability, one will not find enough marked items to finish step 1 before  $$ t<t_{0} $$. Also, with high probability, we'll see enough marked items in  $$ t=t_{0},t_{0}+1 $$.The interesting part is how to get an  $$ \epsilon-approximation $$.

## Final solution

Now, that we have  $$ \theta_{min},\theta_{max} $$, we use the following clever result on page 9:

Let  $$ 0<\theta_{min}\leq \theta\leq \theta_{max} \leq \frac{\pi}{1000} and  $$ \theta_{max}=\theta_{min}(1+\gamma) $$ where  $$ \gamma \leq \frac{1}{5} $$. There exists an integer  $$ r $$ such that the following is true:

Consider tossing a biased coin which is heads with probability  $$ sin^{2}(r\theta) $$ at least  $$ 1000.ln(\frac{1}{\epsilon}) $$ times. 

If more heads are observed, set  $$ \theta_{min}:=\frac{\theta_{max}}{1+0.9 \gamma} $$ else set

 $$ \theta_{max}:=\theta_{min}(1+0.9\gamma) $$.

This process fails to maintain  $$ \theta_{min} \leq \theta \leq \theta_{max} $$ with low probability  $$ \gamma $$. The value  $$ r $$ also has some non-trivial bounds.

The probability of getting heads above is exactly the probability of getting a marked item in  $$ G^{\frac{r-1}{2}}\vert \psi \rangle $$ above.

The upshot is that we can distinguish  $$ \theta_{min},\theta_{max} $$ by measurement by considering instead  $$ r\theta_{min},r\theta_{max} $$ which are nearly orthogonal. Based on our results of measurement, we shave-off either  $$ \theta_{min} $$ or  $$ \theta_{max} $$ by a factor of  $$ 0.9 $$ getting closer and closer(with high probability) to our required  $$ \epsilon- $$estimate of  $$ \theta $$.

## Philosophical musings on Energy and Algorithms

I beg the reader to ignore everything here and close this tab immediately as I have no idea what I'm saying(not that I ever do).

Recently, I came across a few interesting thins=gs:

One was an experimental method to tackle classic difficult computer science problems. One was using chemical reactions with DNA molecules to solve the Hamiltonian path problem which is NP-hard. The problem was that it requires an amount factorial in the number of vertices to work. Another solution uses an optical contraption of cables and beam splitters to get a solution. Again, the drawback is that amount of required energy is exponential in the number of vertices. There is another example of some kind of a bizarre mold which rearranges itself in a manner to give an approximate solution to the Travelling Salesman Problem. 

In fact, there is an entire field of DNA computing. The aim is to use parallel computing to optimize our solutions. The drawback is that the processing speed is slow.

Again, even for Grover's algorithm, note that we must first 'store'/obtain the entire quantum state itself unlike a classic linear-search where the auxilliry space needed is 1. Within a certain degree(spanning all these systems of computing), it seems that we can, to SOME degree, substitute time for space/energy.An obvious thing to note is that you can't decide anything about some new data if you haven't even stored it. More often than not, we are willing to make this sacrifice because we care more for efficiency.

Parallel computing speedups require increasing the number of components. Of course, there is Amdahl's law which puts some kind of a restriction to this.

Aaronson talked about this in one of his informal talks(I think an interview or TedTalk).

The study of complexity theory really may reveal things about physics, nature and energy it seems. In classical computing, there is a limit to how much we can trade space for time so we consider other unconventional types of computing where the threshold for this tradeoff is higher. This is truly an interesting direction to think in.