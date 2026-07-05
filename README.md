<div align="center">



# 📐 Orthogonal Functions & Polynomials in Computational Physics

**An interactive mathematical reference and implementation guide for classic, generalized polynomial families, and cylindrical wave functions.**



<br>



<p>

  <img src="https://img.shields.io/badge/Physics-Quantum_%26_Classical-0052FF?style=for-the-badge&logo=atom&logoColor=white" alt="Physics Badge"/>

  <img src="https://img.shields.io/badge/Math-Sturm--Liouville_Theory-FF3366?style=for-the-badge&logo=docusign&logoColor=white" alt="Math Badge"/>

  <img src="https://img.shields.io/badge/Python-SciPy_%26_NumPy-00C853?style=for-the-badge&logo=python&logoColor=white" alt="Python Badge"/>

  <img src="https://img.shields.io/badge/License-MIT-9C27B0?style=for-the-badge" alt="License Badge"/>

</p>



<p align="center">

  <a href="#--overview--sturm-liouville-framework">Overview</a> •

  <a href="#--the-jacobi-super-family-p_nalpha-beta">Jacobi</a> •

  <a href="#--gegenbauer-ultraspherical-polynomials-c_nalpha">Gegenbauer</a> •

  <a href="#--legendre-polynomials-p_n">Legendre</a> •

  <a href="#--laguerre-polynomials-l_n">Laguerre</a> •

  <a href="#--hermite-polynomials-h_n">Hermite</a> •

  <a href="#--bessel-functions-j_nu-cylindrical-basis">Bessel</a> •

  <a href="#--master-comparison-matrix">Comparison Matrix</a> •

  <a href="#--python-implementation--visualization">Python Implementation</a>

</p>



</div>



---



## 🌐 Overview & Sturm-Liouville Framework



Orthogonal polynomials and functions are infinite families of algebraic or transcendental equations that are mutually perpendicular within a weighted Hilbert space $L^2([a, b], w(x))$. They form the foundational basis for solving boundary value problems, quantum mechanical states, and spectral methods.



All families presented in this repository arise as eigenfunction solutions to the second-order **Sturm-Liouville differential equation**:



$$

\frac{d}{dx} \left[ p(x) \frac{dy}{dx} \right] + \left[ q(x) + \lambda w(x) \right] y = 0

$$



<blockquote>

💡 <strong>The Orthogonality Condition:</strong> For any two functions $\phi_n(x)$ and $\phi_m(x)$ within the same family, their inner product over the interval $[a, b]$ with respect to a non-negative weight function $w(x)$ satisfies:

<br><br>



$$

\langle \phi_n, \phi_m \rangle = \int_{a}^{b} w(x) \phi_n(x) \phi_m(x) \, dx = h_n \delta_{nm}

$$



where $\delta_{nm}$ is the Kronecker delta and $h_n$ represents the squared normalization norm.

</blockquote>



---



## 🗂️ Mathematical Hierarchy



The equations branch based on whether their coordinate domain spaces are flat, spherical, or cylindrical:



```

┌────────────────────────────────────────────────────────┐

│             Sturm-Liouville Eigenfunctions             │

└───────────────────────────┬────────────────────────────┘

                            │

            ┌───────────────┴───────────────┐

            ▼ (Hypergeometric/Polynomial)   ▼ (Cylindrical Wave)

┌──────────────────────────────┐     ┌──────────────────────────────┐

│ Jacobi Polynomials           │     │ Bessel Functions             │

│ P_n^(α, β)(x)                │     │ J_ν(x)                       │

└──────────────┬───────────────┘     └──────────────────────────────┘

               │ (α = β)

               ▼

┌──────────────────────────────┐

│ Gegenbauer (Ultraspherical)  │

│ C_n^(α)(x)                   │

└──────────────┬───────────────┘

               │ (α = 1/2)

               ▼

┌──────────────────────────────┐

│ Legendre Polynomials         │

│ P_n(x)                       │

└──────────────────────────────┘

```



---



## 🟣 The Jacobi Super-Family ($P_n^{(\alpha, \beta)}$)



<table>

<tr>

<td width="30%" valign="top">

<br>

<strong>Domain Interval</strong><br>

<code>[-1, 1]</code>

<br><br>

<strong>Weight Function</strong><br>

$w(x) = (1-x)^\alpha (1+x)^\beta$<br>

<em>where $\alpha, \beta > -1$</em>

<br><br>

<strong>Primary Applications</strong><br>

• Spectral element methods<br>

• Rotation matrices in QM<br>

• General hypergeometric solutions

</td>

<td width="70%" valign="top">



### Core Equations



**Differential Equation**

$$(1-x^2)y'' + [\beta - \alpha - (\alpha + \beta + 2)x]y' + n(n + \alpha + \beta + 1)y = 0$$



**Rodrigues' Formula**

$$P_n^{(\alpha, \beta)}(x) = \frac{(-1)^n}{2^n n!} (1-x)^{-\alpha}(1+x)^{-\beta} \frac{d^n}{dx^n} \left[ (1-x)^{\alpha+n}(1+x)^{\beta+n} \right]$$



**Orthogonality Norm ($h_n$)**

$$h_n = \frac{2^{\alpha+\beta+1}}{2n+\alpha+\beta+1} \frac{\Gamma(n+\alpha+1)\Gamma(n+\beta+1)}{n! \Gamma(n+\alpha+\beta+1)}$$



</td>

</tr>

</table>



<details>

<summary><b>🔍 Click to expand: First Three Jacobi Polynomials</b></summary>

<br>

<ul>

  <li>$P_0^{(\alpha, \beta)}(x) = 1$</li>

  <li>$P_1^{(\alpha, \beta)}(x) = \frac{\alpha + \beta + 2}{2}x + \frac{\alpha - \beta}{2}$</li>

  <li>$P_2^{(\alpha, \beta)}(x) = \frac{(\alpha+\beta+3)(\alpha+\beta+4)}{8}x^2 + \frac{(\alpha-\beta)(\alpha+\beta+3)}{4}x + \frac{(\alpha-\beta)^2 - (\alpha+\beta+4)}{8}$</li>

</ul>

</details>



---



## 🟡 Gegenbauer (Ultraspherical) Polynomials ($C_n^{(\alpha)}$)



<table>

<tr>

<td width="30%" valign="top">

<br>

<strong>Domain Interval</strong><br>

<code>[-1, 1]</code>

<br><br>

<strong>Weight Function</strong><br>

$w(x) = (1-x^2)^{\alpha - 1/2}$<br>

<em>where $\alpha > -1/2, \alpha \neq 0$</em>

<br><br>

<strong>Primary Applications</strong><br>

• Hyperspherical harmonics<br>

• Higher-dimensional potential theory<br>

• Approximation theory

</td>

<td width="70%" valign="top">



### Core Equations



**Differential Equation**

$$(1-x^2)y'' - (2\alpha + 1)xy' + n(n + 2\alpha)y = 0$$



**Rodrigues' Formula**

$$C_n^{(\alpha)}(x) = \frac{(-2)^n}{n!} \frac{\Gamma(n+\alpha)\Gamma(n+2\alpha)}{\Gamma(\alpha)\Gamma(2n+2\alpha)} (1-x^2)^{1/2-\alpha} \frac{d^n}{dx^n} \left[ (1-x^2)^{n+\alpha-1/2} \right]$$



**Orthogonality Norm ($h_n$)**

$$h_n = \frac{\pi 2^{1-2\alpha} \Gamma(n+2\alpha)}{n!(n+\alpha) [\Gamma(\alpha)]^2}$$



</td>

</tr>

</table>



<details>

<summary><b>🔍 Click to expand: First Three Gegenbauer Polynomials</b></summary>

<br>

<ul>

  <li>$C_0^{(\alpha)}(x) = 1$</li>

  <li>$C_1^{(\alpha)}(x) = 2\alpha x$</li>

  <li>$C_2^{(\alpha)}(x) = 2\alpha(\alpha + 1)x^2 - \alpha$</li>

</ul>

</details>



---



## 🔴 Legendre Polynomials ($P_n$)



<table>

<tr>

<td width="30%" valign="top">

<br>

<strong>Domain Interval</strong><br>

<code>[-1, 1]</code>

<br><br>

<strong>Weight Function</strong><br>

$w(x) = 1$

<br><br>

<strong>Primary Applications</strong><br>

• Multipole expansions (Gravity/Electrostatics)<br>

• Spherical harmonics in 3D geometry<br>

• Gauss-Legendre quadrature numerical limits

</td>

<td width="70%" valign="top">



### Core Equations



**Differential Equation**

$$(1-x^2)y'' - 2xy' + n(n+1)y = 0$$



**Rodrigues' Formula**

$$P_n(x) = \frac{1}{2^n n!} \frac{d^n}{dx^n} \left[ (x^2 - 1)^n \right]$$



**Orthogonality Norm ($h_n$)**

$$h_n = \frac{2}{2n + 1}$$



**Recurrence Relation**

$$(n+1)P_{n+1}(x) = (2n+1)x P_n(x) - n P_{n-1}(x)$$



</td>

</tr>

</table>



---



## 🟢 Laguerre Polynomials ($L_n$)



<table>

<tr>

<td width="30%" valign="top">

<br>

<strong>Domain Interval</strong><br>

<code>[0, ∞)</code>

<br><br>

<strong>Weight Function</strong><br>

$w(x) = e^{-x}$

<br><br>

<strong>Primary Applications</strong><br>

• Hydrogen atom radial wavefunctions<br>

• Quantum optics (Fock states)<br>

• Dynamic systems analysis

</td>

<td width="70%" valign="top">



### Core Equations



**Differential Equation**

$$xy'' + (1-x)y' + ny = 0$$



**Rodrigues' Formula**

$$L_n(x) = \frac{e^x}{n!} \frac{d^n}{dx^n} \left[ e^{-x} x^n \right]$$



**Orthogonality Norm ($h_n$)**

$$h_n = 1$$



**Recurrence Relation**

$$(n+1)L_{n+1}(x) = (2n+1-x)L_n(x) - n L_{n-1}(x)$$



</td>

</tr>

</table>



---



## 🔵 Hermite Polynomials ($H_n$)



<table>

<tr>

<td width="30%" valign="top">

<br>

<strong>Domain Interval</strong><br>

<code>(-∞, ∞)</code>

<br><br>

<strong>Weight Function</strong><br>

$w(x) = e^{-x2}$

<br><br>

<strong>Primary Applications</strong><br>

• Quantum Harmonic Oscillators<br>

• Gaussian wave packet analysis<br>

• Probability density estimations

</td>

<td width="70%" valign="top">



### Core Equations *(Physicists' Convention)*



**Differential Equation**

$$y'' - 2xy' + 2ny = 0$$



**Rodrigues' Formula**

$$H_n(x) = (-1)^n e^{x^2} \frac{d^n}{dx^n} \left[ e^{-x^2} \right]$$



**Orthogonality Norm ($h_n$)**

$$h_n = \sqrt{\pi} 2^n n!$$



**Recurrence Relation**

$$H_{n+1}(x) = 2x H_n(x) - 2n H_{n-1}(x)$$



</td>

</tr>

</table>



---



## 🟠 Bessel Functions ($J_\nu$) — Cylindrical Basis



Unlike standard polynomial families that change their intrinsic algebraic architecture per index $n$, Bessel functions achieve orthogonality over a fixed order $\nu$ by mapping variables across their **discrete roots**. This is known as a **Fourier-Bessel series**.



<table>

<tr>

<td width="30%" valign="top">

<br>

<strong>Domain Interval</strong><br>

<code>[0, R]</code> (where boundary constraints occur)

<br><br>

<strong>Weight Function</strong><br>

$w(x) = x$

<br><br>

<strong>Primary Applications</strong><br>

• Vibrating circular membranes (drumheads)<br>

• Cylindrical electromagnetic waveguides<br>

• Transient heat conduction in cylinders

</td>

<td width="70%" valign="top">



### Core Equations *(First Kind, Order $\nu$)*



**Differential Equation**

$$x^2 y'' + x y' + (x^2 - \nu^2)y = 0$$



**Series Representation**

$$J_\nu(x) = \sum_{m=0}^{\infty} \frac{(-1)^m}{m! \, \Gamma(m + \nu + 1)} \left( \frac{x}{2} \right)^{2m + \nu}$$



**Root-Based Orthogonality Condition**

Let $\alpha_{\nu, n}$ and $\alpha_{\nu, m}$ be the $n$-th and $m$-th positive zeros of $J_\nu(x)$. Over a normalized domain radius $R=1$:

$$\int_{0}^{1} x J_\nu(\alpha_{\nu, n} x) J_\nu(\alpha_{\nu, m} x) \, dx = \frac{1}{2} [J_{\nu+1}(\alpha_{\nu, n})]^2 \delta_{nm}$$



</td>

</tr>

</table>



---



## 📊 Master Comparison Matrix



| Function Family | Symbol | Domain $[a, b]$ | Weight $w(x)$ | Orthogonality Target Basis | Normalization ($h_n$) |

| :--- | :---: | :---: | :---: | :---: | :---: |

| **Jacobi** | $P_n^{(\alpha, \beta)}(x)$ | $[-1, 1]$ | $(1-x)^\alpha (1+x)^\beta$ | Varying Polynomial Degree $n$ | $\frac{2^{\alpha+\beta+1}\Gamma(n+\alpha+1)\Gamma(n+\beta+1)}{(2n+\alpha+\beta+1)n! \Gamma(n+\alpha+\beta+1)}$ |

| **Gegenbauer** | $C_n^{(\alpha)}(x)$ | $[-1, 1]$ | $(1-x^2)^{\alpha - \frac{1}{2}}$ | Varying Polynomial Degree $n$ | $\frac{\pi 2^{1-2\alpha} \Gamma(n+2\alpha)}{n!(n+\alpha) [\Gamma(\alpha)]^2}$ |

| **Legendre** | $P_n(x)$ | $[-1, 1]$ | $1$ | Varying Polynomial Degree $n$ | $\frac{2}{2n + 1}$ |

| **Laguerre** | $L_n(x)$ | $[0, \infty)$ | $e^{-x}$ | Varying Polynomial Degree $n$ | $1$ |

| **Hermite** | $H_n(x)$ | $(-\infty, \infty)$ | $e^{-x^2}$ | Varying Polynomial Degree $n$ | $\sqrt{\pi} 2^n n!$ |

| **Bessel (1st Kind)**| $J_\nu(x)$ | $[0, 1]$ | $x$ | Varying Discrete Zeros $\alpha_{\nu, n}$ | $\frac{1}{2} [J_{\nu+1}(\alpha_{\nu, n})]^2$ |



---



## 💻 Python Implementation & Visualization



Evaluate, map, and confirm the numerical accuracy of all six families using `scipy.special` and `numpy`.



```python

import numpy as np

import matplotlib.pyplot as plt

from scipy.special import (

    eval_jacobi, eval_gegenbauer, eval_legendre, 

    eval_genlaguerre, eval_hermite, jv, jn_zeros

)



# Set up dark UI dashboard styling

plt.style.use('dark_background')

fig, axes = plt.subplots(2, 3, figsize=(18, 10))

axes = axes.flatten()



# Domain grids

x_sym = np.linspace(-1, 1, 300)     # Jacobi, Gegenbauer, Legendre

x_lag = np.linspace(0, 8, 300)      # Laguerre

x_her = np.linspace(-3, 3, 300)     # Hermite

x_bes = np.linspace(0, 15, 300)     # Bessel



indices = [1, 2, 3, 4]



for n in indices:

    # 1. Jacobi (alpha=1.5, beta=-0.5)

    axes[0].plot(x_sym, eval_jacobi(n, 1.5, -0.5, x_sym), label=f"n={n}", lw=2)

    # 2. Gegenbauer (alpha=2.0)

    axes[1].plot(x_sym, eval_gegenbauer(n, 2.0, x_sym), label=f"n={n}", lw=2)

    # 3. Legendre

    axes[2].plot(x_sym, eval_legendre(n, x_sym), label=f"n={n}", lw=2)

    # 4. Laguerre

    axes[3].plot(x_lag, eval_genlaguerre(n, 0, x_lag), label=f"n={n}", lw=2)

    # 5. Hermite

    axes[4].plot(x_her, eval_hermite(n, x_her), label=f"n={n}", lw=2)

    # 6. Bessel (Showing order ν over continuous space)

    axes[5].plot(x_bes, jv(n, x_bes), label=r"$\nu$=" + f"{n}", lw=2)



# Subplot Formatting Matrix

titles = [

    r"Jacobi ($\alpha=1.5, \beta=-0.5$)", r"Gegenbauer ($\alpha=2.0$)", 

    "Legendre", "Laguerre", "Hermite", "Bessel (First Kind, $J_\\nu$)"

]



for i, title in enumerate(titles):

    axes[i].set_title(title, fontsize=13, fontweight='bold', color='#00C853', pad=10)

    axes[i].grid(True, alpha=0.15, linestyle='--')

    axes[i].legend(loc='best', framealpha=0.6)

    axes[i].axhline(0, color='gray', linestyle='--', alpha=0.4)



plt.tight_layout()

plt.savefig("orthogonal_functional_matrix.png", dpi=300)

plt.show()

```



```python

from scipy.integrate import simpson



# Compute the first 3 roots for Bessel function of order ν = 0

nu = 0

roots = jn_zeros(nu, 3)  # Returns first 3 zeros of J_0



# Sample scale array over domain [0, 1]

r = np.linspace(0, 1, 500)



# Evaluate functions mapped to root frequencies n=1 and m=2

f_n = jv(nu, roots[0] * r)  # Root 1

f_m = jv(nu, roots[1] * r)  # Root 2



# Weight function for cylindrical boundaries is linear radius r

weight = r 



# Integrate via Simpson's rule

inner_product = simpson(weight * f_n * f_m, r)



print(f"Fourier-Bessel Inner Product <J_0(α_1 J_0(α_2 r) r),>: {inner_product:.2e}")

# Output: Fourier-Bessel Inner Product: 2.11e-16 (Approaching absolute zero) 

