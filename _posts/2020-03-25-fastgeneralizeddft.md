---
layout: post
title: Fast Generalized DFT for finite groups
date: 2020-01-25
description: Group Cohomology
tags: algebra 
categories: cs math
giscus_comments: true
related_posts: false
featured: true
toc:
    sidebar: left
---

Almost 6 months ago, I came across an interesting update through the UT CS theory seminar group on the classic problem on the computation of the Discrete Fourier Transform(DFT) of finite groups. Chris Umans, from Caltech, made some pretty nice improvements to the complexity of the general DFT through some slick combinatorics , which I'll shortly explain. The paper is here.

# Introduction

Well, before I even start, perhaps, I should make some kind of a comment to motivate the problem at hand. A sequence of  $$ n $$ complex numbers  $$ (x_{i}) $$ can be represented by a function  $$ f:\mathbb{Z}_{n} \to \mathbb{C} $$.

A Discrete Fourier Transform of  $$ (x_{i}) $$ sends it to the sequence  $$ (F_{i}) $$ where  $$ F_{i}=\sum\limits_{j=0}^{n-1}x_{j}e^{\frac{-i2\pi k j}{n}} $$.

This motivates the definition of the Fourier transform  $$ \hat{f} $$ of a function from a finite group  $$ f : G \to \mathbb{C} $$ which takes as input a representation  $$ \rho:G \to GL(d_{\rho},\mathbb{C}) $$, i.e

 $$ \hat{f}(\rho)=\sum\limits_{g \in G} f(g)\rho(g) $$

where one must note that here, more generally,  $$ \rho(g) $$ can be matrix-valued.From Maschke's theorem, the DFT of a finite group reduces to a map which takes as input an element  $$ \alpha \in latex \mathbb{C}[G] $$(group ring consisting of all functions from  $$ G $$ to  $$ \mathbb{C} $$ under convolution)and sends it to  $$ \sum\limits_{g} \alpha(g) \bigoplus_{\rho \in Irr(G)}\rho(g) $$. Throughout, one assumes that we have already have the  $$ \rho $$ and chosen a basis for each  $$ \rho $$.

Quite simply, one trivially gets that this requires  $$ O(|G|^{2}) $$ operations. Exponent-one algorithms exist for abelian groups(as one would expect using the decomposition into cyclic groups), supersolvable and certain classes of symmetric and alternating groups.

Throughout the post, let  $$ \omega $$ be the exponent of matrix multiplication(currently it is around 2.38 I guess).

The main result is that Chris Umans achieves an operation complexity of  $$ O(|G|^{\frac{\omega}{2}} $$. Some basic facts from representation theory will be used throughout though I guess most readers would already be familiar with that. For example, it is easy to prove that through the Schur orthogonality relations is that  $$ \sum\limits_{i} |V_{i}|^{2}=|G| $$ where the  $$ V_{i} $$ is the set of all irreducible representations of  $$ G $$. This gives us the useful lemma.

## Lemma 1

For every real number  $$ \alpha \geq 2 $$,  $$ \sum\limits_{\rho \in Irr(G)} dim(\rho)^{\alpha} \leq |G|^{\frac{\alpha}{2}} $$(Proof omitted)

Some facts about the induced representation and Clifford theory are used but it shouldn't be too much of a hassle to discuss it on-the-fly.

## The Support Trick

Let  $$ G $$ be a group and  $$ S $$, a subset. Let's assume that we can caluclate the generalized DFT with respect to  $$ G $$ for all inputs  $$ \alpha \in \mathbb{C}[G] $$ supported on  $$ S $$(i.e components  $$ \alpha_{g}=0 $$ for  $$ g \not\in S $$) in  $$ m $$ operations. Surely, with some extra computational cost(involving the index of  $$ S $$), one can extend this to all inputs because if we can compute DFT supported on  $$ S $$ then we can compute DFT supported on  $$ Sg' $$ by multiplying   $$ \sum\limits_{g} \alpha(g) \bigoplus_{\rho \in Irr(G)}\rho(g) $$ by  $$ \bigoplus_{\rho \in Irr(G)} \rho(g') $$ which has an additional operation cost of  $$ \sum\limits_{\rho \in Irr(G)} O(dim(\rho)^{\omega+\epsilon} $$. We can apply Lemma 1,take appropriate number of 'shifts/translates' by elements of  $$ G $$ to get the following result(see Section 2.3):

## Theorem 1

If a generalized DFT can be computed with respect to  $$ G $$ for all inputs supported on  $$ S $$ in  $$ m $$ operations, then the generalized DFT with respect to  $$ G $$ can be computed for all inputs with operation count

 $$ O(m+|G|^{\frac{\omega}{2}+\epsilon})\frac{|G|log(|G|)}{|S|} $$

The aim is to use the subgroup structure in an attempt to reduce the operation complexity, which brings us to the main idea.

## The Subgroup Reduction

The initial results by Beth and Clausen on this topic dealt with the technique of single subgroup reduction. Let  $$ H \leq G $$ be a subgroup. The main idea is that we calculate  $$ |G:H| $$ many DFTs with respect to  $$ H $$ and lift all these to  $$ G $$ recursively. Note that any irreducible representation  $$ \sigma \in Irr(H) $$ can be obtained as a restriction of an irreducible representation  $$ \rho \in Irr(G) $$.

To elaborate on this, let  $$ g_{1},\cdots,g_{t} $$ be the right coset representatives of  $$ H $$ in  $$ G $$. For any  $$ \alpha \in \mathbb{C}[G] $$, we can write  $$ \alpha=\sum\limits_{g \in G}\alpha_{g}g $$ as

 $$ \alpha=\sum\limits_{i=1}^{t}(\sum_{h \in H} \alpha_{h}^{i}h)g_{i} $$ where  $$ \alpha^{i} \in \mathbb{C}[H] $$. Next, we perform DFT with respect to  $$ H $$ for each  $$ i $$ to get the quantities:

 $$ s_{i}=\sum\limits_{h \in H} \alpha_{h}^{i} \bigoplus_{\sigma \in Irr(H)} \sigma(h) $$. We can lift this to  $$ \bar{s_{i}}=\sum\limits_{h \in H} \alpha_{h}^{i} \bigoplus_{\rho \in Irr(G)} \rho(h) $$ as  $$ Res_{H}^{G}(\rho) $$ decomposes into a sum of elements of  $$ Irr(H) $$. There is no extra computational cost(copying is not counted for some technical reasons) if we assume that we have an  $$ H-adapted $$ basis, i.e a choice of basis for each  $$ \rho \in Irr(G),\rho(h) $$ is a block diagonal matrix with blocks of sizes equal to the dimensions of the irreducible representations of  $$ H $$ for all  $$ h \in H $$

We wish to calculate  $$ \sum\limits_{g \in G}\alpha_{g}g $$ which is simply  $$ \sum\limits_{i=1}^{t}\bar{s_{i}}.( \bigoplus_{\rho \in Irr(G)} \rho(g_{i}) ) $$.

There are  $$ t $$ matrix multiplications of block-diagonal matrices and hence if we denote by  $$ d(\sigma,\rho) $$ the multiplicity of the irrep  $$ \sigma \in Irr(H) $$ in  $$ Res(\rho) $$ for  $$ rho \in Irr(G) $$, we get the count of performing one such multiplication to be:

 $$ \sum\limits_{\sigma \in Irr(H)} \sum\limits_{\rho \in Irr(G)} d(\sigma,\rho) O(dim(\sigma)^{\omega+\epsilon}) \frac{dim(\rho)}{dim(\sigma)} $$ which evaluates to  $$ \sum\limits_{\sigma \in Irr(H)} O(dim(\sigma)^{omega+\epsilon})[G:H] $$ through Frobenius reciprocity, specifically we see that  $$ \sum_{\rho \in Irr(G)} d(\sigma,\rho) dim(\rho) $$ is the dimension of  $$ Ind_{H}^{G}(\sigma) $$. See Theorem 3 of this paper.

Now, we do  $$ [G:H]=t $$ of these multiplications followed by taking the sum which involves  $$ [G:H]|G| $$ operations since there are atmost  $$ |G| $$ non-zero entries in the block diagonals(note that this follows from sum-of-squares equation in the introduction). So, the total cost is

 $$ [G:H]|G|+[G:H]^{2}\sum\limits_{\sigma \in Irr(H)} O(dim(\sigma)^{\omega+\epsilon}) $$. Using Lemma 1(see proof below), we get the following theorem

## Theorem 2

Let  $$ H \leq G $$ be a subgroup, then one can compute a DFT with respect to  $$ G $$ in operation count of  $$ [G:H] $$ DFTs with respect to  $$ H $$ plus  $$ O([G:H]^{2}|H|^{\frac{\omega}{2}+\epsilon} $$

### Proof of Theorem 2:

We've got most of it down. Since  $$ \omega>2 $$, we can use Lemma 1, to get the upper bound  $$ \sum_{\sigma \in Irr(H)} sim(\sigma)^{\omega+\epsilon} \leq |H|^{\frac{\omega}{2}+\epsilon} $$. Now  $$\frac{\omega}{2} >1 $$, so we the upper bound  $$ [G:H]|G|=[G:H]^{2}|H|\leq [G:H]|H|^{\frac{\omega}{2}+\epsilon} $$, this gives as a  $$ O([G:H]^{2}|H|^{\frac{\omega}{2}+\epsilon}) $$ upper bound on the total cost calculated above.

The remaining problem is that we have not stipulated a  $$ H- $$adapted basis. We can convert an arbitrary basis to an  $$ H- $$adapted basis at a cost of  $$ \sum_{\rho \in Irr(G)} O(dim(\rho)^{\omega+\epsilon}) \leq O(|G|^{\frac{\omega}{2}+\epsilon}) using Lemma 1. This is the same bound as the one above for the total cost which proves the theorem.

Using this result, it is not too hard(again, see Theorem 5 of the paper) to get the weaker  $$ 1+\frac{\omega}{4} $$ bound for generalized DFT using induction and Lev's theorem(which guarantees the existence of a subgroup of order atleast  $$ |G|^{\frac{1}{2}} $$)

## Double Subgroup Reduction

If  $$ H,K \leq G $$ are two subgroups, we reduce the problem of computing the DFT with respect to  $$ G $$ to computing it with respect to  $$ H $$ and  $$ K $$.

It is quite easy to see that  $$ H,K $$ are subgroups of  $$ G $$ and  $$ \alpha \in \mathbb{C}[G] $$ supported on  $$ HK $$ and given a fixed way of expressing every  $$ g \in HK $$ as  $$ g=hk $$(not necessarily unique), then one can compute:

 $$ \sum\limits_{g=hk \in HK}\alpha_{g} \bigoplus_{\sigma \in Irr(H),\tau \in Irr(K)}\sigma(g) \otimes \tau(g) $$ with  $$ |H| $$ K-DFTs and  $$ |K| $$ H-DFTs.

The extra computation cost is proportional to  $$ \frac{|G|}{|HK|} $$ and  $$ |H \cap K $$(roughly if one assumes  $$ \omega $$ is close to  $$ 2 $$). The details can be found in either of the papers. This  $$ HK $$ can be translates appropriately(through a probabilistic argument) to get the overhead cost(which will naturally include a  $$ log(|G|) $$ factor). This prevents the pure  $$ \frac{\omega}{2} $$ exponent that is the ultimate goal. This is dealt with using the new technique of 'Triple subgroup reduction' which I'll discuss shortly. I'll state the main theorem for the double subgroup reduction method below:

## Theorem 3:

If  $$ H,K \leq G $$ then the total cost of computing a DFT with respect to  $$ G $$ is

O((|H| K-DFTs+|K| H-DFTs+ $$ |G|^{\frac{\omega}{2}+\epsilon}+(|H||K|)^{\frac{\omega}{2}}\frac{|G|}{|HK|}log(|G|)) $$

(Proof ommited. See section 3(Theorem 12) of this paper by Umans.)

So, to reiterate, the H K-DFTs +K H-DFTs part is obtained through the simple procedure sketched out in the start of this section. The outer  $$ \frac{|G|}{|HK|}log(|G|) $$ is obtained through a simple probabilistic argument of sliding  $$ HKx $$-DFTs with respect to coset representatives  $$ x \in [G:HK] $$. The remaining quantity comes from a series of matrix multiplication and change of basis matrices.

Umans obtains the golden  $$ \frac{\omega}{2} $$ exponent for solvable groups and finite groups of Lie type through this technique.

## Triple subgroup reduction

This bottleneck is overcome by considering the case when  $$ H \cap K=N $$ is normal in  $$ G $$. Some structural group-theoretic theorems that I'll introduce later ensure that this choice is possible. This technique will allow us to get rid of the overhead cost. In the calculation of the intermediate representation  $$ \sum\limits_{g=hk \in HK}\alpha_{g} \bigoplus_{\sigma \in Irr(H),\tau \in Irr(K)}\sigma(g) \otimes \tau(g) $$ needed for the double subgroup reduction method, for the first step, we calculate

 $$ s_{k}=\sum\limits_{h \in H}\alpha_{hk} \bigoplus_{\sigma \in Irr(H)} \sigma(h) $$ for  $$ k \in K' $$, the coset representatives of the subgroup  $$ H $$ in  $$ G $$. The idea of the triple subgroup reduction is that we can write these  $$ s_{k} $$ as a sum of  $$ |N| $$ matrices with the kind of structure that we'll describe in the main theorem. But before that, I must segue into some facts from representation theory since when we're dealing with representations involving normal subgroups, Clifford theory is important.

## A Short Interlude

Consider a normal subgroup  $$ N \unlhd G $$. Consider  $$ Irr(N) $$ and some  $$ \sigma \in Irr(N) $$, then one can obtain a  $$ G-action $$ on  $$ Irr(N) $$ by conjugating the input, more precisely,

 $$ \sigma(n) \mapsto (g.\sigma)(n):=\sigma(gng^{-1}) $$. The thing could naturally be said of the irreducible character. Let  $$ O_{1},\cdots,O_{l} $$ be the orbits of this  $$ G-action $$. If  $$ \rho \in Irr(G) $$, then we can consider  $$ Res_{N}^{G}(\rho) $$ which breaks up into a some of irreducibles in  $$ Irr(N) $$.

## Theorem 4(Clifford's Theorem):

Let  $$ \rho \in Irr(G) $$. Then,

 $$ Res_{N}^{G}(\rho) \simeq e_{\rho}\bigoplus_{\sigma \in O_{i_{\rho}}}\sigma $$ such that  $$ e_{\rho},|O_{i_{\rho}}| $$ divide  $$ [G:N] $$. Additionally, note that all the irreducible representations in the orbit have the same dimension  $$ d_{\rho} $$ and hence  $$ dim(\rho)=d_{\rho}e_{\rho}|O_{i_{\rho}}| $$

Proof omitted(see wiki)


Some stronger divisibility statements could be made on  $$ e_{\rho} $$ and the orbit size  $$ |O_{i_{\rho}}| $$ but it doesn't really matter in our case.

What is really important is that for  $$ \rho \in Irr(G),Res_{N}^{G}(\rho) $$ is completely determined(upto constant) by the orbit  $$ O_{i_{\rho}} $$. Thus, we can partition  $$ Irr(G) $$ into  $$ [S_{k}] $$ where  $$ k $$ corresponds to  $$ O_{k} $$. Through a simple calculation(see below), we get the following useful lemma.

## Lemma 2:

 $$ \sum\limits_{\rho \in S_{k}} sim(\rho)\frac{e_{\rho}}{d_{\rho}}=[G:N] $$

### Proof of Lemma 2:

By definition of the induced representation  $$ Ind_{N}^{G}(\sigma),dim(Ind_{N}^{G}(\sigma))=dim(\sigma)\frac{|G|}{|N|} $$. For  $$ \rho \in Irr(G) $$,let  $$ q(\rho,\sigma) $$ be the number of times  $$ \rho $$ appears in  $$ Ind_{N}^{G}(\sigma) $$, then by decomposition into irreducibles, we get:

 $$ \sum\limits_{\rho \in Irr(G)} dim(\rho)q(\rho,sigma)=dim(\sigma)\frac{|G|}{|N|} $$

Using Frobenius reciprocity,  $$ q(\rho,\sigma)=d(\sigma,\rho) $$(number of times  $$ \sigma $$ appears in  $$ Res_{N}^{G}(\rho) $$). Notice that this  $$ d(\sigma,\rho) $$ is exactly  $$ e_{\rho} $$. The terms in the sum not in the associated orbit become zero and the result follows.

## Inverse DFT

In the notation of Umans, we'll define the inverse DFT when we're given a representation  $$ \rho \in Irr(G) $$. It will take as input, a square matrix  $$ M^{\rho} $$ of order  $$ dim(\rho) $$ and return an element  $$ \alpha \in \mathbb{C}[G] $$ such that:

 $$ \sum\limits_{g \in G} \alpha_{g} \bigoplus_{\rho \in Irr(G)} \rho(g)=M^{\rho} $$

Thankfully, the DFT calculation has a relatively easy computational count from this theorem of Beth-Clausen.

## Lemma 3(Inverse DFT theorem)

If the DFT with respect to  $$ G $$ can be computed in  $$ m $$ operations then the inverse DFT with respect to  $$ G $$, in the same basis, can be computed in atmost  $$ m+|G| $$ operations.

Proof omitted(see Theorem 2.6 from the paper)

Next, we need a technical lemma regarding matrix multiplication.

## Lemma 4:

Let  $$ A $$ be a  $$ p \times q $$ matrix,  $$ B $$, a  $$ q \times r $$ matrix and  $$ C $$, a  $$ r \times t $$ matrix. Then,

 $$ ABC=arr_{p,r}((A \otimes C^{T}).vec(B)) $$ where  $$ vec(B) $$ is the  $$ qr $$-size column vector obtained by traversing the rows of  $$ B $$ and  $$ arr_{p,r} $$ converts the  $$ pr- $$size column into a  $$ p \times r $$ matrix.

Proof is omitted. It is slightly fun to work it out though. See Lemma 7 from the paper.

## Theorem 5:

Let  $$ N \unlhd G $$ and for any  $$ \rho \in Irr(G) $$,  $$ d_{\rho},e_{\rho} $$ be the associated quantities obtained from Clifford's theorem. For any  $$ M=\bigoplus_{\rho \in Irr(G)} M^{\rho} $$(where  $$ M^{\rho} $$ is a  $$ dim(\rho) $$-order square matrix), there exists, with respect to an  $$ N- $$adapted basis, matrices  $$ M_{n}^{\rho} $$ of size  $$ dim(\rho)/d_{\rho} \times e_{\rho} $$ which satisfies:

 $$ \sum\limits_{n \in N} (M_{n}^{\rho} \otimes \underbrace{(I_{d_{\rho}}|\cdots|I_{d_{rho}}}_{|O_{i_{\rho}}|}).\rho(n)=M^{\rho} $$(note that  $$ A|B $$ is row notation,i.e  $$ A,B $$ are rows).

where the matrix  $$ I_{d_{\rho}}|\cdots|I_{d_{rho}} $$ has size  $$ d_{\rho} \times \frac{dim(\rho)}{e_{\rho}} $$

Moreover, these  $$ M_{n}^{\rho} $$ can be chosen in such that there exist unique labellings  $$ \beta^{l} $$ for each  $$ l $$ of the entries of the set of matrices  $$ M_{n}^{\rho} $$ for all  $$ \rho \in S_{l} $$ such that if

 $$ \beta_{\rho_{1};i,j}^{l}=\beta_{\rho_{2};i,j}^{l'} \Rightarrow M_{n;i,j}^{\rho_{1}}=M_{n;i,j}^{\rho_{2}} $$ for all  $$ n \in N $$(here,  $$ \beta_{\rho;i,j}^{l} $$ represents the  $$ (i,j) $$ entry of the matrix  $$ M_{n}^{\rho} $$ where  $$ \rho \in S_{l} $$)

the number of labels(unique by definition) is  $$ r=O(|G/N|log(|G/N|) $$. Additionally, these  $$ M_{n}^{\rho} $$ can be obtained  $$ r $$ DFTs with respect to  $$ N $$.

### Proof of Theorem 5:

Phew!That's quite a long statement. The last paragraph of the statement is a kind-of convoluted matrix combinatorics game where we are trying to convert the block-matrix diagonal  $$ \bigoplus_{\rho \in Irr(G)}M^{\rho} $$ into something of a simpler form involving a block-matrix diagonal where the blocks are of size  $$ 2^{k} $$(I'll explain this soon). This will enable us to proceed with the lifting the intermediate DFT to a full DFT. Now, to get back to the proof,

Since we have an  $$ N- $$adapted basis, the  $$ \rho(n) $$ is of the form  $$ I_{e_{\rho}} \otimes \bigoplus_{\lambda \in O_{l}} \lambda(n) $$.We'll solve for  $$ M_{n}^{\rho} $$ by a sequence of steps:

First, we have  $$ \sum\limits_{n \in N} (M_{n}^{\rho} \otimes \underbrace{(I_{d_{\rho}}|\cdots|I_{d_{rho}})}_{|O_{i_{\rho}}|}. \rho(n)=\sum\limits_{n \in N} M_{n}^{\rho} \otimes (\lambda_{1}|\cdots|\lambda_{|O_{l}|}) $$

Note that the  $$ \lambda_{i} $$ above span the entire vector space  $$ \mathbb{C}^{d_{\rho} \times \frac{dim(\rho)}{e_{\rho}}} $$. I leave it to the reader to verify that the equation

 $$ \sum\limits_{n \in N} M_{n;i,j}^{\rho}(\lambda_{1}|\cdots|\lambda_{|O_{l}|})=

\begin{bmatrix}

M_{i,j.|O_{l}|}^{\rho} \\

\vdots \\

M_{i,j.|O_{l}|+|O_{l}|-1}

\end{bmatrix}

 $$

(*)

can be solved for  $$ M_{n}^{\rho} $$ for all  $$ \rho \in Irr(G) $$(note that the above hint only gives a solution to the  $$ \rho \in O_{l} $$; one just combines the solutions simultaneously) by an inverse DFT with respect to  $$ N $$ where the input is the  $$ M^\rho $$ given to us.

Now, to deal with the last paragraph of the statement. The important thing is the number  $$ r $$. Assume for now that such a labelling exists(we'll show what it is after that). I'd like to pass off a few comments as to what is going on before proceeding.

Trivially , we can take  $$ \beta^{l} $$ to be a unique labelling for every  $$ \rho \in S_{l} $$ and obviously easily ensure that  $$ \beta^{l'} $$ is completely distinct for all  $$ \rho \in S_{l'} $$. This would be give a trivial  $$ r=|G/N|(\textbf{#} S_{k}) $$ from Lemma 2. The point is that we have to minimize this  $$ r $$ as we have to perform  $$ r $$ inverse DFTs(computationally almost as easy as DFT) with respect to  $$ N $$. Getting back into the proof,

It is actually simple, if the labelling  $$ \beta_{\rho_{1};i,j}^{l} $$ and  $$ \beta_{\rho_{2};i,j}^{l'} $$ are equal, say  $$ T $$(by the condition on the labellings, this means that the  $$ (i,j) $$ entry of  $$ M_{n}^{\rho_{1}} $$ and  $$ M_{n}^{\rho_{2}} $$ are equal where  $$ \rho_{1} \in S_{l} $$ and  $$ \rho_{2} \in S_{l'} $$), then the associated  $$ \lambda_{1},\cdots,\lambda_{|O_{l}|} $$ and  $$ \lambda_{1}^{'},\cdots,\lambda_{|O_{l'}|}^{'} $$ from the two equation of the form (*) above are distinct! Replace the  $$ M_{n;i,j}^{\rho} $$ by the label  $$ T=\beta_{\rho_{1};i,j}^{l}=\beta_{\rho_{2};i,j}^{l'} $$ and simply append the  $$ \lambda_{1}^{'},\cdots,\lambda_{|O_{l'}|}^{'} $$ to  $$ (\lambda_{1}|\cdots|\lambda_{|O_{l}|}) $$ and get  $$ T $$ by an inverse DFT with respect to  $$ N $$.

Hence, we need only  $$ r $$ DFTs with respect to  $$ N $$ to get the matrices  $$ M_{n}^{\rho} $$ for all  $$ n \in N $$ and  $$ \rho \in Irr(G) $$ if we have such a labelling.

What's the labelling:

Consider any random block-diagonal matrix  $$ W $$ of the form:

 $$ 2|G/N| $$ block matrices of order  $$ 1 $$

 $$ \lceil 2\frac{|G/N|}{4} \rceil $$ block matrices of order  $$ 2 $$

 $$ \cdots $$

 $$ \lceil 2\frac{|G/N|}{2^{2i}} \rceil $$ block matrices of order  $$ 2^{i} $$

 $$ \cdots $$

 $$ 2 $$ block matrices of order  $$ 2^{\lceil{log_{2}(|G/N|)} \rceil} $$

You can let also let the non-zero entries of  $$ W $$ be distinct if you want to equivalently think of a mapping to actual values instead of positions in a matrix.

Let's say that every column in this matrix is 'unoccupied'.

The domain of the labelling  $$ \beta^{l} $$ is  $$ \bigoplus_{\rho \in S_{l}} \bigoplus_{n \in N}M_{n}^{\rho} $$ represented as a block diagonal matrix. We define  $$ \beta_{l} $$, for every column in the domain of height  $$ w $$(number of non-zero entries), we find  $$ i $$ such that  $$ 2^{i-1}<w\leq 2^{i} $$ and associate to this column of height  $$ w $$, the first unoccupied column of size  $$ 2^{i} $$ top-down. Of course, as one can easily see, there might be some elements in the target matrix  $$ W $$ not associated to anything in the domain. Call this column occupied. How do we know we have enough columns?

There can be atmost  $$ \frac{|G/N|}{w}<\frac{|G/N|}{2^{i-1}} $$ columns of height  $$ w $$ in the the domain since there  $$ |G/N| $$ entries in total(see Lemma 2).

Now, it is easy to check that are atleast  $$ \frac{|G/N|}{2^{i-1}} $$ columns in  $$ W $$ of height  $$ 2^{i} $$ in  $$ W $$.

This entire procedure is just a kind of rearrangement of the domain for efficient lifting to a  $$ DFT $$ with respect to  $$ G $$. This constructions allows us to define the parent matrix/rearranged matrix of  $$ \bigoplus_{\rho \in S_{l}} \bigoplus_{n \in N}M_{n}^{\rho} $$ with respect to the labelling  $$ \beta^{l} $$ as the matrix having same size as  $$ W $$, above, but with entries replaced by the respective entry of  $$ M_{n}^{\rho} $$ if there is a associated labelling to that entry and zero otherwise.

## The Finale

Everything is essentially setup now. Don't worry, we've already played the game. The rules have just changed a bit. After some combinatorial hacks, we got what is needed,  $$ r=O(|G/N|log(|G/N|) $$. Though here, we'll replacing that  $$ G $$ by a subgroup

 $$ G $$ is a subgroup.  $$ H,K $$ are subgroups such that  $$ H \cap K=N \unlhd G $$.  $$ X $$ is the set of coset representatives of  $$ N $$ in  $$ H $$ and  $$ Y $$ is the set of coset representatives of  $$ N $$ in  $$ K $$. Again, through some structural group-theoretic results,we'll later see that  $$ \frac{|G|}{|HK|} $$ is negligible in a certain sense.

Through some simple arguments(strongly recommend seeing  Lemma 3.7 in the paper), we see that if  $$ \alpha \in \mathbb{C}[G] $$ is supported on  $$ HK $$, consider the calculation

 $$ \sum\limits_{n \in N}\sum\limits_{y \in Y}\bigoplus_{\tau \in Irr(K)}P_{n,y} \otimes \tau(ny)^{T} $$ where  $$ P_{n,y} $$ is the parent matrix associated to  $$ /{M_{n,y}^{\sigma}: \sigma \in Irr(H) /} $$ which satisfy

 $$ \sum\limits_{n \in N}(M_{n,y}^{\sigma} \otimes \underbrace{(I_{\sigma}|\cdots|I_{\sigma})}{|O_{i_{\sigma}}|}\sigma(n)=\sum\limits_{h \in H}\alpha_{hy}\sigma(h) $$

with respect to an  $$ N- $$adapted basis for  $$ Irr(H) $$.

Then, the above calculation can computed with  $$ |Y| $$ DFTs with respect to  $$ H $$+ $$ O(|H/N|log(|H/N|)|K| $$ inverse DFTs with respect to  $$ N $$+ $$ O(|H/N\log(|H/N|) $$ DFTs with respect to  $$ K $$.

Now, it remains to see how one can lift this to a DFT with respect to  $$ G $$. Let  $$ S $$, $$ T $$ be the change of basis matrices corresponding to  $$ Res_{H}^{G} $$, $$ Res_{K}^{G} $$, i.e

 $$ S(\bigoplus_{\sigma \in Irr^{*}(H)}\sigma(h))S^{-1}=\bigoplus_{\rho \in Irr(G)} \rho(h) $$ for all  $$ h \in H $$ where  $$ Irr^{*}(H) $$ is the set of irreducible representations of  $$ H $$ that appear in the restrictions of the irreducible representations of  $$ G $$, counted with multiplicity.

Similarly, for  $$ T $$. We also require that the basis change is one which is  $$ N- $$adapted with respect to  $$ Irr(H) $$. Also, for  $$ n \in N=H \cap K $$, we have

 $$ (\bigoplus_{\sigma \in Irr^{*}(H)}\sigma(n))S^{-1}T=S^{-1}T(\bigoplus_{\tau \in Irr^{*}(K)} \tau(n) $$ for all  $$ n \in N $$.

(1)

Consider  $$ \alpha \in \mathbb{C}[G] $$ supported on  $$ HY=HK $$ then we can split up the  $$ G- $$DFT on  $$ \alpha $$ as follows:

 $$ \sum\limits_{h \in H,y \in Y} \alpha_{hy} \bigoplus_{\rho \in Irr(G)}\rho(hy)=

\sum\limits_{y \in Y}(\sum\limits_{h \in H}\alpha_{hy} \bigoplus_{\rho \in Irr(G)}\rho(h)).(\bigoplus_{\rho \in Irr(G)}\rho(y) $$

which can be rewritten using  $$ S,T $$ as:

 $$ \sum\limits_{y \in Y}S(\sum\limits_{h \in H}\alpha_{hy} \bigoplus_{\sigma \in Irr^{*}(H)}\rho(h))S^{-1}T(\bigoplus_{\tau \in Irr^{*}(K)}\tau(y))T^{-1} $$

By the discussion above and using equation (1) above, we can further rewrite this as:

 $$ \sum\limits_{y \in Y}S(\sum\limits_{n \in N} \bigoplus_{\sigma \in Irr^{*}(H)}(M_{n,y}^{\sigma} \otimes \underbrace{(I_{\sigma}|\cdots|I_{\sigma})}{|O_{i_{\sigma}}|} )S^{-1}T(\bigoplus_{\tau \in Irr^{*}(K)}\tau(ny))T^{-1} $$

Consider the quantity  $$ K= (\sum\limits_{n \in N} \bigoplus_{\sigma \in Irr^{*}(H)}(M_{n,y}^{\sigma} \otimes \underbrace{(I_{\sigma}|\cdots|I_{\sigma})}{|O_{i_{\sigma}}|} ) $$ which is in the sum above. Using Lemma 4, calculating  $$ K $$ is equivalent to calculating:

 $$ (\bigoplus_{\sigma \in Irr^{*}(H),\tau \in Irr^{*}(K)} (M_{n,y}^{\sigma} \otimes (I_{\sigma}|\cdots|I_{\sigma})) \otimes \tau(ny)^{T})).vec(S^{-1}T) $$

There are repetitions in the tensor product structure(both sides) of the  $$ \bigoplus $$ on the left hand side and this can be appropriately changed by shifting the entries of  $$ vec(S^{-1}T) $$ to a block structure(for more info, see section 3.3 of the paper). So, finally, calculating  $$ K $$ is equivalent to calculating,

 $$ (\bigoplus_{\sigma \in Irr(H),\tau \in Irr(K)} M_{n,y}^{\sigma} \otimes \tau(ny)^{T})).X $$

where  $$ X $$ is a block-diagonal matrix whose entries are sums of entries in  $$ S^{-1}T $$

Let  $$ P_{n,y} $$ be the parent matrix of  $$ \{M_{n,y}^{\sigma} \} $$. So, in the expression above, we can replace  $$ \bigoplus_{\sigma \in Irr(H)} $$ by  $$ P_{n,y} $$ and see that we have to calculate:

 $$ K'=(\bigoplus_{\tau \in Irr(K)}P_{n,y} \otimes \tau(ny)^{T}).X' $$ where  $$ X' $$ has the 'same data'(see the paper for more info;honestly, I am not sure how to easily express it;the less one says of these matrix combinatorics, maybe the better) as  $$ S^{-1}T $$. We've rearranged all the  $$ M_{n,y}^{\sigma} $$ above into the parent matrix and so we'd have to appropriately move around the elements of  $$ X' $$. Using the earlier facts of representation theory, namely,  $$ \sum\limits_{\tau \in Irr(K)}dim(\tau)^{2}=|K| $$ and that the blocks in the parent matrix have blocks of orders of the form  $$ 2^{k} $$ such that the the sum of squares of the block sizes(not necessarily total number of non-zero elements) is  $$ O(|H/N|log(|H/N|) $$. So, the square blocks of  $$ \bigoplus_{\tau \in Irr(K)}P_{n,y} \otimes \tau(ny)^{T} $$ have dimensions  $$ a_{i} $$ which satisfy  $$ \sum\limits_{i} a_{i}^{2}=O(|H/N|log(|H/N|))|K| $$




















