## VI. Numerical Integration (Slides VI.1–VI.4, by Prof. Eckart Schulz — Numerical Methods for Computer, Lectures 14–16)

### VI.1 Why Numerical Integration

**Core Formula (Definite Integral via Antiderivative):**
$$I = \int_a^b f(x)\,dx$$
The value of this integral is usually calculated by
$$\int_a^b f(x)\,dx = F(b) - F(a) \tag{1}$$
when $F$ is an antiderivative of $f$.

**Worked Example (Basic antiderivative evaluation, annotation):**
$$\int_1^3 x^2\,dx = \frac{x^3}{3}\Big|_1^3 = \frac{3^3}{3} - \frac{1^3}{3} = \frac{26}{3}$$

**Remark:** Sometimes no closed form of the antiderivative is available, such as
$$I = \int_0^1 e^{-x^2}\,dx$$
Annotation: "There is no formula for an antiderivative of $e^{-x^2}$."

Also, in applications one often has no formula for a function $f$, but only knows the values of $f(x)$ at some individual points. In these cases, one may find the value of the integral by a numerical approximation process.

---

### VI.3 Rectangle Rules

**Definition/Core Formula (Setup, recalled from the definition of the integral):**
1. Divide $[a,b]$ into $N$ intervals of equal length:
$$\Delta x = h = \frac{b-a}{N}$$
Get node points $x_0=a,\ x_1=x_0+h,\ x_2=x_0+2h,\dots,x_N=x_0+Nh=b$.
2. The area of a rectangle with length of base $h=\Delta x$ and height $f_{j-1}=f(x_{j-1})$ is $\Delta A_j = h\cdot f_j$.
3. The combined area of all rectangles is
$$I_N = R_{L_N} = \sum_{j=0}^{N-1} f_j\cdot h \quad (\text{"Riemann sum"})$$
4. Then
$$\int_a^b f(x)\,dx = \lim_{N\to\infty} R_{L_N} = \lim_{N\to\infty} h\sum_{j=0}^{N-1} f_j$$

[Diagram: increasing curve $y=f(x)$ on $[a,b]$ with left-endpoint rectangles of width $h$ and heights $f_0,f_1,\dots,f_{N-1}$ shaded underneath, labeled "the height of the rectangle over an interval $[x_j,x_{j+1}]$ is determined by the value of the function $f$ at the left endpoint," $f_j=f(x_j)$, $j=0,\dots,N-1$]

**Core Formula (Composite Left Rectangle Rule):**
$$R_{L_N} = hf_0+hf_1+\cdots+hf_{N-1} = h\sum_{j=0}^{N-1} f_j \tag{6}$$
$$I = \int_a^b f(x)\,dx \approx R_{L_N} = h\sum_{j=0}^{N-1} f_j$$

**Remark (Alternative — Right Endpoint):** Alternatively, the height of a rectangle over an interval $[x_{j-1},x_j]$ is determined by the value of $f(x)$ at the right endpoint: $A_j = hf_j$ ($f_j=f(x_j)$, $j=1,\dots,N$).

[Diagram: same increasing curve with right-endpoint rectangles labeled $f_1,\dots,f_N$]

**Core Formula (Composite Right Rectangle Rule):**
$$R_{R_N} = hf_1+hf_2+\cdots+hf_N = h\sum_{j=1}^N f_j \tag{7}$$
$$I = \int_a^b f(x)\,dx \approx R_{R_N} = h\sum_{j=1}^N f_j$$

---

### VI.4 The Trapezoidal Rule

**Definition (Idea):** Use a trapezoid instead of a rectangle in the approximation of $\int_a^b f(x)\,dx$.

The **basic trapezoidal rule** approximates $I=\int_a^b f(x)\,dx$ (8) by approximating $f$ with a linear function $p_1(x)$ (a polynomial of degree one) which interpolates between the points $(a,f(a))$ and $(b,f(b))$. Geometrically, this gives a trapezoid.

[Diagram: curve $y=f(x)$ on $[a,b]$ with secant line (the degree-one interpolating polynomial $p_1(x)$) connecting $(a,f(a))$ and $(b,f(b))$, shaded trapezoidal region $T$ beneath, base $h=b-a$]

**Core Formula (Area of a Single Trapezoid):**
$$A = \text{length of base} \times \text{average height} = (b-a)\times\frac{f(a)+f(b)}{2} = \frac{h}{2}\times[f(a)+f(b)]$$

**Core Formula (Basic Trapezoidal Rule):**
$$T = \int_a^b p_1(x)\,dx = \text{area of shaded trapezoid} = \frac{(b-a)}{2}\big[f(a)+f(b)\big] \tag{9}$$
Therefore
$$I = \int_a^b f(x)\,dx \approx T = \frac{(b-a)}{2}\big[f(a)+f(b)\big] \tag{10}$$
Annotation: there is in general a large error of approximation using a single trapezoid; to reduce the error, choose a large number of "narrow" trapezoids.

**Core Formula (Composite Trapezoidal Rule — Derivation):**
Divide $[a,b]$ into $N$ equal intervals with nodes $x_0,x_1,\dots,x_N$: $\Delta x = h=\dfrac{b-a}{N}$, $x_j=x_0+jh$, $x_0=a$, $x_N=b$. Then
$$I=\int_a^b f(x)\,dx = \int_{x_0}^{x_1}f(x)\,dx+\int_{x_1}^{x_2}f(x)\,dx+\cdots+\int_{x_{N-1}}^{x_N}f(x)\,dx$$
Approximate each of these integrals by the basic trapezoidal rule; $T_N$ = combined area of all shaded trapezoids:

[Diagram: wavy curve over $[a,b]$ partitioned into $N$ subintervals of width $h$ with trapezoids drawn under the curve between consecutive nodes $x_0,\dots,x_N$; annotation "the errors are much smaller as compared to using rectangles"]

$$T_N = \frac{h}{2}(f_0+f_1)+\frac{h}{2}(f_1+f_2)+\frac{h}{2}(f_2+f_3)+\cdots+\frac{h}{2}(f_{N-1}+f_N)$$
$$= \frac{h}{2}\big[f_0+2f_1+2f_2+\cdots+2f_{N-1}+f_N\big] = \frac{h}{2}\big[f_0+2(f_1+f_2+\cdots+f_{N-1})+f_N\big]$$

**Core Formula (Composite Trapezoidal Rule, boxed):**
$$\boxed{\int_a^b f(x)\,dx \approx T_N = \frac{h}{2}\Big[f_0+2(f_1+f_2+\cdots+f_{N-1})+f_N\Big]} \tag{11}$$

**Theorem/Property (Error of the Trapezoidal Rule):**
$$|I-T_N| = O(h^2)$$
meaning there exists a positive number $M$ so that $|I-T_N|\le Mh^2$ (one can give a formula for $M$, but we need not care). So the error will decrease $\approx \frac14$ times if the length $h$ decreases by half.

**Worked Example 1 ($I=\int_0^2 x^3\,dx$ via composite trapezoidal rule for $N=1,2,4$):**
True value: $I=\int_0^2 x^3\,dx = \dfrac{x^4}{4}\Big|_0^2 = 4$.

*For $N=1$:* $h=2,\ x_0=0,\ x_1=2,\ f_0=0^3=0,\ f_1=2^3=8$.
$$T_1 = \frac{2}{2}(f_0+f_1) = (1)(0+8) = 8$$
[Diagram: line from $(0,0)$ to $(2,8)$ forming a large trapezoid over the curve $y=x^3$; error $|8-4|=4$]

*For $N=2$:* $h=1,\ x_0=0,x_1=1,x_2=2,\ f_0=0,\ f_1=1^3=1,\ f_2=8$.
$$T_2 = \frac12(f_0+2f_1+f_2) = \frac12(0+2\cdot1+8) = 5$$
[Diagram: two trapezoids over $y=x^3$ on $[0,1]$ and $[1,2]$; error $|5-4|=1$]

*For $N=4$:* $h=\dfrac{2-0}{4}=0.5$.

| $x_j$ | 0 | 0.5 | 1 | 1.5 | 2 |
|---|---|---|---|---|---|
| $f_j=x_j^3$ | 0 | 0.125 | 1 | 3.375 | 8 |

$$T_4 = \frac{0.5}{2}\big[f_0+2(f_1+f_2+f_3)+f_4\big] = \frac14\big[0+2(0.125+1+3.375)+8\big] = 4.25$$
[Diagram: four trapezoids over $y=x^3$ on $[0,2]$; error $|4.25-4|=0.25$]

**Table (Convergence of $T_N$):**

| $N$ | $h$ | $T_N$ | $\lvert I-T_N\rvert$ |
|---|---|---|---|
| 1 | 2 | 8 | 4 |
| 2 | 1 | 5 | 1 |
| 4 | 0.5 | 4.25 | 0.25 |
| 8 | 0.25 | 4.0625 | 0.0625 |
| 16 | 0.125 | 4.0156 | 0.0156 |
| 32 | 0.0625 | 4.0039 | 0.0039 |

Annotation: As $h$ gets reduced by a factor of $\frac12$, the error gets reduced by the factor $\frac14$; Error $=O(h^2)$.

**Worked Example 2 (Trapezoidal rule from a data table):**
Estimate $\int_0^1 f(x)\,dx$ using:

| $x$ | 0.0 | 0.2 | 0.4 | 0.6 | 0.8 | 1.0 |
|---|---|---|---|---|---|---|
| $f(x)$ | 1.00000 | 0.99335 | 0.97355 | 0.94107 | 0.89670 | 0.84147 |

$h=0.2$; since $h=\dfrac{1-0}{N}$, $N=\dfrac{1}{0.2}=5$.
$$f_0+f_5 = 1.00000+0.84147=1.84147, \qquad f_1+f_2+f_3+f_4 = 0.99335+\cdots+0.89670=3.80467$$
$$T_5 = \frac{h}{2}\big[f_0+f_5+2(f_1+f_2+f_3+f_4)\big] = \frac{0.2}{2}\big[1.84147+2(3.80467)\big] = 0.94508$$
$$\int_0^1 f(x)\,dx \approx 0.94508$$

**Core Formula (Iterative Composite Trapezoidal Rule):**
Denote $S_N = f_0+2(f_1+f_2+\cdots+f_{N-1})+f_N$, so $T_N = \dfrac{h}{2}S_N$.

[Diagram: sequence of three number lines showing successive halving of subintervals from $N=1$ ($f_0,f_1$) to $N=2$ (new $f_1$ inserted, old $f_1$ relabeled $f_2$) to $N=4$ (new $f_1,f_3$ inserted, previous nodes relabeled $f_2,f_4$), with formulas $S_1=f_0+f_1$, $S_2=S_1+2f_1$, $S_4=S_2+2(f_1+f_3)$]

One can use the composite trapezoidal rule iteratively by halving each subinterval (doubling the number of subintervals) at each step, computing functional values only at the new nodes and adding them to the previous sum.

**Worked Example 3 ($I=\int_0^4 x^2\,dx$ via iterative composite trapezoidal rule, $N=1,2,4,8$):**
True value: $I=\int_0^4 x^2\,dx = \dfrac{x^3}{3}\Big|_0^4 = \dfrac{64}{3}-0 = 21\tfrac13$.

Table of new nodes and function values ($f(x)=x^2$, $b-a=4$):

| | new $x_j$ | $f_j=f(x_j)$ |
|---|---|---|
| $N=1,\ h=4$ | $0\to0$, $4\to16$ | $f_0=0,\ f_1=16$ |
| $N=2,\ h=2$ | $2\to4$ | $f_1^{(\text{new})}=4$ |
| $N=4,\ h=1$ | $1\to1$, $3\to9$ | |
| $N=8,\ h=0.5$ | $0.5\to0.25$, $1.5\to2.25$, $2.5\to6.25$, $3.5\to12.25$ | |

$$S_1=f_0+f_1=0+16=16$$
$$S_2=S_1+2f_1=16+2\cdot4=24$$
$$S_4=S_2+2(f_1+f_3)=24+2(1+9)=44$$
$$S_8=S_4+2(f_1+f_3+f_5+f_7)=44+2(0.25+2.25+6.25+12.25)=86$$

| | $h/2$ | $S_N$ | $T_N=\frac{h}{2}S_N$ | $\lvert I-T_N\rvert$ |
|---|---|---|---|---|
| $N=1,h=4$ | 2 | 16 | 32 | $10.666667 = 32/3$ |
| $N=2,h=2$ | 1 | 24 | 24 | $2.666667=8/3$ |
| $N=4,h=1$ | 0.5 | 44 | 22 | $0.666667=2/3$ |
| $N=8,h=0.5$ | 0.25 | 86 | 21.5 | $0.166667=1/6$ |

**Exercises (as given):**
- $I=\int_{-1}^0 \dfrac{1}{4+t}\,dt$: (1) approximate via composite trapezoidal rule with $h=1,0.5,0.25,0.125,0.0625$; (2) find true value, compute relative error.
- $I=\int_0^2 x\sin x\,dx$: (1) approximate with $h=1,0.5,0.25,0.125$; (2) find true value, compute relative error.
- (Exercise 7.6) $f(x)=e^{-x^2}$: (1) compute $f(x)$ at $x_k=x_0+kh$, $x_0=0,h=0.125,k=0,\dots,8$; (2) approximate $I=\int_0^1 e^{-x^2}dx$ using $T_2,T_4,T_8$.
- (Exercise 7.7) $I=\int_0^2 e^{2x}\sin3x\,dx$: (1) find true value; (2) compute approximate $T_N$ for $N=1,2,4,8,16$ subintervals; (3) summarize relative errors $|I-T_N|$; (4) tabulate $N$, $h$, $T_N$, relative errors.

**Assignment (as given):** Due Tuesday, 6 May — Problems 6.8 (do with calculator), 6.9 (write a computer program; stop when the relative error is $<0.1\%$), 7.5 (do with calculator).
