---
layout: post
title: Topological Constraints on the Universal Approximation of Neural Networks
date: 2019-07-29
description: 
tags: algebra topology neural-net
categories: cs
giscus_comments: false
related_posts: true
featured: true
toc:
    sidebar: left
---

The title may seem like a contradiction given that there is such a thing as the Universal Approximation Theorem which simply states that a neural network with a single hidden layer of finite width(i.e finite number of neurons) can approximate any function on a compact set of  $$ \mathbb{R}^{n} $$ given that the activation function is non-constant,bounded and continuous.

Needless to say, I haven't found any kind of flaws in the existing proofs(see Kolmogrov or Cybenko). However, I thought of something a little simple and scoured the internet for an answer.

What if we allow an arbitrary number of hidden layers and bound the dimension of the hidden layers making them 'Deep, Skinny Neural Networks'? Would that be a universal approximator?

The answer is No and I found it out from a paper by Jesse Johnson who proved it using nothing but basic topology for a particular class of neural networks. This seems quite important because quite often, in application, multiple hidden layers of low dimension are used in machine learning. Also, the kinds of restrictions the author placed on the activation function and the neural network appear quite commonly in the real-world.

Setting Up the Notation

Before I proceed to the proof, I'll just set in place the required notation that will be used throughout.

Let  $$ M(\phi,n_{0},n_{1},\cdots ,n_{l})  $$ be set of all functions in a layered classic feed-forward neural network with activation function  $$ \phi  $$, input dimension  $$ n_{0} $$, output dimension  $$ n_{l} $$ and hidden layer dimension  $$ n_{i} $$ for  $$ i < l $$.

Given this, let  $$ \tilde{M} (\phi,n) $$ to be the union of the family of functions  $$ M(\phi,n_{0},n_{1},\cdots ,n_{l})  $$ where  $$ n_{i} \leq N, 0 \leq i \leq N $$ for some fixed natural number  $$ N $$.

A function in  $$ \tilde{M} (\phi,n) $$ is said to be nonsingular if  $$ \phi $$ is continuous and injective,  $$ n_{i}=n $$ and the weight matrix  $$ W $$ is nonsingular. The set of all functions in the families  $$ \tilde{M} (\phi ,n) $$ for fixed  $$ n $$ and varying activation functions which are continuous and injective is denoted by  $$ \tilde{M} (n) $$.

Given some function  $$ \psi:\mathbb{R}^{n} \mapsto \mathbb{R}^{m} $$ and a compact subset  $$ A $$ of  $$ \mathbb{R}^{n} $$, another function  $$ f $$ is said to  $$ (\epsilon , A)-approximate $$  $$ \psi $$ if for every  $$ x \in A,|\psi(x)-f(x)| <\epsilon $$.

An activation function  $$ \phi $$ is uniformly approximated by injective functions if there if there is a sequence of continuous, injective functions which uniformly converge to  $$ \phi $$. This would allow common activation functions such as ISRU, tanh and the sigmoid function to be approximated trivially. Functions such as RELu have a horizontal line in their graph and it's easy to appropriately choose a sequence of injective functions which will converge to RELu(try to do this yourself).

One key observation is that any function  $$ f \in \tilde{M} (\phi,n) $$ can be written as:

 $$ f=\phi_{\kappa} \circ l_{\kappa} \circ \cdots \circ \phi_{1} \circ l_{1} \circ \phi_{0} \circ l_{0}  $$

(1)

where  $$ \phi_{i} $$ are the activation functions and  $$ l_{i} $$ are linear functions determined by the weights associated with a particular layer. This is typically how we imagine forward propagation of fully connected neural networks to work.

The main theorem of his paper deals with path components associated with pre-images of level sets. So, going forward, it'll be better to put forth a definition.

A function  $$ f:\mathbb{R}^{n} \mapsto \mathbb{R} $$ has unbounded level components if for every  $$ x \in mathbb{R} $$, the path components of  $$ f^{-1}(x) $$ are all unbounded.

Preliminary results

Before, moving onto the main theorem, I'd like to simply list some rather obvious lemmas.

In (1), I mentioned the decomposition of functions in  $$ \tilde{M}(\phi, n) $$. So, now  consider some function  $$ f:\mathbb{R}^{n} \mapsto \mathbb{R}^{m} $$ which can be decomposed as  $$ f=f_{\kappa} \circ \cdots \circ f_{1} \circ f_{0} $$ where each  $$ f_{i}: \mathbb{R}^{n_{i}} \mapsto \mathbb{R}^{n_{i+1}} $$ is a linear function between Euclidean spaces.

If there are another set of functions  $$ g_{i}: \mathbb{R}^{n_{i}} \mapsto \mathbb{R}^{n_{i+1}} $$ than  $$ (\epsilon , A_{i})-approximate $$ each corresponding  $$ f_{i} $$ for some compact sets  $$ A_{i} \subset \mathbb{R}^{n_{i}} $$, then the composition   $$ g=g_{\kappa} \circ \cdots g_{0} $$  $$ (\epsilon,A)-approximates $$  $$ f $$ for some compact set  $$ A \subset \mathbb{R}^{n} $$.

Lemma 1:

If  $$ f $$ is approximated by some function in  $$ \tilde{M} (\phi,n) $$ where the activation function  $$ \phi $$ can be uniformly approximated by injective functions, then  $$ f $$ can be approximated by a function in  $$ \tilde{M} $$

Proof:

The proof is pretty simple so I skip it in typical mathematical snobbery. If you wish to prove it for yourself, start off by showing that every function in  $$ \tilde{M} (\phi, n) $$ can be approximated by a function in  $$ \tilde{M}(n) $$.Note that you can appropriately make  $$ n_{i}=n $$ for every hidden layer even if the width is less than  $$ n $$ by appropriately inserting zeros in the weight matrix. Now, the next hint is a way to deal with those pesky singular linear functions  $$ l_{i} $$. The set of all non singular  $$ n \times n $$ matrices form an open dense set in the space of all  $$ n \times n $$ matrices, i.e the set of all singular matrices form a Lebesgue zero measure set. This can be understood by considering these spaces to be manifolds in  $$ \mathbb{R}^{n^{2}} $$ so perturbing elements appropriately in a singular matrix makes it non-singular so that any arbitrarily small change in the value of the linear transformation associated with the singular function can be approximated by a non-singular one.

Now, you've shown that every function in  $$ \tilde{M} (\phi, n) $$ can be approximated by a function in  $$ \tilde{M}(n) $$ and given that  $$ f $$ is approximated by some function in  $$ \tilde{M} (\phi,n) $$, you can combine the results to prove the lemma.

This section ends with a key lemma on the functions in  $$ \tilde{M} (n) $$.

Lemma 2:

If  $$ f:\mathbb{R}^{n} \mapsto \mathbb{R} $$ is a function in  $$ \tilde{M} (n) $$, then for every  $$ x \in \mathbb{R} $$, the level set  $$ f^{-1}(x) $$ is homeomorphic to an open subset of  $$ \mathbb{R}^{n-1} $$. Hence, it has unbounded level components.

Sketch of the proof:

Again, the lemma is quite easy to prove. I'll provide a rough sketch of the proof. Writing the function  $$ f $$ as:

 $$ f=g \circ f'  $$ where  $$ f':\mathbb{R}^{n} \mapsto \mathbb{R}^{n} $$ is an  linear function and  $$ g=\phi \circ g' $$ where  $$ g' $$ is a linear function to  $$ \mathbb{R} $$. Essentially, we are writing the f as the compositions associated to the last layer of the neural network and the remaining layers.  $$ f' $$ is injective and continuous because the activation function is injective and continuous, and  $$ f $$ is singular by definition.

Once you work through the simple details, it's revealed that  $$ f^{-1}(x) $$ is an open subset of  $$ \mathbb{R}^{n-1} $$. On the other hand,  $$ f^{-1}(x) $$ is also closed in  $$ \mathbb{R}^{n} $$by the properties of continuous functions. If it was bounded, then the set would be a compact subset of  $$ \mathbb{R}^{n} $$ making it empty so  $$ f^{-1}(x) $$ is either unbounded or empty. Hence, the path components of this set are unbounded.




Towards the Main Theorem

The final result of the paper is that deep, skinny networks can only approximate functions with unbounded level components.

What we have proven is that every function that can be approximated by a function in  $$ \tilde{M} (\phi, n) $$ can be approximated by a function in  $$ \tilde{M} (n) $$ and that the level sets of the functions in  $$ \tilde{M} (n) $$ have unbounded level components. Now, it remains to prove that every function approximated by a function in  $$ \tilde{M} (n) $$ also has unbounded level components.

So, the topological constraint is that functions with bounded level components can not be approximated by a function in  $$ \tilde{M} (\phi, n) $$ where  $$ \phi $$ is a continuous activation function that can uniformly approximated by injective functions.

Theorem:

Any function  $$ f $$ approximated by a function in  $$ \tilde{M} (n) $$ has unbounded level components.

Proof:

Assume to the contrary that  $$ f:\mathbb{R}^{n} \mapsto \mathbb{R} $$ has bounded level components. Consider some level set  $$ f^{-1}(x) $$ for  $$ x \in \mathbb{R} $$. $$ f^{-1}(x) $$ is closed and components are also closed.Since, components are bounded, both these sets are compact.

Hence, there exists a number  $$ \lambda>0 $$ such that every element of  $$ f^{-1}(x)\backslash C $$ is at a distance greater than  $$ \lambda $$ from  $$ C $$.

Define  $$ \eta_{C}=\{y \in \mathbb{R}^{n}; ||y-c|| \}< \frac{\lambda}{2}, c \in C \} $$. Let  $$ T $$ be the boundary of this open set  $$ \eta_{C} $$.  $$ T $$ is closed and also bounded since it is at a bounded distance  $$ \frac{\lambda}{2} $$ from  $$ C $$(which is bounded itself).

 $$ f(T) $$ is also compact and  $$ x $$ is disjoint from it. Since the complement of the set is open, there exists some neighborhood  $$ U=[x- \epsilon,x+ \epsilon] $$ of  $$ x $$ that is disjoint from  $$ f(T) $$.

 $$ f^{-1}(U) $$ obviously contains  $$ f^{-1}(x) $$ and has a component  $$ \tilde{C} $$ that contains  $$ C $$.  $$ f^{-1}(U) $$ intersects  $$ \eta_{C} $$ and is disjoint from the boundary  $$ T $$. Therefore,  $$ f^{-1}(U) \subset \eta_{C} $$. So,  $$ \tilde{C} $$ is also compact.

It's given that  $$ f $$ is approximated by a function in  $$ \tilde{M} (n) $$. Let  $$ r=max(\{||c'-c||, c \in C,c' \in \tilde{C} \}) $$. Bear in mind that this number is finite since  $$ \tilde{C} $$ is bounded and contains  $$ C $$.

Let  $$ c $$ be an element of  $$ C $$.

Consider some connected compact neighborhood  $$ A $$ of  $$ c $$ such that there is the boundary is at a distance  $$ R>r $$. The simplest example of such a neighborhood would be the closed ball  $$ B_{R}(c) $$.

So, choose a function  $$ g \in  \tilde{M}(n) $$ that  $$ (\frac{\epsilon}{2},A)-approximates $$  $$ f $$.

 $$ \Rightarrow ||g(y)-f(y)|| <\frac{\epsilon}{2} \forall y\in A $$. Since  $$ f(c)=x $$,

 $$ g(c) \in [x-\frac{\epsilon}{2},x+\frac{\epsilon}{2}] \subset U $$.

Since  $$ g \in \tilde{M} (n) $$, the level components are unbounded, so the components of  $$ g^{-1}(g(c)) $$ are unbounded. We can construct a path  $$ \gamma $$ from  $$ c $$ to a point that is at a distance  $$ R $$ from  $$ c $$ such that every point in  $$ \gamma $$ lies in  $$ A $$. This means that  $$ ||g(y')-f(y')||< \frac{\epsilon}{2} \forall y' \in \gamma $$. Since  $$ \gamma \subset g^{-1}(g(c)) $$, $$ g(y')=g(c) \in [x-\frac{\epsilon}{2},x+\frac{\epsilon}{2}] $$ by the previous equation and inequality.

So,  $$ f(y') \in [x-\epsilon,x+\epsilon]=U $$. The path  $$ \gamma $$ is contained in one of the components of  $$ g^{-1}(U) $$ and since it contains  $$ c $$, this component is  $$ C $$.

But we constructed the path so that it starts from  $$ c $$ and ends at a point whose distance from  $$ c $$ is greater than  $$ r $$. This is a contradiction by the definition of  $$ r $$.

Well, that ends the proof. J. Johnson presents examples of how these restrictions apply to real-world machine learning problems which you can find in the last few pages of his paper.


