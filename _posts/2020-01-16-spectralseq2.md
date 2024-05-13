---
layout: post
title: A Road to the Grothendieck Spectral Sequence:Derived Functors II
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

In the <a href="https://spinorssuck.github.io/blog/2020/spectralseq1/">previous post</a>, I gave a little glimpse into derived functors and somewhat motivated their construction. In this post, we'll get our hands dirty with homological algebra to continue setting up the required machinery and go through many proofs.

In the previous post, I promised to continue the proof of a lemma which establishes a long exact sequence. Before giving the proof, let me mention a few facts which will be useful.

If we're given a short exact sequence  $$ 0 \to I \to A \to B \to 0 $$ in an abelian category where  $$ I $$ is an injective object. From the map  $$ I \to I $$ and the monomorphism  $$ I \hookrightarrow A $$, we can extend to a map  $$ A \to I $$ such that the composition is the identity. Using the Splitting Lemma, one obtains a non-canonical splitting  $$ A \simeq I \oplus B $$. Applying  $$ F $$,

 $$ 0 \to F(A) \to F(I) \oplus F(B) \to F(B) $$.

The identity map  $$ B \to B $$ factors through the projection map  $$ \pi:A \to B $$, the same holds true after applying  $$ F $$, in particular, the last map is surjective!

 $$ 0 \to F(A) \to F(I) \oplus F(B) \to F(B) \to 0 $$.

## Proof of Lemma 1:

### STEP 1:A MORPHISM BETWEEN OBJECTS WITH INJECTIVE RESOLUTION INDUCES A CHAIN MAP BETWEEN THE RESOLUTIONS

Let  $$ \phi:A \to B $$ be a morphism between two objects with injective resolutions  $$ A_{\bullet},B_{\bullet} $$. In the figure below, the map  $$ \phi_{0} $$ is constructed from the fact that  $$ d_{0}:A \to I_{0} $$ is a monomorphism and there is a map  $$ A \to B \to I'_{0} $$ from  $$ A $$ to an injective object.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="https://weeklymathematics.files.wordpress.com/2020/01/df1-1.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Now, there is a monomorphism  $$ I_{0}/ker(d_{1})=I_{0}/Im(d_{0})=Coker(A \to I_{0}) \hookrightarrow I_{1} $$. Next, note that by the commutativity of the square already defined,  $$ \phi_{0} $$ takes  $$ Im(d_{0})=Ker(d_{1}) $$ to  $$ Ker(d'_{1})=Im(d'_{0}) $$ by the fact that  $$ d'{1}d'_{0}=0 $$ by exactness of the lower sequence. This means that the map  $$ \phi_{0} $$ induces a morphism  $$ h_{0}: Coker(A \to I_{0}) \to Coker(B \to I'_{0}) $$ and by exactness, we can compose this with  $$ B/Ker(d'_{1}) $$ to get a map  $$ Coker(A \to I_{0}) \to I'_{1} $$. Since  $$ I'_{1} $$, we get the required map  $$ \phi_{1} $$. Inductively continue this process to get the entire chain map. Note that all the maps defined from the injective object property are not unique.

#### STEP 2:PROVING THAT ANY TWO SUCH EXTENSIONS ARE CHAIN-HOMOTOPIC

Let  $$ f_{n},g_{n} $$ be two chain maps from  $$ A \to I_{\bullet} $$ to  $$ B \to I'_{\bullet} $$.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="https://weeklymathematics.files.wordpress.com/2020/01/df2-1.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

To construct the chain homotopy  $$ \sum_{n}:I_{n} \to I_{n-1} $$ requires  $$ d'_{n} \sum_{n}+\sum_{n+1}d_{n+1}= $$(1). We define the chain homotopy inductively too. Let's start with  $$ sum_{1} $$. By the commutativity of the first square  $$  $$ f_{0},g_{0} $$ take the same values on  $$ Im(d_{0}) $$, we get that  $$ f_{0}-g_{0} $$ factors through  $$ Coker(d_{0}) $$. Using the exactness of the top row, we get a map  $$ I_{0} \to Coker(d_{0}) \hookrightarrow I_{1} $$. Since  $$ I'_{0} $$ is an injective object, we get the required map  $$ \sum_{1}:I_{1} \to I'_{0} $$ and hence  $$ f_{0}-g_{0}=\sum_{1}d_{1} $$.

Assume that we have defined the maps so  $$ \sum_{r} $$ so that (1) holds for all  $$ r \leq n $$. We must construct  $$ \sum_{n+1} $$. Notice that from (1), we have that  $$ (f_{n}-g_{n}-d'_{n}\sum_{n})d_{n}=d'_{n}f_{n-1}-d'_{n}g_{n-1}-d'_{n}\sum_{n}d_{n}=d'_{n}(f_{n-1}-g_{n-1}-\sum_{n}d_{n}) $$

 $$ =d'_{n+1}d'_{n}\sum_{n-1}=0 $$ by exactness and commutativity. Use the same argument above with the new map  $$ f_{n}-g_{n}-d'_{n}\sum_{n} $$ to construct  $$ \sum_{n+1} $$.

### STEP 3:EXACT SEQUENCE INDUCES EXACT SEQUENCE IN INDUCED CHAIN MAP FROM INJECTIVE RESOLUTION(HORSESHOE LEMMA)

Finally, after all that annoying diagram chasing, we've gotten the most basic results. The gist of the story is that a morphism between two objects induces a unique chain map between their injective resolutions up to chain homotopy.

Let  $$ 0 \to A \to B \to C \to 0 $$ be an exact sequence with resolutions  $$ A \to I_{\bullet} $$ and  $$ C \to K_{\bullet} $$. We haven't specified the resolution  $$ B \to J_{\bullet} $$ as we're going to construct it. Define  $$ J_{n}=I_{n} \oplus K_{n} $$. Let's deal with the first row.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="https://weeklymathematics.files.wordpress.com/2020/01/df3-1.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Let  $$ i:I_{n} \to J_{n},\pi:J_{n} \to K_{n} $$ be the usual inclusion and projection maps. We define the map  $$ e^{1} $$ by defining the map onto the components(note that this is an abelian category). The map from  $$ B \to C \to K_{0} $$ is just that.  $$ A \hookrightarrow $$ is a monomorphism. Since  $$ I_{0} $$ is an injective object, we can extend to a map  $$ B \to I_{0} $$. It is easy to see that it commutes.

Now, I leave the inductive step to the reader. Use the Snake Lemma to get an exact sequence of cokernels and repeat the procedure.

STEP 4:OBTAINING THE LONG EXACT SEQUENCE

Now, that we have setup everything needed for the lemma, we see that a short exact sequence  $$ 0 \to A \to B \to C \to 0 $$ yields a short exact sequence in  $$ Ch_{\bullet}(C) $$ of the injective resolutions.

Chopping off  $$ A,B,C $$ doesn't affect exactness upon replacement with  $$ 0 $$. A short exact sequence of the form  $$ 0 \to I_{n} \to J_{n} \to K_{n} $$ splits as we've already shown. We've also shown that on the application of the left exact functor  $$ F $$, it gets upgraded to a short exact sequence

 $$ 0 \to F(I_{n}) \to F(J_{n}) \to F(K_{n}) \to 0 $$. Now, apply the snake lemma to this short exact sequence of chain complexes ,take homology and voila,

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="https://weeklymathematics.files.wordpress.com/2020/01/df4-1.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Note that  $$ R^{0}(F) \simeq F $$. I don't think I've proven this but it is simple enough.

As we've already mentioned in the previous post, an object  $$ A \in C $$ is called F-acyclic if  $$ R^{i}(F(A))=0 $$ for all  $$ i >0 $$. It's great that that all our objects have injective resolutions but it doesn't help that it is not really possible to calculate these resolutions. Towards this goal, let's define an acyclic resolution:

An object  $$ A $$ is said to have an  $$ F-acyclic $$ resolution if there is an exact sequence

 $$ 0 \to A \to C_{0} \to C_{1} \to \cdots  $$ where  $$ C_{i} $$ for  $$ i \geq 0 $$ are all  $$ F-acyclic $$.

## Theorem 1:

For any  $$ F-acyclic $$ resolution  $$ A \to C_{\bullet} $$, the following holds true:

 $$ R^{i}(F(A)) \simeq H^{i}(F(A \to C_{\bullet})) $$

This isomorphism also satisfies the following natural property:

If we have the following commutative chain map for two acyclic resolutions  $$ A \to I_{\bullet} $$ and  $$ B \to I'_{\bullet} $$,

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="https://weeklymathematics.files.wordpress.com/2020/01/df5-1.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Then, the following naturality square commutes

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="https://weeklymathematics.files.wordpress.com/2020/01/df6-1.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

## Proof of Theorem 1:

 $$ 0 \to A \to C_{0} \to C_{1} \to \cdots  $$

Let  $$ K_{0} $$ be the cokernel of the map  $$ A \to C_{0} $$. Similarly, let  $$ K_{i} $$ be the cokernel of the map  $$ C_{i-1} \to C_{i} $$.We can break up the exact sequence into the following short exact sequences:

 $$ 0 \to A \to C_{0} \to K_{0} \to 0 $$ and

 $$ 0 \to K_{i-1} \to C_{i} \to K_{i} \to 0  $$ for  $$ i \geq 1 $$.

Applying  $$ F $$ to both types of exact sequences and using  $$R^{i}F(C_{j})=0 $$ for  $$ i>0 $$, we get

 $$ R^{1}(F(A)) $$ is the cokernel of the map  $$ F(C_{0}) \to F(K_{0}) $$,

 $$ R^{i}(F(A))=R^{i-1}(F(K_{0})) $$ for  $$ i>1 $$,

 $$ R^{1}(F(K^{i-1})) $$ is the cokernel of the map  $$ F(C_{i}) \to F(K_{i}) $$ for  $$ i \geq 1 $$ and  $$ R^{i}(F(K_{j-1})) \simeq R^{i-1}(F(K_{j})) $$ for  $$ i>1 $$ and  $$ j \geq 1 $$.

Take  $$ j=1 $$, for  $$ i>1 $$ use the first equality to get  $$ R^{i}(F(A)) \simeq R^{i-1}(F(K_{0})) $$. Use the second type of equality to get  $$ R^{i}(F(A)) \simeq R^{i-2}(F(K_{1})) $$. Use the equality again, repeatedly, to get  $$ R^{i}(F(A)) \simeq R^{1}(F(K_{i-2})) $$. So, the problem reduces to calculating  $$ R^{1}(F(K_{i})) $$ for  $$ i\geq 0 $$ and additionally finding  $$ R^{1}(F(A)) $$.

### STEP 1:FINDING  $$ R^{1}(F(K_{I})) $$ FOR  $$ I \GEQ 0 $$ AND  $$ R^{1}(F(A)) $$

Consider the part of the sequence  $$ \cdots \to F(C_{i+1}) \to  F(C_{i+2}) \to \cdots  $$. There exists a unique map  $$ F(K_{i+1}) \to F(C_{i+2}) $$ that factors through  $$ F(C_{i+1}) \to F(K_{i+1}) $$. From the diagram below,

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="https://weeklymathematics.files.wordpress.com/2020/01/df7-1.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Using the Snake Lemma, we get the exact sequence,

 $$ 0 \to R^{1}(F(K_{i})) \to coker(F(C_{i+1}) \to F(C_{i+2})) \to F(C_{i+3})  $$

Naturally,  $$ R^{1}(F(K_{i})) \simeq H^{i+2}(F(C_{\bullet})) $$ and this gives from the previous equality,  $$ R^{i}(F(A)) \simeq H^{i}(F(C_{\bullet})) $$ for  $$ i>1 $$.

It remains to deal with the case of  $$ R^{1}(F(A)) $$. We've seen that  $$ R^{1}(F(A)) $$ is the cokernel of the map  $$ F(C_{0}) \to F(K_{0}) $$. Replace  $$ i $$ by  $$ -1 $$ in the above diagram and do the same procedure to get the result.

### STEP 2:NATURALITY

(left as an exercise to the reader.)

## Projective objects, dimension shifting

Before I continue on, I must make sure to inform the reader of the projective object. An object  $$ P \in C $$, an abelian category is said to be a projective object if for every epimorphism  $$ B \to A $$ and a map  $$ \phi: P \to A $$,  $$ \phi $$ can be extended to  $$ B $$ so that the diagram commutes:

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="https://weeklymathematics.files.wordpress.com/2020/01/df8-1.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

As you may have noticed, this is the dual of the injective object and in fact, everything that I have proven and will continue to prove has a dual statement in terms of projective resolutions, projective objects and so on. I must also note something else extremely important. In Lemma 1, the hypothesis can be weakened to  $$ A $$ having an acyclic resolution instead of a injective resolution.

## Theorem 2:

Suppose  $$ A \in C $$, an abelian category and we have the following exact sequence:

 $$ 0 \to A \to I_{0} \to I_{1} \to \cdots \to I_{m} \to M \to 0 $$

If  $$ F $$ is a left exact funtor, then there are canonical isomorphisms  $$ R^{n}(F(M)) \simeq R^{n+m+1}(F(A)) $$ for  $$ n\geq 1 $$and we have the right exact sequence:

 $$ F(I^{m}) \to F(M) \to R^{m+1}(T(A)) \to 0 $$.

## Sketch of Proof 2:

Take the kernel  $$ K_{m} $$ of the morphism  $$ I_{m} \to M $$ and  $$ K_{i} $$ of  $$ I_{m-1} \to K_{m} $$ and so on to split the sequence into many short exact sequences. Now, apply  $$ F $$ to these sequences and use Lemma 1 to get the corresponding long exact sequence for each short exact sequences, notice that the terms involving  $$ I_{k} $$ are destroyed and combine all equalities to get the result.


At first, I thought of ending the derived functor posts here and introducing just the minimum prerequisite material to tackle the Grothendieck Spectral Sequence introducing any extra pieces of information on the way but I've changed my mind and decided to do another part of the Derived Functor sequence.

Specifically, I wanted to talk about Base change, mapping cones and Cartan Eilenberg resolutions in proper detail. Also, I seriously wanted to motivate all this acyclic stuff with some application to sheaf cohomology.





