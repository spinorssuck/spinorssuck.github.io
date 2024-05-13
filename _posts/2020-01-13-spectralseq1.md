---
layout: post
title: A Road to the Grothendieck Spectral Sequence:Derived Functors I
date: 2020-01-13
description: 
tags: algebra algebraic-geometry category-theory
categories: math
giscus_comments: false
related_posts: true
featured: true
toc:
    sidebar: left
---

## Introduction

This is a series of posts which will develop the required material to present the Grothendieck spectral sequence, a few applications of it in algebraic geometry(Lerray sequence, sheaf cohomology etc.) and some other categorical nonsense. This post is meant to be a light glimpse into derived functors and not a full introduction.


I've wanted to post this for a few months but unfortunately I overestimated how much free time I would have in my first semester of college(hurrah!). At one point, I totally forgot that I even maintain a blog! That's why I haven't posted for about 5 months. The title of my blog is now officially fraudulent. There were many new things(both math-related and otherwise) at UT Austin that I wanted to explore in my first semester so I could be forgiven for putting aside my blog. I think I've realized that it is really just a matter of consistency. If I do something regularly, I'll stick to the routine. So maybe, the title of the blog is more aspirational than it is real.

Anyways, enough of the nonsense. Though the Grothendieck spectral sequeuce encodes a lot of data(like all other spectral sequences),it is actually surprisingly simple to motivate and feels almost 'natural' to construct. But I suppose that is really indicative of the Grothendieck's spectacular reformulation of homological algebra that has seeped into modern textbooks that makes it feel so 'natural'. It is truly a beautiful sight to witness how derived functors lead to this elegant construction.So first, let's set up the machinery.

An object  $$ I $$ in a category  $$ C $$ is said to be an injective object if for every morphism  $$ f:X \to I $$ and every monomorphism  $$ i:X \to Y $$, there exists a morphism  $$ h:Y \to I $$ extending the map  $$ f $$ such that the diagram commutes.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/spectralsequence1/1.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

In the abelian category setting, the importance lies in the fact that  $$ I $$ is an inejctive object if and only if the Hom functor is  $$ Hom_{C}(--,I) $$ is exact. If an injective object is at the beginning of a short exact sequence in  $$ C $$, the sequence splits.

A category  $$ C $$ has enough injectives if for every every object  $$ X \in C $$, there exists a monomorphism  $$ X \hookrightarrow I $$ for some injective object  $$ I $$.

An injective reslution of an object  $$X \in C $$, an abelian category is a resolution

 $$ 0 \to X \to I_{0} \to I_{1} \to \cdots  $$ where  $$ I_{k} $$ are injective objects. In particular, this is a quasi isomorphism of chain complexes in  $$ C $$ given by  $$ X \to I_{\bullet} $$ where  $$ X $$ is the complex  $$ 0 \to X \to 0 \cdots  $$.

## Derived Functors

Let's say  $$ A $$ is an abelian category. Consider a short exact sequence in  $$ A $$:

 $$ 0 \to L \to M \to N \to 0 $$

An exact functor is a functor between abelian categories which preserves such sequences. Taking the direct sum, for example, preserves preserves a short exact sequence. Accordingly, we say that functors are left and right exact if they preserve the left and right parts of the short exact sequence. It is a well known that in the case of the category of modules over a ring  $$ R $$,the covariant Hom functor is left exact.  $$ 0 \to L \to M \to N \to 0 $$, then

 $$ 0 \to 0 \to Hom(A,L) \to Hom(A,M) \to Hom(A,N) $$ where  $$ F_{A}(X)=Hom(A,X):A \to Ab $$ is the Hom functor.

The tensor product functor  $$ G(X)=X \otimes_{R} M $$ where  $$ M $$ is an  $$ R-module $$ is known to be right exact. Many of these facts and their proofs can be found in many standard texts on commutative algebra or homological algebra. Some of the arguments in these proofs tend to be quite arduous to work through. An easier way to prove it is to notice that the functors are adjoint and show the equivalent statement that Hom preserves limits which is not too difficult. Taking the dual, yields the statement for tensoring and infact, it yields the completely general version which states that left adjoint functors preserve finite colimits using the Yoneda Lemma. See my other post on adjoint functors if you wish to learn more.

The point of derived functors(which I'll shortly introduce) is to take these 'incomplete' exact sequences where we've 'lost data' to try and construct a long exact sequence. Remember that chain complex

 $$ \cdots \xrightarrow{} C{n+1} \xrightarrow{\partial} C_{n} \xrightarrow{\partial} $$

equipped with 'boundary maps(which I've not labelled) allows us to compute homology  $$ H_{n}=\frac{ker\partial}{Im\partial} $$ which measures how far the sequence is from being exact. ALL the data is in the chain complex itself and the entire process of computing homology/cohomology is just a formalization which turns out to be quite handy. In the same manner, one should treat derived functors as a comfortable formalization using the data we possess. For an object  $$ X \in A $$, we know just one thing:that there is an injective resolution:

 $$ 0 \to X \to I_{0} \to I_{1} \to \cdots  $$.

Now, we take our left exact functor  $$ F $$(contravariant  $$ Hom $$ for example) and apply it to the injective resolution to get  $$ F(X \to I_{\bullet}) $$

 $$ 0 \to F(X) \to F(I_{0}) \to F(I_{1}) \to \cdots  $$

Now, just 'take homology/cohomology' and call it the right derived functor

 $$ R^{i}F(X)=H^{i}(F(X \to I_{\bullet})) $$. But wait, did you notice something?On the left hand side, I don't refer to the injective resolution. That is the essence of the construction, it is independent of the injective resolution of  $$ X $$ upto canonical isomorphism. A proof of this can be found in any standard textbook on algebra in the homological algebra section(Aluffi, Dummit and Foote;I think Hatcher also proves it for the dual case in the section on cohomology). Let's take a closer look at this sequence. Since  $$ F $$ is left exact, we get the following exact sequence:

 $$ 0 \to F(A) \to F(I_{0}) \to F(I_{1}) $$

W get  $$ R^{0}(F(X))=F(X) $$. If we  $$ F $$ is exact, then the all  $$ R^{i}(F(X))=0 $$ would be trivial for  $$ i>0 $$! I guess you could think of this as a way to encode approximation just like in homology/cohomology.

The converse isn't necessarily true. An object  $$ X \in A $$ is said to be  $$\bf{F-acyclic} $$ for a left exact functor if  $$ R^{i}(F(X))=0 $$ for  $$ i > 0 $$.

The final step of this formalization is ensuring that we have the long exact sequence

## Lemma 1:

If  $$ 0 \to L \to M \to N \to 0 $$ is a short exact sequence in an abelian category  $$ A $$ with enough injectives and  $$ F $$ is a left exact functor, there is an LES

 $$ 0 \to L \to M \to N \to \\
\to R^{1}(F(L)) \to R^{1}(F(M)) \to R^{1}(F(N)) \to \cdots  $$

The proof will be deferred to the next post with discussions on its dual, other theorems and special cases such as Ext, Tor.








