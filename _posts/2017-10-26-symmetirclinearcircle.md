---
layout: post
title: Connection between a symmetric linear transformation and the unit sphere
date: 2017-10-26
description: 
tags: algebra
categories: math
giscus_comments: false
related_posts: false
featured: false
toc:
    sidebar: left
---

There is an interesting correspondence among the quadratic form of a symmetric linear transformation  $$ T:V \mapsto V $$on a real Euclidean space,the extreme values of the sphere and the eigenvectors of  $$ T $$

Let  $$ Q(x)=(T(x),x) $$ be the quadratic form associated with a symmetric linar transformation which maps  $$ V $$ into itself,then the set of elements  $$ u $$ in V satisfying  $$ \langle u,u  \rangle=1 $$ is called the unit sphere of  $$ V $$

It's easy to 'picture' all of this so I'll move on to the main theorem

## Theorem

Let   $$ Q(x)=\langle T(x),x \rangle $$ be the quadratic form associated with a symmetric linear transformation  $$ T:V \mapsto V $$  on a real Euclidean space where  $$ V $$ is finite dimensional.Assume that there exists an element  $$ u $$ in  $$ V $$  such that  $$ Q(u) $$ lies in the unit sphere and is an extremum with  $$ \langle u,u \rangle=1 $$.Then, $$ u $$ is an eigenvector for  $$ T $$.

It quickly follows that  $$ Q(u) $$ is the corresponding eigenvalue.

## Proof

Assume first that  $$ Q $$ attains its maximum at  $$ u $$

This means that  $$ Q(x) \leq Q(u)  $$

 $$ \forall x | \langle x,x \rangle=1  $$       (1)

Let  $$ Q(u)=\lambda  $$.So,  $$ Q(u)=\lambda \langle x,x \rangle=\langle \lambda x,x \rangle $$ since  $$ \langle x,x \rangle=1 $$.

The inequality can be changed to  $$ \langle T(x),x \rangle \leq \langle \lambda x,x \rangle $$ when  $$ \langle x,x \rangle=1.     $$                            (2)

This result can be extended to all  $$ x $$ in  $$ V $$ by simply choosing x=ka where ||x||=k and ||a||=1(The proof is left to the reader)

The above inequality can be rewritten as:

 $$ \langle T(x)-\lambda x,x \rangle \leq 0 $$

Define  $$ S(x)=\langle T(x)- \lambda x,x \rangle $$.

This means that  $$ \langle S(x),x \rangle \leq 0 $$.     (3)

Also define  $$ Q'(x)=\langle S(x),x \rangle $$.From the inequalities (1),(2),it can be deduced that equality in (3) holds if x=u.

It is quite clear that  $$ Q'(x) \leq 0 $$ for all  $$ x $$ in  $$ V $$.Also,  $$ S $$ is symmetric.Therefore if  $$ Q'(u)=0 $$ then  $$ S(u)=0 $$(this can be simply proved by taking x=a+tb,expanding Q'(x) through linearity and finding the extreme points by equating the derivative of the obtained quadratic polynomial to 0 )

Therefore,  $$ T(u)=\lambda u $$-which proves the result