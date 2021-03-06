#  18.335J/6.337J: Introduction to Numerical Methods

This is the repository of course materials for the 18.335J/6.337J course at MIT, taught by Prof. [Steven G. Johnson](http://math.mit.edu/~stevenj/), in Spring 2019.

Syllabus
--------

**Lectures**: Monday/Wednesday/Friday 3–4pm (2-190). **Office Hours:** Thursday 4–5pm (2-345).

**Topics**: Advanced introduction to numerical linear algebra and related numerical methods. Topics include direct and iterative methods for linear systems, eigenvalue decompositions and QR/SVD factorizations, stability and accuracy of numerical algorithms, the IEEE floating-point standard, sparse and structured matrices, and linear algebra software. Other topics may include memory hierarchies and the impact of caches on algorithms, nonlinear optimization, numerical integration, FFTs, and sensitivity analysis. Problem sets will involve use of [Julia](http://julialang.org/), a Matlab-like environment (little or no prior experience required; you will learn as you go).

**Prerequisites**: Understanding of linear algebra ([18.06](http://web.mit.edu/18.06/www/), [18.700](http://ocw.mit.edu/OcwWeb/Mathematics/18-700Fall-2005/CourseHome/), or equivalents). 18.335 is a graduate-level subject, however, so much more mathematical maturity, ability to deal with abstractions and proofs, and general exposure to mathematics is assumed than for 18.06!

**Textbook**: The primary textbook for the course is [_Numerical Linear Algebra_ by Trefethen and Bau](http://www.amazon.com/Numerical-Linear-Algebra-Lloyd-Trefethen/dp/0898713617). ([Readable online](http://owens.mit.edu:8888/sfx_local?bookid=9436&rft.genre=book&sid=Barton:Books24x7) with MIT certificates.)

**Other Reading**: Previous terms can be found in [branches of the 18335 git repository](https://github.com/mitmath/18335/branches). The [course notes from 18.335 in much earlier terms](https://ocw.mit.edu/courses/mathematics/18-335j-introduction-to-numerical-methods-fall-2010/) can be found on OpenCourseWare. For a review of iterative methods, the online books [Templates for the Solution of Linear Systems](http://www.netlib.org/linalg/html_templates/Templates.html) (Barrett et al.) and [Templates for the Solution of Algebraic Eigenvalue Problems](http://www.cs.utk.edu/~dongarra/etemplates/book.html) are useful surveys.

**Grading**: 33% problem sets (about six, ~biweekly). 33% **take-home mid-term exam** (posted Monday **Apr. 8** and due Tuesday **Apr. 9**), 34% **final project** (one-page proposal due Friday March 22, project due Wednesday **May 15**).

* Psets will be [submitted electronically via Stellar](https://learning-modules.mit.edu/gradebook/index.html?uuid=/course/18/sp19/18.335).  Submit a good-quality PDF *scan* of any handwritten solutions and *also* a PDF *printout* of a Julia notebook of your computational solutions.

**TA:** [Sung Woo Jeong](http://math.mit.edu/directory/profile.php?pid=1782).

**Collaboration policy**: Talk to anyone you want to and read anything you want to, with three exceptions: First, you **may not refer to homework solutions from the previous terms** in which I taught 18.335. Second, make a solid effort to solve a problem on your own before discussing it with classmates or googling. Third, no matter whom you talk to or what you read, write up the solution on your own, without having their answer in front of you.

**Final Projects**: The final project will be a 8–15 page paper (single-column, single-spaced, ideally using the style template from the [_SIAM Journal on Numerical Analysis_](http://www.siam.org/journals/auth-info.php)), reviewing some interesting numerical algorithm not covered in the course. \[Since this is not a numerical PDE course, the algorithm should _not_ be an algorithm for turning PDEs into finite/discretized systems; however, your project _may_ take a PDE discretization as a given "black box" and look at some other aspect of the problem, e.g. iterative solvers.\] Your paper should be written for an audience of your peers in the class, and should include example numerical results (by you) from application to a realistic problem (small-scale is fine), discussion of accuracy and performance characteristics (both theoretical and experimental), and a fair comparison to at **least one competing algorithm** for the same problem. Like any review paper, you should _thoroughly reference_ the published literature (citing both original articles and authoritative reviews/books where appropriate \[rarely web pages\]), tracing the historical development of the ideas and giving the reader pointers on where to go for more information and related work and later refinements, with references cited throughout the text (enough to make it clear what references go with what results). (**Note:** you may re-use diagrams from other sources, but all such usage must be _explicitly credited_; not doing so is [plagiarism](http://writing.mit.edu/wcc/avoidingplagiarism).) Model your paper on academic review articles (e.g. read _SIAM Review_ and similar journals for examples).

Frequently asked questions about the final project:

1.  _Does it have to be about numerical linear algebra?_ No. It can be any numerical topic (basically, anything where you are computing a conceptually real result, not integer computations), excluding algorithms for discretizing PDEs.
2.  _Can I use a matrix from a discretized PDE?_ Yes. You can take a matrix from the PDE as input and then talk about iterative methods to solve it, etcetera. I just don't want the paper to be about the PDE discretization technique itself.
3.  _How formal is the proposal?_ Very informal—one page describing what you plan to do, with a couple of references that you are using as starting points. Basically, the proposal is just so that I can verify that what you are planning is reasonable and to give you some early feedback.
4.  _How much code do I need to write?_ A typical project (there may be exceptions) will include a working proof-of-concept implementation, e.g. in Julia or Python or Matlab, that you wrote to demonstrate that you understand how the algorithm works. Your code does _not_ have to be competitive with "serious" implementations, and I encourage you to download and try out existing "serious" implementations (where available) for any large-scale testing and comparisons.
5.  _How should I do performance comparisons?_ Be very cautious about timing measurements: unless you are measuring highly optimized code or only care about orders of magnitude, timing measurements are more about implementation quality than algorithms. Better to measure something implementation independent (like flop counts, or matrix-vector multiplies for iterative algorithms, or function evaluations for integrators/optimizers), although such measures have their own weaknesses.

* * *

Lecture Summaries and Handouts
------------------------------

### Lecture 1 (Feb 6)

* [pset 1](psets/pset1.pdf) and accompanying [notebook](https://nbviewer.jupyter.org/github/mitmath/18335/blob/master/psets/pset1.ipynb), due Friday Feb. 15.
* [Newton's method for square roots](notes/newton-sqrt.pdf) and accompanying [notebook](https://nbviewer.jupyter.org/github/mitmath/18335/blob/master/notes/Newton-Square-Roots.ipynb).

Brief overview of the huge field of numerical methods, and outline of the small portion that this course will cover. Key new concerns in numerical analysis, which don't appear in more abstract mathematics, are (i) performance (traditionally, arithmetic counts, but now memory access often dominates) and (ii) accuracy (both floating-point roundoff errors and also convergence of intrinsic approximations in the algorithms).

As a starting example, considered the convergence of Newton's method (as applied to square roots); see the handout and Julia notebook above.

**Further reading:** Googling "Newton's method" will find lots of references; as usual, the [Wikipedia article on Newton's method](https://en.wikipedia.org/wiki/Newton's_method) is a reasonable starting point. Beware that the terminology for the [convergence order](https://en.wikipedia.org/wiki/Rate_of_convergence) (linear, quadratic, etc.) is somewhat different in this context from the terminology for discretization schemes (first-order, second-order, etc.); see e.g. the linked Wikipedia article. Homer Reid's [notes on machine arithmetic](http://homerreid.dyndns.org/teaching/18.330/Notes/RootFinding.pdf) for [18.330](http://homerreid.dyndns.org/teaching/18.330/) are an excellent introduction that covers several applications and algorithms for root-finding. For numerical computation in 18.335, we will be using the Julia language: see this [information on Julia at MIT](https://github.com/mitmath/julia-mit).

### Julia tutorial (Feb 8: 5pm in 32-141) — optional

**Handout:** [Julia cheat-sheet](https://github.com/mitmath/julia-mit/blob/master/Julia-cheatsheet.pdf), [Julia intro slides](https://github.com/mitmath/julia-mit/blob/master/Julia-intro.pdf)

On Friday, 8 February, at 5pm in 32-141, I will give an (attendance-optional!) Julia tutorial, introducing the [Julia programming language and environment](http://julialang.org/) that we will use this term. Please see the [tutorial notes online](https://github.com/mitmath/julia-mit/blob/master/README.md).

Please **bring your laptops**, and try to install Julia and the IJulia interface first via the abovementioned tutorial notes. Several people will be at the tutorial session to help answer installation questions. Alternatively, you can use Julia online at [JuliaBox](https://juliabox.com/) without installing anything (although running things on your own machine is usually faster).

### Lecture 2 (Feb 8)

* [notes on floating-point](notes/lec8handout6pp.pdf) (18.335 Fall 2007; also [slides](notes/lec8.pdf))
* Julia [floating-point notebook](https://nbviewer.jupyter.org/github/mitmath/18335/blob/master/notes/Floating-Point-Intro.ipynb)
* some [floating-point myths](notes/fp-myths.pdf)

New topic: **Floating-point arithmetic**

The basic issue is that, for computer arithmetic to be fast, it has to be done in hardware, operating on numbers stored in a fixed, finite number of digits (bits). As a consequence, only a _finite subset_ of the real numbers can be represented, and the question becomes _which subset_ to store, how arithmetic on this subset is defined, and how to analyze the errors compared to theoretical exact arithmetic on real numbers.

In **floating-point** arithmetic, we store both an integer coefficient and an exponent in some base: essentially, scientific notation. This allows large dynamic range and fixed _relative_ accuracy: if fl(x) is the closest floating-point number to any real x, then |fl(x)-x| < ε|x| where ε is the _machine precision_. This makes error analysis much easier and makes algorithms mostly insensitive to overall scaling or units, but has the disadvantage that it requires specialized floating-point hardware to be fast. Nowadays, all general-purpose computers, and even many little computers like your cell phones, have floating-point units.

Went through some simple examples in Julia (see notebook above), illustrating basic syntax and a few interesting tidbits, in particular on the accuracy of summation algorithms, that we will investigate in more detail later.

Overview of **floating-point** representations, focusing on the IEEE 754 standard (see also handout from previous lecture). The key point is that the nearest floating-point number to _x_, denoted fl(_x_), has the property of _uniform relative precision_ (for |_x_| and 1/|_x_| < than some _range_, ≈10308 for double precision) that |fl(_x_)−_x_| ≤ εmachine|_x_|, where εmachine is the relative "machine precision" (about 10−16 for double precision). There are also a few special values: ±Inf (e.g. for [overflow](https://en.wikipedia.org/wiki/Arithmetic_overflow)), [NaN](https://en.wikipedia.org/wiki/NaN), and ±0 (e.g. for [underflow](https://en.wikipedia.org/wiki/Arithmetic_underflow)).

**Further reading:** [What Every Computer Scientist Should Know About Floating Point Arithmetic](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.22.6768) (David Goldberg, ACM 1991). William Kahan, [How Java's floating-point hurts everyone everywhere](http://www.cs.berkeley.edu/~wkahan/JAVAhurt.pdf) (2004): contains a nice discussion of floating-point myths and misconceptions. Trefethen, lecture 13. Homer Reid's [notes on machine arithmetic](http://homerreid.com/teaching/18.330/Notes/MachineArithmetic.pdf) for [18.330](http://homerreid.com/teaching/18.330/) are another nice introduction to this material.

### Lecture 3 (Feb 11)

* notes on the accuracy of [floating-point summation](notes/naivesum.pdf)
* [notes on backwards stability of summation](notes/summation-stability.pdf) — in class, I instead showed the same thing using the previous accuracy notes as a starting point, but similarly using the L₁ norm.

Analyzed the accumulated floating-point roundoff errors (see notes), explaining the results that we observed experimentally in the Julia notebook of the previous lecture.  In those experiments, all of the inputs were non-negative, so that the "condition number" factor in the derivation equalled 1.   In general, though, if you have *cancellations* between summands of opposite signs, the same analysis shows that the relative error of the output can be arbitrarily large.

**Stability:** Gave the obvious definition of **accuracy**, what we might call "forwards stability" = almost the right answer for the right input. Showed that this is often too strong; e.g. adding a sequence of numbers is not forwards stable. (Basically because the denominator in the relative forwards error, which is the exact sum, can be made arbitrarily small via cancellations.)

Define asymptotic notation O(ε): f(ε) is O(g(ε)) if there exist some constants C, ε₀ > 0 such that |f(ε)| < C|g(ε)| for all |ε|<ε₀. That is, g(ε) is an asymptotic _upper bound_ for f(ε) as ε goes to zero, ignoring constant factors C. (A similar notation is used in computational complexity theory, but in the limit of _large_ arguments n.) In the definitions of stability, we technically require [uniform convergence](https://en.wikipedia.org/wiki/Uniform_convergence): we must have O(ε) errors with the same constants C and ε₀ independent of the inputs x.  (The constants *can* depend on the dimension of x, however.)

More generally, we apply a weaker condition: "stability" = almost the right answer for almost the right input. (Gave the technical version of this, from the book.)

Often, it is sufficient to prove "backwards stability" = right answer for almost the right input. Showed that, in our example of adding a sequence of numbers, backwards stability seems to work where forwards stability failed. Then more rigorously proved that floating-point summation of _n_ numbers is backwards stable.

**Further reading**: See the further reading from the previous lecture. Trefethen, lectures 14, 15, and 3. See also the Wikipedia article on [asymptotic ("big O") notation](https://en.wikipedia.org/wiki/Big_O_notation); note that for expressions like O(ε) we are looking in the limit of _small_ arguments rather than of large arguments (as in complexity theory), but otherwise the ideas are the same.

### Lecture 4 (Feb 13)

* [notes on the equivalence of norms](notes/norm-equivalence.pdf)

When quantifying errors, a central concept is a norm, and we saw in our proof of backwards stability of summation that the choice of norm seems important. Defined norms (as in lecture 3 of Trefethen): for a vector space V, a norm takes any v∈V and gives you a real number ‖v‖ satisfying three properties:

* Positive definite: ‖v‖≥0, and =0 if and only if v=0
* Scaling: ‖αv‖ = |α|⋅‖v‖ for any scalar α.
* [Triangle inequality](https://en.wikipedia.org/wiki/Triangle_inequality): ‖v+w‖≤‖v‖+‖w‖

There are many norms, for many different vector spaces. Gave examples of norms of column vectors: _Lₚ_ norms (usually _p_ = 1, 2, or ∞) and weighted L₂ norms.  A complete (= continuous, essentially) normed vector space is called a [Banach space](https://en.wikipedia.org/wiki/Banach_space), and these error concepts generalize to f(x) when f and x are in any Banach spaces (including scalars, column vectors, matrices, …though infinite-dimensional Banach spaces are trickier).

Especially important in numerical analysis are functions where the inputs and/or outputs are matrices, and for these cases we need matrix norms. The most important matrix norms are those that are related to matrix operations. Started with the Frobenius norm. Related the Frobenius norm ‖A‖F to the square root of the sum of eigenvalues of A\*A, which are called the _singular values_ σ²; we will do much more on singular values later, but for now noted that they equal the squared eigenvalues of A if A\*\=A (Hermitian). Also defined the induced matrix norm, and bounded it below by the maximum eigenvalue magnitude of A (if A is square). For the L₂ induced norm, related it (without proof for now) to the maximum singular value.  A useful property of the induced norm is ‖AB‖≤‖A‖⋅‖B‖.  Multiplication by a unitary matrix Q (Q\* = Q⁻¹) preserves both the Frobenius and L₂ induced norms.

Equivalence of norms. Described fact that any two norms are equivalent up to a constant bound, and showed that this means that **stability in one norm implies stability in all norms.** Sketched proof (_only skimmed this_): (i) show we can reduce the problem to proving any norm is equivalent to e.g. L₁ on (ii) the unit circle; (iii) show any norm is continuous; and (ii) use a result from real analysis: a continuous function on a closed/bounded (compact) set achieves its maximum and minimum, the [extreme value theorem](http://en.wikipedia.org/wiki/Extreme_value_theorem). See notes handout.

**Further reading:** Trefethen, lecture 3. If you don't immediately recognize that A\*A has nonnegative real eigenvalues (it is positive semidefinite), now is a good time to review your linear algebra; see also Trefethen lecture 24.

### Lecture 5 (Feb 15)

* [pset 1 solutions](psets/pset1sol.pdf) and accompanying [notebook](https://nbviewer.jupyter.org/github/mitmath/18335/blob/master/psets/pset1sol.ipynb)
* [pset 2](psets/pset2.pdf), due at 3pm on Friday March 1.

Relate backwards error to forwards error, and backwards stability to forwards error (or "accuracy" as the book calls it). Show that, in the limit of high precision, the forwards error can be bounded by the backwards error multiplied by a quantity κ, the **relative condition number**. The nice thing about κ is that it involves only exact linear algebra and calculus, and is completely separate from considerations of floating-point roundoff. Showed that, for differentiable functions, κ can be written in terms of the induced norm of the Jacobian matrix.

Calculated condition number for square root, summation, and matrix-vector multiplication, as well as solving Ax=b, similar to the book. Defined the condition number of a matrix: for f(x)=Ax, the condition number is ‖A‖⋅‖x‖/‖Ax‖, which is bounded above by κ(A)=‖A‖⋅‖A⁻¹‖.

Related matrix _L_2 norm to eigenvalues of _B_\=_A_\*_A_. _B_ is obviously Hermitian (_B_\*\=_B_), and with a little more work showed that it is positive semidefinite: _x_\*_B__x_≥0 for any _x_. Reviewed and re-derived properties of eigenvalues and eigenvectors of Hermitian and positive-semidefinite matrices. Hermitian means that the eigenvalues are real, the eigenvectors are orthogonal (or can be chosen orthogonal). Also, a Hermitian matrix must be diagonalizable (I skipped the proof for this; we will prove it later in a more general setting). Positive semidefinite means that the eigenvalues are nonnegative.

Proved that, for a Hermitian matrix B, the **Rayleigh quotient** R(x)=x\*Bx/x\*x is bounded above and below by the largest and smallest eigenvalues of B (the "min–max theorem"). Hence showed that the L2 induced norm of A is the square root of the largest eigenvalue of _B_\=_A_\*_A_. Similarly, showed that the L₂ induced norm of A⁻¹, or more generally the supremum of ‖x‖/‖Ax‖, is equal to the square root of the inverse of the smallest eigenvalue of _A_\*._A_

Understanding norms and condition numbers of matrices therefore reduces to understanding the eigenvalues of _A_\*_A_ (or _A__A_\*). However, looking at it this way is unsatisfactory for several reasons. First, we would like to solve one eigenproblem, not two. Second, working with things like _A_\*_A_ explicitly is often bad numerically, because it squares the condition number \[showed that κ(_A_\*_A_)=κ(_A_)2\] and hence exacerbates roundoff errors. Third, we would really like to get some better understanding of _A_ itself. All of these concerns are addressed by the **singular value decomposition** or **SVD**, which we will derive next time.

**Further reading:** Trefethen, lectures 12, 14, 15, 24.  See any linear-algebra textbook for a review of eigenvalue problems, especially Hermitian/real-symmetric ones.  See also [these notes from 18.06](https://nbviewer.jupyter.org/github/stevengj/1806/blob/fall18/lectures/Conditioning.ipynb).

### Lecture 6 (Feb 19 — Tuesday is an "MIT Monday")

Guest lecture by MIT Instructor Dr. [Chris Rackauckas](http://chrisrackauckas.com/): **Modern Differential Equations Solver Software: Where We Are and Where We're Headed**:

> In this talk we will discuss the current state of software in differential equations and see how the continued advances in computer science and numerical methods are likely to impact our software in the near future. Issues such as efficiency improvements for stiff and non-stiff differential equations will be addressed from a numerical analysis standpoint but backed with recent benchmarking results. Newer mathematical topics like random ordinary differential equations, jump diffusion equations, and adaptivity for stochastic differential equations will be introduced and the successes and limitations in current automatic software solutions will be discussed. We will close with a discussion on how recent computational advancements have been influencing the software implementations, specifically showing the effects of generic typing over abstract algorithms and implicit parallelism.

**Further reading:** See Chris's [survey of ODE software](http://www.stochasticlifestyle.com/comparison-differential-equation-solver-suites-matlab-r-julia-python-c-fortran/), his [DifferentialEquations.jl package](https://github.com/JuliaDiffEq/DifferentialEquations.jl) for Julia, and his [video introduction to DifferentialEquations.jl](http://www.stochasticlifestyle.com/intro-solving-differential-equations-julia/).

### Lecture 7 (Feb 20)

Guest lecture by Prof. Alan Edelman: the SVD, relationship to L₂ norms and condition numbers, applications (e.g. principal components analysis).

**Further reading:** Trefethen, lectures 4, 5.

### Lecture 8 (Feb 22)

* [Many viewpoints on linear regression notebook](https://github.com/alanedelman/18.337_2017/blob/master/lectures/Lecture04_0918%20RegressionManyWays/RegressionManyWays.ipynb).

Guest lecture by Prof. Alan Edelman: Generalized SVD (GSVD).  Least-square problems (via QR or SVD) and different viewpoints on linear regression: linear algebra, optimization, statistics, machine learning.

**Further reading:** Trefethen, lectures 7, 11.  [The GSVD: Where are the ellipses?](https://arxiv.org/abs/1901.00485).

### Lecture 9 (Feb 25)

Discussed solution of normal equations. Discussed condition number of solving normal equations directly, and noted that it squares the condition number—not a good idea if we can avoid it.

Introduced the alternative of QR factorization (finding an orthonormal basis for the column space of the matrix). Explained why, if we can do it accurately, this will give a good way to solve least-squares problems.

Gave the simple, but unstable, construction of the Gram-Schmidt algorithm, to find a QR factorization.  Analyzed its O(mn²) complexity (specifically, 2mn² flops), and commented that the "same" projection qqᵀa requires O(m²) operations if you perform it as (qqᵀ)a but O(m) operations if you perform it as q(qᵀa) — matrix operations are associative (but not commutative), but where you put the parentheses can make a big difference in performance!

Discussed loss of orthogonality in classical Gram-Schmidt, using a simple example, especially in the case where the matrix has nearly dependent columns to begin with.

**Further reading:** Trefethen, lectures 7, 8, 18, 19. Per Persson's [2006 18.335 Gram-Schmidt notes](notes/lec5.pdf) are also helpful, as is the [Wikipedia Gram-Schmidt article](https://en.wikipedia.org/wiki/Gram%E2%80%93Schmidt_process).

### Lecture 10 (Feb 27)

* [Gram-Schmidt IJulia notebook](https://nbviewer.jupyter.org/github/mitmath/18335/blob/master/notes/Gram-Schmidt.ipynb)
* Per Persson's [2006 18.335 Householder notes](notes/lec6.pdf) ([handout](notes/lec6handout6pp.pdf))

Discussed loss of orthogonality in classical Gram-Schmidt, using a simple example, especially in the case where the matrix has nearly dependent columns to begin with. Showed modified Gram-Schmidt and argued how it (mostly) fixes the problem. Numerical examples (see notebook).

Re-interpret Gram-Schmidt in matrix form as Q = AR1R2..., i.e. as multiplying A on the right by a sequence of upper-triangular matrices to get Q. The problem is that these matrices R may be very badly conditioned, leading to an inaccurate Q and loss of orthogonality.

Instead of multiplying A on the right by R's to get Q, however, we can instead multiply A on the left by Q's to get R. This leads us to the Householder QR algorithm.  Introduced Householder QR, emphasized the inherent stability properties of multiplying by a sequence of unitary matrices (as shown in pset 2). Show how we can convert a matrix to upper-triangular form (superficially similar to Gaussian elimination) via unitary Householder reflectors.

**Further reading:** Trefethen, lectures 7, 8, 16, 18, 19. It turns out that modified GS is backwards stable in the sense that the product QR is close to A, i.e. the function f(A) = Q\*R is backwards stable in MGS; this is why solving systems with Q,R (appropriately used as discussed in Trefethen lecture 19) is an accurate approximation to solving them with A. For a review of the literature on backwards-stability proofs of MGS, see e.g. [this 2006 paper by Paige et al.](https://epubs.siam.org/doi/10.1137/050630416) \[_SIAM J. Matrix Anal. Appl._ **28**, pp. 264-284\].

### Lecture 11 (Mar 1)

* performance experiments with matrix multiplication ([one-page](notes/matmuls-handout.pdf) or [full-size](notes/matmuls.pdf) versions)
* [ideal-cache terminology](notes/ideal-cache.pdf)
* pset 2 solutions: coming soon
* pset 3: coming soon

Finished Householder QR derivation, including the detail that one has a choice of Householder reflectors...we choose the sign to avoid taking differences of nearly-equal vectors. Gave flop count, showed that we don't need to explicitly compute Q if we store the Householder reflector vectors.

Counting arithmetic operation counts is no longer enough. Illustrate this with some performance experiments on a much simpler problem, matrix multiplication (see handouts). This leads us to analyze memory-access efficiency and caches and points the way to restructuring many algorithms.

Outline of the memory hierarchy: CPU, registers, L1/L2 cache, main memory, and presented simple 2-level ideal-cache model that we can analyze to get the basic ideas.

Analyzed cache complexity of simple row-column matrix multiply, showed that it asymptotically gets no benefit from the cache. Presented blocked algorithm, and showed that it achieves optimal Θ(n³/√Z) cache complexity.

Discussed some practical difficulties of the blocked matrix multiplication: algorithm depends on cache-size _Z_, and multi-level memories require multi-level blocking. Discussed how these ideas are applied to the design of modern linear-algebra libraries (LAPACK) by building them out of block operations (performed by an optimized BLAS).

**Further reading:** Wikipedia has a reasonable [introduction to memory locality](http://en.wikipedia.org/wiki/Locality_of_reference) that you might find useful. The optimized matrix multiplication shown on the handouts is called ATLAS, and you can find out more about it on the [ATLAS web page](http://math-atlas.sourceforge.net/). [Cache-oblivious algorithms](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.34.7911), describing ideal cache model and analysis for various algorithms, by Frigo, Leiserson, Prokop, and Ramachandran (1999). [Notes on the switch from LINPACK to LAPACK/BLAS in Matlab](http://www.mathworks.com/company/newsletters/news_notes/clevescorner/winter2000.cleve.html). The MIT course [6.172](http://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-172-performance-engineering-of-software-systems-fall-2010/index.htm) has two lecture videos ([first](http://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-172-performance-engineering-of-software-systems-fall-2010/video-lectures/lecture-8-cache-efficient-algorithms) and [second](http://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-172-performance-engineering-of-software-systems-fall-2010/video-lectures/lecture-9-cache-efficient-algorithms-ii)) on cache-efficient algorithms, including a discussion of matrix multiplication.