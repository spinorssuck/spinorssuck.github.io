---
layout: post
title: Bousfield Localization of Spectra
date: 2020-05-04
description: math blog post about the bousfield localization of spectra
tags: math
categories: math
giscus_comments: false
related_posts: false
featured: true
toc:
    beginning: true
---

This post is organized as a part of the UT Austin Spring 2020 DRP program.I'd like to thank my mentor Richard Wong for useful directions throughout the semester and introducing me to much of the foundational material in homotopy theory.

This post will be organized as follows:

First, I'll present the basic definitions of the topic(spectra, homotopy groups,CW-spectra,triangulated categories etc).

Second, I';ll introduce finite spectra,  $$ Z_{p} $$-localization of spectra aka. p-local spectra via Bousfield localization, thick subcategories.

Third, I'll discuss the the Thick Subcategory Theorem but avoid technical details.

So, let's begin.

A spectrum  $$ X $$ is a sequence of pointed spaces  $$ \{X_{n} \} $$ and structure maps  $$ \sigma_{n}: \sum X_{n} \to X_{n+1} $$. For example, one can take a pointed space  $$ X $$ and consider the suspensions  $$ \sum^{n} X=S^{n} \wedge X $$. This forms a spectrum with the structure maps the identity. This is the suspension spectrum of  $$ X $$.

One can consider this general spectrum  $$ \{X_{n} \} $$ and suspend it by the integer  $$i $$ to get a spectrum  $$ \sum^{i} X $$ whose components are given by  $$ (\sum^{i} X)_{n}=X_{n+i} $$.

The homotopy groups  $$ \pi_{k}(X) $$ of a spectrum  $$ X $$ are defined as the colimit:

 $$ \pi_{k}(X)=colim_{n} \pi_{n+k}(X_{n}) $$.




Since  $$ \sum $$ is a functor on  $$ Top $$, one is motivated to define maps between spectra  $$ f:X \to Y $$ as a a collection of maps  $$ f_{n}:X_{n} \to Y_{n} $$ such that the obvious diagrams commute.This may not actually be the best definition of maps between spectra but it doesn't matter too much for now.

For example, one can consider  $$ S^{0} $$ and suspend this to get  $$ \mathbb{S} $$, the sphere spectrum, an example of a suspension spectrum.

Given the suspension and loop space functors  $$ \sum, \Omega $$, one has the loop-space adjunction for pointed topological spaces, namely,

 $$ [\sum X,Y] \simeq [X,\Omega Y] $$

Note that  $$ \Omega Y=[S^{1},Y] $$(with compact-open toplogy). This allows us to define  $$ \Omega-spectrum  $$ as spectrum  $$ X $$ where the adjoint map  $$ \tilde{\sigma_{n}}:X_{n} \to \Omega X_{n+1} $$ is a weak homotopy equivalence.

Let's look at an example.

## Eilenberg-MacLane Spectrum

Recall that an Eilenberg-Maclane space corresponding to  $$ (G,n) $$ where  $$ G $$ is an abelian group is a CW-complex  $$ X $$ such that  $$ \pi_{n}(X)=G $$ and  $$ \pi_{k}(X)=0 $$ for  $$ k \neq n $$.Call this CW-complex  $$ K(G,n) $$

We know the following correspondence from algebraic topology : For any CW-complex  $$ X,H^{k}(X;G) \simeq [X,K(G,n)] $$.

Collect these spaces on the index  $$ n $$ to get  $$ \{K(G,n) \} $$. We claim this forms a spectra. What are the structure maps though?

In particular, note that we we have  $$ \pi_{k}(\Omega K(G,n+1))=\pi_{k+1}(K(G,n+1)) $$. By uniqueness of the Eilemberg-McLane space upto homotopy equivalence, we have a homotopy equivalence  $$ \tilde{\sigma}_{n}:K(G,n) \to \Omega K(G,n+1) $$. Take the adjoint of this under the loopspace-adjunction to get the structure maps  $$ \sigma_{n}:\sum K(G,n) \to K(G,n+1) $$.

Hence, this is also an  $$ \Omega- $$spectrum.

## CW-spectra

Well, I suppose some analogy with the classical case is required here. Consider the Quillen-Serre model structure on pointed topological spaces(aka the usual one). Here, the cofibrations are retracts of generalized relative CW inclusions(see [1] for definitions). In particular, the CW complexes are cofibrant objects in this case. We'd like our so called CW complexed to be cofibrant objects in the stable model category on topological sequential spectra(these are the same things as the spectra defined above where  $$ \sum X =S^{1} \wedge X $$).

A CW spectra is a sequence  $$ \{E_{n} \} $$ of CW-complexes where the structure maps  $$ \sigma_{n}:\sum E_{n} \to E_{n+1} $$ map isomorphically into a subcomplex of  $$ E_{n+1} $$. TO prove the above fact, see Prop 0.49 of this.

The cell of a CW complex is the collection  $$ \{A_{n},\sigma_{n+1}(A_{n}),\sigma_{n+2}(A_{n}),\cdots, \} $$ where  $$ A_{n} $$ is a cell of  $$ E_{n} $$ and  $$ A_{n} $$ is not of the form  $$ \sigma_{i}(A_{k}) $$ for some cell  $$ A_{k} \subset E_{n} $$ where  $$ k<n $$. Essentially, you package a cell  $$ A_{n} $$ of some component space in the spectrum and the cells in the higher components obtained from the structure maps such that the original  $$ A_{n} $$ itself is not obtained in this form.

A finite spectrum is a CW-spectrum which has a finite number of cells. Another important property of  $$ Top $$ extends to the case of spectra:CW-Approximation.

A subspectrum  $$ B $$ of a CW spectrum  $$ X $$ is closed if  $$ B $$ is a union of cells and for any cell in  $$ X $$ with some suspension in  $$ B $$, it is in  $$ B $$, that is,  $$ X/B $$ is a CW spectrum. This will be important later in Bousfield localization.

We know that if  $$ X $$ is a topological space, then there exists a CW-Complex  $$ \Gamma X $$ and a homotopy equivalence  $$ \Gamma X \simeq X $$.

This extends as follows:

## CW Approximation for Sequential Spectra:

Let  $$ X $$ be a sequential spectrum then there exists a CW-Spectrum  $$ \Gamma X $$ such that there is a weak homotopy equivalence between  $$ \Gamma X $$ and  $$ X $$.

### PROOF:

By CW-approximation on  $$ Top $$, consider a weak homotopy equivalence  $$ f_{0}: \Gamma X_{0} \sim X_{0} $$. Assume that there exists a collection of weak homotopy equivalences  $$f_{n}: \Gamma X_{k} \sim X_{k} $$ for all  $$ k \leq n $$ which respects the structure maps, we have the following

Consider the composite  $$ \sum \Gamma X_{n} \to \sum X_{n} \to X_{n+1} $$. By CW-Approximation on  $$ Top $$, the second map factorizes as  $$ \sum X_{n} \to \Gamma X_{n+1} \to X_{n+1} $$ where  $$ \Gamma X_{n+1} \to X_{n+1} $$ is a weak homotopy equivalence and the first one is a relative CW inclusion.

## Triangulated Category

Consider an additive category  $$ C $$ an automorphism  $$ \sum  $$ on  $$ C $$(called a shift functor). A triangle in this category is a sequence:

 $$ X \to Y \to Z \to \sum X $$

A morphism of triangles  $$ X \to Y \to Z \to \sum X  $$ and  $$ X' \to Y' \to Z' \to \sum X' $$ with component-wise maps that commute in the obvious diagram.

We have a distinguished class of these triangles called exact triangles/distinguished triangles with respect to which the following axioms are satisfied:

### TR1(COFIBER, TRIANGLES ARE REPLETE)

The triangle  $$ X \to X \to 0 \to \sum X $$ is an exact triangle.

For any map  $$ f: X \to Y $$, there is an object  $$ Z \in C $$ and an exact triangle of the form:

Third, every triangle isomorphic to an exact triangle is exact.

### TR2(SHIFT EXACT TRIANGLE)

If

is an exact triangle if and only if the following triangle is exact:

### TR3(MAPS BETWEEN EXACT TRIANGLES)

If  $$ X \to Y \to Z \to \sum X,X' \to Y' \to Z' \to \sum X' $$ are two exact triangles and if we're given maps between the first two components  $$ X \to X',Y \to Y' $$ which makes the square commute, then there exists a third map  $$  $$Z \to Z' $$ which makes the entire diagram commute.

### TR4(OCTAHEDRAL AXIOM)

This is quite technical condition so I'll just leave this here for self-explanation:

## Homotopy Category of Stable Model Category

The homotopy category of a stable model category, in our case, the category of spectra. This means that loop and suspension functors  $$ \Omega, \sum $$ are equivalences. Note that this isn't the case in  $$ Top^{*} $$.  The projective and injective model structures on chain complexes on an abelina category  $$ A $$ are also a stable model category.

## Smash Product of Spectra

So let  $$ SHC $$ be the stable homotopy category discussed above. We'd like to define a smash product on homotopy category of sequential spectra equipped with its stable model structure,  $$ Ho(S^{N}) $$ defined above. We want a symmetric monoidal product on this category, the smash product, in this case. The situation is a little complicated in general but one could define a naive smash product of sequential sepctra  $$ X,Y $$ as follows:

 $$ X \wedge Y= $$

where the structure maps are:

 $$ \sum (\sum X_{n} \wedge Y_{n}) \simeq \sum X_{n} \wedge \sum Y_{n} \to X_{n+1} \wedge Y_{n+1} $$ where the last map is the smash product of the maps  $$ \sum X_{n} \to X_{n+1} $$ and  $$ \sum Y_{n} \to Y_{n+1} $$ and:

 $$ \sum (X_{n} \wedge Y_{n}) \to \sum X_{n} \wedge Y_{n} $$

To define a symmetric monoidal product, we need a unit. This is the sphere spectrum  $$ \mathbb{S} $$.

## Ring spectra

A ring spectrum  $$ X $$ is a spectrum equipped with a multiplication and unit map  $$ \mu: X \wedge X \to X $$ and  $$ \eta: S \to E $$ such that the following diagram commutes with these monad-like axioms of associativity:

## Bousfield Localization

We wish for a way to add more weak equivalences to a model category which are reflected in the stable homotopy category. To this effect, in a sense, we add more cofibrations to the data of the model category  $$ C $$. We'd also want to get atleast some sort of a functor  $$ C \to L_{W}C $$ with some results on existence/uniqueness where  $$ W $$ is the class of maps that we wish to localize on.

Just like in the case of algebraic localization ,we expect to 'kill off' more than just  $$ W $$ under the localization process. A basic example is the localization with respect to a homology theory. The upshot is that the localizing at primes will prove to be computationally better to handle as we'll see.

We're just going to be looking at localization of CW-spectra with respect to a homology theory here.. Let  $$ Ho^{s} $$ be the category of CW-spectra.

Let  $$ E \in Ho(S^{N}) $$. One can prove that  $$ E_{n}(X)=\pi_{n}(E \wedge X) $$ is a generalized homology theory. Throughout, we'll write this as  $$ E_{*}(X) $$ for simplicity.

Also, fix the notation  $$ [A,B]_{*}=[\sum ^{*} A,B] $$.

A morphism of spectra  $$ f: X \to Y $$ is an  $$ E-equivalence $$ if the map  $$ \tilde{f}:E \wedge X \to E \wedge Y $$ is an isomorphism in  $$ Ho^{s} $$, that is the induced map,  $$ E_{*}(f) $$ is an isomorphism

A spectrum is  $$ E- $$acyclic if  $$ E_{*}(X) $$ =0 $$.

A spectrum  $$ X $$ is  $$ E- $$local if for every  $$ E*- $$equivalence  $$ f: A \to B $$, the induced map  $$ f^{*}:[B,X]_{*} \to [A,X]_{*} $$ is a bijection.

## $$ E_{*}-$$ $$Whithead Theorem:

Let  $$ X,Y \in Ho^{s} $$ be  $$ E- $$local and  $$ f: X \to Y $$ is an  $$E- $$equivalence then  $$ f:X \simeq Y $$ in  $$ Ho^{s} $$.

### PROOF:

The definitions give the equivalences  $$ [Y,X]_{*} \simeq [X,X]_{*} $$ and  $$ [X,Y]_{*} \simeq [Y,Y]_{*} $$ which gives the stable weak equivalence

Ok, we 're now going to get to building this localization functor. Based on everything so far, let  $$ L_{E} $$ be the localization functor we'll construct;For a spectrum  $$ X $$, we want  $$ L_{E}(X) $$ to be  $$ E-local $$ and a natural transformation  $$ q \Rightarrow L_{E} $$.Here,  $$ \lvert X \rvert $$ represents the number of cells of CW spectrum  $$ X $$.

## Lemma 1:

Let  $$ X $$ be a CW-spectrum and  $$ B $$ be a proper closed subspectrum of  $$ X $$ with  $$ E_{*}(E/B)=0 $$. Let  $$ \kappa \geq \lvert \pi_{*}(E) \rvert $$ be a infinite cardinal number. Then, there is a closed subspectrum  $$ W \subset X $$ with at most  $$ \kappa $$ cells such that  $$ W \not \subset B $$ and  $$ E_{*}(W/(W \cap B))=0 $$

### PROOF:

Start off with some  $$ W_{1} $$ such that  $$ \lvert W_{1} \rvert \leq \kappa $$ and  $$ W_{1} \not \subset B $$. Proceed inductively. Given this  $$ W_{n} $$, choose for each  $$ x \in E_{*}(W_{n}/(W_{n} \cap B)) $$, a subspectrum  $$ F_{x} $$ such that  $$ x=0 $$ in  $$ E_{*}((W_{n} \cup F_{x})/((W_{n} \cup F_{x}) \cap B)) $$. This is possible by the hypothesis  $$ E_{*}(E/B)=0 $$. Anyways, define  $$ W_{n+1}=W_{n} \bigcup \cup_{x} F_{x} $$. We get that  $$ \lvert W_{n} \rvert \leq \kappa $$ for all  $$ n $$, $$ W_{n} \not \subset B $$.

Choose  $$ W=\bigcup_{n=1}^{\infty} W_{n} $$ to finish the proof.

## Lemma 2:

There exists an  $$ E-acyclic $$ spectrum  $$ A^{E} $$ such that the a spectrum  $$ Y $$ is  $$ E-local $$ if and only if  $$ [A,Y]_{*}=0 $$.

### PROOF:

By the CW approximation theorem(proven above), let  $$ \{K_{\alpha} \} $$ be a set of CW spectrum representatives of the weak equivalence classes of  $$ E-acyclic $$ spectra with atmost  $$ \kappa $$ cells. Consider  $$ A^{E}=\vee_{\alpha} K_{\alpha} $$. If  $$ Y $$ is  $$E-local $$ then  $$ [A^{E},Y]_{*}=0 $$.

Now, if  $$ [A^{E},Y]_{*}=0 $$ then  $$ [A',Y]_{*}=0 $$ for any  $$ A' $$ formed from the  $$ A $$ under weak equivalence, shift, homotopy cofiber, wedges, summands. Let  $$ C(A^{E}) $$ be this class of spectra. We've to show that all  $$ E-acyclic $$ spectra lie in  $$ C(A^{E}) $$.

Let  $$ X $$ be an  $$ E-acyclic $$ spectra, upto weak equivalence consider the representative  $$ \Gamma X $$. By the previous Lemma(Lemma 1), we start from  $$ B_{0}=0 $$ and get the sequence:

 $$ B_{0}=0 \subset B_{1} \subset \cdots \subset B_{\gamma}=\Gamma X $$ where:

 $$ B_{\lambda} $$ is an  $$ E-acyclic $$ closed subspectrum $$ and

 $$ B_{\lambda+1}=B_{\lambda} \cup W_{\lambda} $$ where  $$ W_{\lambda} $$ is the closed subspectrum from Lemma 1 such that  $$ \lvert W \rvert \leq \kappa,W \not \subset B_{\lambda} $$ and  $$ E_{*}(W/W \cap B_{\lambda})=0 $$ and

For  $$ \lambda $$ a limit ordinal, $$ B_{\lambda}=\bigcup_{\mu<\lambda} B_{\mu} $$

Now, let  $$ K_{\alpha_{0}} $$ be the CW representative of  $$ W_{\lambda}/W_{\lambda}  \cap B_{\lambda} $$. One can see that  $$ B_{\lambda+1}/B_{\lambda} \simeq K_{\alpha_{0}} $$. Assume that  $$ B_{\lambda} \in C(A^{E}) $$.

By shifting, we get the cofiber sequence:

 $$ \Omega K_{\alpha_{0}} \to B_{\lambda} \to B_{\lambda+1} $$ hence  $$ B_{\lambda+1} \in C(A^{E}) $$.

For  $$ \lambda $$ a limit ordinal, consider the triangle:

 $$ \vee_{\mu < \lambda} B_{\mu} \to \vee_{\mu<\lambda}B_{\mu} \to B_{\lambda} $$ where the first map is  $$ 1-\bigvee_{\mu<\lambda}i_{\mu} $$ where  $$ i_{\mu} $$ is the inclusion  $$ B_{\mu} \to B_{\mu+1} $$.Transfinite induction gives that  $$ X \in C(A_{E}) $$.

## Localization theorem:

Every spectrum  $$ X \in Ho^{s} $$ sits in a homotopy cofiber sequence of the form

 $$ A^{E}(X) \to X \to A_{E}(X) $$

which is natural in  $$ X $$ such that  $$ A^{E}(X) $$ is  $$E-acyclic $$ and  $$ A_{E}(X) $$ is  $$ E-local $$

### PROOF:

The proof can be found using the previous lemma in Proposition 2.5 of this followed by Lemma 2.6. It uses a slightly technical 'small object' argument followed  by transfinite induction.

Moore spectrum of an Abelian Group

We're slowly approaching our goal of  $$ Z_{(p)}-localization $$.

Consider an abelian group  $$ A $$, then one has a Moore spectrum  $$ SA $$ is characterized as having the homotopy groups:

 $$ \pi_{i}(SA)=0 $$ for  $$ i <0,\pi_{i}(SA \wedge H\mathbb{Z})=0 $$ for  $$ i>0 $$ and  $$ \pi_{0}(SA)=A $$ where  $$ H\mathbb{Z} $$ is the Eilenberg-Moore spectra of the integers.

Moreover, this is a ring spectrum

For a spectrum  $$ E $$, define  $$ EG :=E \wedge SG $$ where  $$ G $$ is an abelian group. We have the following Universal Coefficient Theorem:

## Universal Coefficient Theorem:

There exists natural exact sequences:

 $$ 0 \to \pi_{n}(X) \otimes G \to (EG)_{n}(X) \to Tor(\pi_{n-1}(X),G) \to 0 $$

Two abelian groups  $$ G_{1},G_{2} $$ have the same acyclicity type if:

 $$ G_{1} $$ is a torsion group iff  $$ G_{2} $$ is a torsion group
For each prime  $$ p $$, $$ G_{1} $$ is uniquely p-divisible iff  $$ G_{2} $$ is uniquely p-divisible.

So, both  $$ \pi_{*}(X) \otimes G $$ and  $$ Tor(\pi_{*}(X),G) $$ are determined by the acyclicity type of  $$ G $$ which gives the the following equivalence of localizations:

## Proposition:

 $$ G_{1},G_{2} $$ have same acyclicity type iff  $$ SG_{1},SG_{2} $$ give equivalent localization functors.

Thus to determine the localization functors is equivalent to considering the cases when  $$ G=\mathbb{Z}_{(J)} $$ and  $$ G=\bigoplus_{p \in J} Z_{p} $$ where  $$ J $$ is a set of primes and  $$ \mathbb{Z}-{(J)} $$ are the integers localized at  $$ J $$. The case  $$ J=\{p\} $$ gives us the so-called p-local spectra.

From ([1], Prop 2.4,Prop2.6), one can determine the following when  $$ X \in Ho^{s} $$:

If  $$ G=\mathbb{Z}_{(J)} $$ then  $$ L_{SG}(X)=SG \wedge X $$

If  $$ G=\bigoplus_{p \in J}Z_{p} $$ then  $$ L_{SG}(X)=\prod\limits_{p\ in J}X \wedge \Omega S \mathbb{Z}_{p^{\infty}} $$. In this case, we have a split exact sequence:

 $$ 0 \to Ext(\mathbb{Z}_{p^{\infty}},\pi_{*}(X)) \to \pi_{*}(L_{SG}(X)) \to Hom(\mathbb{Z}_{p^{\infty}},\pi_{*-1}(X)) \to 0 $$. Also, if  $$ \pi_{n}(X) $$ is finitely generated for all  $$ n $$, then one gets  $$ \pi_{*}(L_{SG}(X)) $$

 $$ =\prod_{p \in J} \mathbb{Z}_{p} \otimes \pi_{*}(X) $$

Moreover,  $$ X $$ is  $$ SG-local $$ if and only if  $$ \pi_{*}(X) $$ are uniquely p-divisible for all  $$ p \not \in J $$.

## Thick Subcategory Theorem

Ok, so one could perform Bousfield localization with respect to more general generalized cohomology theories. For example, one could consider  $$ K(n) $$, Morava K-theory. We're not going to get into any of the actual details. It gives an interesting answer as to what the thick subcategories of the category of finite p-local spectra  $$ F_{p} $$ are.

A full subcategory  $$ F \subset F_{p} $$ is said to be thick if:

For every  $$ C \in F $$, any spectra weakly equivalent to  $$ C $$ are also in  $$ F $$
Given  $$ 0 \to X \to Y \to Z \to 0 $$, a cofibration in  $$ F_{p} $$ and two of  $$ \{X,Y,Z \} $$ are in  $$ F $$ then third is also.
A retract of an object in  $$ F $$ is also in  $$ F $$.

One can prove that if  $$X \in F_{p} $$ and  $$ K(n)_{*}(X)=0 $$ then  $$ K(i)_{*}(X)=0 $$ for  $$ i<n $$. We say that  $$ X $$ is of type  $$ n $$ if  $$ K(n)_{*}(X)\neq 0 $$ but  $$ K(n-1)_{*}(X)=0 $$.Let  $$ C_{\geq n} $$ be the category of spectra in  $$ F_{p} $$ of type  $$ \geq n $$. A major theorem in homotopy theory which can be proven using a weaker version of the nilpotence theorem is the Thick Subcategory Theorem:

## Thick Subcategory Theorem:

The thick subcategories of  $$ F_{p} $$ are exactly  $$ C_{\geq n} $$ for  $$ 0 \leq n <\infty $$.

One can find a proof of this fact in Lurie's notes.























