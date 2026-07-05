<div align="center">

# 📐 Orthogonal Polynomials in Computational Physics & Mathematics
**A comprehensive reference and implementation guide for Legendre, Laguerre, and Hermite polynomials.**

<p>
  <img src="https://img.shields.io/badge/Physics-Quantum%20%26%20Classical-blue?style=for-the-badge&logo=atom" alt="Physics Badge"/>
  <img src="https://img.shields.io/badge/Math-Sturm--Liouville%20Theory-darkred?style=for-the-badge" alt="Math Badge"/>
  <img src="https://img.shields.io/badge/Python-SciPy%20%26%20NumPy-green?style=for-the-badge&logo=python" alt="Python Badge"/>
  <img src="https://img.shields.io/badge/License-MIT-purple?style=for-the-badge" alt="License Badge"/>
</p>

</div>

---

## 📖 Table of Contents
- [Overview & Mathematical Framework](#-overview--mathematical-framework)
- [Legendre Polynomials ($P_n$)](#-legendre-polynomials-p_n)
- [Laguerre Polynomials ($L_n$)](#-laguerre-polynomials-l_n)
- [Hermite Polynomials ($H_n$)](#-hermite-polynomials-h_n)
- [Quick Reference & Comparison Table](#-quick-reference--comparison-table)
- [Python Implementation](#-python-implementation)
- [Contributing & License](#-contributing--license)

---

## 🌐 Overview & Mathematical Framework

Orthogonal polynomials are infinite families of polynomials that are orthogonal to each other under a defined inner product in a weighted Hilbert space $L^2([a, b], w(x))$. They arise naturally as eigenfunction solutions to second-order linear differential equations of the **Sturm-Liouville** form:

$$
\frac{d}{dx} \left[ p(x) \frac{dy}{dx} \right] + \left[ q(x) + \lambda w(x) \right] y = 0
$$

### The Orthogonality Condition
For any two polynomials $P_n(x)$ and $P_m(x)$ of degrees $n$ and $m$ within the same family, their inner product over the interval $[a, b]$ with respect to a non-negative weight function $w(x)$ satisfies:

$$
\langle P_n, P_m \rangle = \int_{a}^{b} w(x) P_n(x) P_m(x) \, dx = c_n \delta_{nm}
$$

where $\delta_{nm}$ is the Kronecker delta and $c_n$ is a normalization constant.

---

## 🔴 Legendre Polynomials ($P_n$)

Legendre polynomials are standard solutions to Legendre's differential equation, occurring widely in Newtonian gravity, electrostatics (multipole expansions), and spherical harmonics.

* **Domain Interval:** $[-1, 1]$
* **Weight Function:** $w(x) = 1$

### Core Equations

| Description | Formula |
| :--- | :--- |
| **Differential Equation** | $(1-x^2)y'' - 2xy' + n(n+1)y = 0$ |
| **Rodrigues' Formula** | $P_n(x) = \frac{1}{2^n n!} \frac{d^n}{dx^n} [(x^2 - 1)^n]$ |
| **Orthogonality Norm** | $\int_{-1}^{1} P_n(x) P_m(x) \, dx = \frac{2}{2n + 1} \delta_{nm}$ |
| **Recurrence Relation** | $(n+1)P_{n+1}(x) = (2n+1)x P_n(x) - n P_{n-1}(x)$ |

<details>
<summary><b>Click to expand: First Four Legendre Polynomials</b></summary>

<br>

<ul>
  <li>$P_0(x) = 1$</li>
  <li>$P_1(x) = x$</li>
  <li>$P_2(x) = \frac{1}{2}(3x^2 - 1)$</li>
  <li>$P_3(x) = \frac{1}{2}(5x^3 - 3x)$</li>
</ul>
</details>

---

## 🟢 Laguerre Polynomials ($L_n$)

Laguerre polynomials and their generalized (associated) counterparts $L_n^{(\alpha)}(x)$ are critical in quantum mechanics, specifically for solving the radial part of the Schrödinger equation for a one-electron atom (the Hydrogen atom).

* **Domain Interval:** $[0, \infty)$
* **Weight Function:** $w(x) = e^{-x}$ *(Standard)* or $w(x) = x^\alpha e^{-x}$ *(Generalized)*

### Core Equations (Standard Form)

| Description | Formula |
| :--- | :--- |
| **Differential Equation** | $xy'' + (1-x)y' + ny = 0$ |
| **Rodrigues' Formula** | $L_n(x) = \frac{e^x}{n!} \frac{d^n}{dx^n} \left[ e^{-x} x^n \right]$ |
| **Orthogonality Norm** | $\int_{0}^{\infty} e^{-x} L_n(x) L_m(x) \, dx = \delta_{nm}$ |
| **Recurrence Relation** | $(n+1)L_{n+1}(x) = (2n+1-x)L_n(x) - n L_{n-1}(x)$ |

<details>
<summary><b>Click to expand: First Four Laguerre Polynomials</b></summary>

<br>

<ul>
  <li>$L_0(x) = 1$</li>
  <li>$L_1(x) = -x + 1$</li>
  <li>$L_2(x) = \frac{1}{2}(x^2 - 4x + 2)$</li>
  <li>$L_3(x) = \frac{1}{6}(-x^3 + 9x^2 - 18x + 6)$</li>
</ul>
</details>

---

## 🔵 Hermite Polynomials ($H_n$)

Hermite polynomials exist in two conventions: the **Physicists' form** $H_n(x)$ (used in quantum harmonic oscillators) and the **Probabilists' form** $He_n(x)$ (used in Gaussian probability and Edgeworth series). Below is the *Physicists' standard*.

* **Domain Interval:** $(-\infty, \infty)$
* **Weight Function:** $w(x) = e^{-x^2}$

### Core Equations (Physicists' Form)

| Description | Formula |
| :--- | :--- |
| **Differential Equation** | $y'' - 2xy' + 2ny = 0$ |
| **Rodrigues' Formula** | $H_n(x) = (-1)^n e^{x^2} \frac{d^n}{dx^n} \left[ e^{-x^2} \right]$ |
| **Orthogonality Norm** | $\int_{-\infty}^{\infty} e^{-x^2} H_n(x) H_m(x) \, dx = \sqrt{\pi} 2^n n! \delta_{nm}$ |
| **Recurrence Relation** | $H_{n+1}(x) = 2x H_n(x) - 2n H_{n-1}(x)$ |

<details>
<summary><b>Click to expand: First Four Hermite Polynomials</b></summary>

<br>

<ul>
  <li>$H_0(x) = 1$</li>
  <li>$H_1(x) = 2x$</li>
  <li>$H_2(x) = 4x^2 - 2$</li>
  <li>$H_3(x) = 8x^3 - 12x$</li>
</ul>
</details>

---

## 📊 Quick Reference & Comparison Table

<div align="center">

| Polynomial Family | Symbol | Interval $[a, b]$ | Weight $w(x)$ | Normalization $c_n$ | Primary Physical Application |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Legendre** | $P_n(x)$ | $[-1, 1]$ | $1$ | $\frac{2}{2n + 1}$ | Multipole expansion, Spherical Harmonics |
| **Laguerre** | $L_n(x)$ | $[0, \infty)$ | $e^{-x}$ | $1$ | Hydrogen atom radial wavefunctions |
| **Hermite** | $H_n(x)$ | $(-\infty, \infty)$ | $e^{-x^2}$ | $\sqrt{\pi} 2^n n!$ | Quantum Harmonic Oscillator, Gaussian Quadrature |

</div>

---

## 💻 Python Implementation

You can easily evaluate and visualize these polynomials using `scipy.special` and `numpy`.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.special import eval_legendre, eval_genlaguerre, eval_hermite

# 1. Setup domains for each family
x_leg = np.linspace(-1, 1, 200)
x_lag = np.linspace(0, 5, 200)
x_her = np.linspace(-2.5, 2.5, 200)

# 2. Evaluate degree n=3 for each polynomial family
n = 3
p_3 = eval_legendre(n, x_leg)
l_3 = eval_genlaguerre(n, 0, x_lag)  # alpha=0 for standard Laguerre
h_3 = eval_hermite(n, x_her)

# 3. Verification of Orthogonality (Legendre n=2 and n=3)
p_2 = eval_legendre(2, x_leg)
integral_approx = np.trapz(p_2 * p_3, x_leg)
print(f"Legendre P_2 and P_3 inner product (should be ~0): {integral_approx:.2e}")
