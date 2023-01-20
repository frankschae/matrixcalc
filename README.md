# Matrix Calculus for Machine Learning and Beyond

This is the course page for an 18.S096 Special Subject in Mathematics at MIT taught in **January 2023** ([IAP](https://elo.mit.edu/iap/)) by
Professors [Alan Edelman](https://math.mit.edu/~edelman/) and [Steven G. Johnson](https://math.mit.edu/~stevenj/).

For a previous version of this course, see [Matrix Calculus in IAP 2022 (OCW)](https://ocw.mit.edu/courses/18-s096-matrix-calculus-for-machine-learning-and-beyond-january-iap-2022/pages/lecture-notes-and-readings/) (also [on github](https://github.com/mitmath/matrixcalc/tree/iap2022)).

**Lectures:** MWF 11am–1pm, Jan 18–Feb 3 in room **2-190** (+ [video recording (MIT only)](https://mit.hosted.panopto.com/Panopto/Pages/Sessions/List.aspx?folderID=a72e3378-1c0f-425d-ae52-af880157e85c) and posted notes).  3 units, *2 problem sets* due Jan 25 and Feb 1 — submitted electronically [via Canvas](https://canvas.mit.edu/courses/17880), no exams.  Piazza discussion forum TBA. TA/grader: TBA.

**Piazza forum:** ask questions on the [18.S096 piazza](https://piazza.com/mit/spring2023/18s096)

**Description:**

> We all know that calculus courses such as 18.01 and 18.02 are univariate and vector calculus, respectively. Modern applications such as machine learning and large-scale optimization require the next big step, "matrix calculus" and calculus on arbitrary vector spaces.
>
> This class covers a coherent approach to matrix calculus showing techniques that allow you to think of a matrix holistically (not just as an array of scalars), generalize and compute derivatives of important matrix factorizations and many other complicated-looking operations, and understand how differentiation formulas must be re-imagined in large-scale computing. We will discuss reverse/adjoint/backpropagation differentiation, custom vector-Jacobian products, and how modern automatic differentiation is more computer science than calculus (it is neither symbolic formulas nor finite differences).

**Prerequisites:** Linear Algebra such as [18.06](https://ocw.mit.edu/courses/mathematics/18-06-linear-algebra-spring-2010/) and multivariate calculus such as [18.02](https://ocw.mit.edu/courses/mathematics/18-02-multivariable-calculus-fall-2007/).

Course will involve simple numerical compuations using the [Julia language](https://github.com/mitmath/julia-mit).   Ideally install it on your own computer following [these instructions](https://github.com/mitmath/julia-mit#installing-julia-and-ijulia-on-your-own-computer), but as a fallback you can run it in the cloud here:
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/mitmath/binder-env/main)

**Topics:**

Here are some of the planned topics:

* Derivatives as linear operators and linear approximation on arbitrary vector spaces: beyond gradients and Jacobians.
* Derivatives of functions with matrix inputs and/or outputs (e.g. matrix inverses and determinants).  Kronecker products and matrix "vectorization".
* Derivatives of matrix factorizations (e.g. eigenvalues/SVD) and derivatives with constraints (e.g. orthogonal matrices).
* Multidimensional chain rules, and the signifance of right-to-left ("forward") vs. left-to-right ("reverse") composition.  Chain rules on computational graphs (e.g. neural networks).
* Forward- and reverse-mode manual and automatic multivariate differentiation.
* Adjoint methods (vJp/pullback rules) for derivatives of solutions of linear, nonlinear, and differential equations.
* Application to nonlinear root-finding and optimization.  Multidimensional Newton and steepest–descent methods.
* Applications in engineering/scientific optimization and machine learning.
* Second derivatives, Hessian matrices, quadratic approximations, and quasi-Newton methods.

## Lecture 1 (Jan 18)

* part 1: [introductory slides](https://docs.google.com/presentation/d/1RqkL3AD6hVrUNpevQ7lhQ3InGr5-quQrnhQPsjvosDU/edit?usp=sharing)
* part 2: derivatives as linear operators — [handwritten notes](https://www.dropbox.com/s/dtdriu0jg1sqoqr/Derivatives%20as%20Linear%20Operators.pdf?dl=0)
* video recording (MIT only): [zoom recording](https://mit.zoom.us/rec/share/zsxeWYPY-zUW63ENT000dYdTt-vvVqvKYfM7J2J1QAvPuHMAXvadv4FDrtXsh_M.1JmilTjYrXV9ycwD?startTime=1674057910000) and [classroom recording](https://mit.hosted.panopto.com/Panopto/Pages/Sessions/List.aspx?folderID=a72e3378-1c0f-425d-ae52-af880157e85c)

Part 1: Overview, applications, and motivation.

Part 2: Re-thinking derivatives as linear operators: f(x+dx)-f(x)=df=f′(x)[dx] — f′ is the [linear operator](https://en.wikipedia.org/wiki/Linear_map) that gives the change df in the *output* from a "tiny" change dx in the *inputs*, to *first order* in dx (i.e. dropping higher-order terms).   When we have a scalar function f(x)∈ℝ of vector inputs x∈ℝⁿ, then this gives us a "row vector" f′(x) since f′(x)dx is a scalar, which we interpret as the *transpose* of the gradient ∇f (which we call a "column" vector), i.e. **df = (∇f)⋅dx = (∇f)ᵀdx**.   When we have a vector function f(x)∈ℝᵐ of vector inputs x∈ℝⁿ, then f'(x) is a linear operator that takes n inputs to m outputs, which we can think of as an m×n matrix called the [Jacobian matrix](https://en.wikipedia.org/wiki/Jacobian_matrix_and_determinant) (typically covered only superficially in 18.02.)

**Further reading**: [matrixcalculus.org](http://www.matrixcalculus.org/) (linked in the slides) is a fun site to play with derivatives of matrix and vector functions.  The [Matrix Cookbook](https://www.math.uwaterloo.ca/~hwolkowi/matrixcookbook.pdf) has a lot of formulas for these derivatives, but no derivations.  Some [notes on vector and matrix differentiation](https://cdn-uploads.piazza.com/paste/j779e63owl53k6/04b2cb8c2f300212d723bea822a6b856085b28e28ca9debc75a05761a436499c/6.S087_Lecture_2.pdf) were posted for 6.S087 from IAP 2021.

**Further reading (fancier math)**: the perspective of derivatives as linear operators is sometimes called a [Fréchet derivative](https://en.wikipedia.org/wiki/Fr%C3%A9chet_derivative) and you can find lots of very abstract (what I'm calling "fancy") presentations of this online, chock full of weird terminology whose purpose is basically to generalize the concept to weird types of vector spaces.  The "little-o notation" o(δx) we're using here for "infinitesimal asymptotics" is closely related to the [asymptotic notation](https://en.wikipedia.org/wiki/Big_O_notation) used in computer science, but in computer science people are typically taking the limit as the argument (often called "n") becomes very *large* instead of very small.  A fancy name for a row vector is a "covector" or [linear form](https://en.wikipedia.org/wiki/Linear_form), and the fancy version of the relationship between row and column vectors is the [Riesz representation theorem](https://en.wikipedia.org/wiki/Riesz_representation_theorem), but until you get to non-Euclidean geometry you may be happier thinking of a row vector as the transpose of a column vector.

## Lecture 2 (Jan 20)
* part 0: examples of linear and nonlinear transformations of ℝ² via images (to be posted)
* part 1: derivatives as linear operators — [handwritten notes](https://www.dropbox.com/s/dtdriu0jg1sqoqr/Derivatives%20as%20Linear%20Operators.pdf?dl=0)
* video recording (MIT only): zoom recording (coming soon) and [classroom recording](https://mit.hosted.panopto.com/Panopto/Pages/Sessions/List.aspx?folderID=a72e3378-1c0f-425d-ae52-af880157e85c)
* part 2: matrix Jacobians via [vectorization](https://en.wikipedia.org/wiki/Vectorization_(mathematics)), notes: 2×2 Matrix Jacobians [(html)](https://rawcdn.githack.com/mitmath/matrixcalc/f2409c96725f45fe35be38ed4d5db246cbf8e231/2x2Jacobians.jl.html) [(pluto notebook source code)](https://github.com/mitmath/matrixcalc/blob/main/2x2Jacobians.jl)
* pset 1: coming soon, due Jan 25

Part 1: Continued discussing derivatives as linear operators, starting with Jacobian matrices.  Reviewed the sum rule d(f+g)=df+dg, the product rule d(fg) = (df)g+f(dg), and the chain rule for f(g(x)) (f'(x)=g'(h(x))h'(x), where this is a *composition* of two linear operations, performing h' then g' — g'h' ≠ h'g'!).   For functions from vectors to vectors, the chain rule is simply the *product of Jacobians*.   Moreover, as soon as you compose 3 or more functions, it can a make a huge difference whether you multiply the Jacobians from left-to-right ("reverse-mode", or "backpropagation", or "adjoint differentiation") or right-to-left ("forward-mode"). Showed, for example, that if you have *many inputs but a single output* (as is common in machine learning and other types of optimization problem), that it is vastly more efficient to multiply left-to-right than right-to-left, and such "backpropagation algorithms" are a key factor in the practicality of large-scale optimization.  Finally, began talking about functions in more general vector spaces, such as functions with **matrix inputs and/or outputs**.  For example, considered f(A)=A³, giving d(A³)=f′(A)[dA]=A²(dA)+A(dA)A+(dA)A² (≠3A²dA!), and f(A)=A⁻¹, giving d(A⁻¹)=-A⁻¹(dA)A⁻¹.

Part 2: Began going into more detail on matrix-valued functions, and their relationship to the "Jacobian matrix" picture.  Converting f′(A) to a conventional "Jacobian matrix" in such cases requires converting matrices A into column vectors vec(A), a process called "vectorization" of the matrix (by a common convention: simply stacking the matrix by columns).  Linear operators like f′(A)[dA]=AdA+dAA can then be expressed as "ordinary" matrices via [Kronecker products](https://en.wikipedia.org/wiki/Kronecker_product).

**Further reading**: The terms "forward-mode" and "reverse-mode" differentiation are most prevalent in [automatic differentiation (AD)](https://en.wikipedia.org/wiki/Automatic_differentiation), which will will cover later in this course. You can find many, many articles online about [backpropagation](https://en.wikipedia.org/wiki/Backpropagation) in neural networks.   There are many other versions of this, e.g. in differential geometry the derivative linear operator (multiplying Jacobians and perturbations dx right-to-left) is called a [pushforward](https://en.wikipedia.org/wiki/Pushforward_(differential)), whereas multiplying a gradient row vector (covector) by a Jacobian left-to-right is called a [pullback](https://en.wikipedia.org/wiki/Pullback_(differential_geometry)).   This [video on the principles of AD in Julia](https://www.youtube.com/watch?v=UqymrMG-Qi4) by [Dr. Mohamed Tarek](https://github.com/mohamed82008) also starts with a similar left-to-right (reverse) vs right-to-left (forward) viewpoint and goes into how it translates to Julia code, and how you define custom chain-rule steps for Julia AD.
