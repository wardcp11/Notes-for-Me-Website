---
title: ODE Solving Methods
tags:
  - ODE
created: 2025-01-01
status:
aliases:
  - Runge-Kutta
  - Linear Multistep
---
Ode solvers are a class of techniques to solve IVP systems of [ordinary differential equations](https://en.wikipedia.org/wiki/Ordinary_differential_equation). The general form can be seen below.
$$
\frac{\partial}{\partial t} = f(t,\mathbf{y}(t)), \mathbf{y}(t_0)=\mathbf{y}_0
$$
General integrators include Runge-Kutta and Linear Multistep methods. 

## Runge-Kutta 

Runge-Kutta methods use only the latest point and a variable step size to establish a weighted average for some desired point. This method relies on matching terms in the Taylor Series to establish some approximation error. A general description can be seen below.
$$
\begin{align*}
\mathbf{y}_{n+1}&=\mathbf{y}_n+h\sum _{j=1}^v b_j f(t_n+c_j h,\xi _j)\\
\xi _j&=\mathbf{y}_n+h \sum_{i=1}^v a_{ji} f(t_n+c_ih, \xi_i)
\end{align*}
$$
The components $a,b,$ and $c$ are components of matrix $A$ and vectors $\mathbf{b},\mathbf{c}$ respectively. These form a structure known as a Butcher tableau that describes how to form the weighted average. These methods include implicit forms which require a root solver e.g. [Backward Euler](https://en.wikipedia.org/wiki/Backward_Euler_method).
## Linear Multistep

Linear Multistep methods rely on creating an interpolating polynomial for previous points and integrating. The general form for these methods can be seen below.
$$
\sum_{j=0}^sa_j \mathbf{y}_{n+j}=h\sum_{j=0}^s b_jf(t_{n+j},\mathbf{y}_{n+j})
$$
Values for $a$ and $b$ are vector values depending on the order of linear multi step method desired. These methods include: BDF, Adams-Bashforth, and Adams-Moulton. Adams-Bashforth methods construct the interpolating polynomial(which is unique) for the last s+1 measurements.

These methods tend to require being "started" by an equal order Runge-Kutta method.