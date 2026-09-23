```markdown
## Final Exam Instructions (Numerical Analysis, SCI19 3111)

**Source:** NumAn_final_recommendations.pdf (updated version)

**Content Type: Core Formula**
**Content Text:**
Exam logistics: Phones and tablets are not allowed; calculators are allowed. Each student may bring one A4 sheet of notes (a cheat sheet). There is no specific dress code. The exam consists of a multiple-choice section and a written section, for a total of 30 points.

**Section:** Theoretical Topics
**Content Type: Definition**
**Content Text:**
1. Understanding the idea and purpose of data fitting (regression) and its difference from interpolation.
2. The Hessian matrix for a two-parameter regression problem, including linear regression as a particular case. Its purpose and positive definiteness in the case of linear regression.
3. Some standard types of regression and the idea of linearization. Linearization formulas for standard cases.
4. Types of errors for data fitting: "naive," absolute, and squared errors. Reasons for using the squared error in regression.
5. Basic understanding of matrix formulas for regression in the case of multiple variables. The pseudoinverse matrix.
6. General understanding of the application of regression to classification problems in machine learning: features, the decision boundary, and the $\sigma$-function (logistic function).
7. Understanding of one-dimensional lattices (grids) used for numerical computation. Uniform and non-uniform grids. Advantages and disadvantages of uniform lattices.
8. The purpose and basic ideas of numerical integration. Examples of integrals that cannot be expressed in terms of elementary functions. A basic understanding of Riemann sums and the class of functions integrable by means of Riemann sums.
9. Knowledge of accuracy estimates for standard numerical integration methods (left and right rectangle rules, midpoint rule, trapezoidal rule, and Simpson's rule) in terms of the step size.
10. Understanding the basic idea behind deriving accuracy estimates for the simplest numerical integration formulas.
11. The concept of an ordinary differential equation (ODE). The general solution of a first-order ODE and an initial condition (initial value problem, or Cauchy problem).
12. General ideas behind methods for the approximate solution of first-order ODEs: Euler's method, the midpoint method, and Runge–Kutta methods. Knowledge of the accuracy estimates for these methods (without derivation).
13. Basic elements of linear algebra, the geometric meaning of determinants and their basic properties, including the multiplicative property of the determinant.
14. Understanding the ideas behind matrix factorizations, such as LU decomposition.

**Section:** Topics for Practical Problems
**Content Type: Worked Example/Proof**
**Content Text:**
1. Constructing a linear regression model from given data and making predictions using the constructed model.
2. Constructing a nonlinear regression model and performing its linearization and delinearization using standard formulas.
3. Ability to select the most appropriate regression model for a given data set presented graphically.
4. Computing the Hessian matrix for a data-fitting problem and analyzing its definiteness.
5. Ability to graphically construct rectangles for numerical integration using a formula of the form
$$x_i^{*} = \alpha x_{i-1} + (1-\alpha) x_i, \qquad \alpha \in [0,1].$$
6. Graphical construction of trapezoids and parabolas for numerical integration using the corresponding methods.
7. Approximate computation of an integral using rectangle and trapezoidal rules on uniform and non-uniform lattices.
8. Approximate computation of an integral using Simpson's (parabola) rule on a uniform lattice.
9. Approximate solution of an initial value problem for a first-order ODE using simple methods, such as Euler's method and the midpoint method.
10. Ability to write down a Runge–Kutta scheme for a given ODE (without performing the subsequent numerical solution).
11. Basic operations with matrices, vectors, and determinants. Projections of vectors. Areas and volumes.
12. Laplace (cofactor) expansion of a determinant. Determinants of lower and upper triangular matrices. Computing the determinant of an $n \times n$ matrix for $n > 3$.
13. LU decomposition for small matrices. Solving simple systems of linear equations using LU decomposition.
```
