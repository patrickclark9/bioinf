---
title: Singular Value Decomposition (SVD)
tags:
  - linear-algebra
  - svd
  - pca
---

# Singular Value Decomposition (SVD)

**Singular Value Decomposition (SVD)** expresses any real matrix as the product of three matrices:

$$
\boxed{A=U\Sigma V^T}
$$

The central idea is that every linear transformation can be decomposed into a rotation or reflection, a scaling (including any change in dimension), and another rotation or reflection.

SVD works for **every matrix**, including rectangular and rank-deficient matrices. QR factorization also exists for every matrix; its simplest Gram–Schmidt construction assumes independent columns.

## 1. Geometric interpretation

Suppose $A\in\mathbb R^{2\times2}$ represents a linear map:

$$
A:\mathbb R^2\rightarrow\mathbb R^2.
$$

Geometrically, SVD explains how a unit circle becomes an ellipse. The singular values determine the lengths of its semiaxes. If a singular value is zero, the ellipse collapses to a line segment or a point.

Matrix multiplication corresponds to composition of maps, applied from right to left:

$$
A\mathbf x=U\left(\Sigma\left(V^T\mathbf x\right)\right).
$$

1. $V^T$ rotates or reflects the input into singular-vector coordinates.
2. $\Sigma$ scales along orthogonal coordinate directions.
3. $U$ rotates or reflects the result into the output directions.

Thus, a complicated linear transformation can be understood through simple geometric operations.

## 2. Understanding the three matrices

For $A\in\mathbb R^{m\times n}$, its full SVD has dimensions:

$$
\underbrace{A}_{m\times n}
=
\underbrace{U}_{m\times m}
\underbrace{\Sigma}_{m\times n}
\underbrace{V^T}_{n\times n}.
$$

### Matrix V — Right singular vectors

The columns of $V$ form an orthonormal basis of the input space $\mathbb R^n$:

$$
V^TV=VV^T=I_n.
$$

These are the input directions that $A$ sends to mutually orthogonal output directions, for the nonzero singular values.

### Matrix Σ — Singular values

$\Sigma$ is a rectangular diagonal matrix. With $p=\min(m,n)$, its diagonal entries are the **singular values**:

$$
\sigma_1\ge\sigma_2\ge\cdots\ge\sigma_p\ge0.
$$

They tell us how much the transformation stretches or compresses a unit vector in each corresponding input direction. A zero singular value means that direction is collapsed to zero.

### Matrix U — Left singular vectors

The columns of $U$ form an orthonormal basis of the output space $\mathbb R^m$:

$$
U^TU=UU^T=I_m.
$$

The left singular vectors associated with nonzero singular values identify the output directions reached from the corresponding right singular vectors.

## 3. A numerical example

Consider:

$$
A=\begin{pmatrix}3&1\\1&3\end{pmatrix}.
$$

One valid SVD is:

$$
U=\frac1{\sqrt2}\begin{pmatrix}1&1\\1&-1\end{pmatrix},
\qquad
\Sigma=\begin{pmatrix}4&0\\0&2\end{pmatrix},
\qquad
V^T=\frac1{\sqrt2}\begin{pmatrix}1&1\\1&-1\end{pmatrix}.
$$

Thus:

$$
\boxed{A=U\Sigma V^T}.
$$

The transformation scales one particular direction by 4 and another perpendicular direction by 2. The input directions are:

$$
\mathbf v_1=\frac1{\sqrt2}\begin{pmatrix}1\\1\end{pmatrix},
\qquad
\mathbf v_2=\frac1{\sqrt2}\begin{pmatrix}1\\-1\end{pmatrix}.
$$

In this example $U=V$, so:

$$
A\mathbf v_1=4\mathbf u_1,
\qquad
A\mathbf v_2=2\mathbf u_2.
$$

More generally, for $i\le p$:

$$
\boxed{A\mathbf v_i=\sigma_i\mathbf u_i}.
$$

**This is the central relationship for understanding SVD:** applying $A$ to a right singular vector produces the corresponding left singular vector, scaled by its singular value.

## 4. How is SVD calculated?

We can construct the singular values and singular vectors using $A^TA$. Starting with $A=U\Sigma V^T$:

$$
\begin{aligned}
A^TA
&=(U\Sigma V^T)^T(U\Sigma V^T)\\
&=V\Sigma^TU^TU\Sigma V^T\\
&=V\Sigma^T\Sigma V^T.
\end{aligned}
$$

This is an eigendecomposition of $A^TA$. Consequently:

$$
\boxed{A^TA\mathbf v_i=\sigma_i^2\mathbf v_i}
$$

for $i\le p$. If $n>m$, the additional eigenvalues of $A^TA$ are zero.

A theoretical construction is:

1. Compute $A^TA$.
2. Find its eigenvalues $\lambda_i$ and an orthonormal eigenbasis $\mathbf v_i$, sorted by decreasing eigenvalue.
3. Compute the singular values $\sigma_i=\sqrt{\lambda_i}$ for $i=1,\ldots,p$.
4. For each nonzero singular value, calculate:

$$
\boxed{\mathbf u_i=\frac{A\mathbf v_i}{\sigma_i}}.
$$

5. Complete the orthonormal basis of $U$, if necessary.

This is useful theoretically; numerical software usually uses more stable algorithms rather than explicitly forming $A^TA$.

## 5. Connection to rank, null space, and determinant

### Rank

The rank of $A$ is the number of nonzero singular values:

$$
\boxed{\operatorname{rank}(A)=\#\{\sigma_i>0\}}.
$$

For example, if:

$$
\Sigma=\begin{pmatrix}5&0&0\\0&2&0\\0&0&0\end{pmatrix},
$$

then $\operatorname{rank}(A)=2$. The transformation maps a three-dimensional input space onto a two-dimensional subspace of the output space.

### Null space

Let $r=\operatorname{rank}(A)$. In the full SVD, all right singular vectors after the first $r$ satisfy:

$$
A\mathbf v_i=0,\qquad i=r+1,\ldots,n.
$$

Therefore:

$$
\boxed{\ker(A)=\operatorname{span}\{\mathbf v_{r+1},\ldots,\mathbf v_n\}}.
$$

This formulation also covers wide matrices, where $V$ has more columns than there are diagonal entries in $\Sigma$.

The rank-nullity theorem follows:

$$
\operatorname{rank}(A)+\operatorname{nullity}(A)=n.
$$

### Determinant

For a square matrix:

$$
\boxed{|\det(A)|=\prod_{i=1}^{n}\sigma_i}.
$$

The absolute determinant is the volume scaling factor of the transformation. SVD shows that this is the product of the scaling factors along orthogonal singular directions.

If any singular value is zero, $\det(A)=0$ and the square matrix is not invertible.

## 6. Reduced SVD and low-rank approximation

Writing $r=\operatorname{rank}(A)$, the compact SVD retains only the nonzero singular values:

$$
A=U_r\Sigma_rV_r^T,
$$

where $U_r\in\mathbb R^{m\times r}$, $\Sigma_r\in\mathbb R^{r\times r}$, and $V_r\in\mathbb R^{n\times r}$.

Equivalently, the matrix is a sum of rank-one matrices:

$$
\boxed{A=\sum_{i=1}^{r}\sigma_i\mathbf u_i\mathbf v_i^T}.
$$

Each term $\sigma_i\mathbf u_i\mathbf v_i^T$ represents one component of the transformation.

Retaining only the largest $k$ singular values gives:

$$
A_k=\sum_{i=1}^{k}\sigma_i\mathbf u_i\mathbf v_i^T.
$$

This is a best approximation to $A$ among matrices of rank at most $k$, in both the Frobenius and spectral norms.

### Illustrative singular value spectrum

| Component | Singular value |
| --- | ---: |
| 1 | 12 |
| 2 | 7 |
| 3 | 3 |
| 4 | 0.9 |
| 5 | 0.3 |
| 6 | 0.05 |

These are hypothetical values. When the first few singular values dominate, a low-rank approximation may preserve much of the matrix's structure.

This is why SVD is used for image compression, noise reduction, and dimensionality reduction.

## 7. Connection to data matrices and PCA

Suppose a dataset has matrix:

$$
X\in\mathbb R^{m\times n},
$$

where rows represent samples and columns represent features, such as gene expression levels.

If each column is centered and $m>1$, compute:

$$
X=U\Sigma V^T.
$$

Then:

- The columns of $V$ are the **principal component directions** in feature space.
- $XV=U\Sigma$ contains the principal component scores of the samples.
- The quantities $\sigma_i^2/(m-1)$ are the variances explained by the corresponding principal components. Any additional feature-space components have zero variance.

PCA can therefore be computed directly through SVD without explicitly constructing the covariance matrix.

## 8. SVD vs QR factorization

| Property | QR | SVD |
| --- | --- | --- |
| Decomposition | $A=QR$ | $A=U\Sigma V^T$ |
| Orthogonal factors in the full form | $Q$ | $U,V$ |
| Other factor | Upper triangular or upper trapezoidal $R$ | Rectangular diagonal $\Sigma$ |
| Main interpretation | Orthogonal output basis and triangular coordinates | Orthogonal input/output directions and scaling |
| Rank information | Through $R$; pivoting helps reveal rank | Through nonzero singular values |
| Main uses | Least squares, linear systems | PCA, low-rank approximation, pseudoinverse |

For a full-column-rank matrix, reduced QR constructs an orthonormal basis for the column space of $A$.

SVD finds orthonormal bases for both the input and output spaces such that the transformation is diagonal scaling in those bases:

$$
\boxed{A\mathbf v_i=\sigma_i\mathbf u_i}.
$$

This equation connects the geometry of linear transformations, rank, null spaces, invertibility, and PCA.
