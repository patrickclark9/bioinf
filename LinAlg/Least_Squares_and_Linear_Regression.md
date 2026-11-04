`# Least Squares and Linear Regression — A Comprehensive Overview

The **least squares problem** is one of the most fundamental problems in linear algebra, numerical optimization, and statistics.

It connects several concepts:

- **Linear algebra:** matrices as linear maps, column spaces, rank, orthogonal projections, pseudoinverses, QR factorization, and SVD.
- **Optimization:** minimizing a quadratic objective function using gradients.
- **Statistics:** estimating regression coefficients, residuals, uncertainty, and hypothesis testing.
- **Machine learning:** fitting predictive models, regularization, and generalization.

The central distinction is that **linear regression specifies a model for the relationship between variables, while ordinary least squares (OLS) is a method used to estimate its parameters.**

We will develop these ideas starting from the linear algebra interpretation and progressing to statistical inference.

---

## 1. The linear regression model

Suppose we have $n$ observations and $p$ explanatory variables (features).

We collect our data in a design matrix:

$$X\in\mathbb R^{n\times p}$$

and our observed responses in a vector:

$$y\in\mathbb R^n$$

The vector of unknown regression coefficients is:

$$\beta\in\mathbb R^p$$

Our linear regression model is:

$$\boxed{y=X\beta+\varepsilon}$$

where $\varepsilon\in\mathbb R^n$ represents the random errors.

For observation $i$, this becomes:

$$y_i=\beta_1x_{i1}+\beta_2x_{i2}+\cdots+\beta_px_{ip}+\varepsilon_i$$

When the model includes an intercept, we typically use a column of ones in $X$, so that:

$$y_i=\beta_0+\beta_1x_{i1}+\cdots+\beta_kx_{ik}+\varepsilon_i$$

Here $p=k+1$, counting the intercept.

### Example: a dataset

Suppose we want to predict a protein's abundance using the expression levels of two genes.

Design matrix and coefficient vector

$$X=\begin{pmatrix}1&2&3\\1&4&2\\1&5&6\\1&7&4\end{pmatrix},\qquad\beta=\begin{pmatrix}\beta_0\\\beta_1\\\beta_2\end{pmatrix}$$

**4 rows**

Observations

**3 columns**

Intercept + 2 features

**3 coefficients**

Unknowns

Remember the linear map interpretation:

$$X:\mathbb R^p\longrightarrow\mathbb R^n$$

The matrix $X$ maps a coefficient vector $\beta$ into a vector of predicted responses.

Once we estimate the coefficients, we obtain:

$$\boxed{\hat y=X\hat\beta}$$

Notice the distinction:

- $y$: observed responses.
- $X\beta$: systematic component of the statistical model.
- $\hat\beta$: estimated coefficients.
- $\hat y$: fitted responses.
- $\varepsilon$: unobservable random errors.
- $e=y-\hat y$: observable residuals after fitting.

The difference between errors and residuals will become particularly important later.

---

## 2. What exactly is the least squares problem?

Suppose the system

$$X\beta=y$$

has no exact solution.

This is common when $n>p$: we have more observations than unknown coefficients, and the observed responses generally do not lie in the column space of $X$.

Instead of finding a coefficient vector satisfying every equation exactly, we seek the vector producing the **smallest total squared discrepancy**.

Mathematically:

$$\boxed{\hat\beta_{\mathrm{OLS}}=\arg\min_{\beta\in\mathbb R^p}\|y-X\beta\|_2^2}$$

Equivalently:

$$\hat\beta=\arg\min_\beta\sum_{i=1}^n(y_i-\hat y_i)^2$$

The objective is called the *residual sum of squares*, or RSS.

$$RSS(\beta)=(y-X\beta)^T(y-X\beta)$$

### Geometric intuition: fitting a straight line

In simple linear regression, the model is:

$$\hat y=b_0+b_1x$$

The algorithm chooses the intercept $b_0$ and slope $b_1$ that minimize the sum of the squared vertical distances between the data points and the regression line.

![Least-squares line, observations, fitted predictions, and vertical residuals](zzRes/least_squares_fit.svg)

Shows an interactive scatterplot where draggable observed points update the least-squares line of best fit. Observed points, fitted predictions, and vertical residual gaps remain visible together while generated datasets vary.

Initial values:
- fitMode: "with_intercept"

Try moving an observed point. The fitted line changes because the coefficients minimizing the RSS change.

We square the residuals because:

1. Positive and negative errors cannot cancel.
2. Large errors receive larger penalties.
3. The objective is differentiable and convex.
4. The resulting optimization problem has a particularly useful algebraic structure.

Squaring also makes ordinary least squares sensitive to outliers.

---

## 3. Least squares as an orthogonal projection

This is arguably the most important geometrical interpretation.

Remember that the columns of $X$ span its column space:

$$\operatorname{Col}(X)\subseteq\mathbb R^n$$

For any coefficient vector $\beta$:

$$X\beta\in\operatorname{Col}(X)$$

Therefore, all possible predictions are constrained to lie inside the column space of $X$.

**The least squares problem consists of finding the vector inside $\operatorname{Col}(X)$ that is closest to $y$.**

![Orthogonal projection of y onto the column space of X](orthogonal_projection.svg)

Conceptual projection geometry: the fitted vector lies in the column space, while the residual points in a perpendicular direction. The plane represents a subspace; the drawing is schematic.

We can decompose $y$ into two components:

$$\boxed{y=\hat y+e}$$

with:

$$\hat y\in\operatorname{Col}(X)$$

and

$$e\perp\operatorname{Col}(X)$$

Consequently:

$$\boxed{X^Te=0}$$

Substituting $e=y-X\hat\beta$:

$$X^T(y-X\hat\beta)=0$$

Therefore:

$$\boxed{X^TX\hat\beta=X^Ty}$$

These are the **normal equations**.

This geometric derivation tells us something remarkable: the same equations that arise from minimizing the objective also arise from requiring the residual vector to be orthogonal to the model's prediction space.

Furthermore, by the Pythagorean theorem, for any $\beta$:

$$\|y-X\beta\|^2=\|y-\hat y\|^2+\|\hat y-X\beta\|^2$$

The second term cannot be negative, proving that $\hat y$ is the closest possible fitted vector.

---

## 4. Derivation using matrix calculus

Now let's derive the OLS estimator analytically.

Our objective is:

$$J(\beta)=\|y-X\beta\|^2$$

Expanding:

$$J(\beta)=(y-X\beta)^T(y-X\beta)$$

Using transpose rules:

$$(y-X\beta)^T=y^T-\beta^TX^T$$

Hence:

$$J(\beta)=y^Ty-y^TX\beta-\beta^TX^Ty+\beta^TX^TX\beta$$

The two middle terms are scalars and transposes of each other. Since a scalar equals its transpose:

$$y^TX\beta=\beta^TX^Ty$$

We get:

$$\boxed{J(\beta)=y^Ty-2\beta^TX^Ty+\beta^TX^TX\beta}$$

### Taking the gradient

We differentiate with respect to the vector $\beta$.

| Term | Gradient with respect to $\beta$ |
|--------|--------|
| $y^Ty$ | $0$ |
| $-2\beta^TX^Ty$ | $-2X^Ty$ |
| $\beta^TX^TX\beta$ | $2X^TX\beta$ |

The last identity works because $X^TX$ is symmetric:

$$(X^TX)^T=X^TX$$

More generally:

$$\nabla_\beta(\beta^TA\beta)=(A+A^T)\beta$$

Combining all terms gives:

$$\boxed{\nabla_\beta J(\beta)=-2X^Ty+2X^TX\beta}$$

### Why do we set the gradient equal to zero?

The gradient represents the direction of steepest increase of a differentiable function.

At a differentiable, unconstrained local minimum, every directional derivative must vanish, so:

$$\nabla_\beta J(\hat\beta)=0$$

However, a stationary point is not necessarily a minimum for an arbitrary function.

We must also consider the Hessian:

$$\boxed{\nabla^2_\beta J(\beta)=2X^TX}$$

For any $v\in\mathbb R^p$:

$$v^TX^TXv=\|Xv\|^2\geq 0$$

Thus $X^TX$ is positive semidefinite, and the least squares objective is convex.

Therefore, **every stationary point is a global minimizer**.

If $X$ has full column rank, the Hessian is positive definite and the minimizer is unique.

Setting the gradient to zero:

$$-2X^Ty+2X^TX\hat\beta=0$$

gives:

$$X^TX\hat\beta=X^Ty$$

If $X^TX$ is invertible, we can solve:

$$\boxed{\hat\beta=(X^TX)^{-1}X^Ty}$$

This is the classic closed-form OLS estimator.

---

## 5. When does the OLS solution exist and when is it unique?

It's essential to distinguish **existence**, **uniqueness**, and **statistical suitability**.

### Case A: $X$ has full column rank

Suppose:

$$\operatorname{rank}(X)=p,\qquad n\ge p$$

Then:

$$X^TX\in\mathbb R^{p\times p}$$

is invertible.

There is exactly one least squares coefficient vector:

$$\hat\beta=(X^TX)^{-1}X^Ty$$

Even when the equation $X\beta=y$ has no exact solution, the least squares solution exists and is unique.

### Case B: $X$ is rank-deficient

Suppose:

$$\operatorname{rank}(X)<p$$

Then:

$$X^TX$$

is singular and cannot be inverted.

This can happen when one feature is a linear combination of other features, as in perfect multicollinearity.

However, **the least squares problem still has at least one solution**.

To see why it is not unique, suppose $v\neq0$ lies in the null space:

$$Xv=0$$

Then:

$$X(\hat\beta+v)=X\hat\beta$$

Thus $\hat\beta$ and $\hat\beta+v$ produce identical fitted responses.

There can be infinitely many coefficient vectors minimizing the objective, but the projected vector $\hat y$ is unique.

### The Moore–Penrose pseudoinverse

A standard way to choose one particular solution is:

$$\boxed{\hat\beta=X^+y}$$

where $X^+$ is the Moore–Penrose pseudoinverse.

This gives the least squares solution with the **smallest Euclidean norm** among all minimizers.

For full-column-rank matrices:

$$X^+=(X^TX)^{-1}X^T$$

The pseudoinverse therefore generalizes the familiar OLS formula to rank-deficient and underdetermined problems.

A crucial distinction: the pseudoinverse resolves algebraic nonuniqueness, but it does not automatically resolve statistical problems such as poor identifiability, omitted variables, or endogeneity.

---

## 6. QR factorization and SVD for solving least squares

Although the formula involving $(X^TX)^{-1}$ is theoretically convenient, it is usually not the best way to compute regression coefficients.

### QR factorization

For full-column-rank $X$, with $n\ge p$, consider the reduced QR decomposition:

$$X=QR$$

where:

$$Q^TQ=I_p$$

and $R\in\mathbb R^{p\times p}$ is upper triangular and invertible.

Substitute into the normal equations:

$$R^TQ^TQR\hat\beta=R^TQ^Ty$$

Using $Q^TQ=I$:

$$R^TR\hat\beta=R^TQ^Ty$$

Canceling $R^T$:

$$\boxed{R\hat\beta=Q^Ty}$$

This system can be efficiently solved using backward substitution.

QR is generally more numerically stable than explicitly forming and inverting $X^TX$.

### Singular value decomposition

For an arbitrary matrix $X$, consider:

$$X=U\Sigma V^T$$

The pseudoinverse can be written as:

$$X^+=V\Sigma^+U^T$$

Consequently:

$$\boxed{\hat\beta=V\Sigma^+U^Ty}$$

The SVD reveals:

- Which directions in coefficient space are identifiable.
- Which singular values are zero, indicating rank deficiency.
- Which singular values are very small, indicating numerical instability.
- Why certain regression coefficients can be extremely sensitive to small changes in data.

Indeed, if $X$ has full column rank, the spectral condition number satisfies:

$$\kappa_2(X^TX)=\kappa_2(X)^2$$

This explains why explicitly forming $X^TX$ can amplify numerical conditioning problems.

| Method           | Main advantage                                     | Limitation                                    |
| ---------------- | -------------------------------------------------- | --------------------------------------------- |
| Normal equations | Simple analytical formula                          | Can be numerically unstable                   |
| QR factorization | Efficient and stable                               | Requires suitable handling of rank deficiency |
| SVD              | Handles rank deficiency and diagnoses conditioning | Generally more computationally expensive      |

---

## 7. The fitted values, residuals, and hat matrix

We can now examine the regression fit itself.

For a full-column-rank design matrix:

$$\hat y=X\hat\beta$$

Substituting the OLS estimator:

$$\hat y=X(X^TX)^{-1}X^Ty$$

Define the **hat matrix**:

$$\boxed{H=X(X^TX)^{-1}X^T}$$

Then:

$$\boxed{\hat y=Hy}$$

It is called the hat matrix because it transforms the observed response vector into its fitted counterpart.

Two important properties:

$$H^T=H$$

and:

$$H^2=H$$

Therefore, $H$ is an orthogonal projection matrix onto $\operatorname{Col}(X)$.

When $X$ is rank-deficient, the same projection can be written more generally as:

$$H=XX^+$$

The residual vector is:

$$e=y-\hat y=(I-H)y$$

The matrix $I-H$ projects onto the orthogonal complement of the column space.

Consequently:

$$X^Te=0$$

And, if an intercept is included:

$$\sum_{i=1}^n e_i=0$$

This latter result follows because the vector of all ones is a column of $X$, and the residuals must be orthogonal to that vector.

---

# Part II — Statistical Interpretation

Up to this point, we have discussed least squares as a deterministic optimization problem.

Now we introduce probability and statistical inference.

## 8. From least squares to ordinary linear regression

In statistical linear regression, we assume that our observations are generated according to:

$$\boxed{y=X\beta+\varepsilon}$$

Here $\beta$ is the unknown true coefficient vector, while $\varepsilon$ represents random variability not explained by the model.

A common set of assumptions is:

1. **Linearity in parameters:** the systematic component is $X\beta$.
2. **Zero conditional mean:** $E[\varepsilon\mid X]=0$.
3. **Homoscedasticity:** errors have constant conditional variance.
4. **Uncorrelated errors:** distinct errors have zero conditional covariance.
5. **Full column rank:** the regression coefficients are identifiable.

Assumptions 3 and 4 can be expressed together as:

$$\operatorname{Var}(\varepsilon\mid X)=\sigma^2I_n$$

Sometimes we additionally assume that errors are normally distributed:

$$\varepsilon\mid X\sim\mathcal N(0,\sigma^2I_n)$$

However, normality is **not required to compute OLS or for the Gauss–Markov theorem**.

It becomes particularly useful for deriving exact small-sample tests and confidence intervals.

Also, independent observations are a common sufficient condition for uncorrelated errors, but independence is stronger than the covariance condition itself.

---

## 9. Is OLS an unbiased estimator?

Recall:

$$\hat\beta=(X^TX)^{-1}X^Ty$$

Substitute the statistical model:

$$y=X\beta+\varepsilon$$

Then:

$$\hat\beta=(X^TX)^{-1}X^T(X\beta+\varepsilon)$$

Distributing:

$$\hat\beta=(X^TX)^{-1}X^TX\beta+(X^TX)^{-1}X^T\varepsilon$$

Therefore:

$$\boxed{\hat\beta=\beta+(X^TX)^{-1}X^T\varepsilon}$$

This equation is fundamental: it shows that the estimated coefficients differ from the true coefficients because of the random errors.

Taking the conditional expectation:

$$E[\hat\beta\mid X]=\beta+(X^TX)^{-1}X^TE[\varepsilon\mid X]$$

If:

$$E[\varepsilon\mid X]=0$$

then:

$$\boxed{E[\hat\beta\mid X]=\beta}$$

The OLS estimator is conditionally unbiased.

In other words, across repeated samples with the same design matrix, the average estimated coefficient vector equals the true coefficient vector.

This does not mean that any particular estimate will be exactly correct.

---

## 10. The Gauss–Markov theorem

One of the most important theoretical results in classical regression is the **Gauss–Markov theorem**.

Under the standard linear model assumptions, including full column rank, zero conditional mean and spherical error covariance:

$$\operatorname{Var}(\varepsilon\mid X)=\sigma^2I$$

the OLS estimator is:

$$\boxed{\text{BLUE}}$$

which means *Best Linear Unbiased Estimator*.

Let's unpack that.

- **Best:** it has the smallest covariance matrix, in the positive-semidefinite ordering, among linear unbiased estimators.
- **Linear:** it is linear in the response vector $y$, for fixed $X$.
- **Unbiased:** its conditional expected value equals $\beta$.
- **Estimator:** it is a statistical procedure for estimating unknown coefficients.

Notice that "best" does not mean OLS always has the lowest predictive error or the smallest mean squared error among all conceivable estimators.

For example, biased estimators such as ridge regression may outperform OLS in prediction, particularly in high-dimensional or highly correlated data.

### Variance of the OLS estimator

Under homoscedastic, uncorrelated errors:

$$\boxed{\operatorname{Var}(\hat\beta\mid X)=\sigma^2(X^TX)^{-1}}$$

This tells us how the uncertainty of the coefficients depends on the design matrix and the error variance.

If features are nearly linearly dependent, $X^TX$ becomes poorly conditioned and coefficient variances can become very large.

---

## 11. Residuals versus statistical errors

This distinction is essential.

The **true error** for observation $i$ is:

$$\varepsilon_i=y_i-x_i^T\beta$$

It depends on the unknown true coefficient vector $\beta$.

The **residual** is:

$$e_i=y_i-x_i^T\hat\beta$$

It uses the estimated coefficients instead.

Hence:

$$\boxed{e_i\neq\varepsilon_i\quad\text{in general}}$$

Using matrix notation:

$$e=(I-H)y$$

Since $y=X\beta+\varepsilon$ and $(I-H)X=0$:

$$\boxed{e=(I-H)\varepsilon}$$

The residuals are therefore transformations of the true errors.

They are not identical to those errors, and they are generally correlated with one another even when the original errors are uncorrelated.

Under the classical covariance assumptions:

$$\operatorname{Var}(e\mid X)=\sigma^2(I-H)$$

Therefore:

$$\operatorname{Var}(e_i\mid X)=\sigma^2(1-h_{ii})$$

The diagonal entry $h_{ii}$ measures the leverage of observation $i$.

High-leverage observations have greater potential to influence the fitted regression.

---

## 12. Estimating the residual variance

The error variance $\sigma^2$ is unknown, so we estimate it using the residual sum of squares.

For a full-column-rank model with $p$ estimated coefficients and $n>p$:

$$\boxed{s^2=\frac{RSS}{n-p}}$$

Why do we divide by $n-p$, rather than $n$?

Because fitting the $p$ coefficients uses $p$ degrees of freedom.

In fact:

$$E[RSS\mid X]=(n-p)\sigma^2$$

Therefore:

$$E[s^2\mid X]=\sigma^2$$

under the classical assumptions.

The estimated standard error of the regression is:

$$s=\sqrt{\frac{RSS}{n-p}}$$

The estimated covariance matrix of the coefficient estimator is:

$$\widehat{\operatorname{Var}}(\hat\beta)=s^2(X^TX)^{-1}$$

The standard error of each coefficient is the square root of the corresponding diagonal entry.

---

## 13. Normality, maximum likelihood, and OLS

OLS can also be derived through maximum likelihood under Gaussian errors.

Assume:

$$y\mid X\sim\mathcal N(X\beta,\sigma^2I)$$

The likelihood is:

$$L(\beta,\sigma^2)=(2\pi\sigma^2)^{-n/2}\exp\left(-\frac{1}{2\sigma^2}\|y-X\beta\|^2\right)$$

The log-likelihood is:

$$\ell(\beta,\sigma^2)=-\frac n2\log(2\pi\sigma^2)-\frac{1}{2\sigma^2}\|y-X\beta\|^2$$

For fixed $\sigma^2$, the first term does not depend on $\beta$.

Therefore, maximizing the log-likelihood is equivalent to minimizing:

$$\|y-X\beta\|^2$$

Thus:

$$\boxed{\hat\beta_{\mathrm{MLE}}=\hat\beta_{\mathrm{OLS}}}$$

when $X$ has full column rank.

This gives OLS a probabilistic interpretation, but **OLS itself does not require Gaussian errors**.

An interesting detail: the Gaussian maximum likelihood estimator for $\sigma^2$ uses $RSS/n$, while the conventional unbiased estimator uses $RSS/(n-p)$.

---

# Part III — Regression Diagnostics and Alternatives

## 14. How do we evaluate linear regression?

Finding coefficients that minimize the training RSS does not necessarily mean the statistical model is appropriate or that predictions will generalize well.

Several measures are useful.

### Residual sum of squares

$$RSS=\sum_{i=1}^n(y_i-\hat y_i)^2$$

Smaller RSS means a better fit on the training data, for the same response dataset.

### Mean squared error and root mean squared error

$$MSE=\frac1n\sum_{i=1}^n(y_i-\hat y_i)^2$$

$$RMSE=\sqrt{MSE}$$

These definitions use $n$ for a dataset's average squared prediction error; the degrees-of-freedom-adjusted variance estimator discussed earlier is a different quantity.

### Coefficient of determination

For an OLS model with an intercept:

$$\boxed{R^2=1-\frac{RSS}{TSS}}$$

where:

$$TSS=\sum_{i=1}^n(y_i-\bar y)^2$$

$R^2$ measures the fraction of observed response variation explained by the regression, using this standard decomposition.

For a conventional in-sample OLS fit with an intercept, $0\le R^2\le1$. This range is not guaranteed for every regression setting, notably out-of-sample predictions.

A high training $R^2$ does not automatically imply good predictive performance.

---

## 15. What happens when regression assumptions fail?

An important distinction is that **violating a statistical assumption does not mean the least squares optimization problem stops having a solution**.

OLS remains mathematically well-defined. What changes is the interpretation or statistical quality of its estimates.

| Situation | Consequence | Common response |
|--------|--------|--------|
| Heteroscedasticity | Conventional standard errors may be wrong; OLS may be inefficient | Robust standard errors or WLS |
| Correlated errors | Classical inference becomes unreliable; OLS may be inefficient | GLS or time-series methods |
| Perfect multicollinearity | Coefficients are not uniquely identifiable | Remove redundant columns or use regularization |
| Severe near-multicollinearity | Coefficients become unstable | Ridge, principal component regression, PLS |
| Outliers | Squared errors can dominate the fit | Robust regression |
| Endogeneity | OLS can be biased and inconsistent | Instrumental variables or suitable causal methods |
| Incorrect functional form | Linear predictor may systematically miss structure | Feature transformations or nonlinear models |
| Many features relative to observations | Overfitting or nonunique coefficients | Ridge, lasso, dimensionality reduction |

One subtle point: non-normality alone does not invalidate OLS unbiasedness or Gauss–Markov optimality. It mainly affects exact distributional inference, particularly in small samples.

### Weighted Least Squares (WLS)

If observations have different error variances, we can minimize a weighted objective:

$$\boxed{\hat\beta_{\mathrm{WLS}}=\arg\min_\beta(y-X\beta)^TW(y-X\beta)}$$

where $W$ is a positive-definite weighting matrix, often diagonal.

The solution is:

$$\boxed{\hat\beta_{\mathrm{WLS}}=(X^TWX)^{-1}X^TWy}$$

assuming the relevant inverse exists.

When the error covariance is diagonal, the statistically efficient weights are proportional to the inverse error variances.

### Generalized Least Squares (GLS)

If the error covariance is:

$$\operatorname{Var}(\varepsilon\mid X)=\Sigma$$

where $\Sigma$ is positive definite, GLS minimizes:

$$(y-X\beta)^T\Sigma^{-1}(y-X\beta)$$

and gives:

$$\boxed{\hat\beta_{\mathrm{GLS}}=(X^T\Sigma^{-1}X)^{-1}X^T\Sigma^{-1}y}$$

WLS with diagonal inverse-variance weights is a special case of GLS.

### Ridge regression

Ridge regression modifies the objective:

$$\boxed{\hat\beta_{\mathrm{ridge}}=\arg\min_\beta\left[\|y-X\beta\|^2+\lambda\|\beta\|^2\right]}$$

For $\lambda>0$:

$$\hat\beta_{\mathrm{ridge}}=(X^TX+\lambda I)^{-1}X^Ty$$

assuming all coefficients, including any intercept, are penalized as written. In practice, the intercept is commonly left unpenalized and predictors are standardized.

Ridge introduces bias, but can substantially reduce estimator variance and improve prediction.

### Partial Least Squares (PLS)

PLS is conceptually different.

Instead of estimating coefficients directly in the original feature space, PLS constructs latent components from $X$, taking their relationship with $y$ into account.

It is often useful when:

- Features are strongly correlated.
- The number of features is large.
- The number of observations is relatively small.
- We want dimensionality reduction oriented toward predicting the response.

PLS should not be considered a universal replacement for OLS when assumptions fail. In particular, it does not automatically solve heteroscedasticity, endogeneity, or model misspecification.

---

## 16. A worked numerical example

Consider three observations:

$$(x_1,y_1)=(1,2),\qquad(x_2,y_2)=(2,3),\qquad(x_3,y_3)=(3,5)$$

We want to fit:

$$\hat y_i=\beta_0+\beta_1x_i$$

The matrices are:

$$X=\begin{pmatrix}1&1\\1&2\\1&3\end{pmatrix},\qquad y=\begin{pmatrix}2\\3\\5\end{pmatrix}$$

Calculate:

$$X^TX=\begin{pmatrix}3&6\\6&14\end{pmatrix}$$

and:

$$X^Ty=\begin{pmatrix}10\\23\end{pmatrix}$$

Therefore, the normal equations are:

$$\begin{pmatrix}3&6\\6&14\end{pmatrix}\begin{pmatrix}\hat\beta_0\\\hat\beta_1\end{pmatrix}=\begin{pmatrix}10\\23\end{pmatrix}$$

This gives:

$$3\hat\beta_0+6\hat\beta_1=10$$

$$6\hat\beta_0+14\hat\beta_1=23$$

Solving:

$$\boxed{\hat\beta_0=\frac13,\qquad\hat\beta_1=\frac32}$$

Our fitted line is:

$$\boxed{\hat y=\frac13+\frac32x}$$

The fitted values and residuals are:

| $x_i$ | Observed $y_i$ | Fitted $\hat y_i$ | Residual $e_i$ |
|--------|--------|--------|--------|
| 1 | 2 | 1.8333 | 0.1667 |
| 2 | 3 | 3.3333 | −0.3333 |
| 3 | 5 | 4.8333 | 0.1667 |

Notice that:

$$\sum_i e_i=0$$

and:

$$\sum_i x_ie_i=0$$

These are exactly the orthogonality conditions:

$$X^Te=0$$

The residual sum of squares is:

$$RSS=\left(\frac16\right)^2+\left(-\frac13\right)^2+\left(\frac16\right)^2$$

$$\boxed{RSS=\frac16}$$

Since $n=3$ and $p=2$, the unbiased error variance estimate is:

$$s^2=\frac{1/6}{3-2}=\frac16$$

And, since $\bar y=10/3$:

$$TSS=\frac{14}{3}$$

so:

$$\boxed{R^2=1-\frac{1/6}{14/3}=\frac{27}{28}\approx0.9643}$$

The model explains approximately 96.4% of the response variation in these three observations, although such a tiny dataset cannot establish reliable predictive performance.

---

## 17. Connecting all the concepts

Here is a concise map of the entire theory.

**Statistical model**

$y=X\beta+\varepsilon$

**Optimization problem**

$\min_\beta\|y-X\beta\|_2^2$

Calculus

$\nabla J=0$

Geometry

$X^Te=0$

**Normal equations**

$X^TX\hat\beta=X^Ty$

**OLS coefficients**

$\hat\beta=(X^TX)^{-1}X^Ty$

When X has full column rank

**Fitted values and residuals**

$\hat y=X\hat\beta,\quad e=y-\hat y$

## 18. The distinctions worth remembering

| Concept | Meaning |
|--------|--------|
| Linear regression | A statistical model expressing the response as a linear function of unknown coefficients plus error |
| Least squares | An optimization principle minimizing squared residuals |
| OLS estimator | The rule mapping data $(X,y)$ to least squares coefficient estimates |
| OLS estimate | The numerical coefficient vector obtained from a particular dataset |
| Normal equations | First-order optimality conditions for least squares |
| Pseudoinverse | Gives the minimum-norm least squares solution, even without full rank |
| QR / SVD | Numerical linear algebra methods used to compute least squares solutions |
| Residuals | Observable differences between observed and fitted responses |
| Errors | Unobserved differences between responses and their true systematic component |
| Gauss–Markov | Conditions under which OLS is the best linear unbiased estimator |
| WLS / GLS | Methods that account for non-spherical error covariance |
| Ridge / PLS | Methods that can stabilize estimation or prediction with correlated, numerous predictors |

The most important conceptual conclusion is that there are **three distinct levels of understanding**:

1. **Algebraically**, least squares attempts to solve a generally inconsistent linear system.
2. **Geometrically**, least squares projects the observed vector onto the column space of the design matrix.
3. **Statistically**, OLS estimates unknown regression coefficients, and its properties depend on assumptions about how the data were generated.

Keeping these three perspectives separate—but understanding how they connect—is the foundation for more advanced topics such as ridge regression, generalized least squares, principal component regression, partial least squares, and statistical inference.
