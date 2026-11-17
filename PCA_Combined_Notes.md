# Principal Component Analysis (PCA)

Principal component analysis expresses centered observations in an orthonormal basis ordered by the variance along each direction. Keeping the full basis gives an invertible change of coordinates. Keeping the first $k$ directions gives the $k$-dimensional linear subspace that captures the most sample variance and minimizes squared reconstruction error.

## 1. Centered data and the covariance matrix

Let $X\in\mathbb R^{n\times p}$, with $n\ge 2$ observations and $p$ features. Row $i$ is $x_i^T$, where $x_i\in\mathbb R^p$ is the centered observation written as a column vector. Each feature column has mean zero, so $\mathbf 1_n^T X=0$. The sample covariance matrix is

$
S=\frac{1}{n-1}X^TX\in\mathbb R^{p\times p}.
$

Since $S$ is real, symmetric, and positive semidefinite, it has an orthonormal eigenbasis with nonnegative eigenvalues.

## 2. Why PCA finds eigenvectors

For a unit direction $w\in\mathbb R^p$, the scalar projection of observation $i$ is $x_i^Tw$. Collecting these projections gives the score vector $t=Xw\in\mathbb R^n$. Because $X$ is centered, the scores have mean zero, and their sample variance is

$$
\operatorname{Var}(Xw)
=\frac{1}{n-1}\sum_{i=1}^{n}(x_i^Tw)^2
=\frac{1}{n-1}(Xw)^T(Xw)
=w^TSw.
$$

We maximize $w^TSw$ subject to $w^Tw=1$. The unit-length constraint makes the optimization depend on the direction alone. The Lagrangian and its stationarity condition are

$$
\mathcal L(w,\lambda)=w^TSw-\lambda(w^Tw-1),
\qquad
\nabla_w\mathcal L=2Sw-2\lambda w=0.
$$

Thus $Sw=\lambda w$. Multiplying on the left by $w^T$ gives $w^TSw=\lambda$, so the first principal direction $w_1$ is a unit eigenvector for the largest eigenvalue $\lambda_1$.

Each subsequent direction solves the same problem with additional orthogonality constraints:

$$
w_k\in
\underset{\substack{\lVert w\rVert_2=1\\w^Tw_j=0\ (j<k)}}{\arg\max}
\ w^TSw.
$$

For example, PC2 captures the largest variance available among directions perpendicular to PC1. Choosing the eigenvectors in this order gives $\lambda_1\ge\lambda_2\ge\cdots\ge\lambda_p\ge 0$. Within an eigenspace for a repeated eigenvalue, any orthonormal basis is valid.

## 3. Loadings, scores, and the change of basis

Collect the principal directions into $L=[w_1,\ldots,w_p]$. Its columns are often called loading vectors or weight vectors. They form an orthonormal basis of the original feature space $\mathbb R^p$. The eigenvectors themselves are expressed in the original feature coordinates.

$$
S=L\Lambda L^T,\qquad
L^TL=LL^T=I_p,\qquad
T=XL.
$$

Entry $t_{ij}=x_i^Tw_j$ is the coordinate of observation $i$ along principal direction $j$. Row $i$ of $T$ contains all the coordinates of that observation in the principal-component basis. Column $j$, $t_j=Xw_j$, contains the scores of all $n$ observations on component $j$. Thus each direction $w_j$ is in $\mathbb R^p$ and each score vector $t_j$ is in $\mathbb R^n$.

The sample covariance matrix of the centered scores is diagonal:

$$
\operatorname{Cov}(T)
=\frac{1}{n-1}T^TT
=L^TSL
=\Lambda.
$$

Each score column has variance $\lambda_j$, and distinct score columns have zero sample covariance. With all $p$ directions, $T$ has $p$ columns and the centered data can be recovered exactly as $X=TL^T$.

## 4. Truncation and reconstruction

Retaining $L_k=[w_1,\ldots,w_k]\in\mathbb R^{p\times k}$ gives $T_k=XL_k\in\mathbb R^{n\times k}$. Each row of $T_k$ gives the $k$ coordinates of an observation in the retained basis. Multiplication by $L_k^T$ expresses the projected observations back in the original feature coordinates:

$$
\widehat X=T_kL_k^T=XL_kL_k^T.
$$

Here $L_kL_k^T$ is the orthogonal projector onto the retained subspace. Among all $p\times k$ matrices $Q$ with orthonormal columns, the PCA basis $L_k$ minimizes $\lVert X-XQQ^T\rVert_F^2$. The squared reconstruction error and the cumulative explained variance ratio are

$$
\lVert X-\widehat X\rVert_F^2
=(n-1)\sum_{j=k+1}^{p}\lambda_j,\qquad
\text{Explained variance ratio}
=\frac{\sum_{j=1}^k\lambda_j}{\sum_{j=1}^{p}\lambda_j},
$$

where the ratio is defined when total sample variance is positive. Maximizing retained variance minimizes discarded variance, which is proportional to the squared reconstruction error.

## 5. How many components have nonzero variance?

Full PCA supplies $p$ orthonormal directions. The number of components with positive variance is $r=\operatorname{rank}(X)$:

$$
\operatorname{rank}(S)=\operatorname{rank}(X)\leq\min(n-1,p).
$$

The ranks agree because $v^TX^TXv=\lVert Xv\rVert_2^2$, so $X^TX$ and $X$ have the same null space. Centering gives $\mathbf 1_n^T X=0$, so all columns of $X$ lie in the $(n-1)$-dimensional subspace of $\mathbb R^n$ perpendicular to $\mathbf 1_n$. This gives the upper bound $n-1$. The actual rank can be smaller.

If $\lambda_j=0$, then $\lVert Xw_j\rVert_2^2=(n-1)\lambda_j=0$, so that entire score column is zero. Keeping the $r$ positive-variance components is sufficient to reconstruct $X$ exactly. For example, a centered $50\times 100$ matrix has 100 principal directions in a full eigenbasis and at most 49 with positive variance.

## 6. Computing PCA through the SVD

Using a full singular value decomposition $X=U\Sigma V^T$, we obtain

$$
S=V\frac{\Sigma^T\Sigma}{n-1}V^T,\qquad
T=XV=U\Sigma.
$$

The columns of $V$ are principal directions, and their covariance eigenvalues are the diagonal entries of $\Sigma^T\Sigma/(n-1)$. Each nonzero singular value $\sigma_j$ gives $\lambda_j=\sigma_j^2/(n-1)$. This computes PCA directly from the centered data matrix without explicitly forming $X^TX$.

## Source answers

- [Formal mathematical explanation of PCA](https://chatgpt.com/s/t_6afaca4cbc808191b9c8f5a6a990c598)
- [Interpretation of $T=XL$](https://chatgpt.com/s/t_6afaca6df6488191bc43ff1f56fa5b1d)
- [Full PCA, truncation, and rank-deficient data](https://chatgpt.com/s/t_6afaca7b92248191a010b46685fb495a)
