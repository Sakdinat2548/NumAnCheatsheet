## Quiz 6: Linear Regression Basics

**Source:** quiz06-1.pdf (Numerical Analysis) — Time: 30 minutes, Maximum score: 7 points. An equivalent Thai-language version of the quiz is included in the same file.

**Content Type: Core Formula**
**Content Text:**
$$\hat{y} = \phi(x) = a_0 + a_1 x,$$
$$a_1 = \frac{\overline{xy} - \bar{x}\,\bar{y}}{\overline{x^2} - \bar{x}\,\bar{x}}, \qquad a_0 = \bar{y} - a_1 \bar{x},$$
where
$$\bar{x} = \frac{1}{n+1}\sum_{i=0}^{n} x_i, \quad \bar{y} = \frac{1}{n+1}\sum_{i=0}^{n} y_i, \quad \overline{x^2} = \frac{1}{n+1}\sum_{i=0}^{n} x_i^2, \quad \overline{xy} = \frac{1}{n+1}\sum_{i=0}^{n} x_i y_i.$$

**Content Type: Core Formula**
**Content Text:**
Total squared error for linear regression:
$$S(a_0, a_1) = \sum_{i=0}^{n} (y_i - a_0 - a_1 x_i)^2.$$

**Content Type: Worked Example/Proof**
**Content Text:**
A student records the number of cups of coffee consumed before studying and the number of exercises completed during one hour:

| cups of coffee | 0 | 1 | 2 | 3 |
|---|---|---|---|---|
| exercises completed | 3 | 5 | 8 | 7 |

1. (4 points) Construct the linear regression model for the given data.
2. (1.5 points) Plot the data points and sketch the regression line.
3. (1.5 points) Use the regression model to predict how many exercises the student would complete after drinking 4 cups of coffee. Mark the corresponding point on the graph.
4. (Optional problem for 3 extra points) For the linear regression model constructed above, the Hessian matrix of $S$ with respect to $a_0$ and $a_1$ is
$$H = \begin{pmatrix} \dfrac{\partial^2 S}{\partial a_0^2} & \dfrac{\partial^2 S}{\partial a_0 \partial a_1} \\[2mm] \dfrac{\partial^2 S}{\partial a_1 \partial a_0} & \dfrac{\partial^2 S}{\partial a_1^2} \end{pmatrix}.$$
Compute $\det H$ and show that it is positive.
*Hint: You do not need to use the Cauchy–Schwarz inequality. Compute the Hessian determinant directly using the given data points.*

---

## Quiz 7: Rectangle and Trapezoidal Rules

**Source:** quiz07-1.pdf (Numerical Analysis) — Time: 25 minutes, Maximum score: 11 points. An equivalent Thai-language version of the quiz is included in the same file.

**Content Type: Core Formula**
**Content Text:**
Rectangle areas: $h_i f(x_i^{*})$, where
$$x_i^{*} = 0.2\,x_{i-1} + 0.8\,x_i, \qquad i = 1, 2, \ldots, n.$$
Non-uniform lattice:
$$x_k = \frac{3\ln(1 + k/n)}{\ln 2} - 1, \qquad k = 0, 1, 2, \ldots, n.$$

**Content Type: Worked Example/Proof**
**Content Text:**
1. (5 points) For the function $f(x)$ shown in Figure 1, construct rectangles with areas $h_i f(x_i^{*})$, where
$$x_i^{*} = 0.2 x_{i-1} + 0.8 x_i, \qquad i = 1, 2, \ldots, n.$$
Use the non-uniform lattice
$$x_k = \frac{3\ln(1+k/n)}{\ln 2} - 1, \qquad k = 0, 1, 2, \ldots, n,$$
with $n = 5$, i.e., using a lattice consisting of six points.
[Diagram: Figure 1 — graph of $f(x) = x^3 - 1.25x^2$, $x \in [-1, 2]$, showing a cubic curve dipping below zero between roughly $x=0$ and $x=1$ before rising steeply after $x=1.5$.]

2. For the function $g(x)$ shown in Figure 2:
   - (2 points) Construct trapezoids with bases of lengths $h_i$. Use a uniform lattice with step size $h = \pi/4$.
   - (2 points) Use the constructed trapezoids to compute an approximate value $\widetilde{I}$ of the integral over the interval $[0, 3\pi/2]$.
   - (2 points) Compute the exact value
   $$I = \int_0^{3\pi/2} g(x)\,dx.$$
   Find the absolute error of the numerical approximation $\widetilde{I}$.
[Diagram: Figure 2 — graph of $g(x) = \sin x$, $x \in [0, 3\pi/2]$, a standard sine curve rising to 1 at $\pi/2$, crossing zero at $\pi$, and falling to $-1$ near $3\pi/2$.]

---

## Quiz 8: Simpson's Rule

**Source:** quiz08.pdf (Numerical Analysis) — Time: 25 minutes, Maximum score: 7 points. An equivalent Thai-language version of the quiz is included in the same file.

**Content Type: Worked Example/Proof**
**Content Text:**
1. (2 points) Divide the interval $[0, 240]$ into 6 equal subintervals and schematically sketch the corresponding parabolas in the figure below.
[Diagram: Figure 1 — a blank set of axes over $x \in [0, 240]$, $y \in [-5, 5]$, showing a wave-like curve (two oscillations) for the student to sketch approximating parabolas onto.]

2. (5 points) Using Simpson's rule, construct a numerical approximation for the integral
$$\int_2^4 \frac{dx}{\ln x}$$
using a uniform lattice of 9 points ($n = 8$). Calculate the approximate value of the integral.

---

## Quiz 9: Numerical ODEs Basics

**Source:** quiz09-1.pdf (Numerical Analysis) — Time: 35 minutes, Maximum score: 12 points. An equivalent Thai-language version of the quiz is included in the same file.

**Content Type: Core Formula**
**Content Text:**
Standard fourth-order Runge–Kutta (RK4) stage values:
$$k_1 = f(x_i, y_i), \quad k_2 = f\!\left(x_i + \frac{h}{2}, y_i + \frac{h}{2}k_1\right), \quad k_3 = f\!\left(x_i + \frac{h}{2}, y_i + \frac{h}{2}k_2\right), \quad k_4 = f(x_i+h, y_i+hk_3).$$

**Content Type: Worked Example/Proof**
**Content Text:**
1. (1 point) Solve the initial value problem, i.e., find the particular solution of the ODE corresponding to the initial condition
$$y(x_0) = y_0, \qquad x_0 = \frac{1}{2}, \qquad y_0 = \frac{1}{4},$$
if the general solution of the ODE is known:
$$y(x) = -\frac{1}{4} + \frac{x}{2} + Ce^{-2x}.$$

2. (2 points) Determine whether
$$y = Ce^x - 2\cos(2x) - 2\sin(2x)$$
is the general solution of the ODE
$$y' = y + 5\sin(2x).$$
Justify your answer.

3. The figure below shows a fragment of the exact solution of the initial value problem
$$\begin{cases} y' = x - 4y, \\ y(0) = -3/4. \end{cases}$$
[Diagram: Figure showing the exact solution curve on $x \in [0, 1]$, starting near $y = -0.9$ at $x=0$ and rising smoothly to approach $y \approx 0.15$ at $x = 1$.]

   a) (3 points) Using Euler's method, calculate the points $(x_0, y_0), (x_1, y_1), (x_2, y_2), (x_3, y_3)$ with step size $h = 0.2$.
   b) (1 point) Approximately mark the points calculated in the previous part on the graph and draw the corresponding Euler polygonal line (segments).
   c) (4 points) Using the midpoint method, calculate the points $(x_0, y_0), (x_1, y_1), (x_2, y_2)$ with step size $h = 0.2$. Plotting the points or the polygonal line is not needed.
   d) (1 point) Calculate the absolute errors of Euler's method and the midpoint method at $x = x_2 = 0.4$, given that the exact solution at this point is
   $$y(0.4) \approx -0.101304.$$

4. (3 extra points) For the ODE
$$y' = f(x,y) = xy + \frac{1}{x},$$
write down the values of $k_1, k_2, k_3$, and $k_4$ to be used in the standard fourth-order Runge–Kutta scheme with step size $h = \frac{1}{12}$. You do not need to carry out the numerical calculations. Recall that
$$k_1 = f(x_i, y_i), \quad k_2 = f\!\left(x_i + \frac{h}{2}, y_i + \frac{h}{2}k_1\right), \quad k_3 = f\!\left(x_i + \frac{h}{2}, y_i + \frac{h}{2}k_2\right), \quad k_4 = f(x_i+h, y_i+hk_3).$$
