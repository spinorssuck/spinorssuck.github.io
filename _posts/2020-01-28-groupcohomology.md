---
layout: post
title: Bar resolutions, Group Cohomology and some cool applications
date: 2020-03-28
description: An exposition of group cohomology.
tags: math category-theory algebra
categories: math
giscus_comments: true
related_posts: false
featured: true
toc:
    sidebar: left
---

The format of this post will be a little unorganized. I start off with the definition of group cohomology without giving much motivation. Then, I properly define a bar resolution for groups in complete detail. With this setup, I properly motivate group cohomology, work out some extremely interesting examples to see why one should care about this particular free resolution. I've also decided to make another post later on a generalization of the bar resolution to the case of monads and a further generalization to  $$ E_{\infty}- $$algebras. I am currently taking a course on Homotopy Type Theory  and I've found it blissfully interesting so there might be a few posts in the future on that too. I've only recently noticed that I've never actually posted anything on either algebraic topology or homotopy theory, which is actually my main interest so I might update that soon enough.

A representation of a group  $$ G $$ over a field  $$ K $$ is just a  $$ K[G]- $$module. It is a common philosophy that one can study the structure of a group by studying its representations. In some sense, group cohomology relates to topology but I'll get to this later on in the post.

Consider  $$ \mathbb{Z} $$ as a  $$ K[G]-module $$ where  $$ K[G] $$ acts trivially and let  $$ M $$ be a representation,i.e  $$ \mathbb{Z}[G]- $$module. Extend this to a  $$ K[G]-module $$. The group cohomology  $$ H^{n}(G,M) $$ with coefficients in  $$ M $$ is defined by

 $$ H^{n}(G,M) := Ext_{\mathbb{Z}[G]}^{n}(\mathbb{Z},M)  $$. One can immediately see that  $$ H^{0}(G,M) \simeq Hom_{\mathbb{Z}[G]}(\mathbb{Z},M) $$. A map  $$ f $$ in  $$ Hom_{\mathbb{Z}[G]}(\mathbb{Z},M) $$ satisfies  $$ f(g. \lambda)=g.f(\lambda) $$. But since the action on  $$ \mathbb{Z} $$ is trivial, $$ f(g. \lambda)=f(\lambda)=\lambda f(1) $$. This implies that  $$ \lambda f(1)=\lambda g.f(1) $$. Sending  $$ f(1) $$ to any element of  $$ M $$ corresponds exactly to the fixed points  $$ M^{G} $$. So,  $$ H^{0}(G,M) $$ corresponds to the fixed points  $$ M^{G} $$.

## Bar Resolution

So, let's describe these things in terms of the bar resolution. The calculation of the  $$ Ext $$ functor entails finding a projective resolution  $$  F_{\bullet} \mapsto X \to 0 $$ and applying the contravariant  $$ Hom(-,B) $$ functor. Taking 'homology' yields  $$ Ext $$. The bar resolution actually gives such a resolution, in fact, a free resolution.

Let  $$ B_{n} $$ be the free  $$ \mathbb{Z}[G]-module $$ on  $$ G^{n} $$, that is, the set of symbols  $$ (g_{1} \otimes g_{2} \otimes \cdots \otimes g_{n}) $$ for  $$ n \geq 1 $$ and  $$ B_{0} := \mathbb{Z}[G] $$ where all those expressions are simply formal symbols for the generated free module. We have the following free resolution, whose maps will be described soon.

 $$ \cdots \to B_{2} \to B_{1} \to \mathbb{Z}[G] \to \mathbb{Z} \to 0 $$

where

the augmentation map  $$ \epsilon:\mathbb{Z}[G] \to \mathbb{Z} $$ is given by  $$ \epsilon(1_{g})=1 $$ on the basis elements.

 $$ d_{i}: B_{i} \to B_{i-1} $$ is given by:

 $$ d_{n}=\sum\limits_{i=0}^{n} d_{i} $$ where the maps  $$ d_{i} $$ is defined on the basis of the free module which extends to the entire group.

 $$ d_{0}(g_{0} \otimes g_{1} \cdots \otimes g_{n})=g_{0}(g_{1} \otimes g_{2} \otimes \cdots \otimes g_{n}) $$,

 $$ d_{i}(g_{0} \otimes g_{1} \cdots \otimes g_{n})=(g_{0} \otimes \cdots \otimes g_{i}g_{i+1} \otimes g_{i+2} \otimes \cdots \otimes g_{n} $$ for  $$ 0 <i <n $$. Keep note of the dimension above. Finally,

 $$ g_{n}(g_{0} \otimes g_{1} \cdots \otimes g_{n})=((g_{0} \otimes g_{1} \cdots \otimes g_{n-1}) $$.

There is topological motivation for this seemingly bizarre construction.Let us say that the aim is to somehow construct a simplicial object from  $$ G^{n} $$. For every ordered  $$ (n+1)- $$tuple, one can insert a  $$ n- $$simplex and  $$ G $$ can act on these faces by diagonal action:

 $$ g.(g_{0},\cdots,g_{n})=(g.g_{0},\cdots,g.g_{n}) $$

If any element of the tuple is  $$ 1 $$, the simplex degenerates into lower dimension, for example from the differential maps we saw above,  $$ (g_{0} \otimes \cdots g_{i}g_{i+1} \otimes \cdots \otimes g_{n})=(g_{0} \otimes g_{i-1} \otimes g_{i+2} \otimes  \cdots \otimes g_{n}) $$ if  $$ g_{i}g_{i+1}=1 $$. The differnetial maps match with the this interpretation of degeneracy and face maps of the simiplicial object.You can alternatively also define a normalized version of the bar resolution where the maps  $$ B_{n} $$ are replaced by tuples where the element are non-identity. It is easy to check that the sequence is a chain complex though this involves some annoying calculations. Also, the sequence is exact as we'll show in the following lemma.

### Lemma 1

The sequence above is a chain complex that is  $$ d_{j-1} \circ d_{j}=0 $$ for  $$ j \geq 1 $$ and  $$ \epsilon \circ d_{0}=0 $$. It is also a  $$ \mathbb{Z}[G] $$-free resolution i.e it is exact.

#### Proof

The first step is to prove that it is a chain complex.

Pick a basis element  $$ (g) \in B_{1} $$. $$ d_{1}((g))=1_{g}-1_{e} $$  $$ \Rightarrow \epsilon((g)-(1))=\epsilon((g))-\epsilon((1))=1-1=0 $$.

I encourage the reader to work out the case for  $$ d_{2} $$. Now, for  $$ i>2 $$, we can do a little trick to simplify the calculations. Define a new set of  $$ \mathbb{Z}[G]- $$modules  $$ C_{i} $$ by

 $$ C_{i}=\mathbb{Z}[G^{i+1}] $$ for  $$ i \geq 0 $$ with the  $$ \mathbb{Z}[G] $$ action given by a diagonal action on the tuples as follows

 $$ 1_{g}.(g_{1} \otimes \cdots \otimes g_{i})=(gg_{1} \otimes \cdots \otimes gg_{i} $$.

I will omit the details but essentially, what happens is that  $$ 1_{g}.(1 \otimes g^{-1}g_{1} \otimes \cdots \otimes g^{-1}g_{i})=(g_{1} \otimes \cdots \otimes g_{i}) $$ where we have a bijection of those tuples. So, we just hacked our module  $$ C_{i} $$ to be a free  $$ \mathbb{Z}[G]- $$module on one lower dimension. Verify that it is indeed a bijection and you get an isomorphism  $$ \phi_{i}:B_{i} \simeq C_{i} $$ for  $$ i \geq 0 $$ given by

 $$ \phi_{n}(g_{1} \otimes \cdots \otimes g_{n})=(1 \otimes g_{1}g_{2} \otimes \cdots \otimes g_{1}g_{2} \cdots g_{n}) $$.

Isomorphism follows trivially from the fact that left multiplication by  $$ g $$ is a bijection on a group. There may be other ways to map the basis elements too.

Define  $$ \delta_{i}:C_{i} \to C_{i-1} $$ by

 $$ \delta_{n}(g_{1} \otimes \cdots \otimes g_{n})=\sum\limits_{i=0}^{n} (g_{1} \otimes \cdots \hat{g_{i}} \otimes \cdots \otimes g_{n}) $$.

We have that  $$ \delta \circ \delta=0 $$ by the usual calculation one encounters in chain complexes. This will obviously be useful soon. We shall prove that  $$ j \geq 2,\delta_{j} \circ \phi_{j}=\phi_{j-1} \circ d_{j} $$ from which it follows that  $$ \delta_{j-1} \circ \delta_{j} \circ \phi_{j}=0=\delta-{j-1} \circ \phi_{j-1} \circ d_{i}=\phi_{j-2} \circ d_{j-1} \circ d_{i}=0 $$ iff  $$ d^{2}=0 $$ since  $$ \phi_{i} $$ is an isomorphism.

 $$ \delta_{j}\phi_{j}(g_{1} \otimes \cdots \otimes g_{j})=\delta_{j}((1 \otimes g_{1}g_{2} \otimes \cdots \otimes g_{1}g_{2} \cdots g_{n})) $$

Now apply  $$ \delta_{j} $$ to this expression and check that it is equal to  $$ \phi_{j-1} \circ d_{j} $$. It is a slightly annoying calculation but much less painful than dealing with the original equation. Now, it remains to deal with the case for  $$ j=2 $$(we've already done j=1), which I've already left as an exercise to the reader. Anyways, moving onto the next step

The second step is to prove that the complex is chain-homotopic to the identity.

We define the chain homotopy  $$ \sum_{i}:B_{i} \to B_{i+1} $$ for  $$ i\geq -1 $$(taking the -1 case as  $$ \mathbb{Z} $$)on the basis elements by

 $$ \sum_{i}(1_{g}.(g_{1} \otimes g_{2} \otimes \cdots \otimes g_{n})=(g \otimes g_{1} \otimes \cdots \otimes g_{n}) $$, simply adding the element  $$ g $$ to the symbol. We simply use the isomorphism  $$ \phi:B_{i} \to C_{i} $$ and transfer the entire problem to the  $$ C_{i} $$'s to get

 $$ \sum_{i}(1_{g}. \phi(g_{1} \otimes \cdots \otimes g_{i})=\sum_{i}(1_{g}.(1 \otimes g_{1} \otimes \cdots \otimes g_{1}g_{2} \cdots g_{i})) \\

=\sum_{i}(g \otimes gg_{1} \otimes \cdots \otimes gg_{1} \otimes \cdots \otimes g_{i}=(1 \otimes g \otimes gg_{1} \otimes \cdots \otimes gg_{1} \otimes \cdots \otimes g_{i}) $$ so we get that

 $$ \sum \circ \phi(g_{1} \otimes \cdots \otimes g_{n}=(1 \otimes g_{1} \otimes \cdots \otimes g_{n}) $$. Now I leave it to the reader to verify through simple calculations that

 $$ h_{j-1}(\phi_{j}) + \delta_{j+1} \circ h_{j}=id_{C_{j}} $$ for  $$ j \geq 1 $$. Lower cases can be dealt with separately.

## Group cohomology again, and a few applications

Ok, now that we've constructed this  $$ \mathbb{Z}[G]- $$module resolution. By definition,  $$ H^{n}(G;M):=Ext_{\mathbb{Z}[G]}^{n}(\mathbb{Z},M) \simeq H^{n}(Hom_{\mathbb{Z}[G]}(B_{n},A)) $$

Now, it's great that we've got a free resolution but obviously the hope is that one gets some meaningful results with the bar resolution. Let's observe a few key ideas.

 $$ Hom_{\mathbb{Z}[G]}(B_{n},A) \simeq Map(G^{n},A) $$

on the level of sets. Basically, assigning the values at the basis elements gives all  $$ \mathbb{Z}[G]- $$maps from  $$ B_{n} $$ to  $$ A $$ by extending linearly.

## Motivation

Let's look at some low-dimensional cases to see what exactly is going on.

I describe  $$ H^{0}(G,A) \simeq A^{G} $$ in the first section of the post.

Just like as described in the first section, even  $$ Hom_{\mathbb{Z}[G]}(F_{n},A) \simeq C^{n}(G,A) $$, the collection of maps  $$ G^{n} \to A $$ since specifying the values on the basis elements determines the entire homomorphism. Under this representation, the boundary maps  $$ d_{n}:C^{n}(G,A) \to C^{n+1}(G,A) $$ can be written more explicitly as:

 $$ d(f)(g_{0},\cdots,g_{n})=g_{0}f(g_{1},\cdots,g_{n})+\sum\limits_{i=1}^{n}(-1)^{i}f(g_{0},\cdots,g_{i-1},g_{i}g_{i+1},g_{i+2},\cdots,g_{n}+(-1)^{n+1}f(g_{0},\cdots,g_{n-1}) $$

We can call the elements of  $$ ker(d_{n}) $$  $$ Z^{n}(G,A) $$ and the elements of  $$ Im(d_{n-1}) $$ as  $$ B_{n} $$, the cycles and boundaries respectively or cocycles and coboundaries, if one wishes to be more precise. It is a chain complex and it is exact though I won't bother much with the details. The upshot is that know we have the following description of the cohomology group

 $$ H^{n} \simeq Ext_{\mathbb{Z}[G]}^{n}(\mathbb{Z},A) \simeq \frac{Z_{n}}{B_{n}} $$.

Great! Now we have just one final simple thing to put in place before we look at some applications.

## Theorem 1

Suppose  $$ 0 \to A \to B \to C \to 0 $$ is a short exact sequence of  $$ \mathbb{Z}[G]- $$modules, then there is right-derived long exact sequence:

 $$ 0 \to A^{G} \to B^{G} \to C^{G} \to H^{1}(G,A) \to H^{2}(G,B) \to H^{2}(G,C) \to \cdots  $$

I covered the proof of this theorem for the general case of derived functors in my other post.

I guess, as a simple consequence of the proof of dimension shifting I completed in the other post(or you could prove easily on your own), we have the following theorem which is useful in the context of group cohomology.

## Theorem 2 (Dimension Shifting)

If  $$ 0 \to A \to B \to C \to ) $$ is a short exact sequence of  $$ \mathbb{Z}[G]- $$modules such that  $$ B^{G} \simeq Hom(G,B) \simeq 0 $$ is trivial, then we have the following natural(wrt to chian complex morphisms) isomorphisms

 $$ H^{n+1}(G,A) \simeq H^{n}(G,C) $$ for  $$ n \geq 1 $$. The result essentially allows us to compute homology by computing homology of with respect to some other representation in a lower dimension. Now, let us move onto some examples.

## The Extension Problem

This is probably most the classical application of group cohomology which I am sure the reader is already quite familiar with so I shall discuss it only little detail.

A classical problem in group theory was to find all possible extensions of a group by a normal subgroup. If we have two groups  $$ H,N $$, it is natural to ask what groups  $$ G $$ are extensions of  $$ H $$ by  $$ N $$, that is, fit into the exact sequence

 $$ 1 \to N \to G \to H \to 1 $$

An obvious example is a the direct product  $$ H \times N $$. One could also add the extra condition that it be a split exact sequence which is equivalent to a semidirect-product  $$ N \ltimes H $$. Two extensions are said to be equivalent if the following diagrams commute:

Let's think of a few extensions of groups. For the groups  $$ \mathbb{Z}_{2},\mathbb{Z}_{3} $$, we have the trivial extension  $$ \mathbb{Z}_{2} \times \mathbb{Z} _{3} $$ and the well known extension  $$ \mathbb{Z}_{2} \ltimes \mathbb{Z}_{3} $$ where  $$ \mathbb{Z}_{2} $$ acts by inversion on  $$ \mathbb{Z}_{3} $$.This is the dihedral group  $$ D_{6} $$ of order 6.(Sorry if I have messed up the order of placement of the normal subgroup, I never remember how it works. I think I may have even messed up the semidirect product symbol too. Who cares, I always hated that symbol anyways and abhor the idea of trying to fix it).

We're going to prove that the elements of the cohomology group  $$ H^{2}(G,A) $$ are in one-to-one correspondence to extensions up to equivalence. We begin by first defining a section on the level of sets as follows: If there is an extension of the form

We would like to define an action  $$ G $$ on  $$ A $$ from the exact sequence. Since the sequence is exact, there exists some  $$ e_{g} $$ such that  $$  \pi(e_{g})=g $$. A section is basically a choice of such  $$ e_{g} $$'s. We'll explain the representative notation soon.  $$ e_{g} $$ acts on  $$ i(a) $$ by conjugation  $$ e_{g}i(a)e_{g}^{-1} $$. Note that  $$ \pi(e_{g}i(a))=g.1=g $$ and also that conjugation by this element  $$ e_{g}i(a)i(a')i_{a}^{-1}e_{g}^{-1}=e_{g}i(a')e_{g}^{-1} $$ since  $$ A $$ is abelian. So, the action is independent of the choice of  $$ g $$.

Let the section be  $$ \sigma: G \to E $$. Each  $$ \sigma(g) $$ represents an equivalence class  $$ Ag $$. Both  $$ \sigma(g)\sigma(h) $$ and  $$ \sigma(gh) $$ are in the same equivalence class  $$ Agh $$ for  $$ g,h \in G $$, so by exactness, there is a unique  $$ f_{g,h} \in A $$ satisfying

 $$ \sigma(g)\sigma(h)=f_{g,h}\sigma(gh) $$

Define a function  $$ f:G \times G \to A $$ by  $$ f(g,h)=f_{g,h} $$, the value determined above. Note that every element in  $$ E $$ can be written uniquely as  $$ i(a).\sigma(g) $$ by exactness. Let's see how multiplication works in  $$ E $$:

 $$ i(a_{1})\sigma(g)i(a_{2})sigma(h)=i(a_{1})\sigma(g)i(a_{2})\sigma(g)^{-1}\sigma(g)\sigma(h) $$. Since  $$ \sigma(g)i(a_{2})\sigma(g) \in i(A) $$, $$ \Rightarrow =i(a_{1}) i(g.a_{2}) f(g,h)\sigma(gh) $$. Since  $$ A $$ is abelian

 $$ \Rightarrow =(i(a_{1}+ g.a_{2}+f(g,h))\sigma(gh) $$ where  $$ g.a_{2} $$ is the action of  $$ G $$ defined above.

Associativity of multiplication in  $$ E $$(I leave it to the reader to check this) gives the equality:

 $$ g.f(h,k)-f(gh,k)+f(g,hk)-f(g,h)=0 $$ which is exactly the condition for  $$ f $$ to be in  $$ Z(G,A) $$. Finally, let  $$ \sigma_{1} $$ be another section of the extension and let  $$ f_{1} $$ be its factor set. We'll show next that  $$ f $$ and  $$ f_{1} $$ differ by a coboundary, an element of  $$ B(G,A0 $$ which implies that every extension has a well-defined cohomology class in  $$ H^{2}(G,A) $$.

Obviously,  $$ \sigma (g),\sigma_{1}(g) $$ lie in the same coset  $$ Ag $$ since they both map to  $$ g $$ under  $$ \pi $$. This implies that there is a unique  $$ c_{g} $$ such that  $$ \sigma(g)=i(c_{g})\sigma_{1}(g) $$. Define  $$ c:G \to A $$ by  $$ c(g)=c_{g} $$.

 $$ \Rightarrow \sigma(g)\sigma(h)=i(f(g,h)) \sigma(gh)=i(f(g,h)+c(gh))\sigma(gh) $$

Also,

 $$ \sigma(g)\sigma(h)=(c(g)\sigma_{1}(g))(c(h)\sigma_{1}(h))=(c_{g}+g.c_{g}+f(g,h))\sigma_{1}(gh) $$ Equating the two expressions yields,

 $$ f_{1}(g,h)=f(g,h)+(gc(h)-c(gh)+c(g)) $$ giving the needed result.

Now, we have to prove the opposite assertion , that, an element of  $$ H^{2}(G,A) $$ yields a unique(upto equivalence) extension of  $$ G $$ by  $$ A $$. I encourage the reader to find the remaining details in a textbook like Dummit and Foote or Aluffi(I am nor sure if he covers it though).

The element  $$ 0 $$ in  $$ H^{2}(G,A) $$ corresponds to a split extension because then the section  $$ \sigma $$ is a genuine homomorphism and so  $$ f=0 $$.

## Schur-Zassenhaus Theorem

Consider the exact sequence of groups:

[Insert Image]

If  $$ gcd(|G|,|A|)=1 $$ then the sequence is split, equivalently,

If the order of  $$ A $$, a normal subgroup of  $$ E $$, is coprime to the order of the index of  $$ A $$ in  $$ E $$, then there is a semidirect product such that  $$ E \simeq A \ltimes G $$ for some complement  $$ G $$.

We'll first deal with the abelian case and that'll turn out to be useful in the general proof. Towards, that we have the following Lemma.

### Lemma 2

Let  $$ G $$ be a finite group of order  $$ m $$ and let  $$ A $$ be an abelian group with  $$ G-action $$, then  $$ H^{n}(G,A) $$ are  $$ \mathbb{Z}_{m}- $$modules, that is, they are annihilated on multiplication by  $$ m $$.

#### Proof

Let  $$ B_{\bullet} $$ be the bar resolution of  $$ G $$ and let  $$ \eta $$ be the endomorphism of  $$ B_{\bullet} $$ given by multiplication by  $$ (m-N) $$ on  $$ \mathbb{B_{0}} \simeq \mathbb{Z}[G] $$ and multiplication by  $$ m $$ for  $$ B_{i} $$ for  $$ i \geq 1 $$. We show that  $$ \eta $$ is nullhomotopic. Consider the chain homotopy  $$ \sum_{n}:B_{n} \to B_{n+1} $$ given by the formula on the basis elements

 $$ \sum_{n}(g_{1} \otimes \cdots \otimes g_{n})=\sum_{g \in G}(g_{1} \otimes \cdots \otimes g_{n} \otimes g) $$

I leave it as an exercise to the reader to show that it is nullhomotopic, a trivial calculation.

### Corollary 2.1

Let  $$ G $$ be a finite group of order  $$ m $$ and let  $$ A $$ be either a vector space over  $$ \mathbb{Q} $$ or a  $$ \mathbb{Z}[\frac{1}{m}]- $$module then  $$ H^{n}(G,A)=0 $$ for  $$ n \neq 0 $$.

#### Proof

Multiplication by  $$ m $$ is an isomorphism on  $$ A $$ in either case. Applying $$ Hom_{\mathbb{Z}[G]}(-,A) $$ to the bar resolution  $$ B_{\bullet} $$, consider a class  $$ [\phi] \in Ext_{\mathbb{Z}[G]}(B_{\bullet},A) $$.

 $$ \phi(mx)=m.\phi(x) $$ which is  $$ 0 $$ only if  $$ \phi(x) $$ is  $$ 0 $$. So,  $$ H^{n}(G,A)=0 $$.

This resolves the Schur-Zassenhaus theorem for the abelian case below.

### Corollary 2.2

If  $$ A $$ is an abelian group, then  $$ H^{2}(G,A)=0 $$ so every extension of  $$ G $$ by  $$ A $$ is split.

With this, we reduce the proof of the general case to this specific case through some techniques. Before that though, there's just a random group theory fact we're going to use.

### Lemma 3

Let  $$ G $$ be a group and let  $$ P $$ by a Sylow-p subgroup. Then,  $$ N(P) $$ is a subgroup of  $$ N(Z(P)) $$.

(we omit this proof)

### Proof of Schur-Zassenhaus Theorem

We proceed by induction on  $$ n $$, the order of  $$ 'A' $$, the first element in the sequence. Let  $$ p $$ be a prime that divides  $$n=ord(A) $$ and consider  $$ P $$, a Sylow-p subgroup of  $$ A $$. We know that  $$ Z(P) \neq {0} $$ by standard group theory via. the class equation, for example. Consider  $$ N_{E}(Z(S)) $$, the normalizer of  $$ Z(S) $$ in  $$ E $$. Using Frattinis's argument,

 $$ \lvert E \rvert=\frac{ \lvert N(P) \rvert . \lvert A \rvert}{\lvert N(P) \cap A \rvert} $$.

So, the index  $$ m $$ divides  $$ \lvert N(P) \rvert $$ and  $$ N(P) $$ is a subgroup of  $$ N(Z(P)) $$ by Lemma 3. So,  $$ m \vert N(Z(P)) $$. So, we get an extension

 $$ 0 \to (A \cap N(Z(P)) \to N(Z(P)) \to G \to 0 $$ by the Second Isomorphism Theorem and using Frattini's argument. If  $$ N(Z(P)) \neq E $$, using the induction hypothesis, this sequence splits so there is a subgroup of  $$ N $$ which is isomorphic to  $$ G $$. On the other hand, if  $$ N(Z(P)) =E $$, we get that  $$ Z(P) \ltriangle N(Z(P)) $$ and we get the extension

 $$ 0 \to A/Z(P) \to E/Z(P) \to G \to 1 $$ by the Third Isomorphism theorem. This splits by the induction hypothesis. Let  $$ G' $$ be the subgroup of  $$ E/Z(P) $$ isomorphic to  $$ G $$. Pulling back, let  $$ E_{1}:=\pi^{-1}(G') $$ where  $$ \pi $$ is the natural quotient map  $$ \pi:E \to E/Z(P) $$. From this, we get the extension,

 $$ 0 \to Z(P) \to E_{1} \to G' \to 0 $$. Using Corollary 2.2(since  $$ Z(P) $$ is abelian), there is  subgroup of  $$ E_{1} $$ isomorphic to  $$ G' $$ so there is a subgroup of  $$ E $$ isomorphic to  $$ G' $$ which, as established, is isomorphic to  $$ G $$. Q.E.D


