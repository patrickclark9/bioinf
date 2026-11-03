---
title: "NMF In Depth"
tags:
  - linear-algebra
  - machine-learning
  - NMF
source: "https://chatgpt.com/share/6ae21bbb-e08c-83eb-be5d-d22646ecfbd3"
---

# Non-Negative Matrix Factorization (NMF): In-Depth Explanation

**Non-Negative Matrix Factorization (NMF)** is a dimensionality-reduction technique that decomposes a non-negative matrix into the product of two smaller, non-negative matrices.

Its main idea is that **complex observations can be represented as additive combinations of a small number of underlying patterns**.

Unlike PCA or SVD, NMF imposes non-negativity, which often makes the resulting components easier to interpret.

We'll explore its mathematical definition, geometric interpretation, optimization, relationship to SVD and PCA, and practical applications.

## 1. Mathematical definition

Suppose we have a data matrix

$$
X\in\mathbb R_{\geq0}^{m\times n}
$$

where:

- $m$ = number of observations (e.g., biological samples).
- $n$ = number of features (e.g., gene-expression measurements).

NMF seeks two matrices:

$$
\boxed{X\approx WH}
$$

with

$$
W\in\mathbb R_{\geq0}^{m\times k}
$$

$$
H\in\mathbb R_{\geq0}^{k\times n}
$$

where $k$ is the number of latent components, usually much smaller than $m$ and $n$.

### What do W and H represent?

In the sample-by-feature convention:

- **$W$** represents how strongly each observation expresses each latent component.
- **$H$** describes which features characterize each component.

Consider a gene-expression dataset with 100 patients and 5,000 genes.

$$
X_{100\times5000}\approx W_{100\times3}H_{3\times5000}
$$

Here, $k=3$ indicates that we're approximating each patient's gene-expression profile using just three underlying expression programs.

For instance, the components might represent cell proliferation, immune activity, and metabolism.

Importantly, NMF does not know these biological meanings in advance. They are interpretations assigned after examining the features associated with each component.

## 2. NMF as a matrix mapping

Since you've been studying matrices as linear maps, this is an especially useful connection.

Recall that for a matrix

$$
A\in\mathbb R^{m\times n}
$$

we can interpret

$$
A:\mathbb R^n\rightarrow\mathbb R^m
$$

as a linear transformation.

Now consider

$$
X\approx WH
$$

The dimensions imply the mapping composition

$$
\mathbb R^n
\xrightarrow{H}
\mathbb R^k
\xrightarrow{W}
\mathbb R^m
$$

So $H$ maps a vector from the original $n$-dimensional space into a $k$-dimensional space, and $W$ maps it back into $\mathbb R^m$.

There is an important qualification: **NMF is fundamentally a factorization of a data matrix, rather than an automatically learned encoder–decoder pair**. Although the matrix product can be interpreted as a composition of linear maps, $H$ is not necessarily a feature-to-latent encoding operator for new observations.

For the sample-by-feature convention, a more intuitive interpretation comes from considering each row of $X$.

For observation $i$:

$$
\boxed{x_i\approx\sum_{a=1}^{k}W_{ia}H_{a,:}}
$$

Thus, each observation is approximated as a linear combination of the rows of $H$.

Because every coefficient is non-negative, this is an **additive representation**.

## 3. Geometric interpretation

NMF is best understood geometrically as finding a set of non-negative building blocks whose combinations approximate the observations.

Suppose we have two-dimensional observations.

If the two basis vectors are $h_1$ and $h_2$, NMF approximates an observation $x$ as

$$
x\approx a h_1+b h_2
\qquad a,b\geq0
$$

The vectors span a **convex cone**, not necessarily the entire plane.

This is a major difference from ordinary linear combinations.

With unconstrained coefficients, we can add or subtract vectors:

$$
x=ah_1+bh_2,\qquad a,b\in\mathbb R
$$

But in NMF:

$$
a,b\geq0
$$

Therefore, we cannot subtract one latent component from another. We can only add non-negative amounts of each component.

This is why NMF often produces a parts-based representation.

### Connection with span and rank

We know that

$$
\operatorname{rank}(WH)\leq \min(\operatorname{rank}(W),\operatorname{rank}(H))\leq k
$$

Therefore, $WH$ is at most a rank-$k$ matrix.

If $k$ is small, we are approximating a high-dimensional data matrix using a low-rank structure.

However, there is a subtle distinction between ordinary rank and non-negative rank:

$$
\operatorname{rank}(X)\leq \operatorname{rank}_+(X)
$$

where $\operatorname{rank}_+(X)$ is the smallest $k$ for which an exact non-negative factorization exists.

A matrix can have ordinary rank 3 but require more than three non-negative factors for an exact decomposition.

So NMF is not simply ordinary low-rank factorization with a cosmetic positivity constraint. The constraint changes the mathematical problem.

## 4. A numerical example

Consider three samples measured across three genes:

$$
X=
\begin{pmatrix}
5&4&0\\
0&1&5\\
5&5&5
\end{pmatrix}
$$

Suppose these observations are generated by two expression patterns:

$$
H=
\begin{pmatrix}
1&1&0\\
0&0.2&1
\end{pmatrix}
$$

And each sample has the following component weights:

$$
W=
\begin{pmatrix}
5&0\\
0&5\\
5&5
\end{pmatrix}
$$

Their product is

$$
WH=
\begin{pmatrix}
5&5&0\\
0&1&5\\
5&6&5
\end{pmatrix}
$$

This is close to $X$, although not exact.

We can interpret the components as follows:

- Component 1 is associated with genes 1 and 2.
- Component 2 is associated primarily with gene 3, with a small contribution from gene 2.
- Sample 1 predominantly expresses component 1.
- Sample 2 predominantly expresses component 2.
- Sample 3 expresses both components.

The approximation error is

$$
X-WH=
\begin{pmatrix}
0&-1&0\\
0&0&0\\
0&-1&0
\end{pmatrix}
$$

Consequently,

$$
\|X-WH\|_F^2=2
$$

This brings us to how NMF actually finds its factors.

## 5. The optimization problem

Unlike SVD, NMF does not generally have a closed-form global solution.

Instead, it is formulated as an optimization problem:

$$
\boxed{
\min_{W,H\geq0}\frac12\|X-WH\|_F^2
}
$$

Recall the Frobenius norm:

$$
\|A\|_F=\sqrt{\operatorname{tr}(A^\top A)}
$$

Therefore,

$$
\|X-WH\|_F^2
=\sum_{i=1}^{m}\sum_{j=1}^{n}(X_{ij}-(WH)_{ij})^2
$$

We want to find $W,H$ such that their product is as close as possible to the original data.

### Why is this difficult?

The problem is **not jointly convex** in $W$ and $H$.

To see why, notice that each element of the reconstruction contains products between unknown variables:

$$
(WH)_{ij}=\sum_{a=1}^kW_{ia}H_{aj}
$$

However:

- Holding $H$ fixed, optimization over $W$ is convex.
- Holding $W$ fixed, optimization over $H$ is convex.

This motivates alternating optimization.

### Alternating Non-Negative Least Squares (ANLS)

The algorithm proceeds by fixing one factor and optimizing the other.

$$
W^{(t+1)}
=\arg\min_{W\geq0}\|X-WH^{(t)}\|_F^2
$$

then

$$
H^{(t+1)}
=\arg\min_{H\geq0}\|X-W^{(t+1)}H\|_F^2
$$

Repeating these steps reduces (or leaves unchanged) the reconstruction objective when each subproblem is solved appropriately.

But this does not guarantee finding the global optimum.

### Multiplicative updates

A classical algorithm uses multiplicative updates:

$$
\boxed{
H\leftarrow H\odot
\frac{W^\top X}{W^\top WH}
}
$$

$$
\boxed{
W\leftarrow W\odot
\frac{XH^\top}{WHH^\top}
}
$$

where $\odot$ denotes elementwise multiplication and division is also performed elementwise.

For non-negative inputs and factors, these updates preserve non-negativity, assuming denominators are handled correctly.

These formulas come from the gradient of the squared-error objective:

$$
\nabla_H f=W^\top WH-W^\top X
$$

$$
\nabla_W f=WHH^\top-XH^\top
$$

A limitation is that multiplicative updates may converge slowly, and entries initialized exactly at zero tend to remain zero.

Modern software often uses coordinate descent or other constrained optimization algorithms.

## 6. Interactive intuition: combining latent components

The example below shows how a non-negative mixture of two gene-expression patterns changes as their weights change.

### Markdown version of the interactive mixture

The original visualization has two non-negative weight sliders. Their displayed values are $W_1=3.0$ and $W_2=2.0$.

G1–G4 are synthetic genes. Component 1 emphasizes G1/G2; component 2 emphasizes G3/G4.

$$
x=3.0h_1+2.0h_2
$$

All coefficients are non-negative, so there is no subtraction between patterns.

Increasing the first weight adds more of the first pattern, particularly its G1/G2 contributions; increasing the second adds more of the second pattern, particularly its G3/G4 contributions. Setting either weight to zero removes that component. Setting both to zero gives a zero profile. The contribution of each component scales linearly with its weight.

## 7. NMF vs PCA vs SVD

All three methods can be used to find low-dimensional structure in data, but they impose different mathematical conditions.

| Property | NMF | PCA | Truncated SVD |
| --- | --- | --- | --- |
| Non-negative input required | Yes | No | No |
| Non-negative factors | Yes | No | No |
| Orthogonal components | Not required | Yes | Yes, singular vectors |
| Components can subtract | No | Yes | Yes |
| Globally optimal rank-$k$ reconstruction | Not guaranteed | Yes, for centered data | Yes, in Frobenius norm |
| Interpretation | Additive building blocks | Directions of maximum variance | Dominant singular directions |

### NMF components are not orthogonal

Recall that PCA identifies orthogonal directions:

$$
v_i^\top v_j=0\quad(i\neq j)
$$

NMF imposes no such condition.

Two NMF components can overlap substantially in the features they represent.

For example, two biological pathways can share several genes. NMF permits these features to contribute to multiple components.

### NMF and the spectral theorem

Since you're also studying the spectral theorem, it helps to connect the ideas.

SVD relies on eigenvalue decompositions of the symmetric positive semidefinite matrices

$$
X^\top X,\qquad XX^\top
$$

The spectral theorem guarantees orthonormal eigenbases for these symmetric matrices.

This leads to

$$
X=U\Sigma V^\top
$$

Truncated SVD gives the optimal rank-$k$ approximation:

$$
X_k=U_k\Sigma_kV_k^\top
$$

in the Frobenius norm, by the Eckart–Young–Mirsky theorem.

NMF instead seeks

$$
X\approx WH,\qquad W,H\geq0
$$

Its factors are generally neither eigenvectors nor singular vectors, and there is no equivalent universal spectral decomposition that directly solves the NMF optimization problem.

### Visual comparison

- **NMF:** The basis directions bound a non-negative cone. Reconstructions combine these directions with non-negative coefficients; the directions need not be orthogonal.
- **PCA / SVD:** The component directions are orthogonal. Signed coefficients allow movement in either direction along each axis.

A particularly important point is that **PCA typically centers the data before decomposition**, whereas standard NMF does not, because centering would generally create negative values.

## 8. NMF is not unique

Suppose we find a factorization

$$
X\approx WH
$$

Let $D$ be any positive diagonal matrix.

Then

$$
WH=(WD)(D^{-1}H)
$$

Both new factors remain non-negative.

Therefore, the same reconstruction can be obtained with different component scales.

This is called scaling ambiguity.

There is also permutation ambiguity: we can reorder the components without changing the product.

More generally, NMF can admit distinct factorizations that are not just rescalings or permutations.

Consequently, NMF components are not automatically unique biological or physical entities.

For interpretable results, researchers often normalize the components, use multiple random initializations, and assess their stability.

## 9. Choosing the number of components $k$

The parameter $k$ is crucial.

A small $k$ produces a compressed, simpler representation but may lose important structure.

A large $k$ reconstructs the original data better but risks fitting noise or generating redundant components.

### Markdown version of the reconstruction-error chart

The original chart plots the number of components ($k=1$ through $8$) on the horizontal axis and illustrative reconstruction error on the vertical axis. It shows a decreasing curve with diminishing improvement: early components produce larger reductions, while later components add progressively smaller gains. An elbow marks a possible compromise between model complexity and reconstruction quality. The values are hypothetical, not results from a fitted model.

The approximation error cannot increase when the optimal allowed rank $k$ increases, since a model with more components can reproduce a smaller model by assigning zero weights to extra components.

In practice, we might consider:

- Reconstruction error and an elbow in the error curve.
- Stability of components over multiple random initializations.
- Biological interpretability or domain relevance.
- Cross-validation and held-out data performance.

There is no universally correct value of $k$.

## 10. Different loss functions

The squared Frobenius norm is not the only possible NMF objective.

The choice of loss reflects assumptions about the data.

### Euclidean NMF

$$
D_E(X\|WH)=\frac12\|X-WH\|_F^2
$$

Often associated with an additive Gaussian-noise model.

### Kullback–Leibler NMF

Generalized KL divergence:

$$
D_{KL}(X\|WH)=\sum_{ij}
\left[
X_{ij}\log\frac{X_{ij}}{(WH)_{ij}}
-X_{ij}+(WH)_{ij}
\right]
$$

with the conventional zero-value limits.

KL divergence can be appropriate for non-negative count-like measurements and is closely associated with Poisson modeling.

### Itakura–Saito NMF

$$
D_{IS}(X\|WH)
=\sum_{ij}
\left[
\frac{X_{ij}}{(WH)_{ij}}
-\log\frac{X_{ij}}{(WH)_{ij}}-1
\right]
$$

This divergence is scale-invariant and is widely used in audio and spectral decomposition contexts.

These objectives produce different solutions, even for the same data.

## 11. NMF for gene expression, proteomics, and metabolomics

NMF is particularly interesting in omics because many measurements are naturally non-negative.

Consider

$$
X=
\begin{pmatrix}
\text{sample 1 expression profile}\\
\text{sample 2 expression profile}\\
\vdots\\
\text{sample m expression profile}
\end{pmatrix}
$$

Each row contains measurements for $n$ genes.

With

$$
X\approx WH
$$

we obtain $k$ latent expression programs.

For example:

Hypothetical latent programs from NMF

| **Component** | **Highly weighted features** | **Possible interpretation** |
| --- | --- | --- |
| 1 | MKI67, TOP2A, PCNA | Proliferation |
| 2 | CD3D, CD8A, GZMB | Immune activity |
| 3 | HK2, LDHA, PFKP | Glycolytic activity |

Illustrative patterns, not an empirical NMF result.

For each patient, the corresponding row of $W$ gives the weights of these programs.

This allows us to compare samples according to latent biological patterns rather than thousands of individual features.

However, there are important practical considerations.

**Preprocessing:** Standardized z-scores and mean-centered data contain negative values, making them incompatible with standard NMF. Log-transformed positive data can be used, provided the resulting matrix is non-negative.

**Feature scaling:** Genes or proteins with much larger intensities may dominate a squared-error objective.

**Interpretation:** Components can reflect batch effects, sample composition, technical variation, or normalization artifacts rather than genuine biological processes.

**Sparsity:** Adding regularization can encourage each component to involve fewer features, potentially improving interpretation.

A typical regularized objective is

$$
\min_{W,H\geq0}
\frac12\|X-WH\|_F^2
+\lambda_W\|W\|_1
+\lambda_H\|H\|_1
$$

where $\lambda_W,\lambda_H$ control sparsity. Without normalization or other constraints, scaling ambiguity must also be considered when interpreting such penalties.

## 12. NMF vs clustering

NMF is related to clustering, but the two are not equivalent.

In conventional hard clustering, a sample belongs to exactly one cluster.

In NMF, a sample can express multiple components simultaneously.

For example:

$$
W_i=(0.7,\ 0.2,\ 0.1)
$$

might indicate that sample $i$ is predominantly associated with component 1 but also exhibits components 2 and 3.

These values are not automatically probabilities; a row of $W$ does not necessarily sum to one.

You can nevertheless obtain a hard assignment by taking the largest coefficient:

$$
\operatorname{cluster}(i)=\arg\max_a W_{ia}
$$

after choosing an appropriate scaling convention.

NMF is therefore especially useful when the underlying processes overlap.

## 13. Important mathematical properties

Here is a condensed summary connecting NMF to other linear algebra concepts you've been studying.

| Concept | Relationship to NMF |
| --- | --- |
| Matrix multiplication | $WH$ reconstructs the original matrix |
| Linear maps | The factorization represents a composition of compatible linear maps |
| Rank | $\operatorname{rank}(WH)\leq k$ |
| Column space | Columns of $WH$ lie in $\operatorname{Col}(W)$ |
| Row space | Rows of $WH$ lie in $\operatorname{Row}(H)$ |
| Frobenius norm | Common measure of reconstruction error |
| Orthogonality | Not required |
| Eigenvectors | NMF components generally are not eigenvectors |
| Convexity | Convex in each factor separately, not jointly |
| Uniqueness | Not guaranteed |

One additional mathematical point deserves attention.

Since

$$
X\approx WH
$$

we can expand the product as

$$
\boxed{
WH=\sum_{a=1}^{k}w_a h_a^\top
}
$$

where $w_a$ is column $a$ of $W$ and $h_a^\top$ is row $a$ of $H$.

Each term

$$
w_a h_a^\top
$$

is a rank-one non-negative matrix (unless one factor is zero).

Thus, **NMF approximates a matrix by adding together $k$ non-negative rank-one matrices**.

This is perhaps the most fundamental way to understand the decomposition.

## 14. Final intuition

Think of NMF as decomposing observations into reusable building blocks.

For example, if we measure the expression of 5,000 genes in 100 patients, NMF may identify several recurring gene-expression programs. Each patient is then described by the non-negative amount of each program present in their profile.

The difference from SVD is fundamental:

$$
\underbrace{X\approx U_k\Sigma_kV_k^\top}_{\text{SVD: optimal low-rank approximation}}
$$

versus

$$
\underbrace{X\approx WH,\quad W,H\geq0}_{\text{NMF: additive low-rank approximation}}
$$

**SVD finds the best low-rank approximation without sign constraints. NMF sacrifices that unconstrained optimality in pursuit of additive, potentially more interpretable components.**

The central insight is that NMF simultaneously performs dimensionality reduction and discovers latent patterns—but their scientific meaning, stability, and uniqueness must be evaluated rather than assumed.
