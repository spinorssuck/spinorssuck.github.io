---
layout: post
title: Legendre Polynomials, Irrationality
date: 2018-08-05
description: 
tags: analysis algebra irrational
categories: math
giscus_comments: false
related_posts: false
featured: false
toc:
    sidebar: left
---

## Introduction

The Legendre polynomials are a set of polynomial solutions to the Legendre's Differential equation:

 $$ (1-x^{2})y^{''}-2xy^{'}+n(n+1)y=0  $$

The edifice of most irrationality arguments use the fact the repeated integration by parts can be used on generating functions involving the polynomial.Another useful property is that these polynomials have integer coefficients.

Now,I'll present a few important examples which display this property.

## Irrationality of e^s

One simple but exemplary application of this property is the irrationality of  $$ e^{s} $$ for all  $$ s \in \mathbb{Q} $$.

Here,we use the Legendre polynomial given by:

 $$ P_{n}(x)=\frac{1}{n!} \frac{d^{n}}{dx^{n}} x^{n}(1-x)^{n}  $$ defined on  $$ [0,1] $$.

Now,consider the following integral,

 $$ I_{n}= \int\limits_{0}^{1} P_{n}(x)e^{sx} dx =\frac{1}{n!} \int\limits_{0}^{1} \frac{d}{dx} (\frac{d^{n-1}}{dx^{n-1}} x^{n}(1-x)^{n} )e^{sx} dx  $$ (1)


 $$ \Rightarrow n!I_{n}=[\frac{d^{n-1}}{dx^{n-1}} e^{sx}]_{0}^{1}-\frac{1}{s}\int\limits_{0}^{1} \frac{d^{n-1}}{dx^{n-1}} e^{sx} dx  $$

Using the Leibniz product rule,

 $$ n! I_{n}=[e^{sx} \sum\limits_{k=0}^{n-1}  {(n-1) \choose k} \frac{d^{k}}{dx^{k}}x^{n} \frac{d^{n-1-k}}{dx^{n-1-k}}  (1-x)^{n}]_{0}^{1} - \int\limits_{0}^{1} \frac{d^{n-1}}{dx^{n-1}} \frac{d}{dx}(e^{sx}) dx  $$

Notice that the sum vanishes as it involves  $$ x,(1-x) $$

 $$ n!I_{n}=- \int\limits_{0}^ {1} \frac{d^{n-1}}{dx^{n-1}}  \frac{d}{dx}(e^{sx}) dx  $$

Each successive integration by parts under the interval  $$ [0,1] $$ will have the same effect.So,performing  $$ n-1 $$-fold partial integration.

 $$ n!I_{n}=(-1)^{n} \int\limits_{0}^{1} x^{n}(1-x)^{n} \frac{d^{n}}{dx^{n}} e^{sx} dx  $$

 $$\Rightarrow I_{n}=(-1)^{n} \frac{s^{n}}{n!} \int\limits_{0}^{1} x^{n}(1-x)^{n} e^{sx} dx  $$

For all  $$ x $$ such that  $$ 0 \leq x <1,e^{sx}<e^{x} $$.Also  $$ t(t-1)=t-t^{2} $$ has a global maximum at  $$ t=\frac{1}{2} $$.

 $$ \frac{1}{2}-(\frac{1}{2})^{2}=\frac{1}{4}  $$

Therefore, $$ |I_{n}|<\frac{s^{n}}{n!} \int\limits_{0}^{1} (\frac{1}{4})^{n} e^{s} dx

=(\frac{s}{4})^{n} \frac{e^{s}}{n!}  $$ (2)

From equation 1,we see that  $$I_{n} $$ has terms of the type

 $$ \int\limits_{0}^{1} e^{sx} x^{m} dx $$ for  $$ m \leq n $$.

Now,making the substitution  $$ u=sx $$ and using  $$ du=sdx $$,

 $$ \int\limits_{0}^{1} e^{sx} x^{m} dx=\frac{1}{s^{m+1}} \int\limits_{0}^{s} e^{u} x^{m} du  $$

Using  $$m-fold $$ partial integration,we can see that  $$ \int\limits_{0}^{s} e^{u} x^{m} du =A+Be^{s} $$ where  $$ A,B \in \mathbb{Z} $$

Thus, $$ I_{n} $$ can be expanded as follows:

 $$ I_{n}=\sum\limits_{k=0}{n} \frac{1}{s^{k+1}}(A_{k}+B_{k}e^{s})  $$ for some  $$ A_{k},B_{k}e^{s} \in \mathbb{Z} $$

 $$ I_{n}=\frac{1}{s^{n+1}}(A_{n}+B_{n}e^{s}) $$ for some  $$ A_{n},B_{n} \in \mathbb{Z} $$.

Assume that  $$e^{s} $$ is rational. $$ e^{s}=\frac{p}{q} $$.

 $$ |I_{n}| > \frac{1}{s^{n+1}q} $$.

From inequality 2,

 $$ (\frac{s}{4})^{n} \frac{e^{s}}{n!} > \frac{1}{s^{n+1}q} $$.It's easy to see that for some large  $$ n $$,the inequality will flip.So,this is a contradiction. $$ e^{s} $$ is irrational

A similar approach can be taken to prove the irrationality of  $$ \pi^{2} $$ using the integral  $$ I_{n}=\int\limits_{0}^{1} sin(\pi x) P_{2n}(x) dx  $$

## Irrationality Exponent

For any real number  $$ x $$ ,consider the set of real numbers  $$S=latex \mu  $$ such that

 $$ \left| x-\frac{p}{q} \right| < \frac{1}{q^{\mu}} $$,then  $$ \mu(x)=inf(S) $$ is the irrationality exponent of  $$ x $$.

It is a measure of how well an irrational number can be approximated by a rational.

Legendre-type polynomials were used by M. Hata,J. Reine Angrew,Alladi,ML Robinson to obtain irrationality exponents for a wide variety of numbers including  $$ \frac{\pi}{\sqrt{3}},ln(2),ln(1+\frac{p}{q}) $$.

M.Hata ingeniously used the Legendre-type polynomial  $$ P_{n,m,\delta}(x)=\frac{x^{\delta}}{n!} \frac{d^{n}}{dx^{n}} x^{n+\delta} (1-x)^{n+m}  $$ for  $$ \delta \in \mathbb{Q} \cap (0,1)  $$ to establish an irrationality exponent for the hypergeometric function  $$ _{2}F_{1}(1;1-\delta;2-\delta)(x)=(1-\delta) \sum\limits_{n=1}^{\infty} \frac{x^{n-1}}{n-\delta} $$.

Through these polynomials,he also established irrationality exponents for  $$ \frac{\pi}{\sqrt{3}}+ln(3),\frac{\pi}{\sqrt{3}}+\sqrt{3}ln(2+\sqrt{3})  $$.