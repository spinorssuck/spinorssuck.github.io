---
layout: post
title: Bousfield Localization of Spectra
date: 2020-05-04
description: math blog post about the bousfield localization of spectra
tags: math
categories: math
giscus_comments: true
related_posts: false
toc:
    beginning: true
---

This post is organized as a part of the UT Austin Spring 2020 DRP program.I'd like to thank my mentor Richard Wong for useful directions throughout the semester and introducing me to much of the foundational material in homotopy theory.

This post will be organized as follows:

First, I'll present the basic definitions of the topic(spectra, homotopy groups,CW-spectra,triangulated categories etc).

Second, I';ll introduce finite spectra, $$ Z_{p}$$-localization of spectra aka. p-local spectra via Bousfield localization, thick subcategories.

Third, I'll discuss the the Thick Subcategory Theorem but avoid technical details.

So, let's begin.

## Introduction,Examples

A spectrum $$ X $$ is a sequence of pointed spaces $$ \{X_{n} \} $$ and structure maps $$ \sigma_{n}: \sum X_{n} \to X_{n+1} $$. For example, one can take a pointed space $$ X $$ and consider the suspensions $$ \sum^{n} X=S^{n} \wedge X $$. This forms a spectrum with the structure maps the identity. This is the suspension spectrum of $$ X $$.

One can consider this general spectrum $$ \{X_{n} \} $$ and suspend it by the integer $$ i $$ to get a spectrum $$ \sum^{i} X $$ whose components are given by $$ (\sum^{i} X)_{n}=X_{n+i} $$.

The homotopy groups $$ \pi_{k}(X) $$ of a spectrum $$ X $$ are defined as the colimit:

$$ \pi_{k}(X)=colim_{n} \pi_{n+k}(X_{n}) $$.

Since $$ \sum $$ is a functor on $$ Top $$, one is motivated to define maps between spectra $$ f:X \to Y $$ as a a collection of maps $$ f_{n}:X_{n} \to Y_{n} $$ such that the obvious diagrams commute.This may not actually be the best definition of maps between spectra but it doesn't matter too much for now.

For example, one can consider $$ S^{0} $$ and suspend this to get $$ \mathbb{S} $$, the sphere spectrum, an example of a suspension spectrum.

Given the suspension and loop space functors $$ \sum, \Omega $$, one has the loop-space adjunction for pointed topological spaces, namely,

$$ [\sum X,Y] \simeq [X,\Omega Y] $$

Note that $$ \Omega Y=[S^{1},Y] $$(with compact-open toplogy). This allows us to define $$ \Omega-spectrum $$ as spectrum $$ X $$ where the adjoint map $$ \tilde{\sigma_{n}}:X_{n} \to \Omega X_{n+1} $$ is a weak homotopy equivalence.

Let's look at an example.

### Eilenberg-Maclane Spectra

Recall that an Eilenberg-Maclane space corresponding to $$ (G,n) $$ where $$ G $$ is an abelian group is a CW-complex $$ X $$ such that $$ \pi_{n}(X)=G $$ and $$ \pi_{k}(X)=0 $$ for $$ k \neq n $$.Call this CW-complex $$ K(G,n) $$

We know the following correspondence from algebraic topology : For any CW-complex $$ X,H^{k}(X;G) \simeq [X,K(G,n)]$$.

Collect these spaces on the index $$ n$$ to get $$ \{K(G,n) \}$$. We claim this forms a spectra. What are the structure maps though?

In particular, note that we we have $$ \pi_{k}(\Omega K(G,n+1))=\pi_{k+1}(K(G,n+1))$$. By uniqueness of the Eilemberg-McLane space upto homotopy equivalence, we have a homotopy equivalence $$ \tilde{\sigma}_{n}:K(G,n) \to \Omega K(G,n+1) $$. Take the adjoint of this under the loopspace-adjunction to get the structure maps $$ \sigma_{n}:\sum K(G,n) \to K(G,n+1) $$.

Hence, this is also an $$ \Omega- $$ spectrum. $$

### CW-Spectra

Well, I suppose some analogy with the classical case is required here. Consider the Quillen-Serre model structure on pointed topological spaces(aka the usual one). Here, the cofibrations are retracts of generalized relative CW inclusions(see [1] for definitions). In particular, the CW complexes are cofibrant objects in this case. We'd like our so called CW complexed to be cofibrant objects in the stable model category on topological sequential spectra(these are the same things as the spectra defined above where $$ \sum X =S^{1} \wedge X $$).

A CW spectra is a sequence $$ \{E_{n} \} $$ of CW-complexes where the structure maps $$ \sigma_{n}:\sum E_{n} \to E_{n+1} $$ map isomorphically into a subcomplex of $$ E_{n+1} $$. TO prove the above fact, see Prop 0.49 of this.

The cell of a CW complex is the collection $$ \{A_{n},\sigma_{n+1}(A_{n}),\sigma_{n+2}(A_{n}),\cdots, \} $$ where $$ A_{n} $$ is a cell of $$ E_{n} $$ and $$ A_{n} $$ is not of the form $$ \sigma_{i}(A_{k}) $$ for some cell $$ A_{k} \subset E_{n} $$ where $$ k<n$$. Essentially, you package a cell $$ A_{n}$$ of some component space in the spectrum and the cells in the higher components obtained from the structure maps such that the original $$ A_{n}$$ itself is not obtained in this form.

A finite spectrum is a CW-spectrum which has a finite number of cells. Another important property of $$ Top$$ extends to the case of spectra:CW-Approximation.

A subspectrum $$ B$$ of a CW spectrum $$ X$$ is closed if $$ B$$ is a union of cells and for any cell in $$ X$$ with some suspension in $$ B$$, it is in $$ B$$, that is, $$ X/B$$ is a CW spectrum. This will be important later in Bousfield localization.

We know that if $$ X$$ is a topological space, then there exists a CW-Complex $$ \Gamma X$$ and a homotopy equivalence $$ \Gamma X \simeq X$$.

This extends as follows: