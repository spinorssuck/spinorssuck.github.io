---
layout: post
title: Irrationality of basic trigonometric and hyperbolic functions at rational values
date: 2020-03-28
description: 
tags: analysis algebra irrational
categories: math
giscus_comments: false
related_posts: false
featured: true
toc:
    sidebar: left
---

## Introduction

A few days ago, while rummaging through my shelves, I stumbled upon a book by the number theorist Ivan Niven entitled "Irrational Numbers"-a relatively unknown book in my opinion. Obscured by stationery and other paraphernalia, the edge of the book peeked out of my drawer-its cover shrouded in dust and its title almost indiscernible if not for the striking glow of morning sunlight from my large window revealing its dark red tint. I wiped off the dust and peeked into its contents.

This was one of the first 'real' math textbooks that I ever read in high school along with Apostol's books on Calculus and Lang's Linear Algebra. I distinctly remember reading it for the first time when I was 13. It was undoubtedly quite difficult at the time, considering that I had little exposure to proof-based mathematics. Though the book is rather drab in its exposition, it undoubtedly had some interesting and simple mathematical facts about irrationality which you wouldn't naturally find anywhere else except for some old number theory papers.

One of those little mathematical gems is the irrationality of trigonometric and hyperbolic functions at rational arguments. I shall soon prove that  $$ cos(x) $$ is irrational if  $$ x \in \mathbb{Q} \backslash \{ 0 \}  $$.

## Lemma 1

If  $$ h \in \mathbb{Z}[x] $$ and  $$ f(x)=\frac{x^{n}h(x)}{n!} $$ is a polynomial in  $$ \mathbb{Q}[x] $$, then  $$ f^{(k)}(0) \in \mathbb{Z} $$ for $$ k \in \mathbb{Z^{+}}  $$ and  $$ f^{(k)}(0) $$ is divisible by  $$ n+1 $$ if  $$ k \neq n $$. However, it is divisible by  $$ n+1 $$ at  $$ k=n $$ if  $$ h(0)=0 $$.




I'll leave the proof to the reader since its quite simple and involves nothing more than playing around with the polynomials.

## Lemma 2

Let  $$ f \in \mathbb{R}[x] $$ and define  $$ F(x) $$ as such:
 $$ F(x)=f((r-x)^{2}) $$ where  $$ r \in \mathbb{R} $$
Then,  $$ f^{(k)}(r)=0 $$ if  $$ k $$ is an odd integer.

Again, I'll leave the trivialities of calculations and polynomial manipulations to the reader.

Now, to the main theorem.

## Theorem

 $$ sin(x),cos(x),tan(x) $$ are all irrational for non-trivial rational values of  $$ x $$.

### PROOF:

Let  $$ q=\frac{a}{b} $$ where  $$ a,b \in \mathbb{Q} $$. Define a function  $$ f(x) $$ as follows:

 $$ f(x)=\frac{x^{p-1}(a-bx)^{2p}(2a-bx)^{p-1}}{(p-1)!} $$

where  $$ p $$ is an odd prime.
Substituting the expression for  $$ q $$,

 $$ f(x)=\frac{(r-x)^{2p}(r^{2}-(r-x)^{2})^{p-1}b^{3p-1}}{(p-1)!} $$                              (1)

Notice how we obtained a polynomial in  $$ (r-x)^{2} $$ and of the form presented in Lemma 1. Also, observe that  $$ f(x)>0 $$ for all values of  $$ x \in \mathbb{R} $$( $$ p-1 $$ is even) .

The next is to obtain an upper bound for  $$ f(x) $$ when  $$ x \in (0,r) $$.

 $$ 0 < f(x) < \frac{r^{2p}r^{2(p-1)}b^{3p-1}}{(p-1)!}=\frac{r^{4p-2}b^{3p-1}}{(p-1)!} $$  (I1)

Define another function  $$ F(x):=f(x)+\sum\limits_{n=1}^{2p-1} (-1)^{n} f^{(2p)}(x) $$

Observe that  $$ F'(x) $$ is a polynomial which is an alternating sum of odd-order derivatives of the polynomial  $$ f(x) $$. Since  $$ f(x) $$ is clearly a polynomial in  $$ (r-x)^{2} $$, by Lemma 2,  $$ F'(r)=0 $$.

Equation (1) shows that  $$ f(x) $$ is of the form of polynomial presented in Lemma 1. Hence,  $$ f^{(k)} $$ is an integer for all values of  $$ k \in \mathbb{Z}^{+} $$. Now, it remains to calculate the value of the  $$ p-1 $$th derivative at  $$ x=0 $$.

Clearly  $$ f(x) $$ is of the form  $$ f(x)=\frac{x^{p-1}h(x)}{(p-1)!} $$ where  $$ h(x) \in \mathbb{Z}[x] $$ and  $$ deg(h(x))>p-1 $$ which means that  $$ h^{(i)}(x) $$ doesn't vanish for  $$ 1 \leq i \leq p-1 $$. The constant term in  $$ h(x) $$ is  $$ a^{2p}(2a)^{p-1} $$.

With these facts in mind, simple calculations(which I'll again omit for the sake of brevity) show that  $$ f^{(p-1)}(0)=\textit{constant term of h(x)}=2^{p-1}a^{3p-1} $$.      (2)

Now we fix the odd prime  $$ p $$ so that  $$ p>a $$. It quickly follows that  $$ f^{(p-1)}(0) $$ is nor divisible by  $$ p $$.

Also, by Lemma 1,  $$ f^{(k)}(0) $$ is a multiple of  $$ p-1+1=p $$ for all  $$ k $$.

It is quite clear that  $$ F(0) \in \mathbb{Z} $$. Observe that when evaluating  $$ F(0) $$, all terms are divisible by  $$ p $$(as established above) except for  $$ f^{(p-1)}(0) $$ which we've proven is not divisible by  $$ p $$.

So,  $$ F(0) $$ is an integer which is not divisible by  $$ p $$.

Now, we study the polynomial  $$ f(r-x) $$.

 $$ f(r-x)=\frac{x^{2p}(r^{2}-x^{2})^{p-1}b^{3p-1}}{(p-1)!} $$

 $$ f(r-x)=\frac{x^{p-1}(x^{p+1}(r^{2}-x^{2})^{p-1}b^{3p-1})}{(p-1)!} $$

Again  $$ f(r-x) $$ is of the form of the polynomial presented in Lemma 1, hence  $$ f^{(k)}(r-0)=f^{(k)}(r) $$ is divisible by  $$ p $$ for every  $$ k $$(note that we don't have to deal with the exception in Lemma since  $$ x $$ is a factor of the integer polynomial so when evaluated at  $$ x=0 $$, it is zero.  $$ h(x)=x^{p+1}(r^{2}-x^{2})^{p-1}b^{3p-1} $$.

This implies that  $$ F(r)=pm $$ for some  $$ m\in \mathbb{Z} $$.          (3)

With all this in mind, let's find this derivative:

 $$ \frac{d}{dx} \{F'(x)sin(x)-F(x)cos(x) \}=F^{2}(x)sin(x)+F'(x)cos(x)-F'(x)cos(x)+F(x)sin(x)=F^{2}(x)sin(x)+F(x)sin(x)=f(x)sin(x) $$(see the equation for  $$ F(x) $$ above).

This may not seem so intuitive but it is one of Niven's original techniques to establish irrationality. What follows is taking the integral of the function above within some interval so as to obtain an in integer and making some chosen value arbitrarily small to obtain a contradiction. Again, if this seems like a frivolously hazy argument, it's best to see Ivan Niven's proof for the irrationality of  $$ \pi $$ and other papers where he uses the same techniques to obtain a clearer idea of the clever choices of polynomials and integrals involved(click here for Niven's proof for the irrationality of  $$ \pi $$).

 $$ \int\limits_{0}^{r} f(x)sin(x) dx=F'(r)sin(r)-F(r)cos(r)+F(0)=-F(r)cos(r)+F(0) $$  (since  $$ F'(r)=0 $$).                          (4)

First, we prove the irrationality of  $$ cos(x) $$ for rational arguments. Assume that  $$ cos(r)=\frac{d}{k} $$ for integers  $$ d,k>0 $$.

Using equation (3) and the fact that  $$ F(0) $$ is an integer,say  $$ q $$, that is not divisible by  $$ p $$(which we already proved),

 $$ \Rightarrow k \int\limits_{0}^{r} f(x)sin(x) dx=-pmd+kq $$

Now, we impose another condition on  $$ p $$. We already selected  $$ p $$ to be greater than  $$ a $$. Now, select it to also be greater than  $$ k $$. This means that  $$ p $$ doesn't divide  $$ kq $$ which implies that the right-hand side  $$ -pmd+kq $$ is a non-zero integer.                                        (5)

Now, we use the inequality established above(see I1) on  $$ f(x) $$ and the fact that  $$ |sin(x)| \leq 1 $$ to obtain:

 $$ |k \int\limits_{0}^{r} f(x)sin(x) dx|<kr \frac{r^{4p-2}b^{3p-1}}{(p-1)!} $$

Now as  $$ p $$ extends to infinity(there are infinite choices for  $$ p $$ which satisfy its constraints), the upper bound for the above expression tends to zero. Choose  $$ p $$ sufficiently large so that  $$ |k \int\limits_{0}^{r} f(x)sin(x) dx|<1 $$.

But from  $$ (5) $$, it's quite clear that such a choice would bring about a contradiction. Hence,  $$ cos(x) $$ is irrational for non-trivial rational values of  $$ x $$.

The next goal is to prove the irrationality of  $$ sin(x),tan(x) $$.

Assume that  $$ sin(r) $$ for some non-trivial rational number  $$ r $$.

Since,  $$ cos(2r)=1-2sin^{2}(r) $$, this implies that  $$ cos(2r) $$ is also rational which is a contradiction.

Again, if  $$ tan(r) $$ were rational, then

 $$ cos(2r)=\frac{1-tan^{2}(r)}{1+tan^{2}(r)} $$ would also be rational which is a contradiction. In fact, if you noticed above, we also indirectly established the irrationality of  $$ sin^{2}(r) $$. Using  $$ cos(2r)=2cos^{2}(r)-1 $$ would prove the irrationality of  $$ cos^{2}(r) $$.

## Corollary

The inverse trigonometric functions  $$ arccos(x),arcsin(x),arctan(x) $$ are all irrational for non-trivial rational arguments

### PROOF:

Assume that  $$ arcsin(r)=k $$ where  $$ r \in \mathbb{Q} \backslash \{0\} $$ and  $$ k\in Q $$. This implies that  $$ sin(k)=r $$ which is a contradiction. This method can be used for the other functions too.

## Theorem

The hyperbolic functions  $$ sinh(x),cosh(x),tanh(r) $$ are irrational for non-trivial rational values of  $$ x $$.

### SKETCH OF THE PROOF:

Define  $$ f(x) $$ the same way as in the previous proof except the condition of  $$ p $$ being an odd prime can be relaxed to  $$ p $$ being a positive integer. Now, assume that  $$ cosh(r)=\frac{a}{b} $$ where  $$ a,b \in \mathbb{Z} $$,define  $$ F(x) $$ as follows:

 $$ F(x):=f(x)+\sum\limits_{n=1}^{2p-1} f^{(2p)}(x) $$

In this case, consider the following integral

 $$ \int\limits_{0}^{r} f(x) sinh(x) dx=F(r)cosh(r)-F'(r)sinh(r)-F(0) $$ and proceed with the proof in a parallel manner to obtain the results.

In another post(click here), I already proved the irrationality of  $$ sin(r) $$ using Legendre polynomials. Along with that, I also proved the irrationality of  $$ e^{r} $$ for rational values of  $$ r $$. You can use Ivan Niven's techniques to prove the same the same but it's considerably messier(check his book "Irrational Numbers" for the proof;I can't find it anywhere else).

However if you established the above result, it is easy to see that if  $$ e^{r} $$ is rational then  $$ e^{-r} $$ is rational so,  $$ cosh(r)=\frac{e^{r}+e^{-r}}{2} $$ is rational which is a contradiction.

Using these same techniques, he also proved that  $$ e $$ is transcendental i.e there exists no polynomial  $$ p \in \mathbb{Z}[x] $$ such that  $$ p(e)=0 $$. In this case, I prefer Niven's proof to the other proofs that exist notably Hilbert's and Lindemann's proofs.

While my posts usually revolve(and will continue to revolve) around either algebraic topology, algebraic geometry or abstract algebra, I will occasionally post about number theory. In fact, I had planning for a while to discuss Mahler's classification of transcendental numbers and his revolutionary techniques to establish the transcendentality of numbers using the so-called Mahler functions.