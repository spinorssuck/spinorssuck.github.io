---
layout: post
title: Slick Proof of Hilbert's Nullstellensatz
date: 2019-05-07
description: 
tags: algebra algebraic-geometry
categories: math
giscus_comments: false
related_posts: true
featured: false
toc:
    sidebar: left
---

## Introduction

It is a well known fact that there are multiple proofs for the Nullstellensatz which do not use Noether's normalization lemma. Serge Lang's proof(in his book) and Zariski's proof both fall under this category. In fact, Daniel Allcock of UT Austin posted a proof which essentially builds from the edifice of Zariski's proof(see that here). He claims that it is the simplest proof for the Nullstellensatz and frankly this is quite true considering the proof uses nothing more than basic field theory, is only one page long and just requires some familiarity with transcendence bases, and the transcendence degree. Yet in the true spirit of simplicity, T. Tao has presented a proof which uses nothing more than the extended Euclidean algorithm and "high school algebra" albeit with a lengthy case-by-case analysis(see the proof here).

Most of these proofs(except Tao's) go about proving the 'Weak' Nullstellensatz and obtain the 'Strong' Nullstelensatz through the famous Rabinowitsch trick.

But a few days, I found something truly magnificent, a proof by Enrique Arrondo in the American Mathematical Monthly which proves the Nullstellensatz using a weaker version of Noether normalization and techniques similar to that of Tao, Ritrabata Munshi. The proof is essentially a simplification of a proof by R. Munshi.

Here, I present a special case of the normalization lemma.

## Lemma 1

If  $$ F $$ is an infinite field and  $$ f \in F[x_{1},x_{2},\cdots ,x_{n}] $$ is a non-constant polynomial and  $$ n \geq 2 $$ whose total degree is  $$ d $$, then there exists  $$ a_{1},a_{2},\cdots ,a_{n-1} \in F $$ such that the coefficient of  $$ x_{n}^{d} $$ in

 $$ f(x_{1}+a_{1}x_{n},x_{2}+a_{2}x_{n},\cdots ,x_{n-1}+a_{n-1}x_{n},x_{n}) $$

is non-zero.

### Proof:

Let  $$ f_{d} $$ represent the homogenous component of  $$ f $$ of degree  $$ d $$.So, the coefficient of  $$ x_{d}^{n} $$ in  $$ f(x_{1}+a_{1}x_{n},x_{2}+a_{2}x_{n},\cdots,x_{n-1}+a_{n-1}x_{n},x_{n}) $$ is  $$ f_{d}(a_{1},\cdots,a_{n-1},1) $$. As a polynomial in  $$ F[x_{1},\cdots,x_{n-1}] $$, there is some point  $$ (a_{1},\cdots,a_{n-1} \in F^{n-1}) $$ where  $$ f_{d}(a_{1},\cdots,a_{n-1},1) $$ doesn't vanish. Choose such a point to establish the  $$ a_{i} $$ and this guarantees a non-zero coefficient of  $$ x_{n}^{d} $$.

With this, we're ready to tackle the 'Weak' Nullstellensatz.

## Weak Nullstellensatz

Let  $$ F $$ be an algebraically closed field and  $$ I $$ be a proper ideal of  $$ F[x_{1},\cdots ,x_{n}] $$. Then, there exists some  $$ (a_{1},\cdots ,a_{n}) \in F^{n} $$ such that  $$ f(a_{1},\cdots ,a_{n})=0 \forall f \in F $$ i.e  $$ V(I) \neq \phi $$.

### Proof of Weak Nullstellsatz:

We prove this by inducting on  $$ n $$. It is obviously true in the case  $$ n=1 $$ because  $$ F[x] $$ is a principal ideal domain and so if  $$ g $$ is the generator of the proper ideal, then since  $$ F $$ is algebraically closed, $$ g $$ has some zero and hence every polynomial in the proper ideal  $$ I $$ has a common zero.

Assume that the result holds true for the case  $$ n-1 $$. Now the 'change of co-ordiantes' depicted through the map  $$ (x_{1},\cdots,x_{n}) \mapsto (x_{1}+a_{1}x_{n},x_{2}+a_{2}x_{n},\cdots,x_{n-1}+a_{n-1}x_{n},x_{n}) $$ is a ring isomorphism from  $$ F[x_{1},\cdots,x_{n}] $$ to itself. Hence, ideals are preserved and an element in  $$ I $$ can be transformed under a change of variables to a monic polynomial  $$ g \in F[x_{1},\cdots,x_{n}] $$(This can be achieved through some scaling argument which I'll hand-wave out of this proof). So, by the induction hypothesis, there exists some  $$ (a_{1},a_{2},\cdots,a_{n-1}) $$ which is zero for every polynomial in  $$ I' $$. Fix this point  $$ (a_{1},a_{2},\cdots, a_{n-1}) $$ and the monic polynomial   $$ g $$ for the following arguments.

Let  $$ I' $$ be the polynomials of the ideal  $$ I $$ which don't contain the indetermiante  $$ x_{n} $$. It is obvious that  $$ I' $$ is a proper ideal of  $$ F[x_{1},\cdots,x_{n-1}] $$.

Now, one constructs a set  $$ J $$ as follows:

 $$ J=\{f(a_{1},a_{2},\cdots ,a_{n-1},x_{n})|f \in I \} $$. We prove that  $$ J $$ is a proper ideal of  $$ F[x_{n}] $$. It is quite clear that  $$ J $$ is an ideal. All that remains to prove is that it doesn't contain the identity.

Assume that there exists some  $$ f \in I $$ such that  $$ f(a_{1},\cdots ,a_{n-1},x_{n})=1 $$. Writing  $$ f $$ as a polynomial in  $$ F[x_{n}] $$ with coefficients in  $$ F[x_{1},\cdots ,x_{n-1}] $$.

 $$ f=f_{d}x_{n}^{d}+ \cdots+ f_{1}x_{n}+f_{0} $$ where all  $$ f_{i} \in I' $$ for  $$ 0 \leq i \leq d $$. Clearly, $$ f_{i}(a_{1},\cdots ,a_{n-1})=0 $$ when  $$ i \neq 0 $$. Hence,  $$ f_{0}(a_{1},\cdots ,a_{n-1})=1 $$.

Similarly, we can write the polynomial  $$ g \in I $$ as follows:

 $$ g=x_{n}^{e}+g_{e-1}x_{n}^{e-1}+\cdots +g_{1}x_{n}+g_{0} $$ where all  $$ g_{i} \in F[x_{1}, \cdots ,x_{n-1}] $$. Let  $$ Res(f,g) $$ be the resultant of the two polynomials i.e the determinant of their associated Sylvester matrix. Notice that  $$ Res(f,g) \in F[x_{1},\cdots ,x_{n-1}] $$.

 $$ Res_{F[x_{1},\cdots ,x_{n-1}]}(f,g)=

\begin{vmatrix}

f_{0} & f_{1} &\cdots &f_{d} & 0 & 0 & \cdots &0 \\

0 & f_{0} &\cdots & f_{d-1} & f_{d} & 0 & \cdots & 0 \\

\vdots & \vdots & \ddots & \vdots & \vdots & \vdots & \vdots & \vdots \\

0 & \cdots & 0 & f_{0} & f_{1} & \cdots & f_{d-1} & f_{d} \\

g_{0} & g_{1} & \cdots & g_{e-1} & 1 & 0 & \cdots &0\\

0 & g_{0} & \cdots & g_{e-2} & g_{e-1} & 1  & \cdots & 0\\

\vdots & \vdots & \ddots & \vdots & \vdots & \vdots & \vdots & \vdots \\

0 & \cdots & 0 & g_{0} & g_{1} & \cdots & g_{e-1} & 1 \\

\end{vmatrix}

 $$.

There are  $$ d  $$ rows of the  $$ f_{i}'s $$ and  $$ e $$ rows of the  $$ g_{i}'s $$.

I'll leave it to the reader to the verify that  $$ Res(f,g) \in I' $$( you can use the Leibinz's rule).

However, when  $$ Res(f,g) $$ is evaluated at  $$ (a_{1},\cdots ,a_{n-1}) $$, all the elements above the diagonal become zero and all the elements on the diagonal become 1(note that  $$ f_{0} $$ is 1 at this point).Hence, we obtain a lower traingular matrix whose determinant is the product of the diagonal elements which are all 1.

 $$ Res(f,g)(a_{1},\cdots ,a_{n-1})=1 $$. But  $$ Res(f,g) \in I' $$ and all elements of  $$ I' $$ have this point as a common zero. This unearths a contradiction which proves that  $$ J $$ dosn't contain  $$ 1 $$, hence it is a proper ideal of  $$ F[x_{n}] $$. Since the polynomial ring on a single variable is a principal ideal domain, there exists some generator  $$ h(x_{n}) \in J $$. Since,  $$ F $$ is algebraically closed,  $$ h(x_{n}) $$ has some zero in the field  $$ F $$, say  $$ a_{n} $$ or is itself  $$ 0 $$.

This means that  $$ f(a_{1}, \cdots ,a_{n-1},a_{n})=0 \forall f \in I $$ which completes the proof.

The strong Nullstellensatz can be derived from the 'weak' version using the well-known Rabinowitsch trick, which I'm sure many are aware of. You can find it <a href="https://en.wikipedia.org/wiki/Rabinowitsch_trick"> here </a>.


