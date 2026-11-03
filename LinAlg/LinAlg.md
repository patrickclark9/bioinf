# Understanding matrices as linear maps

*Detailed overview of the discussion on rows, columns, matrix products, determinants and PCA*

The discussion developed one connected idea: a matrix represents a linear transformation. Its rows explain how output coordinates are calculated, its columns show where the standard basis vectors go, and its determinant describes how a square transformation changes oriented volume. These viewpoints describe the same operation from different angles.

## The matrix represents the rule

For a matrix A, the corresponding map is T_A(x) = Ax. The input is the vector x, the output is Ax, and A contains the coefficients that specify the rule. A matrix represents a particular linear map once bases have been chosen for the input and output spaces; the discussion uses standard coordinates.

For example, A = [[2, 0], [0, 3]] sends (x₁, x₂) to (2x₁, 3x₂). It stretches the horizontal coordinate by 2 and the vertical coordinate by 3. The input (1, 2) becomes (2, 6). Throughout this document, semicolons inside matrix brackets separate rows.

## Rows calculate individual output coordinates

$$
A=\begin{pmatrix}2&5\\3&4\end{pmatrix},\qquad x=\begin{pmatrix}1\\2\end{pmatrix},\qquad Ax=\begin{pmatrix}12\\11\end{pmatrix}
$$

The first row defines f₁(x) = 2x₁ + 5x₂, and the second defines f₂(x) = 3x₁ + 4x₂. Each row is a scalar valued linear map from the input space to the real numbers. Combining those scalar outputs gives the full vector valued transformation. This answers the initial question about what a row means in the map.

## Why an n by m matrix maps Rᵐ to Rⁿ

$$
A:\ n\times m,\qquad x:\ m\times1,\qquad Ax:\ n\times1
$$

The m columns match the m input coordinates. The n rows produce n output coordinates. Thus A represents T_A: Rᵐ → Rⁿ. The domain is Rᵐ; the codomain is Rⁿ. The actual set of attainable outputs, called the image, can be smaller than the codomain.

$$
A=\begin{pmatrix}1&2&3\\4&5&6\end{pmatrix},\qquad A\begin{pmatrix}1\\2\\3\end{pmatrix}=\begin{pmatrix}14\\32\end{pmatrix}
$$

This 2 by 3 example turns three input components into two output components. Remember the dimensions by reading columns as inputs and rows as outputs.

Source: Understanding Matrix Maps, shared ChatGPT conversation, reviewed 25 October 2026.

[Shared conversation](https://chatgpt.com/share/6ade2216-524c-83eb-a3eb-38ef00cfdf10)

## Data matrices and principal component scores

The conversation then applied the same mathematics to a data matrix X with n observations and m features. In the usual arrangement, each row records one observation and each column records one feature across all observations. A data table and a linear transformation are compatible interpretations of the same array.

### One row can be both an observation and a rule

$$
X=\begin{pmatrix}2&5&1\\4&3&2\\6&7&3\\8&5&4\end{pmatrix}
$$

This example contains four patients and three gene expression measurements. The first row, (2, 5, 1), is Patient 1’s feature profile. The first column, (2, 4, 6, 8)ᵀ, contains Gene 1’s measurements across all four patients.

When X multiplies a vector w = (w₁, w₂, w₃)ᵀ, that first row becomes the coefficients of the rule 2w₁ + 5w₂ + w₃. The output Xw has four entries, one for each patient. Therefore the map represented by this matrix goes from R³ to R⁴.

$$
(Xw)_i=X_{i1}w_1+X_{i2}w_2+\cdots+X_{im}w_m
$$

The vector w supplies one weight per feature. Each row combines those weights with one observation’s measured values. Equivalently, Xw is a weighted sum of the columns of X. The row view emphasizes individual scores; the column view emphasizes combining feature profiles across observations.

### Applying the map X to a vector w

The user’s interpretation was confirmed: writing Xw means applying the linear map represented by X to the input w. More explicitly, T_X(w) = Xw. Although X contains measurements, its multiplication still follows the same rules as any other matrix transformation.

The larger example in the chat used 100 patients and 500 genes. X has shape 100 by 500, w has 500 entries, and Xw has 100 entries. The output contains one number per patient, rather than one number per gene.

### How this becomes PCA

In principal component analysis, X is centered by subtracting each feature’s mean across observations. A unit loading vector w defines a principal direction in feature space. The dot product of each centered observation with w gives its score along that direction, so Xw collects the component scores for all observations.

The distinction between spaces matters: w lies in the m dimensional feature space, while the vector of all sample scores lies in Rⁿ. PCA chooses informative directions w; multiplication by X calculates the corresponding scores. Centering and the unit length convention make the projection interpretation precise.

## Matrix products compose transformations

The discussion next connected ordinary matrix multiplication to the map interpretation. Multiplying A by B applies the transformation A separately to every column of B. This is also the coordinate description of composing two linear maps.

### The column interpretation of a product

$$
B=\begin{bmatrix}b_1&\cdots&b_p\end{bmatrix},\qquad AB=\begin{bmatrix}Ab_1&\cdots&Ab_p\end{bmatrix}
$$

Every column bⱼ is a vector that A can transform. Placing the transformed columns beside one another gives AB. In particular, the jth column of a product records what the composite transformation does to the jth standard basis vector.

### The rightmost transformation acts first

$$
(AB)x=A(Bx),\qquad T_{AB}=T_A\circ T_B
$$

In AB, the input x first passes through B, then through A. In BA, it first passes through A, then through B. Saying that A is applied to the columns of B is consistent with this order: B’s columns already describe the images of basis vectors after B has acted.

### The stretch and shear example

$$
A=\begin{pmatrix}1&1\\0&1\end{pmatrix},\qquad B=\begin{pmatrix}2&0\\0&3\end{pmatrix}
$$

A shears horizontally: A(x, y)ᵀ = (x + y, y)ᵀ. B stretches horizontally by 2 and vertically by 3. The two possible products are:

$$
AB=\begin{pmatrix}2&3\\0&3\end{pmatrix},\qquad BA=\begin{pmatrix}2&2\\0&3\end{pmatrix}
$$

Stretching first and then shearing produces (2x + 3y, 3y). Shearing first and then stretching produces (2x + 2y, 3y). The contribution from the vertical coordinate reaches the horizontal output with a different scale, which is why the products differ.

For the input (0, 1)ᵀ, AB gives (3, 3)ᵀ, whereas BA gives (2, 3)ᵀ. Matrix multiplication is therefore generally noncommutative. Some particular pairs of matrices do commute, but equality is not a general rule.

### Dimensions must allow the composition

$$
A:\ n\times m,\qquad B:\ m\times p,\qquad AB:\ n\times p
$$

B maps Rᵖ into Rᵐ, and A then maps Rᵐ into Rⁿ. The intermediate dimensions match. The reverse product BA requires p = n; it may be undefined even when AB is defined. If both products exist for rectangular matrices, their shapes can still differ, so they need not be comparable as equal matrices.

## Columns and the geometry of the determinant

The image discussed in the chat led to the geometric role of columns. The standard basis vectors e₁ and e₂ describe unit steps along the coordinate axes. Multiplying a matrix by a basis vector selects the corresponding column.

### The columns are transformed basis vectors

$$
M=\begin{pmatrix}a&c\\b&d\end{pmatrix},\qquad Me_1=\begin{pmatrix}a\\b\end{pmatrix},\qquad Me_2=\begin{pmatrix}c\\d\end{pmatrix}
$$

Write these columns as u = (a, b)ᵀ and v = (c, d)ᵀ. Any vector (s, t)ᵀ equals se₁ + te₂. By linearity, M(s, t)ᵀ = su + tv. Once we know the images of the basis vectors, we know the image of every vector.

### Why the fourth vertex is the sum of the columns

The unit square has vertices 0, e₁, e₂ and e₁ + e₂. Their images under M are 0, u, v and u + v. The square therefore becomes the parallelogram whose side vectors are u and v.

$$
u+v=\begin{pmatrix}a+c\\b+d\end{pmatrix}=M\begin{pmatrix}1\\1\end{pmatrix}
$$

To reach the fourth vertex, move along u and then along a translated copy of v, or along v and then a translated copy of u. The opposite sides are translated copies of the original side vectors. The location of this vertex follows directly from linearity.

### The notation distinction in the chat

The conversation used two arrangements of the letters a, b, c and d. For M = [a c; b d], the columns are (a, b)ᵀ and (c, d)ᵀ. For A = [a b; c d], the columns are (a, c)ᵀ and (b, d)ᵀ. Both arrangements have determinant ad − bc, but they usually represent different maps. Read the entries down each column before assigning the side vectors.

### Signed area and ordinary area

$$
\det(M)=ad-bc,\qquad \text{Area}=|ad-bc|
$$

A positive determinant preserves orientation; a negative determinant reverses it. The absolute value gives the ordinary nonnegative area. A zero determinant means the columns are linearly dependent, so the parallelogram collapses to a line segment or a point.

More generally, area after transformation equals |det(M)| times area before transformation. The unit square has area 1, so its image has area |det(M)|. The determinant gives an area scale factor, rather than a length scale factor. A determinant of 1 preserves area even when lengths and angles change.

## Volume scaling and the failure of an inverse

### From area to higher dimensional volume

For a square n by n matrix A, the columns are the images of the n standard basis vectors. They form the edges of the image of the unit hypercube. That object is a parallelogram in two dimensions, a parallelepiped in three dimensions and a parallelotope in general.

$$
\text{Volume of the column parallelotope}=|\det(A)|
$$

The determinant itself is oriented volume; its absolute value is geometric volume. A magnitude above 1 expands n dimensional volume, a magnitude strictly between 0 and 1 contracts it, and a magnitude of 1 preserves it. A negative sign adds an orientation reversal. A zero determinant means that the image occupies a lower dimensional subspace and has zero n dimensional volume.

For A = [2 0; 0 3], det(A) = 6. The unit square becomes a rectangle of area 6. This example connects the coordinate rule, the column picture and the determinant in one calculation.

### An inverse must recover every input uniquely

$$
y=Ax,\qquad x=A^{-1}y,\qquad A^{-1}A=AA^{-1}=I
$$

An inverse reverses the map. If distinct inputs produce the same output, no function can determine which input to recover from that output alone. This is the information loss behind singularity.

$$
A=\begin{pmatrix}1&2\\2&4\end{pmatrix},\qquad \det(A)=4-4=0
$$

Here A(x₁, x₂)ᵀ = (x₁ + 2x₂, 2x₁ + 4x₂)ᵀ. Every output lies on the line y₂ = 2y₁. Both (2, 0)ᵀ and (0, 1)ᵀ map to (2, 4)ᵀ, so the original input cannot be recovered uniquely. The columns are dependent, the area collapses and the transformation is not invertible.

### The determinant proof

If A had an inverse, taking determinants in A⁻¹A = I would give det(A⁻¹) det(A) = 1. If det(A) were zero, the left side would be zero, a contradiction. For a square matrix, nonzero determinant is also sufficient for an inverse to exist.

$$
\det(A)\ne0\iff\operatorname{rank}(A)=n\iff A\text{ is invertible}
$$

These equivalent statements connect algebra and geometry: independent columns, full dimension, nonzero volume and a reversible transformation all describe the same situation for a square matrix.

## Rank covariance and the connection back to PCA

### Rectangular matrices are described through rank

The ordinary determinant applies to square matrices. A 100 by 500 data matrix therefore has no ordinary determinant. Its rank measures the dimension of its image, with rank(X) at most min(n, m). Full rank means achieving that maximum; it does not always mean every input direction can be recovered.

In particular, if m exceeds n, even a full rank map from Rᵐ to Rⁿ loses input directions. If n exceeds m and the columns are independent, the map can be one to one while its image occupies only an m dimensional subspace of Rⁿ. This refines the dimensionality language used in the discussion.

### The covariance matrix is square

$$
C=\frac{X^{\mathsf T}X}{n-1},\qquad C\text{ has shape }m\times m
$$

This formula assumes n > 1 and that the columns of X have been centered. The covariance matrix describes variation and relationships between features. Its eigenvectors give principal component directions; its eigenvalues λ₁ through λₘ give the variances along those directions.

$$
\det(C)=\lambda_1\lambda_2\cdots\lambda_m
$$

Covariance eigenvalues are nonnegative. If every eigenvalue is positive, C is invertible and its determinant is positive. If at least one eigenvalue is zero, the determinant is zero: the centered observations have no variation along at least one feature direction. Exact feature dependence or too few independent observations can cause this.

For example, if one gene is always twice another gene, a feature direction is redundant. Centering also gives rank(X) at most min(n − 1, m). Thus, for 100 patients and 500 genes, the centered covariance matrix has rank at most 99 and is necessarily singular. This is a consequence of the dimensions, rather than evidence that PCA cannot be performed.

### How to interpret the determinant in PCA

The covariance determinant combines the variances across all principal directions. Its numerical size depends strongly on feature units and scale, so it is not a useful standalone score of data quality or a substitute for inspecting explained variance. Individual eigenvalues and their proportions explain which directions contain most of the variation.

Keep the transformations distinct: X maps a loading vector to sample scores, while C maps feature space to itself. The determinant of C is the volume scale factor of the covariance map; it is not directly the geometric volume occupied by a collection of data points.

### The central connections to retain

Rows compute output coordinates. Columns are transformed basis vectors. Products compose maps, with the rightmost acting first. The absolute determinant gives volume scaling for square maps. A zero determinant means a square map loses information and has no inverse. Rank extends the dimensionality discussion to rectangular data matrices, and PCA uses loading directions and covariance eigenvalues to describe variation.
