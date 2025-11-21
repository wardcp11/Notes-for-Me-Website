---
title: Three Body Problem
tags:
  - ODE
created: 2025-01-01
status: Almost Complete
---
## Problem Statement:
We want to find the system of ordinary differential equations for 3 bodies in free space isolated from all other matter.

## Solution:
Beginning the problem as simple as possible requires us to assign 3 particles positions.

Let $\bf{\hat{r}_1}, \bf{\hat{r}_2}, \bf{\hat{r}_3}$ be the position vectors of particles 1-3 respectively. To solve this problem numerically we can begin at forces between objects.

We can make the assumption that bodies obey Newtonian gravity. The force applied on body $m$ exerted on body $n$.
$$
\mathbf{F_{mn}}=-G\frac{m_m m_n}{r^2} \mathbf{\hat{r}_{mn}}
$$
With direction vector given as
$$
\mathbf{\hat{r}_{mn}} = \frac{\mathbf{\hat{r}}_m - \mathbf{\hat{r}}_n}{|\mathbf{\hat{r}}_m - \mathbf{\hat{r}}_n|}
$$
Where $r$
$$
r=|\mathbf{\hat{r}_m} - \mathbf{\hat{r}_n}|
$$
To ease the problem we need to break the problem into orthogonal components, e.g. $\bf{\hat{x}}, \bf{\hat{y}},  \bf{\hat{z}}$.
$$
\begin{align*}
F_x &= \mathbf{F} \cdot \mathbf{\hat{x}} \longleftrightarrow \mathbf{F_x} = [F_x, F_y, F_z][1,0,0]^T\\
F_y &= \mathbf{F} \cdot \mathbf{\hat{y}} \longleftrightarrow \mathbf{F_y} = [F_x, F_y, F_z][0,1,0]^T\\
F_z &= \mathbf{F} \cdot \mathbf{\hat{z}} \longleftrightarrow \mathbf{F_z} = [F_x, F_y, F_z][0,0,1]^T\\
\end{align*}
$$
Plugging in the full formula for the forces.
$$
\begin{align*}
F_{mn,x} = -G\frac{m_1 m_2}{r^2} \frac{\mathbf{\hat{r}}_m - \mathbf{\hat{r}}_n}{|\mathbf{\hat{r}}_m - \mathbf{\hat{r}}_n|} \cdot \bf{\hat{x}}\\
F_{mn,y} = -G\frac{m_1 m_2}{r^2} \frac{\mathbf{\hat{r}}_m - \mathbf{\hat{r}}_n}{|\mathbf{\hat{r}}_m - \mathbf{\hat{r}}_n|} \cdot \bf{\hat{y}}\\
F_{mn,z} = -G\frac{m_1 m_2}{r^2} \frac{\mathbf{\hat{r}}_m - \mathbf{\hat{r}}_n}{|\mathbf{\hat{r}}_m - \mathbf{\hat{r}}_n|} \cdot \bf{\hat{z}}\\
\end{align*}
$$
Simplifying further using the definition for $r$.
$$
\begin{align*}
F_{mn,x} = -Gm_m m_n \frac{\mathbf{\hat{r}}_m - \mathbf{\hat{r}}_n}{|\hat{r}_m - \hat{r}_n|^{3/2}} \cdot \bf{\hat{x}}\\
F_{mn,y} = -Gm_m m_n \frac{\mathbf{\hat{r}}_m - \mathbf{\hat{r}}_n}{|\hat{r}_m - \hat{r}_n|^{3/2}} \cdot \bf{\hat{y}}\\
F_{mn,z} = -Gm_m m_n \frac{\mathbf{\hat{r}}_m - \mathbf{\hat{r}}_n}{|\hat{r}_m - \hat{r}_n|^{3/2}} \cdot \bf{\hat{z}}
\end{align*}
$$
Noticing that the only vector components are held in $\mathbf{\hat{r}_m} - \mathbf{\hat{r}_n}$.
$$
\begin{align*}
(\mathbf{\hat{r}_m}-\mathbf{\hat{r}_n})\cdot \mathbf{\hat{x}} &= x_m-x_n\\
(\mathbf{\hat{r}_m}-\mathbf{\hat{r}_n})\cdot \mathbf{\hat{y}} &= y_m-y_n\\
(\mathbf{\hat{r}_m}-\mathbf{\hat{r}_n})\cdot \mathbf{\hat{z}} &= z_m-z_n\\
\end{align*}
$$
This finally allows us to write our forces in the simplest form.
$$
\begin{align*}
F_{mn,x} = -Gm_m m_n \frac{\hat{x}_m - \hat{x}_n}{|\hat{r}_m - \hat{r}_n|^{3/2}}\\
F_{mn,y} = -Gm_m m_n \frac{\hat{y}_m - \hat{y}_n}{|\hat{r}_m - \hat{r}_n|^{3/2}}\\
F_{mn,z} = -Gm_m m_n \frac{\hat{z}_m - \hat{z}_n}{|\hat{r}_m - \hat{r}_n|^{3/2}}
\end{align*}
$$
Critically, the force on a single particle is the sum of the force from all other particles as shown below.
$$
F_m=\sum_{n\neq m}-G\frac{m_m m_n}{|\hat{r}_m - \hat{r}_n|^{3/2}} \mathbf{\hat{r}_{mn}}
$$
Dot products distribute under this and therefore
$$
\begin{align*}
F_{mx}&=F_{mix}+F_{mjx}\\ i,j&\neq m
\end{align*}
$$
### Note:
While it is likely not a good idea, it is possible to plug in the explicit definition for $r$. (This is likely the easiest way to implement in a generic coding language.)
$$
r=\sqrt{(x_m-x_n)^2 + (y_m-y_n)^2 + (z_m-z_n)^2}
$$
## Forming the System
$$
\frac{\partial}{\partial t}
\begin{bmatrix}
\mathbf{\hat{r}}_1\\
\mathbf{\hat{r}}_2\\
\mathbf{\hat{r}}_3\\
\mathbf{\hat{v}}_1\\
\mathbf{\hat{v}}_2\\
\mathbf{\hat{v}}_3
\end{bmatrix}=
\begin{bmatrix}
\mathbf{\hat{v}}_1\\
\mathbf{\hat{v}}_2\\
\mathbf{\hat{v}}_3\\
\mathbf{\hat{a}}_1\\
\mathbf{\hat{a}}_2\\
\mathbf{\hat{a}}_3
\end{bmatrix}=
\begin{bmatrix}
\mathbf{\hat{v}}_1\\
\mathbf{\hat{v}}_2\\
\mathbf{\hat{v}}_3\\
\mathbf{\hat{F}}_1/m_1\\
\mathbf{\hat{F}}_2/m_2\\
\mathbf{\hat{F}}_3/m_3
\end{bmatrix}
$$
We can now fully expand into components
$$
\frac{\partial}{\partial t}
\begin{bmatrix}
x_1\\
y_1\\
z_1\\
x_2\\
y_2\\
z_2\\
x_3\\
y_3\\
z_3\\
v_{1x}\\
v_{1y}\\
v_{1z}\\
v_{2x}\\
v_{2x}\\
v_{2x}\\
v_{3x}\\
v_{3x}\\
v_{3x}\\
\end{bmatrix}=
\begin{bmatrix}
v_{1x}\\
v_{1y}\\
v_{1z}\\
v_{2x}\\
v_{2x}\\
v_{2x}\\
v_{3x}\\
v_{3x}\\
v_{3x}\\
F_{1x}/m_1\\
F_{1y}/m_1\\
F_{1z}/m_1\\
F_{2x}/m_2\\
F_{2y}/m_2\\
F_{2z}/m_2\\
F_{3x}/m_3\\
F_{3y}/m_3\\
F_{3z}/m_3
\end{bmatrix}
=
\begin{bmatrix}
v_{1x}\\
v_{1y}\\
v_{1z}\\
v_{2x}\\
v_{2x}\\
v_{2x}\\
v_{3x}\\
v_{3x}\\
v_{3x}\\
(F_{12x} + F_{13x})/m_1\\
(F_{12y} + F_{13y})/m_1\\
(F_{12z} + F_{13z})/m_1\\
(F_{21x} + F_{23x})/m_2\\
(F_{21y} + F_{23y})/m_2\\
(F_{21z} + F_{23z})/m_2\\
(F_{31x} + F_{32x})/m_3\\
(F_{31y} + F_{32y})/m_3\\
(F_{31z} + F_{32z})/m_3\\
\end{bmatrix}
$$
Gross, but this is the most straightforward implementation of a force body diagram. This can be implemented using an [[ODE Solvers|ODE solver]]. A simplification to the system is possible by the use of [Jacobi coordinates](https://en.wikipedia.org/wiki/Jacobi_coordinates). I will attempt to do this at a later date.