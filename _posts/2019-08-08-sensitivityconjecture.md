---
layout: post
title: Monads I, The Eilenberg-Moore category, Adjunction and Kleisli categories
date: 2020-03-28
description: An introduction to Monads and the Eilenberg-Moore category
tags: math
categories: math
giscus_comments: false
related_posts: false
featured: true
toc:
    beginning: true
---

## Introduction

If you aren't aware, one month ago, the Sensitivity Conjecture, a 30-year old problem, was proven by Hao Hung, an assistant professor at Emory University in just a little more than 2 pages using particularly simple methods albeit cleverly implemented. The proof is very easy to understand and requires nothing more than basic linear algebra. You can find it here.

A few days ago, Donald Knuth simplified the already simple proof of H. Hung and could fit all his arguments in half a page. What really shocked me when I heard the news is that Knuth is still alive. I could have sworn that it was only a few days ago when I was skimming through a textbook on Discrete Mathematics and saw a bio with a black-and-white pic of him in one of the chapters related to computational complexity in the same manner that I'd see pictures and mini-biographies of other 20th century giants such as Grothendieck and Nash relegated to the margins of math textbooks and online articles romantically detailing the course of their fabled lives.

Now that I've realized that he's well and alive, it shocks me equally to learn that at the age of 81, he is still able to contribute to research.

I'm not exactly going to regurgitate Knuth's proof but what I'll present certainly uses the same ideas. I must note here than Knuth's proof itself is inspired by a comment on Scott Aronson's blog which provided a method to prove the conjecture without using Cauchy's Interlacing Theorem.

If you don't know what the Sensitivity Conjecture, I'll state it below.

If  $$ f:\{0,1\}^{n} \mapsto \{0,1 \}  $$ is a boolean function where the domain is the graph of the  $$ n-dimensional $$ cube denoted by  $$ Q^{n}=\{0,1 \}^{n} $$. So, a particular input  $$ x $$ is just a string of 0s and 1s. The local sensitivity of  $$ f $$ at an input  $$ x $$ is the number of indices in the 'string' of  $$ x $$ that you can flip and not change the output. The local block sensitivity of  $$ f $$ at input  $$ x $$ is the number of disjoint subsets of the set of indices  $$ \{0,1,2 \cdots, n \} $$ such that the output doesn't change when every index corresponding to a block flips in the input string of  $$ x $$. The sensitivity and block sensitivity are defined to be the maximum of these corresponding measures over all the inputs.

The sensitivity conjecture basically states that the block sensitivity is polynomially correlated to sensitivity.

Throughout the article, I denote block sensitivity and sensitivity by  $$ bs $$ and  $$ s $$ respectively.

## Sensitivity Conjecture

> There is a constant  $$ k>0 $$ such that  $$ bs(f) < s(f)^{k} $$

Since Gotsman and Linial proved an equivalence related to induced subgraphs of the  $$ n-dimensional $$ cube in 1992, the Sensitivity Conjecture follows as a consequence to the following problem:

### Theorem

> Any induced subgraph  $$ H $$ of  $$ Q^{n} $$ with  $$ |V(H)|=2^{n-1}+1 $$ satisfies  $$ \Delta{H} \geq \sqrt{n}  $$.

## Useful Lemmas

### Lemma 1

> Recursively define a sequence of square matrices as follows:
>  $$ A_{1}=\begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix}
> A_{n}=\begin{bmatrix} A_{n-1} & I_{2^{n-1}} \\ I_{2^{n-1}} & -A_{n-1} \end{bmatrix}  $$
> Then  $$ A_{n} $$ has eigenvalues  $$ \sqrt{n},-\sqrt{n} $$ of multiplicities  $$ 2^{n-1} $$ and  $$ 2^{n-1} $$ respectively.

### Lemma 2

> Let  $$ H $$ be an undirected graph with  $$ |V(H)|=n $$ and  $$ A_{H} $$ is a  $$ m \times m $$ symmetric matrix where  $$ a_{ij} $$ is equal to either  $$ 1 $$ or  $$ -1 $$ if there is an edge joining vertex  $$ i $$ and  $$ j $$ and  $$ 0 $$ if there isn't.
> Then,  $$ \Delta (H) \geq \lambda_{1} $$ where  $$ \lambda_{1} $$ is the largest eigenvalue of  $$ A_{H} $$.

Note: If you replace -1 by 1 in every entry of  $$ A_{H} $$, you get the adjacency matrix of  $$ H $$.

Let  $$ H $$ be an undirected graph with  $$ |V(H)|=n $$ and  $$ A_{H} $$ is a  $$ m \times m $$ symmetric matrix where  $$ a_{ij} $$ is equal to either  $$ 1 $$ or  $$ -1 $$ if there is an edge joining vertex  $$ i $$ and  $$ j $$ and  $$ 0 $$ if there isn't.

Then,  $$ \Delta (H) \geq \lambda_{1} $$ where  $$ \lambda_{1} $$ is the largest eigenvalue of  $$ A_{H} $$.

Note: If you replace -1 by 1 in every entry of  $$ A_{H} $$, you get the adjacency matrix of  $$ H $$.

## Proof of Theorem 1

Consider the sequence of matrices  $$ A_{n} $$ from Lemma 1. For the (2^{n-1}+1)-vertex induced subgraph  $$ H $$, consider the principal submatrix  $$ A_{H} $$ of  $$ A_{n} $$. Using Lemma 2,  $$ \Delta (H) \geq \lambda_{1}(A_{H}) $$. The aim now is to lower bound  $$ \lambda_{1}(A_{H}) $$ by  $$ \sqrt{n} $$.

Let  $$ E $$ be the eigenspace of  $$ \sqrt{n} $$ in  $$ A_{n} $$.  $$ dim(E)=2^{n-1} $$. The spectral norm of a matrix  $$ A $$ is  $$ \| A \|=sup\{\|Au\|;\|u \|=1 \}  $$. It is a well known fact that the spectral norm of a real symmetric matrix is equal to the greatest eigenvalue.

Let  $$ U $$ be the space of all unit vectors in  $$ A_{H} $$. Then, this space can be extended to a space  $$ U' $$ in  $$ A_{n} $$ by inserting 0 in the coordinates which don't correspond to the rows of  $$ A_{H} $$. Since  $$ H $$ has  $$ 2^{n-1}+1 $$ vertices,  $$ A_{H} $$ is a  $$ (2^{n-1}+1) \times (2^{n-1}+1) $$ submatrix. Hence,  $$ dim(U')\geq 2^{n-1}+1 $$. Since  $$ 2^{n} $$ is the size of the square matrix  $$ A_{n} $$, this means that there is some vector  $$ x $$ that is in both  $$ E $$ and  $$ U' $$.

Combining these facts, we get  $$ \lambda_{1} \geq \|A x\|=\sqrt{n} \|x\|=\sqrt{n} $$.

Hence,  $$ \Delta (H) \geq \sqrt{n} $$.

Well, that's the end of the proof. Using results from Nisan and Szegedy, H. Hung actually established a result slightly stronger than the originial Sensitivity conjecture i.e  $$ bs(f) <2s(f)^{4}  $$.