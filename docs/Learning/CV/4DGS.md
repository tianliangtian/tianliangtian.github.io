# 4 Dimension Gaussian Splatting

## Gaussian Distribution

### Covariance

For a given random vector $X:\Omega \rightarrow R^{n}$, its **covariance matrix** $\Sigma$ is the $n\times n$ square matrix whose extries are given by $\Sigma_{ij}=Cov[X_{i},X_{j}]=E[(X_{i}-E[X_{i}])(X_{j}-E[X_{j}])]$

$$
\Sigma=E[(X-E[X])(X-E[X])^{T}] 
$$

**Proposition:** Suppose that $\Sigma$ is the covariance matrix corresponding to some random vector $X$. Then $\Sigma$ is symmetric positive semidefinite

!!! note "positive semidefinite"

    A symmetric matrix $A\in S^{n}$ is **positive semidefinite** (PSD) if for all vectors $x^{T}Ax\geq 0$
 
$\textit{proof}\text{: For any vector }z\in R^{n} \text{, observe that}$

$$
z^{T}\Sigma z= \sum_{i=1}^{n}\sum_{j=1}^{n}\Sigma_{ij}z_{i}z_{j}\\
=E[\sum_{i=1}^{n}\sum_{j=1}^{n}(X_{i}-E[X_{i}])(X_{j}-E[X_{j}])z_{i}z_{j}]
$$

$\text{Observe that the quantity inside the brackets is of the form}$ 

$$
\sum_{i=1}^{n}\sum_{j=1}^{n}x_{i}x_{j}z_{i}z_{j}=(x^{T}z)^{2}\geq 0\\
$$

$\text{, which complete the proof}$

### Gaussian Distribution

* $X\sim Normal(\mu,\sigma^{2})$: also known as univariate Gaussian distribution

$$
f(x)=\frac{1}{\sqrt{2\pi}\sigma}e^{-\frac{1}{2\sigma^{2}}(x-\mu)^{2}}
$$

* $X\sim \mathcal{N}(\mu,\Sigma)$ For multivariate Gaussian, where mean $\mu\in R^{d}$ and covariance matrix $\Sigma$ is symmetric positive deﬁnite $d\times d$ matrix 

$$
f_{X_{1},X_{2},\dots,X_{d}}(x_1,x_2,\dots,x_{d};\mu,\Sigma)=\frac{1}{(2\pi)^{d/2}|\Sigma|^{1/2}}\exp(-\frac{1}{2}(x-\mu)^{T}\Sigma^{-1}(x-\mu))
$$

**Proposition:** $\Sigma=E[(X-\mu)(X-\mu)^{T}]=E[X^{2}]-\mu\mu^{T}$

!!! note

    In the definition of multivariate Gaussians, we required that the covariance matrix $\Sigma$ be symmetric positive definite. That's because we need $\Sigma^{-1}$ exists, which means $\Sigma$ is full rank. Since any full rank symmetric positive semidefinite matrix is necessarily symmetric positive definite, it follows that $\Sigma$ must be symmetric positive definite.

#### Isocontour

!!! note

    For a function $f : R^2 → R$, an isocontour is a set of the form $\{x\in R^{2}:f(x)=c\}$ for some $c\in R$

Consider the case where $d=2$ and $\Sigma$ is diagonal. For some constant $c\in R$ and all $x1,x2\in R$, we have

$$
\begin{aligned}
c&=\frac{1}{2\pi \sigma_{1}\sigma_{2}}\exp{(-\frac{1}{2\sigma_{1}^{2}}(x_{1}-\mu_{1})^{2}-\frac{1}{2\sigma_{2}^{2}}(x_{2}-\mu_{2})^{2})} \\
1&=\frac{(x_{1}-\mu_{1})^{2}}{2\sigma_{1}^{2}\log{\frac{1}{2\pi c\sigma_{1}\sigma_{2}}}}+\frac{(x_{2}-\mu_{2})^{2}}{2\sigma_{2}^{2}\log{\frac{1}{2\pi c\sigma_{1}\sigma_{2}}}}
\end{aligned}
$$

Defining

$$
r_{1}=\sqrt{2\sigma_{1}^{2}\log{(\frac{1}{2\pi c\sigma_{1}\sigma_{2}})}}\\
r_{2}=\sqrt{2\sigma_{2}^{2}\log{(\frac{1}{2\pi c\sigma_{1}\sigma_{2}})}}\\
$$

It follows that

$$
1=\left(\frac{x_{1}-\mu_{1}}{r_{1}}\right)^{2}+\left(\frac{x_{2}-\mu_{2}}{r_{2}}\right)^{2}
$$

When $\Sigma$ is diagonal, it is the equation of an **axis-aligned ellipse**, while a **rotated ellipses** when not diagonal.

In $d$ dimensional case, the level sets form geometrical structures known as **ellipsoid** in $R^{d}$

#### Closure properties

**Theorem:** Suppose that $y\sim\mathcal{N}(\mu,\Sigma)$ and $z\sim\mathcal{N}(\mu',\Sigma')$ are independent Gaussian distributed random variables, where $\mu,\mu'\in R^{d}$ and $\Sigma,\Sigma'\in S^{d}_{++}$. Then, their sum is also Gaussian:

$$
y+z\sim \mathcal{N}(\mu+\mu',\Sigma+\Sigma')\\
$$


**Theorem**: Suppose that

$$
\begin{bmatrix}
x_{A} \\
x_{B}
\end{bmatrix}
\sim\mathcal{N}
\left(
\begin{bmatrix}
x_{A} \\
x_{B}
\end{bmatrix}
,
\begin{bmatrix}
\Sigma_{AA} & \Sigma_{AB}\\
\Sigma_{BA} & \Sigma_{BB}
\end{bmatrix}
\right)
$$

where $x_{A}\in R^{n},x_{B}\in R^{d}$ and the dimensions of the mean vectors and covariance matrix subblocks are chosen to match $x_{A}$ and $x_{B}$. Then, the marginal densities are Gaussian:

$$
\begin{aligned}
p(x_A)&=\int_{x_{B}\in R^{d}}p(x_{A},x_{B};\mu,\Sigma)dx_{B}\\
p(x_B)&=\int_{x_{A}\in R^{n}}p(x_{A},x_{B};\mu,\Sigma)dx_{A}\\
\\
x_{A}&\sim \mathcal{N}(\mu_{A},\Sigma_{AA})\\
x_{B}&\sim \mathcal{N}(\mu_{B},\Sigma_{BB})
\end{aligned}
$$

**Theorem**: Suppose that

$$
\begin{bmatrix}
x_{A}\\
x_{B}\\
\end{bmatrix}
\sim\mathcal{N}
\begin{pmatrix}
\begin{bmatrix}
x_{A}\\
x_{B}\\
\end{bmatrix}
,
\begin{bmatrix}
\Sigma_{AA}&\Sigma_{AB}\\
\Sigma_{BA}&\Sigma_{BB}\\
\end{bmatrix}
\end{pmatrix}
$$

where $x_{A}\in R^{n},x_{B}\in R^{d}$ and the dimensions of the mean vectors and covariance matrix subblocks are chosen to match $x_{A}$ and $x_{B}$. Then, the conditional densities are Gaussian:

$$
\begin{aligned}
p(x_{A}|x_{B})&=\frac{p(x_{A},x_{B};\mu,\Sigma)}{\int_{x_{A}\in R^{n}}p(x_{A},x_{B};\mu,\Sigma)dx_{A}}\\
p(x_B|x_{A})&=\frac{p(x_{A},x_{B};\mu,\Sigma)}{\int_{x_{B}\in R^{d}}p(x_{A},x_{B};\mu,\Sigma)dx_{B}}\\
\\
x_{A}|x_{B}&\sim \mathcal{N}(\mu_{A}+\Sigma_{AB}\Sigma_{BB}^{-1}(x_{B}-\mu_{B}),\Sigma_{AA}-\Sigma_{AB}\Sigma_{BB}^{-1}\Sigma_{BA})\\
x_{B}|x_{A}&\sim \mathcal{N}(\mu_{B}+\Sigma_{BA}\Sigma_{AA}^{-1}(x_{A}-\mu_{A}),\Sigma_{BB}-\Sigma_{BA}\Sigma_{AA}^{-1}\Sigma_{AB})
\end{aligned}
$$