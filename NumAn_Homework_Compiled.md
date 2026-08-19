```markdown
## Homework 01

**Question 1:** Verify that
$$x = \frac{-b + \sqrt{b^2 - c^2}}{2a}$$
is not a solution of the quadratic equation
$$ax^2 + bx + c = 0.$$

**Question 2:** Read about Cardano's formula for solving cubic equations (for example: https://math.vanderbilt.edu/schectex/courses/cubic/). Why is it sometimes preferable to compute an approximate numerical solution instead of using the exact formula?

**Question 3:** Verify that
$$y = Ce^x,$$
where $C$ is an arbitrary constant, is an exact closed-form solution of the differential equation
$$\frac{dy}{dx} = y.$$

---

## Homework 02

*Note: Homework assignments are optional but strongly recommended. Completing them can significantly improve your understanding of the material.*

**Question 1:** Using the standard product rule
$$(uv)' = u'v + uv',$$
derive a formula for the derivative of a product of four functions:
$$(fghk)' = \ldots$$

**Question 2:** Evaluate the following sum without directly using any known summation formula:
$$1 + 2 + 3 + \cdots + 9.$$
Using simple algebraic manipulations, transform the sum into the form
$$\frac{9(9+1)}{2}.$$

**Question 3:** Evaluate the following sum without directly using any known summation formula:
$$2 + 4 + 6 + 8 + \cdots + 18 + 20$$

**Question 4:** Find the following derivatives using the standard rules of differentiation:

a) $x^3 + 2x^{11/3} + x\sin x$

b) $e^x \cos x - 10\ln x$

**Question 5:** Evaluate the following integrals using the standard rules of integration (you may need to recall some basic Calculus):

a) $\displaystyle\int (x^{7/2} + x^{-7/2})\,dx$

b) $\displaystyle\int_{-1-\pi}^{-1+\pi} \sin(x+1)\,dx$

---

## Homework 03

**Question 1:** Suppose the exact and approximate solutions of a problem are
$$f(x) = e^{-x}\sin x + e^{x}\cos x,$$
and
$$\tilde{f}(x) = 1.25e^{-x}\sin x + 1.01e^{x}\cos x.$$
Using a calculator or computational software, evaluate the function at the three points
$$x = \frac{\pi}{6}, \frac{\pi}{4}, \frac{\pi}{3},$$
and compute the MAE and RMSE. What can you conclude about the contributions of the terms containing $\sin x$ and $\cos x$ to the overall error?

**Question 2:** Convert the following polynomial from centered form to the standard form:
$$(x-1)^3 - (x-1)^2 - (x-1) + 13.$$

**Question 3:** Rewrite the following polynomial in centered form with center $x_0 = -2$:
$$x^3 + 2x^2 - 7x + 11.$$

**Question 4:** Convert the following polynomial from the standard form to the nested form:
$$x^5 + 3x^4 + x + 1.$$
Hint: Observe that a term of the form $a_k x^k$ may be rewritten as
$$x \cdot (0 + a_k x^{k-1}),$$
which allows missing powers of $x$ to be incorporated into the nested representation.

**Question 5:** Convert the following polynomial from the nested form to the standard form:
$$1 + x\cdot(-2 + x\cdot(3 + x\cdot(-4 + x))).$$
Count the number of arithmetic operations required to evaluate the polynomial in both forms, and verify that they are bounded by
$$2n \quad \text{and} \quad \frac{n(n+3)}{2},$$
respectively.

**Question 6:** Let $p_n(x)$ and $q_m(x)$ be arbitrary polynomials of degrees $n$ and $m$, respectively. What can you say about the degree of the following polynomials?

a) $p_n(x) + q_m(x)$

b) $p_n(x) \cdot q_m(x)$

In each case, determine the degree whenever possible. If it cannot be determined uniquely, state the best possible bound and explain why.

---

## Homework 04

**Question 1:** Divide the polynomial
$$p_5(x) = x^5 - 3x^3 + 1$$
by $x - 2$ using Horner's method. Express $p_5(x)$ in the form
$$p_5(x) = (x-2)q(x) + r.$$
Verify that $p_5(2) = r$. Then:

a) Evaluate $q(2)$ using Horner's method.

b) Compute $p_5'(2)$ by first differentiating the polynomial and then applying Horner's method.

c) Compare the results obtained in the previous two parts. They should be the same. Can you explain why?

**Question 2:** Use Horner's method to show that $x + 1$ is a factor of
$$x^n + 1$$
for every odd positive integer $n$ (i.e., $n = 1, 3, 5, 7$, etc.). Derive a general formula for the quotient, and verify by examples that the result does not hold when $n$ is even.

**Question 3:** In the lecture, we applied Horner's method to the polynomial
$$p_n(x) = x^n - 1,$$
where $n$ is an even positive integer, and obtained the factorization
$$x^n - 1 = (x+1)\left(x^{n-1} - x^{n-2} + \cdots + x - 1\right).$$
Let us denote
$$x^{n-1} - x^{n-2} + \cdots + x - 1 = p_{n-1}(x).$$
Now divide $p_{n-1}(x)$ by $x+1$ using Horner's method. Denote the quotient by $p_{n-2}(x)$. Then divide $p_{n-2}(x)$ by $x+1$, denote the quotient by $p_{n-3}(x)$, and continue this process repeatedly.

As we observed in the lecture, after $n-1$ applications of Horner's method, this process produces the centered form of the polynomial at $x = -1$.

Deriving a general factorization formula for arbitrary even $n$ may be challenging at first. Instead, one can start with the cases $n = 2, 4, 6, \ldots$, look for a pattern, and then formulate a conjecture for general even $n$.

**Question 4:** Recall the chain rule by differentiating the polynomial
$$z(x) = \left(x^3 + 2x^2 - 7x + 3\right)^2.$$
What is the degree of this polynomial? What is the degree of its derivative?

---

## Homework 05

**Question 1:** Given the polynomial
$$p_5(x) = 2x^5 - 3x^3 + x + 9,$$
evaluate $p_5(-2)$ using Horner's method. Using the resulting Horner table, express $p_5(x)$ in the form
$$p_5(x) = (x+2)q(x) + r.$$

**Question 2:** For the polynomial $p_5(x)$ from the previous problem, compute $p_5'(-2)$. Do this in two different ways:

a) Apply Horner's method directly to the derivative $p_5'(x)$.

b) Apply Horner's method to the quotient $q(x)$ obtained in the previous problem.

**Question 3:** Divide the polynomial
$$6x^3 + 8x^2 - 26x + 12$$
by $3x - 2$ using Horner's method.

**Question 4:** For the function
$$f(x) = \cos x - \sin x,$$
construct the Taylor polynomials of degrees $n = 1, 2,$ and $3$ centered at $x = \pi$.

It is recommended that you visualize the function and its Taylor polynomial approximations using a computer algebra system such as Maxima, Maple, MATLAB, or a similar package.

Note: You may need to recall the derivatives
$$(\sin x)' = \cos x, \quad (\cos x)' = -\sin x.$$

**Question 5:** For the function
$$f(x) = \sin^2(2x),$$
construct the Taylor polynomial of degree 4 centered at $x = 0$.

Hint: Recall the chain rule:
$$[f(g(x))]' = f'(g(x))\,g'(x).$$

---

## Homework 06

**Question 1:** Expand the function
$$f(x) = \cos(4x)$$
into its Maclaurin series up to $n = 8$. Try to identify the general pattern of the coefficients.

**Question 2:** Write the truncation error $R_n(x)$ for the function $f(x)$ in both the integral form and the Lagrange form.

**Question 3:** Estimate the maximum absolute value of the truncation error $R_n(x)$ from the previous problem on the interval $[-3, 2]$.

**Question 4:** Suppose that, in the previous problem, the required approximation error is less than $0.001$. Determine a suitable value of $n$ that guarantees this level of accuracy.

**Question 5:** Expand the function
$$f(x) = \sin(e^x)$$
into its Taylor series. Write the truncation error $R_n(x)$ in the Lagrange form. What can you say about the upper bound for $|R_n(x)|$ on the interval $[0, 4]$?

---

## Homework 07 (Lecture 9)

**Question 1:** Given the two interpolation points
$$\{(1, 4), (3, 2)\},$$
construct the interpolating polynomial of degree 1.

**Question 2:** Using the same interpolation points,
$$\{(1, 4), (3, 2)\},$$
construct the family of all interpolating polynomials of degree at most 3. How many free parameters does this family have?

**Question 3:** Consider the following five interpolation points:
$$\{(1, 1), (2, 4), (3, 7), (6, 17), (8, 23)\}.$$

a) Construct the system of linear equations for the coefficients of the interpolating polynomial of degree at most 4.

b) Write the system in matrix form
$$Vx = y,$$
where $x$ and $y$ are column vectors.

c) Using the Vandermonde determinant formula,
$$\det(V) = \prod_{0 \le i < j \le 4} (x_j - x_i),$$
compute the determinant of the coefficient matrix $V$.

---

## Homework 08 (Lecture 11)

*This homework consists of five problems. The first two are algorithmic exercises designed to help you practice constructing Lagrange interpolation polynomials. Students are strongly encouraged to complete these problems, as they provide essential preparation for the upcoming quiz. The remaining three problems are intended to develop your geometric intuition, giving a deeper understanding of the geometric meaning and properties of the Lagrange interpolation polynomial.*

**Question 1:** Evaluate the function
$$f(x) = e^{-x^2}$$
at the points
$$x = -3, -1, 0, 1, 3.$$
Using these interpolation nodes, write down at least the first two Lagrange basis polynomials, $\ell_0(x)$ and $\ell_1(x)$. Verify that $\ell_0(-3) = 1$ and $\ell_1(-1) = 1$.

**Question 2:** Consider the function
$$f(x) = \tan x.$$

a) Construct the Lagrange interpolation polynomial $p(x)$ using the three interpolation points
$$x = 0, 1, 1.4.$$

b) Evaluate $p(1.3)$. Compute the absolute and relative errors of this approximation.

c) Use the constructed polynomial to extrapolate the value at $x = 1.56$. Again, compute the absolute and relative errors of the approximation.

**Question 3:** [Image: Figure 1 — graphs of $f(x) = \sin^2 x$ (gray curve) and $g(x) = \cos^2 x$ (black curve) plotted on the interval $[0, 2\pi]$]

Figure 1 shows the graphs of the functions
$$f(x) = \sin^2 x, \quad g(x) = \cos^2 x,$$
on the interval $[0, 2\pi]$. Choose several points, for example
$$x = 0, \frac{\pi}{4}, \frac{\pi}{2}, \pi, \frac{3\pi}{2}, 2\pi,$$
and determine graphically the values of
$$h(x) = f(x) + g(x).$$
Sketch a graph of the function $h(x)$.

**Question 4:** [Image: Figure 2 — graph of a function $w(x)$ oscillating between $-1$ and $1$ over the interval $[0.3, 1.0]$]

Figure 2 shows the graph of a function $w(x)$. Sketch the graphs of
$$w_1(x) = \frac{1}{2}w(x), \quad w_2(x) = -\frac{1}{2}w(x).$$
Verify graphically that
$$w_1(x) + w_2(x) = 0,$$
that is, their sum is the identically zero function.

**Question 5:** [Image: Figure 3 — three graphs on the interval $[0.3, 1.0]$: $f(x)$ (solid gray curve), $g(x)$ (solid black curve), and $h(x)$ (black dashed curve)]

Figure 3 contains three graphs: $f(x)$ (solid gray curve), $g(x)$ (solid black curve), and $h(x)$ (black dashed curve). It is known that
$$h(x) = \alpha f(x) + \beta g(x).$$
Estimate suitable values of the coefficients $\alpha$ and $\beta$. In other words, express $h(x)$ approximately as a linear combination of the basis functions $f(x)$ and $g(x)$.

*Hint: Select two points at which at least one of the functions $f$ or $g$ is nonzero. Evaluate (approximately) the values of $f$, $g$, and $h$ at these points, construct a system of two linear equations, and solve it to obtain approximate values of $\alpha$ and $\beta$. If your calculations are correct, you should obtain values close to $\alpha \approx 0.5$ and $\beta \approx 2$.*
```
