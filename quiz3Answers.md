# Answers to Quiz 3: Truncation Error (Numerical Analysis)

The formulas for the truncation error are

$$R_n(x) = \int_{x_0}^{x} \frac{(x-t)^n}{n!} f^{(n+1)}(t)\, dt$$

and

$$R_n(x) = \frac{f^{(n+1)}(\xi)}{(n+1)!} (x-x_0)^{n+1}, \quad \xi \in [\min(x_0, x), \max(x_0, x)].$$

---

## 1.

**(a) (2 points)**

$$f(x) = \sin(3x) \simeq 3x - \frac{3^3 x^3}{3!} + \frac{3^5 x^5}{5!} - \frac{3^7 x^7}{7!} + \dots \simeq 3x - \frac{9x^3}{2} + \frac{81x^5}{40} - \frac{243x^7}{560} + \dots$$

**(b) (2 points)**

$$\sum_{k=0}^{n} \frac{(-1)^k 3^{2k+1} x^{2k+1}}{(2k+1)!}$$

**(c) (1 point)**

This is a Taylor series as

$$\lim_{n \to \infty} |R_n(x)| = 0$$

for any $x$.

---

## 2. Write the truncation error $R_n(x)$ for the function $f(x)$ from the previous problem:

**(a) (1.5 points)**

$$R_{2m+1}(x) = (-1)^{m+1} \frac{3^{2m+2}}{(2m+1)!} \int_0^x (x-t)^{2m+1} \sin(3t)\, dt$$

**(b) (1.5 points)**

$$R_{2m+1}(x) = (-1)^{m+1} \frac{3^{2m+2} \sin(3\xi)}{(2m+2)!} x^{2m+2}$$

---

## 3. (2 points)

$$|R_{2m+1}(x)| \leqslant \frac{3^{2m+2}}{(2m+2)!} \cdot 4^{2m+2} = \frac{12^{2m+2}}{(2m+2)!}, \quad x \in [-3, 4].$$

---

## 4. (2 points)

Suppose that the required approximation error from the previous problem is less than $10^{-5}$. Determine a suitable value of $n$ that guarantees this level of accuracy.

$$R_m = \frac{12^{2m+2}}{(2m+2)!} < 10^{-5}$$

For $m = 19$, $2m+2 = 40$, $R_m \simeq 1.8 \times 10^{-5} > 10^{-5}$.

For $m = 20$, $2m+2 = 42$, $R_m \simeq 1.5 \times 10^{-6} < 10^{-5}$.

Thus, $m = 20$ and $2m + 2 = 42$.

---

## 5. (2 extra points)

$$|R_{2m+1}(x)| \leqslant \frac{3^{2m+2}}{(2m+2)!} x^{2m+2}.$$

- As $2m+1$ cannot be equal to $8$, we assume $2m+1 = n = 9$. Then,

$$\frac{3^{10}}{10!} x^{10} < 10^{-7}.$$

$$x < 0.30120005620392776.$$

- If we take $2m+1 = n = 7$,

$$\frac{3^{8}}{8!} x^{8} < 10^{-7}.$$

$$x < 0.16732807342047598.$$
