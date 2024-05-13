---
layout: post
title: What exactly are adjoint functors?
date: 2019-01-12
description: 
tags: algebra category-theory
categories: math
giscus_comments: false
related_posts: true
featured: true
toc:
    sidebar: left
---

## Introduction

Below, I'll repost an answer I gave to a question on Quora about the importance of adjoint functors. It is a simple exposition which focuses on the intuition behind their construction and gives a few examples with explanations that can aid anyone who is beginning to learn about adjoint functors. I'll probably add more detail on the  $$ BC $$ and throw in a few more diagrams later.

As another answer has already pointed out, adjoint functors are ubiquitous in many constructions across mathematics and that is enough reason to consider them important. But to help appreciate it more, I think a slightly different interpretation of a natural transformation will be helpful.

Let C be a small category and consider the nerve  $$ NC $$ of the category which is a simplicial set whose n-simplices are the strings:

 $$ X_{0} \mapsto X_{1} \mapsto \cdots \mapsto X_{n} $$ where  $$ X_{i} $$ are obviously the objects and the arrows are the morphisms in the category. The kth-face maps can be obtained by simply deleting  $$ X_{k} $$ . The classifying space  $$ BC $$ is then realized as the geometrization of  $$ NC $$ (turn the entire construction into a formal CW complex). For example, in the simple case of a poset where morphisms are determined by order,  $$ BC $$ has the points of  $$ J $$ as its vertices and the size-k totally ordered subsets as it’s  $$ k-simplices $$.

So, a functor  $$ F:C \to D $$ induces a CW-complex map  $$ F*:BC \to BD $$ from the category of small categories to the category of CW complexes. I encourage the reader to work through this construction for the sake of clarity.




I’ll leave out a few details here but I’ll say that it is in this sense that a natural transformation  $$ C<->D $$ is essentially a homotopy  $$ BC \times I<-> BD $$ . You can then think of adjoint functors as homotopy equivalences on categories. Hence, they do correspond to something weaker than a homeomorphism which is often why many call adjoint functors ‘conceptual inverses’. The concept of an adjoint functor is a special case of an adjunction in 2-categories where these ideas make more sense. The Wikipedia page motivates it by considering a functor F:C \to D and finding the problem for which F is the most efficient solution. This is why these adjoint functors always come in pairs. Let’s review the definition and look at a few interesting examples for all this to make more sense.

Two functors  $$ F:D \to C , G:C \to D $$ are said to be adjoint i.e  $$ F \dashv G $$ if there exists a natural isomorphism of the hom-sets  $$ Hom_{C}(FY,X) \sim Hom_{D}(Y,FX) $$ . The equivalent counit-unit definition which is often easier to work with is that are natural isomorphisms  $$ \epsilon:FG \Rightarrow 1 $$ and  $$ 1 \Rightarrow GF $$ such that the following triangles commute:

The other answer has presented one of the simplest and most important examples, the free-forgetful functor on groups. I’ll present an example of a ‘free-forgetful’-type adjunction which may be a little harder to notice.

Let  $$ C $$ be a category, say the category of groups or something else. Take two objects  $$ a,b \in C $$ . We will study the product  $$ a \times b $$ . The product  $$ a \times b $$ is defined by the maps to  $$ a $$ and  $$ b $$ so that if  $$ c^{'} $$ maps to both  $$ a $$ and  $$ b $$ , then there is a unique morphism  $$ f:c^{'} \to a \times b $$ which makes the diagram commute. Let’s construct a functor  $$ F: C \times C \to C $$ defined by  $$ (a,b) \to a \times b $$ . Damn, did you notice that? We just lost information as there is no map from  $$ C \to C \times C $$ that can you can compose to get the identity.  $$ a \times b $$ can probably be constructed in different ways as a product. Well, it hardly matters, let’s try to do something inverse-like. Take an object  $$ c \in C $$ and do the only thing you can think of, that is, send it to  $$ (c,c) $$ . Let this be the diagonal map  $$ \Delta :C \to C \times C $$. Notice that a pair of morphisms  $$ c \to a, c \to b $$ in  $$ C $$ is the same thing as a morphism  $$ (c,c) \to (a,b) in C \times C $$ . So we have the hom-set natural isomorphism  $$ Hom_{C \times C}(\Delta(c),(a,b)) \simeq Hom_{C}(c,a \times b) $$ . The counit is the pair of projection maps(a single morphism in  $$ C \times C $$ ) for  $$ a \times b $$ and the unit takes  $$ c $$ to  $$ c \times c  $$(verify these facts and the components of the natural transformations). A nice mnemonic I once heard was that left adjoints(here  $$ \Delta $$ ) are ‘liberal’ and generate free things.
Let’s look at a simple example in topology. Let  $$ HausC $$ be the category of compact Hausdorff spaces. Define  $$ F:HausC \to Top $$ which essentially returns the topological space and forgets the separation axiom and compactness. The ‘most efficient solution’ to this optimization is the functor  $$ \beta:Top \to HausC $$ , the Stone-Cech compactification functor.  $$ \beta X $$ satisfies the universal property that any map  $$ X \to Y $$ where Y is compact and Hausdorff factors through \beta X .
Another extremely important adjunction is the Hom-Tensor adjunction. Let  $$ M,N $$ be rings and consider the categories  $$ MMod,NMod $$ of modules over these rings. Let  $$ X $$ be a  $$ (M,N) $$ bi-module and define  $$ F(D)=D \otimes_{M} X $$ and  $$ G(C)=Hom_{N}(X,C) $$ . We have a natural isomorphism  $$ Hom_{N}(D \otimes_{M} X,C) \simeq Hom_{R}(D,Hom_{M}(N,X)) $$ which can be verified by constructing the units,counits,a simple exercise. It is not free-forgetful in any obvious sense like the previous examples.
Again, a basic example arises from considering partially ordered sets. If  $$ C  $$ and  $$ D $$ are two posets then they are naturally categories. A pair of adjoint functors  $$ F \dashv G $$ in this case is a Galois connection which means that  $$ F(c) \leq d $$ if and only if  $$ c \leq F(d) $$ , in other words, a natural isomorphism  $$ Hom_{D}(F(c),d) \simeq Hom_{C}(c,F(d)) $$ . Again, this doesn’t look like a free-forgetful pair.

The best way to understand adjoint functors is to encounter more exmaples of adjunction. As a guiding principle, you can expect to find adjunctions in ‘symmetric and inverse-like’ constructions. The left and right adjoints have many interesting properties, like preserving colimits and limits respectively. This can be proven quite easily once you establish that the Hom-functor preserves arbitrary limits. In fact, there is a class of theorems that allow one to establish left/right adjoints for a functor based on how it acts on limits and colimits.