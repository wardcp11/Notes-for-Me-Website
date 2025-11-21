---
title: ODE Solving Methods
tags:
  - ODE
created: 2025-01-01
draft: false
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
The components $a,b,$ and $c$ are components of matrix $A$ and vectors $\mathbf{b},\mathbf{c}$ respectively. These form a structure known as a Butcher tableau that describes how to form the weighted average.