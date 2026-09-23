## VII.1 Numerical Differentiation (by Prof. Eckart Schulz — Numerical Methods for Computer, Lectures 17–20)

**Definition (Numerical Differentiation):**
Numerical differentiation of a function $f(x)$ means approximating the value of its derivative $f'(x)$. It is used for functions with very complicated derivatives, or when only functional values (as opposed to a formula for the function) are given. It is also important for finding numerical solutions of differential equations.

**Definition (Derivative, Recalled):**
$$f'(x_0) = \lim_{h\to0}\frac{f(x_0+h)-f(x_0)}{h} \tag{1}$$
So when $h$ is small (close to zero, positive or negative):
$$f'(x_0) \approx \frac{f(x_0+h)-f(x_0)}{h} \tag{2}$$

**Remark (Geometric Interpretation):** Geometrically, we approximate $f'(x_0)$ — the slope of the tangent line of $f(x)$ at $(x_0,f(x_0))$ — by the slope of the secant line through $(x_0,f(x_0))$ and $(x_0+h,f(x_0+h))$.
[Diagram: curve $y=f(x)$ with tangent line at $x_0$ and secant line through $(x_0,f(x_0))$ and $(x_0+h,f(x_0+h))$]

### Approximation of the First Order Derivative

There are 3 common ways to approximate $f'(x_0)$ by the slope of a secant line ($h$ small and positive):

**Definition (Case 1 — Forward Difference):** Using the secant line at $x_0$ and $x_0+h$:
$$f'(x_0) \approx \frac{f(x_0+h)-f(x_0)}{h}$$
(identical to equation (2) for $h>0$).
[Diagram: curve with secant line through $(x_0,f(x_0))$ and $(x_0+h,f(x_0+h))$]

**Definition (Case 2 — Backward Difference):** Using the secant line at $x_0-h$ and $x_0$:
$$f'(x_0) \approx \frac{f(x_0)-f(x_0-h)}{h}$$

**Definition (Case 3 — Central Difference):** Using the secant line at $x_0-h$ and $x_0+h$:
$$f'(x_0) \approx \frac{f(x_0+h)-f(x_0-h)}{2h}$$
[Diagram: curve with secant line through $(x_0-h,f(x_0-h))$ and $(x_0+h,f(x_0+h))$]

### Error Analysis

**Theorem/Property (Case 1 — Forward Difference Error):**
Express $f(x_0+h)$ via first-order Taylor polynomial at $x_0$:
$$f(x_0+h) = f(x_0)+f'(x_0)h+\frac{f''(\xi_1)}{2}h^2, \qquad x_0<\xi_1<x_0+h$$
Solving for $f'(x_0)$:
$$f'(x_0) = \underbrace{\frac{f(x_0+h)-f(x_0)}{h}}_{\text{forward difference quotient}} - \underbrace{\frac{f''(\xi_1)}{2}h}_{\text{error term}}$$
When $f''(x)$ is continuous, it is nearly constant on $[x_0,x_0+h]$, so for small $h$: $\text{error}\approx\text{const}\cdot h$. We write $\text{error}=O(h)$.

**Theorem/Property (Case 2 — Backward Difference Error):**
$$f(x_0-h) = f(x_0)+f'(x_0)(-h)+\frac{f''(\xi_2)}{2}(-h)^2, \qquad x_0-h<\xi_2<x_0$$
$$f'(x_0) = \underbrace{\frac{f(x_0)-f(x_0-h)}{h}}_{\text{backward difference quotient}} + \underbrace{\frac{f''(\xi_2)}{2}h}_{\text{error term}}$$
When $f''(x)$ continuous, nearly constant on $[x_0-h,x_0]$: $\text{error}=O(h)$.

**Theorem/Property (Case 3 — Central Difference Error):**
Using second-order Taylor polynomials:
$$f(x_0+h) = f(x_0)+f'(x_0)h+\frac{f''(x_0)}{2}h^2+\frac{f'''(\xi_1)}{6}h^3$$
$$f(x_0-h) = f(x_0)+f'(x_0)(-h)+\frac{f''(x_0)}{2}(-h)^2+\frac{f'''(\xi_2)}{6}(-h)^3$$
where $x_0-h<\xi_2<x_0$ and $x_0<\xi_1<x_0+h$. Subtracting:
$$f(x_0+h)-f(x_0-h) = f'(x_0)(2h)+\frac{f'''(\xi_1)+f'''(\xi_2)}{6}h^3$$
Solving for $f'(x_0)$:
$$f'(x_0) = \underbrace{\frac{f(x_0+h)-f(x_0-h)}{2h}}_{\text{central difference quotient}} - \underbrace{\frac{f'''(\xi_1)+f'''(\xi_2)}{12}h^2}_{\text{error term}} \tag{3}$$
When $f'''(x)$ continuous, nearly constant on $[x_0-h,x_0+h]$: $\text{error}\approx\text{const}\cdot h^2$, so $\text{error}=O(h^2)$.

**Remark:** The central difference tends to give smaller errors of approximation.

**Worked Example/Note (Central difference as the average of forward and backward differences):**
$$\frac12\big[\text{forward difference}+\text{backward difference}\big] = \frac12\left[\frac{f(x_0+h)-f(x_0)}{h}+\frac{f(x_0)-f(x_0-h)}{h}\right] = \frac{f(x_0+h)-f(x_0-h)}{2h} = \text{central difference}$$
**"The central difference is the average of the forward difference and the backward difference formulas!!!"**

### Rounding Error Considerations

**Remark:** In practice, $h$ cannot be made too small because of rounding errors. Write
$$f(x_0+h) = f_1+e_1 \qquad \text{and} \qquad f(x_0-h) = f_{-1}+e_{-1}$$
where $f_1,f_{-1}$ are rounded values and $e_1,e_{-1}$ the rounding errors. If we replace the central divided difference $\dfrac{f(x_0+h)-f(x_0-h)}{2h}$ by the rounded values $\dfrac{f_1-f_{-1}}{2h}$, the error $\dfrac{e_1-e_{-1}}{2h}$ is introduced. Thus the total error in (3) is:
$$E(f,h) = \frac{e_1-e_{-1}}{2h} - \frac{f'''(\xi_1)+f'''(\xi_2)}{12}h^2 \tag{4}$$
Suppose we know: (1) the maximal rounding error $\epsilon$ (corresponding to the precision used), (2) $M=\max_{a\le x\le b}|f'''(x)|$.

**Theorem/Property (Best Choice of $h$ for Central Differences):**
By (4):
$$|E(f,h)| \le \frac{|e_1|+|e_{-1}|}{2h}+\frac{|f'''(\xi_1)|+|f'''(\xi_2)|}{12}h^2 \le \frac{\epsilon+\epsilon}{2h}+\frac{M+M}{12}h^2 = \frac{\epsilon}{h}+\frac{M}{6}h^2$$
Find $h$ minimizing $g(h)=\dfrac{\epsilon}{h}+\dfrac{M}{6}h^2$. Using calculus, $g(h)$ is smallest when
$$h = \left(\frac{3\epsilon}{M}\right)^{1/3}$$
which is the best (approximate) choice of $h$ for central differences.

**Worked Example 1:**
Given table:

| $x_k$ | 0.2 | 0.3 | 0.4 |
|---|---|---|---|
| $f(x_k)$ | $-0.3341$ | $-0.1769$ | $0.0138$ |

Estimate $f'(x_k)$ using forward, backward, and central differences for all $x_k$ where possible.

**Solution:**
1) Forward differences:
$$\text{at } x_k=0.2:\quad \frac{f(x_k+h)-f(x_k)}{h} = \frac{-0.1769-[-0.3341]}{0.1} = 1.572$$
$$\text{at } x_k=0.3:\quad \frac{f(x_k+h)-f(x_k)}{h} = \frac{0.0138-[-0.1769]}{0.1} = 1.907$$

2) Backward differences:
$$\text{at } x_k=0.3:\quad \frac{f(x_k)-f(x_k-h)}{h} = \frac{-0.1769-[-0.3341]}{0.1} = 1.572$$
$$\text{at } x_k=0.4:\quad \frac{f(x_k)-f(x_k-h)}{h} = \frac{0.0138-[-0.1769]}{0.1} = 1.907$$
**We notice:** backward diff. at $x_k=0.3$ = forward diff. at $x_k=0.2$; backward diff. at $x_k=0.4$ = forward diff. at $x_k=0.3$.

3) Central difference:
$$\text{at } x_k=0.3:\quad \frac{f(x_k+h)-f(x_k-h)}{2h} = \frac{0.0138-[-0.3341]}{0.2} = 1.7395$$
or: $\frac12\big[\text{fwd diff.}+\text{bwd diff. at }x_k=0.3\big] = \frac12[1.907+1.572] = 1.7395$

### Approximating Higher Order Derivatives

**Theorem/Property (Second Order Forward Difference — Derivation):**
Start with 2nd order Taylor polynomial at $x_0$:
$$f(x_0+h) = f(x_0)+f'(x_0)h+\frac{f''(x_0)}{2}h^2+O(h^3) \tag{5}$$
Replace $h$ by $2h$:
$$f(x_0+2h) = f(x_0)+f'(x_0)(2h)+\frac{f''(x_0)}{2}(2h)^2+O(h^3) \tag{6}$$
Multiply (5) by 2 and subtract from (6):
$$f(x_0+2h)-2f(x_0+h) = -f(x_0)+f''(x_0)h^2+O(h^3)$$
Solve for $f''(x_0)$:
$$f''(x_0) = \frac{f(x_0+2h)-2f(x_0+h)+f(x_0)}{h^2}+O(h)$$

**Core Formula (Second Order Forward Difference):**
$$f''(x_0) \approx \frac{f(x_0+2h)-2f(x_0+h)+f(x_0)}{h^2}$$

**Core Formula (Second Order Backward Difference, obtained similarly):**
$$f''(x_0) \approx \frac{f(x_0)-2f(x_0-h)+f(x_0-2h)}{h^2}$$

**Theorem/Property (Second Order Central Difference — Derivation):**
Start with 3rd order Taylor polynomials:
$$f(x_0+h) = f(x_0)+f'(x_0)h+\frac{f''(x_0)}{2}h^2+\frac{f'''(x_0)}{6}h^3+O(h^4)$$
$$f(x_0-h) = f(x_0)+f'(x_0)(-h)+\frac{f''(x_0)}{2}(-h)^2+\frac{f'''(x_0)}{6}(-h)^3+O(h^4)$$
Add both equations:
$$f(x_0+h)+f(x_0-h) = 2f(x_0)+2\cdot\frac{f''(x_0)}{2}h^2+O(h^4)$$
Solve for $f''(x_0)$:
$$f''(x_0) = \frac{f(x_0+h)-2f(x_0)+f(x_0-h)}{h^2}+O(h^2)$$

**Core Formula (Second Order Central Difference):**
$$f''(x_0) \approx \frac{f(x_0+h)-2f(x_0)+f(x_0-h)}{h^2}$$

**Worked Example 1 (continued):**
Same table as before. Estimate $f''(x_k)$ using second order forward, backward, and central differences for all $x_k$ where possible.

$$\text{2nd order forward diff. at } 0.2 = \text{2nd order central diff. at } 0.3 = \text{2nd order backward diff. at } 0.4$$
$$= \frac{0.0138-2\cdot[-0.1789\ (\text{i.e. } {-0.1769})]+[-0.3341]}{(0.1)^2}$$

Note: computed value $= 3.35$.

### Summary Tables of Difference Formulas

**Core Formula (Forward Differences), Error: $O(h)$:**
$$f'(x_k) \approx \frac{f(x_{k+1})-f(x_k)}{h}$$
$$f''(x_k) \approx \frac{f(x_{k+2})-2f(x_{k+1})+f(x_k)}{h^2}$$
$$f'''(x_k) \approx \frac{f(x_{k+3})-3f(x_{k+2})+3f(x_{k+1})-f(x_k)}{h^3}$$
$$f^{(4)}(x_k) \approx \frac{f(x_{k+4})-4f(x_{k+3})+6f(x_{k+2})-4f(x_{k+1})+f(x_k)}{h^4}$$

**Core Formula (Backward Differences), Error: $O(h)$:**
$$f'(x_k) \approx \frac{f(x_k)-f(x_{k-1})}{h}$$
$$f''(x_k) \approx \frac{f(x_k)-2f(x_{k-1})+f(x_{k-2})}{h^2}$$
$$f'''(x_k) \approx \frac{f(x_k)-3f(x_{k-1})+3f(x_{k-2})-f(x_{k-3})}{h^3}$$
$$f^{(4)}(x_k) \approx \frac{f(x_k)-4f(x_{k-1})+6f(x_{k-2})-4f(x_{k-3})+f(x_{k-4})}{h^4}$$

**Core Formula (Central Differences), Error: $O(h^2)$:**
$$f'(x_k) \approx \frac{f(x_{k+1})-f(x_{k-1})}{2h}$$
$$f''(x_k) \approx \frac{f(x_{k+1})-2f(x_k)+f(x_{k-1})}{h^2}$$
$$f'''(x_k) \approx \frac{f(x_{k+2})-2f(x_{k+1})+2f(x_{k-1})-f(x_{k-2})}{2h^3}$$
$$f^{(4)}(x_k) \approx \frac{f(x_{k+2})-4f(x_{k+1})+6f(x_k)-4f(x_{k-1})+f(x_{k-2})}{h^4}$$

### Summary Box (as handwritten on slide)

**Core Formula (If we have a grid on $[a,b]$ of equally spaced nodes $h=x_{k+1}-x_k$ for all $k$):**
1) Forward difference: $f'(x_k)\approx\dfrac{f(x_{k+1})-f(x_k)}{h}$, Error: $O(h)$
2) Backward difference: $f'(x_k)\approx\dfrac{f(x_k)-f(x_{k-1})}{h}$, Error: $O(h)$

**We notice:** forward difference at $x_k$ = backward difference at $x_{k+1}$.

3) Central difference: $f'(x_k)\approx\dfrac{f(x_{k+1})-f(x_{k-1})}{2h}$, Error: $O(h^2)$

**Best choice of $h$ (approximately):**
$$h = \sqrt[3]{\frac{3\epsilon}{M}}, \qquad \epsilon=\text{max. possible rounding error}, \qquad M=\max_{a\le x\le b}|f'''(x)|$$

### Exercises (as given)

**Exercise:**
Given table:

| $x_k$ | 0.2 | 0.4 | 0.6 | 0.8 | 1 |
|---|---|---|---|---|---|
| $f(x_k)$ | 0.9933 | 0.9735 | 0.9410 | 0.8967 | 0.8414 |

- Estimate $f'(x_k)$ using forward, backward, and central differences for all $x_k$ where possible. What do you notice?
- Estimate $f''(x_k)$ using second order forward, backward, and central differences for all $x_k$ where possible. What do you notice?
- Estimate $f'''(x_k)$ using third order forward, backward, and central differences for all $x_k$ where possible. What do you notice?

Given table:

| $x_k$ | 0.5 | 0.6 | 0.7 |
|---|---|---|---|
| $f(x_k)$ | 1.0000 | 0.2840 | 0.2484 |

- Estimate $f'(x_k)$ using forward, backward, and central differences for all $x_k$ where possible.
- Estimate $f''(x_k)$ using second order forward, backward, and central differences for all $x_k$ where possible.

**Exercise:**
Consider $f(x)=\sin\pi x+\cos\pi x$ and $x_k=kh$, $k=0,1,2,\dots,N$.
- Make a table of values for $f(x_k)$ for $h=0.2$ and $N=5$.
- Make a table of values for $f(x_k)$ for $h=0.1$ and $N=10$.
- Make a table of values for $f(x_k)$ for $h=0.05$ and $N=20$.
- For each of the above 3 tables, estimate $f'(0.4)$ by central difference. Then compute the approximation error (using the correct value of $f'(0.4)$), and check whether it is $O(h^2)$.
- For each of the above 3 tables, estimate $f''(0.6)$ by backward difference. Then compute the approximation error (using the correct value of $f''(0.6)$), and check whether it is $O(h)$.
