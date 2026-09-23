## VI.5 Simpson's Rule (by Prof. Eckart Schulz — Numerical Methods for Computer)

**Definition (Basic Simpson's Rule Setup):**
To approximate $I=\int_a^b f(x)\,dx$, approximate $f$ by a quadratic function $p_2(x)$ which interpolates between the points $(x_0,f_0)$, $(x_1,f_1)$, $(x_2,f_2)$, where
$$x_0=a,\qquad x_1=\frac{a+b}{2},\qquad x_2=b,\qquad f_0=f(x_0),\ f_1=f(x_1),\ f_2=f(x_2)$$
and the length of each subinterval is $h=\dfrac{b-a}{2}$.

[Diagram: curve $y=f(x)$ approximated by parabola $y=p_2(x)$ interpolating the points $(x_0,f_0),(x_1,f_1),(x_2,f_2)$ over $[a,b]$, with two subintervals each of width $h$, shaded region between curve and parabola]

**Core Formula (One-Third Rule / Basic Simpson's Rule):**
Finding $p_2(x)$ (e.g. via Newton–Gregory interpolation) and integrating over $[a,b]$:
$$S_2 = \int_a^b p_2(x)\,dx = \frac{h}{3}(f_0+4f_1+f_2) \tag{12}$$
called the **one third rule**. Therefore
$$I = \int_a^b f(x)\,dx \approx S_2 = \frac{h}{3}(f_0+4f_1+f_2) \tag{13}$$
The application of Simpson's Rule must begin with two subintervals.

**Worked Example 4:**
Find the integral of $f(x)=0.2+25x-200x^2+675x^3-900x^4+400x^5$ on $[a,b]=[0,0.8]$ with $x_0=0,x_1=0.4,x_2=0.8$.

Using $S_2=\dfrac{h}{3}(f_0+4f_1+f_2)$ with $h=0.4$:
$$f_0=f(0.0)=0.2,\qquad f_1=f(0.4)=2.456,\qquad f_2=f(0.8)=0.232$$
$$S_2 = \frac{0.4}{3}\big[0.2+4(2.456)+0.232\big] = 1.367467$$
$$\int_0^{0.8} f(x)\,dx \approx 1.367467$$

**Definition/Core Formula (Composite Simpson's Rule — Derivation):**
Divide $[a,b]$ into $2N$ (even) equal intervals with nodes $x_0,x_1,\dots,x_{2N}$: $h=\dfrac{b-a}{2N}$, $x_j=x_0+jh$, $j=0,\dots,2N$, $x_0=a,x_{2N}=b$. Then
$$I=\int_a^b f(x)\,dx = \int_{x_0}^{x_2}f(x)\,dx+\int_{x_2}^{x_4}f(x)\,dx+\cdots+\int_{x_{2N-2}}^{x_{2N}}f(x)\,dx$$
Apply the basic Simpson's rule over each adjacent subinterval pair $[x_{j-1},x_j]$ and $[x_j,x_{j+1}]$, $j=1,3,5,\dots,2N-1$, and sum:
$$S_{2N} = \frac{h}{3}(f_0+4f_1+f_2)+\frac{h}{3}(f_2+4f_3+f_4)+\cdots+\frac{h}{3}(f_{2N-2}+4f_{2N-1}+f_{2N})$$

[Diagram: wavy curve $f$ over $[a,b]$ divided into pairs of subintervals of width $h$, each pair fitted with its own interpolation parabola through $(x_0,f_0),(x_1,f_1),(x_2,f_2)$ then $(x_{j-1},f_{j-1}),(x_j,f_j),(x_{j+1},f_{j+1})$, etc., up to $[x_{2N-2},x_{2N}]$; annotation "use the basic Simpson's rule on $[x_0,x_2]$", "on $[x_2,x_4]$", ..., "on $[x_{2N-2},x_{2N}]$"]

**Core Formula (Composite Simpson's Rule, boxed):**
After rearranging:
$$\boxed{S_{2N} = \frac{h}{3}\Big[f_0+f_{2N}+4(f_1+f_3+\cdots+f_{2N-1})+2(f_2+f_4+\cdots+f_{2N-2})\Big]} \tag{14}$$
$$I=\int_a^b f(x)\,dx \approx S_{2N}$$

**Theorem/Property (Error of Composite Simpson's Rule):**
$$|I-S_{2N}| = O(h^4)$$
Therefore the error will decrease approximately 16 times if the length $h$ of the subintervals is halved.

**Worked Example 5 ($I=\int_0^1 x\ln(x+1)\,dx$ via Simpson's Rule):**
Subinterval setups: $N=2,h=0.5$; $N=4,h=0.25$; $N=8,h=0.125$.

Function values $f(x)=x\ln(x+1)$ at the nodes:

| new node $x_j$ | $f_j$ |
|---|---|
| $N=2,h=0.5$: 0.000 | 0.00000 |
| 0.500 | 0.20273 |
| 1.000 | 0.69315 |
| $N=4,h=0.25$: 0.250 | 0.05579 |
| 0.750 | 0.41971 |
| $N=8,h=0.125$: 0.125 | 0.01472 |
| 0.375 | 0.11942 |
| 0.625 | 0.30344 |
| 0.875 | 0.55030 |

$$S_2 = \frac{h}{3}\big[f_0+4f_1+f_2\big] = \frac{0.5}{3}\big[0.0+4(0.20273)+0.69315\big] = 0.25068$$
$$S_4 = \frac{h}{3}\big[f_0+f_4+4(f_1+f_3)+2f_2\big] = \frac{0.25}{3}\big[0.0+0.69315+4(0.05579+0.41971)+2(0.20273)\big] = 0.25005$$
$$S_8 = \frac{h}{3}\big[f_0+f_8+4(f_1+f_3+f_5+f_7)+2(f_2+f_4+f_6)\big]$$
$$= \frac{0.125}{3}\big[0.0+0.69315+4(0.01472+0.11942+0.30344+0.55003)+2(0.05579+0.20273+0.41971)\big] = 0.25000$$

**Worked Example (True Value via Integration by Parts):**
$$I = \int_0^1 x\ln(x+1)\,dx$$
Let $u=\ln(x+1)$, $dv=x\,dx$ (by parts):
$$= \frac{x^2}{2}\ln(x+1)\Big|_0^1 - \frac12\int_0^1 \frac{x^2}{x+1}\,dx$$
$$= \left(\frac12\ln2-0\right) - \frac12\int_1^2 \frac{(u-1)^2}{u}\,du \qquad (u=x+1\Rightarrow x=u-1,\ dx=du)$$
$$= \frac12\ln2 - \frac12\int_1^2 \frac{u^2-2u+1}{u}\,du = \frac12\ln2 - \frac12\int_1^2\Big[u-2+\frac1u\Big]du$$
$$= \frac12\ln2 - \frac12\left[\frac{u^2}{2}-2u+\ln u\right]_1^2 = \frac12\ln2-\frac12\big[(2-4+\ln2)-(\tfrac12-2+0)\big] = \frac14 = 0.25$$

**Table (Errors compared to true value $I=0.25$):**

| $2N$ | Error $\lvert I-S_{2N}\rvert$ |
|---|---|
| 2 | $\lvert 0.25-0.25068\rvert = 0.00068$ (about $\frac{1}{16}\times$) |
| 4 | $\lvert 0.25-0.25005\rvert = 0.00005$ |
| 8 | $\lvert 0.25-0.25000\rvert = 0.00000$ ($S_8=I$ when computing with 5-digit accuracy) |

**Additional Worked Example ($I=\int_0^2 \dfrac{1}{1+x^2}\,dx$, comparing Simpson's and Trapezoidal rules):**
Estimate $I$ using (a) Simpson's rule and (b) the trapezoidal rule, with $h=1,0.5,0.25,0.125$.

*Step 1 — Correct value:*
$$I = \int_0^2 \frac{1}{1+x^2}\,dx = \tan^{-1}x\Big|_0^2 = \tan^{-1}(2)-\tan^{-1}(0) = 1.107149 \approx 1.10715 \ (5\text{-digit precision})$$

*Step 2 — Table of function values* $f(x)=\dfrac{1}{1+x^2}$ at nodes for $h=1,0.5,0.25,0.125$ (indices $f_0,f_1,\dots$ relabeled at each refinement level):

| $h=1$ | $N=2$ [trapez.] / $2N=2$ [Simpson] | $x_i=0,1,2$ | $f_i=1,\ 0.5,\ 0.2$ |
|---|---|---|---|
| $h=0.5$ | $N=4$ [trapez.] / $2N=4$ [Simpson] | $x=0.5,1.5$ | $f=0.8,\ 0.30769$ |
| $h=0.25$ | $N=8$ [trapez.] / $2N=8$ [Simpson] | $x=0.25,0.75,1.25,1.75$ | $f=0.94118,\ 0.64,\ 0.39024,\ 0.24615$ |
| $h=0.125$ | $N=16$ [trapez.] / $2N=16$ [Simpson] | $x=0.125,0.375,\dots,1.875$ | $f=0.98462,\ 0.87671,\ 0.71910,\ 0.56657,\ 0.44138,\ 0.34595,\ 0.27768,\ 0.22145$ |

*Trapezoidal rule computations:*
$$T_2 = \frac{h}{2}\big[f_0+2f_1+f_2\big] = \frac12\big[1+2(0.5)+0.2\big] = \frac{22}{2}\cdot\frac{1}{10}=1.1$$
$$T_4 = \frac{h}{2}\big[f_0+2(f_1+f_2+f_3)+f_4\big] = \frac{0.5}{2}\big[1+2(0.8+0.5+0.30769)+0.2\big] = 1.103845 \quad (Q_4=4.41538)$$
$$T_8 = \frac{h}{2}\big[Q_4+2(f_1+f_3+f_5+f_7)\big] = \frac{0.25}{2}\big[4.41538+2(0.94118+0.64+0.39024+0.24615)\big] = 1.106315 \quad (Q_8=8.85052)$$
$$T_{16} = \frac{h}{2}\big[Q_8+2(f_1+f_3+f_5+\cdots+f_{15})\big] = \frac{0.125}{2}\big[8.85052+2(4.43026)\big] = 1.10694$$

*Errors:*
$$|I-T_2| = |1.10715-1.1| = 0.00715$$
$$|I-T_4| = |1.10715-1.103845| = 0.003305 \approx \tfrac14\times \text{previous}$$
$$|I-T_8| = |1.10715-1.106315| = 0.000835 \approx \tfrac14\times \text{previous}$$
$$|I-T_{16}| = |1.10715-1.10694| = 0.00021$$

**Assignment (as given):**
1) Complete the above for Simpson's Rule.
2) Do Exercise 7.5 using Simpson's Rule.
3) Do Exercises 7.6 and 7.11. Due: Thursday, May 8.

**Exercises (as given):**
- Estimate $\int_1^3 x^3\,dx$ using Simpson's rule with $h=1$; compute the error compared to its true value.
- Let $I=\int_0^1(2^{-x}+x^3)\,dx$: (1) use Simpson's Rule with $h=0.5,0.25,0.125$; (2) find the true value and compare.
- Let $I=\int_0^2 \dfrac{1}{1+x^2}\,dx$: (1) use Simpson's Rule with $h=1,0.5,0.25,0.125$; (2) compute the true value and compare with estimates via relative errors; compare also to exercise 7.1.
- Use Simpson's rule to approximate $I$ in exercise 7.6 by computing $S_2,S_4,S_8$.
- Use Simpson's Rule to find approximate values of $I$ in exercise 7.7, dividing $[0,2]$ into $2,4,6,8,16$ subintervals: (1) compute errors $|I-S_{2N}|$; (2) summarize results in a table with columns $2N$, corresponding $h$, $S_{2N}$, and errors; compare with the table in exercise 7.7.
