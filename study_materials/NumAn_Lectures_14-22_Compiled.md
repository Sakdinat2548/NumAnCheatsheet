## Lecture 14: Data Fitting and Linear Regression

**Definition:**
Data fitting (regression) is distinguished from interpolation: interpolation requires the fitted function to pass through all data points, while data fitting seeks a function giving the *best overall approximation*, minimizing the sum of squared deviations.

**Definition (Data and Error):**
Given data $\{(x_0,y_0), (x_1,y_1), \dots, (x_n,y_n)\}$ ($n+1$ points), define the deviations
$$d_i = y_i - \phi(x_i), \quad i = 0,\dots,n$$

**Worked Example (Ways to estimate error):**
1. *Naive sum:* $S = \sum_{i=0}^n d_i$ — rejected because positive and negative errors can cancel.
   Example: $x_0=1,y_0=2$; $x_1=2,y_1=1$; fitted line through $(1,1),(2,2)$: $d_0 = 2-1=1$, $d_1=1-2=-1$, $S = d_0+d_1 = 0$.
2. *Absolute value:* $S = \sum_{i=0}^n |d_i|$ — rejected because $|\cdot|$ is not differentiable, inconvenient for minimization.
   Example: $S = |1| + |-1| = 2$.
3. *Squared error:* $S = \sum_{i=0}^n d_i^2$ — chosen method.
   Example: $S = 1^2 + (-1)^2 = 2$.

**Core Formula (General Fitting Setup):**
Let $\phi = \phi(x, a_0, a_1, \dots, a_\ell)$, $\ell \geq 1$, depend on parameters. Define
$$S = \sum_{i=0}^n d_i^2 = \sum_{i=0}^n \left(y_i - \phi(x_i, a_0,\dots,a_\ell)\right)^2$$
To minimize $S$, set partial derivatives to zero:
$$\frac{\partial S}{\partial a_k} = -2\sum_{i=0}^n \left(y_i - \phi(\cdots)\right)\frac{\partial \phi}{\partial a_k} = 0, \quad k = 0,\dots,\ell$$
This yields a system of $\ell+1$ equations.

**Theorem/Property (Minimum Conditions, One Variable Recall):**
For $y = \phi(x)$, minimum at $x_0$ requires:
(1) $\phi'(x_0) = 0$
(2) $\phi''(x_0) > 0$

**Theorem/Property (Minimum Conditions, Two Parameters):**
For $S = S(a_0, a_1)$, minimum requires:
(1) $\dfrac{\partial S}{\partial a_0} = 0,\ \dfrac{\partial S}{\partial a_1} = 0$
(2) Hessian matrix
$$H = \begin{pmatrix} \dfrac{\partial^2 S}{\partial a_0^2} & \dfrac{\partial^2 S}{\partial a_0 \partial a_1} \\ \dfrac{\partial^2 S}{\partial a_1 \partial a_0} & \dfrac{\partial^2 S}{\partial a_1^2} \end{pmatrix}$$
must be positive definite, i.e., for a symmetric $2\times2$ matrix: $\dfrac{\partial^2 S}{\partial a_0^2} > 0$ and $\det H > 0$.

**Core Formula (Linear Regression Model):**
$$\hat{y} = \phi(x) = a_0 + a_1 x$$

**Worked Example/Proof (Deriving the Normal Equations):**
$$\frac{\partial S}{\partial a_0} = -2\sum_{i=0}^n (y_i - a_0 - a_1 x_i) = 0$$
$$\frac{\partial S}{\partial a_1} = -2\sum_{i=0}^n (y_i - a_0 - a_1 x_i)x_i = 0$$
Dividing by $-2$ and expanding using $\sum(a+b) = \sum a + \sum b$:
$$\begin{cases} \sum_{i=0}^n y_i - (n+1)a_0 - a_1\sum_{i=0}^n x_i = 0 \\ \sum_{i=0}^n x_i y_i - a_0 \sum_{i=0}^n x_i - a_1 \sum_{i=0}^n x_i^2 = 0 \end{cases}$$
Dividing both equations by $(n+1)$:
$$\begin{cases} \dfrac{1}{n+1}\sum y_i - a_0 - \dfrac{a_1}{n+1}\sum x_i = 0 \\ \dfrac{1}{n+1}\sum x_i y_i - \dfrac{a_0}{n+1}\sum x_i - \dfrac{a_1}{n+1}\sum x_i^2 = 0 \end{cases} \quad (*)$$

**Definition (Averaged Values / Notation):**
$$\bar{x} = \frac{1}{n+1}\sum_{i=0}^n x_i, \quad \bar{y} = \frac{1}{n+1}\sum_{i=0}^n y_i$$
$$\overline{xy} = \frac{1}{n+1}\sum_{i=0}^n x_i y_i, \quad \overline{x^2} = \frac{1}{n+1}\sum_{i=0}^n x_i^2$$
Note: $\overline{x^2} \neq \bar{x}\cdot\bar{x}$.

**Core Formula (Linear Regression Parameters):**
From $(*)$: $a_0 + a_1\bar{x} = \bar{y}$ and $a_0\bar{x} + a_1\overline{x^2} = \overline{xy}$.
Using Cramer's rule with $\Delta = \overline{x^2} - \bar{x}\cdot\bar{x}$:
$$\boxed{a_1 = \frac{\overline{xy} - \bar{x}\bar{y}}{\overline{x^2} - \bar{x}\cdot\bar{x}}, \qquad a_0 = \bar{y} - a_1\bar{x}}$$

**Theorem/Property (Convexity / Hessian Positive Definiteness):**
$$\frac{\partial^2 S}{\partial a_0^2} = 2(n+1) > 0, \qquad \frac{\partial^2 S}{\partial a_0 \partial a_1} = 2\sum_{i=0}^n x_i, \qquad \frac{\partial^2 S}{\partial a_1^2} = 2\sum_{i=0}^n x_i^2$$
$$\det H = 4\left[(n+1)\sum_{i=0}^n x_i^2 - \left(\sum_{i=0}^n x_i\right)^2\right]$$
By the **Cauchy–Schwarz inequality**:
$$m\sum_{i=1}^m x_i^2 \geq \left(\sum_{i=1}^m x_i\right)\left(\sum_{i=1}^m x_i\right), \quad m = n+1$$
Hence $\det H \geq 0$; if there exist at least two distinct $x_i \neq x_j$, then $\det H > 0$, so $H$ is positive definite and the critical point is the unique global minimum (the objective is strictly convex).

**Worked Example (Battery Charging Data):**
Data: $t$ (minutes) $= 0,10,20,30,40,50,60$; charge (%) $= 5,10,15,25,35,40,45$; $n=6$.
$$\bar{x} = \frac{1}{7}(0+10+\cdots+60) = \frac{210}{7} = 30$$
$$\bar{y} = \frac{1}{7}(5+10+15+25+35+40+45) = \frac{175}{7} = 25$$
$$\overline{xy} = \frac{1}{7}\sum x_i y_i \approx 1035.71, \qquad \overline{x^2} = \frac{1}{7}\sum x_i^2 = 1300$$
$$a_1 = \frac{1035.71 - 30\cdot25}{1300 - 30^2} \approx 0.714285 \approx 0.714$$
$$a_0 = 25 - 0.714\cdot 30 = 3.57$$
$$\boxed{\phi(x) = 0.714x + 3.57}$$

**Core Formula (Excel Method):**
In MS Excel (or free alternatives): select two data columns → **Insert → Scatter Plot** → add a linear trendline; Excel displays the regression equation.

---

## Lecture 15: Multivariable Data Fitting and Linearization

**Core Formula (Multivariable Regression Model):**
$$\hat{y} = \phi(x_1, x_2, \dots, x_m) = a_0 + a_1 x_1 + a_2 x_2 + \cdots + a_m x_m$$

**Definition (Notation for Multivariable Case):**
$\vec{x}^{(i)} = (x_1^{(i)}, x_2^{(i)}, \dots, x_m^{(i)})$ — point number $i$; index $j$ — dimension.
$$S(\vec{a}) = \sum_{i=0}^n \left(y^{(i)} - \phi(x_1^{(i)}, \dots, x_m^{(i)})\right)^2$$

**Core Formula (Matrix Form):**
$$X = \begin{pmatrix} 1 & x_1^{(0)} & x_2^{(0)} & \cdots & x_m^{(0)} \\ \vdots & & & & \vdots \\ 1 & x_1^{(n)} & x_2^{(n)} & \cdots & x_m^{(n)} \end{pmatrix}_{(n+1)\times(m+1)}, \quad \bar{a} = \begin{pmatrix}a_0\\a_1\\\vdots\\a_m\end{pmatrix}, \quad \bar{y} = \begin{pmatrix}y^{(0)}\\y^{(1)}\\\vdots\\y^{(n)}\end{pmatrix}$$
$$S(\vec{a}) = \|\bar{y} - X\bar{a}\|^2, \quad \text{where } \|\bar{u}\|^2 = u_0^2+u_1^2+\cdots+u_n^2$$

**Worked Example/Proof (Deriving the Normal Equations, Matrix Form):**
$$\frac{\partial S}{\partial a_0} = -2\sum_{i=0}^n (y_i - a_0 - a_1 x_i) = 0, \qquad \frac{\partial S}{\partial a_1} = -2\sum_{i=0}^n x_i(y_i - a_0 - a_1 x_i) = 0$$
In vector/matrix notation, the gradient condition $\nabla_{\bar a}\|\bar y - X\bar a\|^2 = 0$ gives:
$$X^T(\bar{y} - X\bar{a}) = 0 \implies X^T\bar{y} - X^TX\bar{a} = 0 \implies X^TX\bar{a} = X^T\bar{y}$$
Multiplying both sides by $(X^TX)^{-1}$:
$$\boxed{\bar{a} = (X^TX)^{-1}X^T\bar{y}}$$

**Definition (Pseudo-inverse Matrix):**
$$X^+ = (X^TX)^{-1}X^T$$
called the **Moore–Penrose pseudoinverse**. Remark: if $X$ is square ($n=m$), then $X^+ = X^{-1}(X^T)^{-1}X^T = X^{-1}$ (since $(X^T)^{-1}X^T = I$). In practice, typically $n \neq m$.

**Worked Example (Geometry of Linear Regression and ML, $m=2$):**
$$\hat{y} = \phi(x) = a_0 + a_1x_1 + a_2x_2$$
The plane $\hat{y}=0$, i.e. $a_0+a_1x_1+a_2x_2=0$, intersected with the $x_1x_2$-plane gives a **decision boundary** separating "class 1" and "class 2" points.
[Diagram: 3D plane $\hat y = a_0+a_1x_1+a_2x_2$ intersecting the $x_1,x_2$ plane; top-down view showing decision boundary separating two point classes]

**Core Formula (Logistic/Sigmoid Function, ML remark):**
$$\sigma(z) = \frac{1}{1+e^{-z}}$$
Maps $(-\infty,\infty) \to [0,1]$; used in ML for classification instead of a plain linear function: $\sigma(a_0+a_1x_1+a_2x_2) \in [0,1]$.

**Definition (Linearization/Straightening):**
Given coordinates $(x,y)$ and a curve $\ell = \ell(x,y)$, transform to new coordinates $(\xi,\eta)$ via $\xi = f(x,y)$, $\eta = g(x,y)$ so that $\ell$ becomes a straight line $\ell = \ell(\xi,\eta)$. This is called **straightening** or **linearization**. Analogously in 3D: $\xi=f(x,y,z)$, $\eta=g(x,y,z)$, $\zeta=h(x,y,z)$ transforming a surface $\pi(x,y,z)$ into a plane $\pi(\xi,\eta,\zeta)$.

**Core Formula (Standard Linearization Cases):**

1. $y = Ae^{Bx}$: Take $\ln y = \ln A + Bx$.
$$\tilde{x} = x,\quad \tilde{y} = \ln y,\quad a_0 = \ln A,\quad a_1 = B \quad\Longleftrightarrow\quad x=\tilde x,\ y=e^{\tilde y},\ A=e^{a_0},\ B=a_1$$

2. $y = Ax^n$: Take $\ln y = \ln A + n\ln x$.
$$\tilde{x} = \ln x,\quad \tilde{y} = \ln y,\quad a_0 = \ln A,\quad a_1 = n \quad\Longleftrightarrow\quad x=e^{\tilde x},\ y=e^{\tilde y},\ A=e^{a_0},\ n=a_1$$

3. $y = A + \dfrac{B}{x}$:
$$\tilde{x} = \frac{1}{x},\quad \tilde{y}=y,\quad a_0=A,\quad a_1=B \quad\Longleftrightarrow\quad x=\frac{1}{\tilde x},\ y=\tilde y,\ A=a_0,\ B=a_1$$

4. $y = \dfrac{1}{A+Bx}$: (Homework — slides by Prof. E. Schulz)

5. $y = \dfrac{Ax}{B+x}$: Take $\dfrac{1}{y} = \dfrac{1}{x}$-based substitution: let $\tilde y = 1/y$, $\tilde x = 1/x$.
$$\tilde{y} = \frac{B+\tilde x^{-1}\cdot(\ldots)}{A} \;\Rightarrow\; \tilde y = \frac{1}{A} + \frac{B}{A}\tilde x$$
$$y=\frac1{\tilde y},\ x=\frac1{\tilde x},\ a_0=\frac1A,\ a_1=\frac BA$$

**Remark:** Not every function can be linearized, e.g. $\phi(x) = a_0 e^{-x}\sin(a_1+2\pi x)$ — possibly not linearizable.
[Diagram: oscillating decaying curve that supposedly cannot be transformed into a straight line]

**Worked Example (Nonlinear Regression $y = \dfrac{Ax}{B+x}$):**
Data: $x=1,2,3,4$; $y=0.45,0.81,1.05,1.13$.
Substitutions: $\tilde x = 1/x$, $\tilde y = 1/y$.
$$\tilde x: 1,\ 0.5,\ 0.3(3),\ 0.25 \qquad \tilde y: 2.2(2),\ 1.235,\ 0.952,\ 0.885$$
Linear regression on $(\tilde x, \tilde y)$, $n=3$ (4 points):
$$\bar{\tilde x} = \frac14(1+0.5+0.33+0.25) \approx 0.52$$
$$\bar{\tilde y} \approx 1.3075, \qquad \overline{\tilde x\tilde y} \approx 0.8375, \qquad \overline{\tilde x^2} \approx 0.35535$$
$$a_1 = \frac{0.52\cdot1.3075 - 0.8375}{(0.52)^2 - 0.35535} \approx 1.855, \qquad a_0 = 1.3075 - 1.855\cdot0.52 \approx 0.743$$
$$\hat{\tilde y} = \tilde\phi(\tilde x) = 0.743 + 1.855\tilde x$$
Back-transform: $a_0 = 1/A \Rightarrow A = 1/a_0$; $a_1 = B/A \Rightarrow B = Aa_1 = a_1/a_0$.
$$y = \frac{\frac{1}{a_0}x}{\frac{a_1}{a_0}+x} \approx \frac{\frac{1}{0.743}x}{\frac{1.855}{0.743}+x} \approx \frac{1.346x}{2.497+x}$$
$$\boxed{y = \frac{1.346x}{2.497+x}}$$

**Core Formula (Nonlinear Regression Algorithm):**
1. Linearize the data via change of variables $\tilde x = f(x,y)$, $\tilde y = g(x,y)$.
2. Construct the linear regression model $\tilde y = a_0 + a_1\tilde x$ and find $a_0, a_1$.
3. Use the inverse transform to recover parameters $A, B$ of the nonlinear model from $a_0, a_1$.
4. Write down the nonlinear regression and check the fit.

---

## Lecture 16: Numerical Integration (Introduction)

**Core Formula (Definite Integral / Riemann Sum Approximation):**
$$I = \int_a^b f(x)\,dx$$
Partition $[a,b]$: $a = x_0 < x_1 < \cdots < x_n = b$, with subinterval width $h_i = x_i - x_{i-1}$.
For sample point $x_i^* \in [x_{i-1}, x_i]$:
$$\int_a^b f(x)\,dx \approx \sum_{i=1}^n f(x_i^*) h_i$$

[Diagram: Three-panel figure illustrating construction of a rectangle approximating area under $f(x)$ on $[x_{i-1},x_i]$: (1) choosing a subinterval, (2) choosing sample point $x_i^*$, (3) constructing the rectangle of height $f(x_i^*)$ and width $h_i$]

**Definition (Uniform Lattice):**
A lattice (grid/mesh) is **uniform** if $h_i = \text{const} = h$ for all $i$, where $h = \dfrac{b-a}{n}$. Then:
$$\int_a^b f(x)\,dx \approx h\sum_{i=1}^n f(x_i^*)$$
General (non-uniform) lattice: $h_i = x_i - x_{i-1}$, $i=1,\dots,n$ ($n+1$ points total).

**Definition (Riemann Integral):**
$$\int_a^b f(x)\,dx = \lim_{\max_j h_j \to 0} \sum_{i=1}^n h_i f(x_i^*)$$
**Restrictions on $f(x)$:** $|f(x)| < R < \infty$ (bounded on $[a,b]$); $f(x)$ can have only a countable number of jump discontinuities.
[Diagram: Function with a jump discontinuity still being integrable; function with countably many jumps (e.g. at $1,2,3,\dots,10^6$) still integrable]

**Remark:** A non-uniform grid is useful when the function changes rapidly on some parts of the interval and slowly on others — finer subintervals can be used where needed (regions of rapid change), coarser ones elsewhere.

**Worked Example (Choosing sample points, exercises):**
- $n=5$, uniform lattice, $x_i^* = x_{i-1} + h_i/3$: draw rectangles.
[Diagram: Rectangles constructed under a wavy function using sample points at $1/3$ into each subinterval]
- $h$ (should be $n=5$), $x_i^* = x_{i-1} + 2h_i/3$: draw rectangles.
[Diagram: Similar construction with sample points at $2/3$ into each subinterval]
- Non-uniform lattice, midpoint sample $x_i^* = \dfrac{x_{i-1}+x_i}{2}$: draw rectangles.
[Diagram: Non-uniform grid with midpoint rectangles under an oscillating function]

**Core Formula (Nonlinear Regression Algorithm — recap from Lecture 15):**
1. Linearize the data using a suitable change of variables $\tilde x = f(x,y)$, $\tilde y = g(x,y)$.
2. Construct linear regression $\tilde y = a_0 + a_1\tilde x$, determine $a_0,a_1$.
3. Inverse transform to get original parameters $A,B$.
4. Verify resulting nonlinear model fits original data.

---

## Lecture 17: Numerical Integration (Continued)

**Definition (Rectangle Rules):**
For subinterval $[x_{i-1}, x_i]$, choice of $x_i^*$:
1. **Left-rectangle rule:** $x_i^* = x_{i-1}$
2. **Right-rectangle rule:** $x_i^* = x_i$
3. **Midpoint rule:** $x_i^* = \dfrac{x_{i-1}+x_i}{2}$

**Theorem/Property (Accuracy Table):**
| Method | Error |
|---|---|
| Left-rectangle | $O(h)$ |
| Right-rectangle | $O(h)$ |
| Midpoint | $O(h^2)$ |

Remark: if $|h| < 1$, midpoint rule is generally best; if $|h| \geq 1$, left/right rules may be better.

**Worked Example ($I = \int_0^1 x^2\,dx$, uniform lattice $h=0.25$):**
Exact: $I = \dfrac{x^3}{3}\Big|_0^1 = \dfrac13 \approx 0.33(3)$.

*Left rectangle:*
$$\tilde I_{\text{Left}} = h(f_0+f_1+f_2+f_3), \quad x_0=0,x_1=\tfrac14,x_2=\tfrac12,x_3=\tfrac34$$
$$f_0=0,\ f_1=\tfrac1{16},\ f_2=\tfrac14,\ f_3=\tfrac34$$
$$\tilde I_{\text{Left}} = \tfrac14\left(0+\tfrac1{16}+\tfrac14+\tfrac{9}{16}\right) = \tfrac{17}{64} \approx 0.266$$
Absolute error: $e_A = |I - \tilde I| \approx |0.333-0.266| \approx 0.067$

*Midpoint rule:*
$$x_i^*: \tfrac18,\tfrac38,\tfrac58,\tfrac78; \qquad f_i^*: \tfrac1{64},\tfrac9{64},\tfrac{25}{64},\tfrac{49}{64}$$
$$\tilde I_{\text{Mid}} = h(f_1^*+f_2^*+f_3^*+f_4^*) = \tfrac14\cdot\tfrac{1+9+25+49}{64} = \tfrac{84}{256} \approx 0.328$$
$$e_A = |0.328-0.333| \approx 0.005$$

**Summary table of errors for $h=0.25$:**
| Rule | Absolute Error |
|---|---|
| Left-rect. | 0.067 |
| Midpoint | 0.005 |
| Trapezoid | 0.011 |

**Core Formula (Trapezoidal Rule Derivation):**
Area of a trapezoid with parallel sides $Q_1, Q_2$ and width $h$:
$$\text{Area} = A_1 + A_2 = hQ_1 + \frac{h}{2}(Q_2-Q_1) = h\left(\frac{Q_1+Q_2}{2}\right)$$

**Core Formula (Composite Trapezoidal Rule, general non-uniform grid):**
$$\tilde I_{\text{Tr}} = \frac12\sum_{i=1}^n \left(f(x_{i-1})+f(x_i)\right)h_i$$

**Core Formula (Left/Right/Midpoint Rules, general non-uniform grid):**
$$\tilde I_{\text{Left}} = \sum_{i=1}^n h_i f(x_{i-1}), \qquad \tilde I_{\text{Right}} = \sum_{i=1}^n h_i f(x_i), \qquad \tilde I_{\text{Mid}} = \sum_{i=1}^n h_i f\!\left(\frac{x_{i-1}+x_i}{2}\right)$$

**Core Formula (Uniform Lattice Versions):**
$$\tilde I_{\text{Left}}^{\text{uni}} = h\sum_{i=1}^n f(x_{i-1}), \qquad \tilde I_{\text{Right}}^{\text{uni}} = h\sum_{i=1}^n f(x_i), \qquad \tilde I_{\text{Mid}}^{\text{uni}} = h\sum_{i=1}^n f\!\left(\frac{x_{i-1}+x_i}{2}\right)$$
$$\boxed{\tilde I_{\text{Tr}}^{\text{uni}} = \frac{h(f_0+f_n)}{2} + h\sum_{i=1}^{n-1} f_i} \quad \left(O(h^2), \text{ same order as midpoint rule}\right)$$

**Worked Example (Trapezoidal Rule on $I=\int_0^1 x^2\,dx$, $h=0.25$):**
$$x_i: 0, \tfrac14, \tfrac12, \tfrac34, 1; \qquad f_i: 0, \tfrac1{16}, \tfrac14, \tfrac9{16}, 1$$
$$\tilde I_{\text{Tr}}^{\text{uni}} = \frac{\tfrac14(0+1)}{2} + \tfrac14\left(\tfrac1{16}+\tfrac14+\tfrac9{16}\right) = \tfrac18 + \tfrac{14}{4\cdot16} = \tfrac{4}{32}+\tfrac{7}{32} = \tfrac{11}{32} \approx 0.344$$
$$e_A = |0.333-0.344| = 0.011$$

---

## Lecture 18: Numerical Integration (Error Estimates — Completed)

**Theorem/Property (Error Estimate for the Left Rectangle Rule):**
For subinterval $[x_{i-1},x_i]$ of length $h_i$, exact contribution $I_i = \int_{x_{i-1}}^{x_i} f(x)\,dx$, approximated by $R_i = h_i f(x_{i-1})$.

**Worked Example/Proof:**
By Taylor's theorem with Lagrange remainder, $f(x) = f(x_{i-1}) + f'(\xi_x)(x-x_{i-1})$ for some $\xi_x$ between $x_{i-1}$ and $x$. Integrating:
$$I_i = h_i f(x_{i-1}) + \int_{x_{i-1}}^{x_i} f'(\xi_x)(x-x_{i-1})\,dx$$
Local error: $E_i = I_i - R_i = \int_{x_{i-1}}^{x_i} f'(\xi_x)(x-x_{i-1})\,dx$.
Let $M_1 = \max_{x\in[a,b]}|f'(x)|$. Then:
$$|E_i| \leq M_1 \int_{x_{i-1}}^{x_i}(x-x_{i-1})\,dx = M_1\cdot\frac{h_i^2}{2}$$
Summing over all subintervals: $|E| = |I-R| \leq \sum_{i=1}^n |E_i| \leq \frac{M_1}{2}\sum_{i=1}^n h_i^2$.
For a uniform grid ($h_i=h$, $h=\frac{b-a}{n}$): $|E| \leq \frac{M_1}{2}nh^2$. Since $nh=b-a$:
$$\boxed{|I-R| \leq \frac{M_1(b-a)}{2}h}$$
Thus the composite left-rectangle rule has **global error $O(h)$**. Same order for the right-rectangle rule.

**Theorem/Property (Error Estimate for the Midpoint Rule):**
Expand about midpoint $c_i = \frac{x_{i-1}+x_i}{2}$ using Taylor's theorem:
$$f(x) = f(c_i) + f'(c_i)(x-c_i) + \frac{f''(\xi_x)}{2}(x-c_i)^2$$
Integrated over the symmetric interval, the $f'(c_i)$ term vanishes since $\int_{x_{i-1}}^{x_i}(x-c_i)\,dx=0$. With $M_2 = \max_{x\in[a,b]}|f''(x)|$:
$$\boxed{|I-I_{\text{mid}}| \leq \frac{M_2(b-a)}{24}h^2}$$
Thus the composite midpoint rule has **global error $O(h^2)$** — one order more accurate than the rectangle rules.

**Definition/Core Formula (Simpson's / Parabolic Rule):**
Uses a quadratic polynomial (parabola) to approximate $f$ on each subinterval, rather than a constant or line. Global error of the composite rule is $O(h^4)$, at the cost of additional function evaluations and a more complex formula.

**Remark:** For integrals with no elementary antiderivative, correctness of a Simpson's rule computation can be checked against another method (e.g. the simpler trapezoidal rule); close agreement suggests the result is likely correct.

---

## Lecture 19: Introduction to Numerical Differentiation

**Worked Example (Simpson's Rule on Uniform Mesh):**
General composite Simpson's (parabola) rule formula ($n$ even, $n=2m$):
$$I_{\text{parab}} = \frac{h}{3}\left\{f_0+f_n+4\sum_{i=1}^{n/2}f_{2i-1}+2\sum_{i=1}^{n/2-1}f_{2i}\right\}$$
Notation: $f_k = f(x_k)$.

**Worked Example ($I = \int_1^2 e^{x^2}\,dx$, $n=4$):**
$h = \dfrac{2-1}{4} = 0.25$; $x_0=1, x_1=\tfrac54, x_2=\tfrac32, x_3=\tfrac74, x_4=2$.
$$f_0 = e^1 \approx 2.7,\quad f_1 = e^{(5/4)^2}\approx 4.77,\quad f_2 = e^{(3/2)^2}\approx 9.49,\quad f_3 = e^{(7/4)^2}\approx 21.38,\quad f_4=e^4\approx 54.6$$
$$I_{\text{parab}} \approx \frac{0.25}{3}\Big(2.7+4(4.77+21.38)+2(9.49)+54.6\Big) \approx 15.073$$

**Worked Example (Comparison with Trapezoidal Rule):**
$$T_1 = h(f_0+f_2) \approx 0.25(2.7+9.49) \approx 3.0475$$
$$T_2 = h(f_2+f_4) \approx 0.25(9.49+54.6) \approx 16.0225$$
$$I_{\text{Trap}} = T_1+T_2 \approx 19.07$$
Remark: values (15.073 vs 19.07) are reasonably close, suggesting calculations are likely correct (used as a consistency check since the integral $\int e^{x^2}dx$ has no elementary closed form).

**Definition (Divided Difference / Finite Difference for Numerical Differentiation):**
$$f'(x) \approx \frac{f(x+h)-f(x)}{h}$$
At a point $x_i$ with local step $h_i$:
$$f'(x_i) \approx \frac{f(x_i+h_i)-f(x_i)}{h_i} = \frac{f_i - f_{i-1}}{h_i}$$
Remark: There are many ways to approximate $f'(x)$; in the context of ODEs these are usually called **finite differences**.

**Definition (General ODE and Reduction to First Order):**
An ODE of order $n$: $F(x,y,y',y'',\dots,y^{(n)}) = 0$. Assuming solvable for the highest derivative:
$$y^{(n)} = f(x,y,y',\dots,y^{(n-1)})$$
Example: $F(\cdots) = x^3y''' - \sin(x)y' + y^2 = 0$ ($n=3$) gives $y''' = \dfrac{-y^2+\sin(x)y'}{x^3}$.
This course considers only $n=1$: $F(x,y,y')=0 \implies y' = f(x,y)$.

**Core Formula (Euler's Method — Simple Idea):**
Approximate $y'$ by divided difference:
$$y' \approx \frac{y_{i+1}-y_i}{h} = f(x_i,y_i), \quad i=0,1,\dots,n$$
$$\boxed{y_{i+1} = y_i + hf(x_i,y_i), \qquad x_{i+1}=x_i+h}$$
Given initial conditions (IC) $(x_0,y_0)$.
[Diagram: Polygonal approximate solution curve constructed via Euler segments, starting from $(x_0,y_0)$]

---

## Lecture 20: Numerical Solution of 1st Order ODEs

**Definition (First-Order ODE):**
$$\frac{dy}{dx} = f(x,y)$$
General solution: $y = y(x,C)$, a family of curves depending on an arbitrary constant $C$.

**Worked Example (Separable Equation):**
$$y' = \frac{x}{y} \implies y\,dy = x\,dx \implies \frac{y^2}{2} = \frac{x^2}{2}+C \implies y^2 = x^2+C_1$$

**Worked Example (Linear Equation, elementary solution):**
$$y' = y+x \quad\Rightarrow\quad y = Ce^x - x - 1$$
**Proof/Check:** $(Ce^x-x)' = Ce^x - 1$; substituting $y=Ce^x-x-1$ into $y'=y+x$: LHS derivative $Ce^x-1$; RHS $y+x = Ce^x-x-1+x = Ce^x-1$. ✓ Confirmed a solution, but with only one arbitrary constant form checked; the general solution is $y=Ce^x-x-1$.

Example (checking $y=Ce^x-x$ is NOT a general solution... shown not satisfying identically unless adjusted): the correct general solution family is $y=Ce^x-x-1$.

**Worked Example (Testing candidate general solutions):**
For $y'=y$: general solution $y=Ce^x$. Check: $(Ce^x)'=Ce^x$ ✓ (identically true for any $C$).
Candidate $y=C\sin x$: $(C\sin x)' = C\cos x \neq C\sin x$ — **not a solution**.

**Definition (Initial Value Problem / Cauchy Problem):**
$$\begin{cases} y' = f(x,y) \\ y(x_0)=y_0 \end{cases}$$
An IVP cannot be posed for every ODE at every point; existence/uniqueness depends on conditions on $f(x,y)$ (studied in ODE theory). This course assumes existence of a unique solution.

**Worked Example (IVP for $y'=y+x$):**
$x_0=1, y_0=4$. From $y=Ce^x-x-1$: $4 = Ce^1-1-1 = Ce-2 \Rightarrow Ce=2 \Rightarrow C=2/e\approx0.74$.
$$y^* = \frac{2}{e}e^x - x - 1 \approx 0.74e^x - x - 1$$

**Worked Example (Circle Family IVP):**
$y' = -x/y \Rightarrow y\,dy = -x\,dx \Rightarrow \frac{y^2}{2}=-\frac{x^2}{2}+C \Rightarrow \frac{y^2}{2}+\frac{x^2}{2}=C=\frac{R^2}{2}$.
IVP: $y_0=2, x_0=2$: $\frac{4}{2}+\frac{4}{2}=C \Rightarrow C=4$. Solution: $\frac{(y^*)^2}{2}+\frac{x^2}{2}=4$ (circle of radius $R=2$, using $C=R^2/2$).
[Diagram: Family of concentric circles $\frac{y^2}{2}+\frac{x^2}{2}=C$ for varying $C$, with $R=2$ circle highlighted]

**Core Formula (Algorithm for solving IVP from general solution):**
Substitute $x=x_0, y=y_0$ into the general solution and solve for constant $C$.

**Worked Example ($y'=xy+1$, non-elementary solution):**
$$y = e^{x^2/2}\left(C+\int e^{-x^2/2}\,dx\right)$$
The integral cannot be expressed in elementary functions — motivates numerical methods.

**Core Formula (Euler's Method, Full Statement):**
$$\begin{cases} y_{i+1} = y_i + hf(x_i,y_i) \\ x_{i+1} = x_i+h \end{cases}, \qquad i=0,1,\dots,n, \quad (x_0,y_0) \text{ given}$$
Geometrically: a polygonal line of tangent-line segments ("Euler's segments").
[Diagram: Polygonal path through points $(x_0,y_0), (x_1,y_1), (x_2,y_2),\ldots$ approximating the true solution curve]

**Worked Example (Euler's Method on $y'=y+x$, $x_0=0,y_0=1,h=0.25$):**
Exact solution: from $y=Ce^x-x-1$, $1=Ce^0-0-1 \Rightarrow C=2$, so $y^*=2e^x-x-1$.
$$x_1=0.25,\quad y_1 = y_0+h(x_0+y_0) = 1+0.25(1+0)=1.25$$
$$x_2=0.5,\quad y_2 = y_1+h(x_1+y_1)=1.25+0.25(0.25+1.25)=1.25+0.375=1.5625$$
$$x_3=0.75,\quad y_3=y_2+h(x_2+y_2)=1.5625+0.25(0.5+1.5625)=1.5625+0.515625=2.078125$$
Exact at $x_3=0.75$: $y^*=2e^{0.75}-0.75-1 \approx 2(2.117)-1.75 \approx 4.23-1.75\approx 2.48$
**Remark: Euler's method is not very exact.**

**Theorem/Property (Euler's Method Global Error):**
$$y(x_i)-y_i = O(h)$$
**Proof/Derivation:** By Taylor's formula, $y(x+h)=y(x)+hy'(x)+\frac{h^2}{2}y''(\xi)=y(x)+hf(x,y(x))+O(h^2)$.
If $y_i = y(x_i)$ exactly, one Euler step gives $y_{i+1}=y(x_i)+hf(x_i,y(x_i))$, while the exact solution satisfies $y(x_{i+1})=y(x_i)+hf(x_i,y(x_i))+O(h^2)$. So the **local truncation error** per step is $O(h^2)$. With $N=\frac{b-x_0}{h}=O(1/h)$ steps, the accumulated (**global**) error is:
$$O\left(\frac{1}{h}\right)\cdot O(h^2) = O(h)$$

**Core Formula (Improved Euler Method / Midpoint Method Derivation):**
Idea: change the slope approximation to use the midpoint of the interval.
$$x_{i+\frac12} = x_i+\frac{h}{2}, \qquad y_{i+\frac12} = y_i + \left(x_{i+\frac12}-x_i\right)f(x_i,y_i) = y_i+\frac{h}{2}f(x_i,y_i)$$
$$\boxed{y_{i+1} = y_i + hf\left(x_{i+\frac12}, y_{i+\frac12}\right), \qquad x_{i+1}=x_i+h}$$

**Worked Example (Midpoint Method on $y'=y+x$, $x_0=0,y_0=1,h=0.25$):**
$$x_{0+\frac12}=0.125, \quad y_{0+\frac12} = y_0+\frac{h}{2}f(x_0,y_0) = 1+0.125(0+1)=1.125$$
$$y_1 = y_0+hf(x_{0+\frac12},y_{0+\frac12}) = 1+0.25(0.125+1.125) = 1+0.25(1.25) = 1.3125$$
Exact at $x_1=0.25$: $y^*=2e^{0.25}-0.25-1 \approx 2(1.284)-1.25 \approx 2.567-1.25 \approx 1.318$.
**Comparison at $x_1=0.25$:** Exact $\approx1.318$; Euler's $\approx1.25$; Midpoint $\approx1.3125$ — midpoint much closer than Euler's.

**Theorem/Property (Midpoint Method Global Error):**
$$y(x_i)-y_i = O(h^2)$$

**Core Formula (Classical 4th-Order Runge–Kutta Method, RK4):**
For $y'=f(x,y)$:
$$k_1 = f(x_n,y_n)$$
$$k_2 = f\left(x_n+\frac{h}{2}, y_n+\frac{h}{2}k_1\right)$$
$$k_3 = f\left(x_n+\frac{h}{2}, y_n+\frac{h}{2}k_2\right)$$
$$k_4 = f(x_n+h, y_n+hk_3)$$
$$\boxed{y_{n+1} = y_n + \frac{h}{6}(k_1+2k_2+2k_3+k_4)}, \qquad x_{i+1}=x_i+h$$

**Theorem/Property (RK4 Global Error):**
$$y(x_n)-y_n = O(h^4)$$
Higher accuracy comes at the cost of more function evaluations of $f(x,y)$ per step.

**Theorem/Property (Summary Table on Global Accuracy):**
| Method | Global error |
|---|---|
| Euler's method | $O(h)$ |
| Midpoint method | $O(h^2)$ |
| RK4 | $O(h^4)$ |

**Remark (Nonuniform Meshes / Adaptive Grids):**
Non-uniform ("adaptive") lattices adjust grid points according to the steepness/behavior of the solution; construction of adaptive grids is beyond the scope of the course.

---

## Lecture 20 (Final Remarks): Runge–Kutta Recap Example

**Worked Example (IVP Setup Recap):**
$$\begin{cases} y' = x+y \\ y(5)=3 \end{cases} \quad \Rightarrow \quad x_0=5,\ y_0=3$$
Assume general solution $y = x+C$. Substituting $(x_0,y_0)=(5,3)$: $3 = 5+C \Rightarrow C=-2$. This solves the IVP (Cauchy problem).

**Core Formula (Runge–Kutta Method Recap):**
$$\begin{cases} y'=f(x,y) \\ y(x_0)=y_0 \end{cases} \implies y_{i+1} = y_i + \frac{h}{6}(k_1+2k_2+2k_3+k_4)$$
Fourth-order Runge–Kutta method (RK4), global error $O(h^4)$.

**Worked Example (RK4 Setup for $y'=f(x,y)=xy+\frac{1}{x}$, $h=\frac{1}{12}$):**
$$k_1 = f(x_i,y_i) = x_iy_i+\frac{1}{x_i}$$
$$k_2 = f\left(x_i+\frac{h}{2}, y_i+\frac{h}{2}k_1\right) = \left(x_i+\frac{h}{2}\right)\left(y_i+\frac{h}{2}k_1\right) + \frac{1}{x_i+\frac{h}{2}}$$
$$y_{i+1} = y_i + \frac{h}{6}\left(k_1 + 2k_2 + 2k_3+k_4\right)$$
Remark: "Idea: just apply the formulas."

---

## Lectures 21–22: Elements of Numerical Linear Algebra

**Definition (Scalar Product):**
For vectors $\bar{a}=(a^x,a^y)$, $\bar{b}=(b^x,b^y)$ (2D) or $\bar a=(a^x,a^y,a^z)$, $\bar b=(b^x,b^y,b^z)$ (3D):
$$\bar{a}\cdot\bar{b} = a^xb^x+a^yb^y = |\bar a||\bar b|\cos\alpha$$
where $|\bar a| = \|\bar a\|_2 = \sqrt{(a^x)^2+(a^y)^2}$ (length).

**Definition (Projection of One Vector onto Another):**
From geometry, with $\bar c = \text{proj}_{\bar b}\bar a$: $|\bar c| = |\bar a|\cos\alpha$, and since $\bar a \cdot \bar b = |\bar a||\bar b|\cos\alpha$:
$$\boxed{\text{proj}_{\bar b}\bar{a} = \frac{\bar{a}\cdot\bar{b}}{|\bar{b}|}}, \qquad \text{proj}_{\bar a}\bar{b} = \frac{\bar{a}\cdot\bar{b}}{|\bar{a}|}$$

**Definition (Standard Basis Projections):**
With standard basis $\bar\imath=(1,0)$, $\bar\jmath=(0,1)$ (so $|\bar\imath|=|\bar\jmath|=1$):
$$\text{proj}_{\bar\imath}\bar{a} = \frac{\bar a\cdot\bar\imath}{|\bar\imath|} = \bar a\cdot\bar\imath = a^x, \qquad \text{proj}_{\bar\jmath}\bar{a} = \frac{\bar a\cdot\bar\jmath}{|\bar\jmath|} = \bar a\cdot\bar\jmath = a^y$$

**Worked Example (Projection Example):**
$\bar a=(0,1)$, $\bar b=(2,0)$. $\text{proj}_{\bar\jmath}\bar a = \bar a\cdot\bar\jmath = a^y = 1$. $\text{proj}_{\bar\imath}\bar b = \bar b\cdot\bar\imath = b^x = 2$. Also $a^y b^x = 1\cdot2=2$.

**Theorem/Property (Determinant as Oriented Area — Derivation):**
For $\bar a=(a^x,a^y)$, $\bar b=(b^x,b^y)$, construct a bounding rectangle of area $R=a^yb^x$ and a corner rectangle $R_1=a^xb^y$. From the figure, the area of the parallelogram spanned by $\bar a,\bar b$ equals $R-R_1$:
$$S = a^yb^x - a^xb^y$$
And the determinant:
$$\det: \left|\begin{matrix}\bar a\\ \bar b\end{matrix}\right| = \begin{vmatrix} a^x & b^x \\ a^y & b^y \end{vmatrix} = a^xb^y - b^xa^y = -S$$
**Conclusion:** The area of the parallelogram equals $\det(\bar a\ \bar b)$, up to a sign ($\pm$).

**Theorem/Property (2×2 Determinant as Oriented Area, alternate derivation):**
Using areas $S_1 = a^xb^y$ (with one vector axis-aligned) and $S_2 = \begin{vmatrix}a^x & b^x\\ a^y & b^y\end{vmatrix}$-type expressions:
$$S_1 = \begin{vmatrix} a^x & 0 \\ 0 & b^y \end{vmatrix} = a^xb^y - 0 = a^xb^y$$
$$S_2 = \begin{vmatrix} a^x & b^x \\ a^y & b^y \end{vmatrix} = a^xb^y-a^yb^x$$
$$-S_2 = \begin{vmatrix} b^x & a^x \\ b^y & a^y \end{vmatrix} = a^yb^x - a^xb^y$$
$$S_1 - S_2 = \begin{vmatrix} a^x & b^x \\ a^y & b^y \end{vmatrix} = a^xb^y-b^xa^y$$
**Property:** det of a $2\times2$ matrix is the oriented area of a parallelogram.

**Theorem/Property (Determinant as Volume, 3D Extension):**
For unit vector $(0,0,1)$ extended to 3D, "Volume $= d\cdot\beta\cdot 1 = $ Area":
$$\begin{vmatrix} 0 & 0 & 1 \\ a^x & b^x & 0 \\ a^y & b^y & 0 \end{vmatrix} = \begin{vmatrix} a^x & b^x \\ a^y & b^y \end{vmatrix}$$

**Theorem/Property (Determinant Column Property):**
The determinant does not change if we add a column-vector orthogonal to its column-vectors (of length 1):
$$\begin{vmatrix}a^x & b^x \\ a^y & b^y\end{vmatrix} = a^x\cdot b^y - a^y b^x = a^x\cdot\left|\begin{matrix}0&1\\b^y&0\end{matrix}\right|_{(1\times1)\text{-cofactor-like}} - b^x\left(\cdots\right)$$
$$= a^x\left(\begin{vmatrix}0&1\\b^y&0\end{vmatrix}\right) - b^x\left(\begin{vmatrix}1&0\\a^y&0\end{vmatrix}\right)$$

**Core Formula (3×3 Determinant Expansion via Projections):**
For column vectors $\bar a,\bar b,\bar c$:
$$\begin{vmatrix} a^x & b^x & c^x \\ a^y & b^y & c^y \\ a^z & b^z & c^z \end{vmatrix} = a^x\begin{vmatrix}1&0&0\\0&b^y&c^y\\0&b^z&c^z\end{vmatrix} + b^x\begin{vmatrix}0&1&0\\a^y&0&c^y\\a^z&0&c^z\end{vmatrix} + c^x\begin{vmatrix}0&0&1\\a^y&b^y&0\\a^z&b^z&0\end{vmatrix}$$
using $\text{proj}_{yz}\bar b$, $\text{proj}_{yz}\bar c$ terms.

**Definition (Minor and Cofactor):**
For a matrix entry $a_{ij}$, the **minor** $\text{Minor}(a_{ij})$ is the determinant of the submatrix obtained by deleting row $i$ and column $j$.
Example: $\text{Minor}(a_{11}) = \begin{vmatrix}a_{22}&a_{23}\\a_{32}&a_{33}\end{vmatrix}$, $\text{Minor}(a_{32}) = \begin{vmatrix}a_{11}&a_{13}\\a_{21}&a_{23}\end{vmatrix}$.

$$\boxed{\text{cofactor}(a_{ij}) = (-1)^{i+j}\text{Minor}(a_{ij})}$$

**Worked Example (Cofactor Calculation):**
$$\text{cofac}(a_{23}) = (-1)^{2+3}\text{Minor}(a_{23}) = -\begin{vmatrix}a_{11}&a_{12}\\a_{31}&a_{32}\end{vmatrix} = -(a_{11}a_{32}-a_{31}a_{12}) = a_{31}a_{12}-a_{11}a_{32}$$

**Theorem/Property (Laplace Expansion / Cofactor Expansion Formula):**
$$\det A_{n\times n} = \sum_{j=1}^n a_{kj}\cdot\text{cofac}(a_{kj}), \quad k\in[1,n]$$
E.g., expanding along the first row ($k=1$):
$$\boxed{\det A_{n\times n} = \sum_{j=1}^n a_{1j}\cdot\text{cofac}(a_{1j})}$$

**Worked Example (3×3 Determinant via Laplace Expansion):**
$$A = \begin{vmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 10 \end{vmatrix}$$
$$\text{cofac}(a_{11}) = (-1)^{1+1}\begin{vmatrix}5&6\\8&10\end{vmatrix} = 5\cdot10-6\cdot8$$
$$\text{cofac}(a_{12}) = (-1)^{1+2}\begin{vmatrix}4&6\\7&10\end{vmatrix} = -(4\cdot10-7\cdot6)$$
$$\text{cofac}(a_{13}) = (-1)^{1+3}\begin{vmatrix}4&5\\7&8\end{vmatrix} = 4\cdot8-5\cdot7$$
$$\det A = 1\cdot(5\cdot10-6\cdot8) + 2\cdot(-1)(4\cdot10-7\cdot6) + 3\cdot(4\cdot8-5\cdot7)$$

**Theorem/Property (Row Swap Property):**
$$\begin{vmatrix}\text{row}_1\\ \text{row}_2\\ \vdots\end{vmatrix} = -\begin{vmatrix}\text{row}_2\\ \text{row}_1\\ \vdots\end{vmatrix}$$
Example: $\begin{vmatrix}a^y & b^y\\ a^x & b^x\end{vmatrix} = a^yb^x - a^xb^y$.

**Worked Example (Determinant via Row Swap and Cofactor Expansion):**
$$\begin{vmatrix} 5&6&7\\ 0&0&1\\ 8&9&10 \end{vmatrix} = -\begin{vmatrix}0&0&1\\5&6&7\\8&9&10\end{vmatrix} = -\left(1\cdot\text{cofac}(1)\right) = -\left(1\cdot\begin{vmatrix}5&6\\8&9\end{vmatrix}\right) = -\begin{vmatrix}5&6\\8&9\end{vmatrix}$$

**Definition (Triangular Matrices):**
A **lower triangular matrix** has zero entries above the main diagonal:
$$\begin{pmatrix}a_{11}& & \\ &a_{22}& \\ \text{(some numbers)}& &a_{nn}\end{pmatrix}, \quad \text{e.g. } \begin{pmatrix}1&0&0\\-1&2&0\\7&6&5\end{pmatrix}$$
An **upper triangular matrix** has zero entries below the main diagonal:
$$\begin{pmatrix}a_{11}&\text{(some numbers)}& \\ &a_{22}& \\ 0& &a_{nn}\end{pmatrix}, \quad \text{e.g. } \begin{pmatrix}1&-1&7\\0&2&6\\0&0&5\end{pmatrix}$$

**Theorem/Property (Determinant of a Triangular Matrix):**
$$\begin{vmatrix}a_{11}&0\\a_{21}&a_{22}\end{vmatrix} = a_{11}\cdot\text{cofac}(a_{11}) = a_{11}a_{22}$$
$$\begin{vmatrix}a_{11}&0&0\\a_{21}&a_{22}&0\\a_{31}&a_{32}&a_{33}\end{vmatrix} = a_{11}\cdot\text{cofac}(a_{11}) = a_{11}\begin{vmatrix}a_{22}&0\\a_{32}&a_{33}\end{vmatrix} = a_{11}a_{22}\cdot\text{cofac}(a_{22}) = a_{11}a_{22}a_{33}$$
$$\boxed{\det(\text{triangular})_{n\times n} = a_{11}\cdot a_{22}\cdots a_{nn}}$$

**Worked Example (5×5 Triangular Determinant):**
$$\det\begin{pmatrix}1&0&0&0&0\\7&2&0&0&0\\11&-8&3&0&0\\34&1&7&4&0\\81&-5&3&12&5\end{pmatrix} = 1\times2\times3\times4\times5 = 5! = 120$$

**Definition (LU Decomposition):**
Under suitable conditions, a matrix $A$ can be written as
$$A = L\cdot U$$
where $L$ is lower triangular and $U$ is upper triangular. (For a general nonsingular matrix, row permutations may be required, giving $PA=LU$ with permutation matrix $P$; this course restricts to cases requiring no permutations.)

**Worked Example (2×2 LU Decomposition):**
$$A = \begin{pmatrix}1&2\\3&4\end{pmatrix} = \begin{pmatrix}\ell_{11}&0\\ \ell_{21}&\ell_{22}\end{pmatrix}\begin{pmatrix}u_{11}&u_{12}\\0&u_{22}\end{pmatrix} = \begin{pmatrix}\ell_{11}u_{11} & \ell_{11}u_{12}\\ \ell_{21}u_{11} & \ell_{21}u_{12}+\ell_{22}u_{22}\end{pmatrix}$$
This gives 4 equations, 6 unknowns; assume $\ell_{11}=1,\ \ell_{22}=1$:
$$\begin{cases} 1 = u_{11} \\ 2 = u_{12} \\ 3 = \ell_{21}u_{11} \\ 4 = \ell_{21}u_{12}+u_{22} \end{cases} \implies u_{11}=1,\ u_{12}=2,\ \ell_{21}=3,\ u_{22}=4-3\cdot2=-2$$
$$\boxed{\begin{pmatrix}1&2\\3&4\end{pmatrix} = \begin{pmatrix}1&0\\3&1\end{pmatrix}\begin{pmatrix}1&2\\0&-2\end{pmatrix}}$$

**Theorem/Property (Multiplicative Property of Determinant):**
$$\det(P\cdot Q) = \det P \cdot \det Q$$
Hence, since $A = LU$:
$$\boxed{\det A = \det L \cdot \det U}$$

**Worked Example (Determinant via LU):**
$$\det A = \begin{vmatrix}1&2\\3&4\end{vmatrix} = 1\cdot4-2\cdot3 = -2$$
$$\det L = \begin{vmatrix}1&0\\3&1\end{vmatrix} = 1, \qquad \det U = \begin{vmatrix}1&2\\0&-2\end{vmatrix} = -2$$
$$\det A = 1\cdot(-2) = -2 \checkmark$$

**Worked Example (3×3 LU Decomposition):**
$$A = \begin{pmatrix}1&2&3\\4&5&6\\7&8&10\end{pmatrix} = \begin{pmatrix}1&0&0\\\ell_1&1&0\\\ell_2&\ell_3&1\end{pmatrix}\begin{pmatrix}u_1&u_2&u_3\\0&u_4&u_5\\0&0&u_6\end{pmatrix}$$
Matching entries:
$$u_1=1,\ u_2=2,\ u_3=3$$
$$\ell_1u_1=4 \Rightarrow \ell_1=4; \qquad \ell_1u_2+u_4=5 \Rightarrow u_4 = 5-4\cdot2=-3; \qquad \ell_1u_3+u_5=6 \Rightarrow u_5=6-4\cdot3=-6$$
$$\ell_2u_1=7 \Rightarrow \ell_2=7$$
$$\ell_2u_2+\ell_3u_4=8 \Rightarrow 14+\ell_3(-3)=8 \Rightarrow \ell_3=\frac{8-14}{-3}=2$$
$$\ell_2u_3+\ell_3u_5+u_6=10 \Rightarrow 21+2(-6)+u_6=10 \Rightarrow u_6=10-21+12=1$$
$$\boxed{\begin{pmatrix}1&2&3\\4&5&6\\7&8&10\end{pmatrix} = \begin{pmatrix}1&0&0\\4&1&0\\7&2&1\end{pmatrix}\begin{pmatrix}1&2&3\\0&-3&-6\\0&0&1\end{pmatrix}}$$
Check: $\det L = 1\cdot1\cdot1=1$, $\det U = 1\cdot(-3)\cdot1=-3$, $\det A = 1\cdot(-3) = -3$.

**Core Formula (LU Decomposition for Solving Linear Systems):**
Given $A\bar x = \bar y$ with $A=LU$:
$$Ax = L(Ux) = y \implies \begin{cases} Uz\ (\text{define } z=Ux) \\ Lz = y \end{cases} \implies \begin{cases} Lz = y \\ Ux = z \end{cases}$$
In many cases, solving these two triangular systems (via **forward substitution** for $Lz=y$ and **backward substitution** for $Ux=z$) is much easier than solving the original system directly. This procedure is closely related to **Gaussian elimination**.

**Worked Example (Solving $A\bar x=\bar y$ via LU Decomposition):**
$$A = \begin{pmatrix}1&2\\3&4\end{pmatrix} = \begin{pmatrix}1&0\\3&1\end{pmatrix}\begin{pmatrix}1&2\\0&-2\end{pmatrix}, \qquad \bar y = \begin{pmatrix}1\\-1\end{pmatrix}$$
Step 1 — solve $Lz=y$:
$$\begin{pmatrix}1&0\\3&1\end{pmatrix}\begin{pmatrix}z_1\\z_2\end{pmatrix} = \begin{pmatrix}1\\-1\end{pmatrix} \implies \begin{cases} z_1=1 \\ 3z_1+z_2=-1 \end{cases} \implies z_1=1,\ z_2=-1-3=-4$$
$$z = \begin{pmatrix}1\\-4\end{pmatrix}$$
Step 2 — solve $Ux=z$:
$$\begin{pmatrix}1&2\\0&-2\end{pmatrix}\begin{pmatrix}x_1\\x_2\end{pmatrix} = \begin{pmatrix}1\\-4\end{pmatrix} \implies \begin{cases} x_1+2x_2=1 \\ -2x_2=-4 \end{cases} \implies x_2=2,\ x_1=1-4=-3$$
$$\boxed{x = \begin{pmatrix}-3\\2\end{pmatrix}}$$
