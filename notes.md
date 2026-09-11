# The Second Heavy-Ball Riddle

<p class="subtitle">Convergence beyond the prescribed Lyapunov family</p>

<p class="byline">Research notes · September 9, 2026 · Revised September 10, 2026</p>

## Abstract

What happens when an optimization method admits neither a familiar Lyapunov certificate nor a periodic counterexample? The second Heavy-Ball riddle turns this question into a concrete problem about smooth strongly convex functions.

We exhibit the exact normalized parameters

$$
(q,a,b)=\left(\frac1{100},\frac{113}{50},\frac35\right)
$$

at which the prescribed two-point linear/quadratic Lyapunov family fails, yet no nonconstant finite cycle exists in any finite dimension. More strongly, throughout an explicit parameter box around this point, every trajectory on every admissible fixed objective converges globally at a uniform linear rate.

The mechanism is instructive. **Two consecutive observations can support a locally expanding step. Constraints linking observations farther apart on the same objective prevent that expansion from persisting indefinitely.** These longer-range constraints certify convergence even when the prescribed two-point certificates cannot.

The exposition develops the geometry first and then supplies the full analytical argument. Long arithmetic tables are expandable in the HTML and included in full in the PDF. Original figures, reproducible checks, and the underlying proof and review records accompany the notes.

## 1. The question behind the gap

With a fixed step size $\gamma$ and momentum $\beta$, Heavy-Ball updates

$$
x_{t+1}=x_t-\gamma\nabla f(x_t)+\beta(x_t-x_{t-1}).
$$

To study an algorithm over a whole function class, one often looks for either a decreasing energy or a counterexample that cycles forever. The two approaches provide different kinds of evidence: a common energy can establish a guarantee for every objective, while one cycle refutes such a guarantee.

Goujaud, Taylor, and Dieuleveut posed two riddles about Heavy-Ball. Their second asks whether there are parameters admitting neither their Lyapunov certificates nor a cycle, and what the dynamics then do. The certificate template and its quantifiers are essential; see [Section 3 of the original paper](https://arxiv.org/html/2502.19916v1#S3).

The structure of these notes follows the [ODI exposition of the first riddle](https://odi.inf.ethz.ch/blog/heavy-ball-one-dimension/): problem, precise result, construction, proof, and verification. That post studies one-dimensional cycles and non-acceleration. Here we study convergence beyond a specified certificate family.

### 1.1 Function class and normalization

For $0<\mu<L$, set

$$
q=\frac\mu L,\qquad a=L\gamma,\qquad b=\beta.
$$

Divide the objective by the original smoothness constant $L$, and continue to denote it by $f$. We write $\mathcal F_{q,1}(\mathbb R^d)$ for globally differentiable functions satisfying, for all $x,y\in\mathbb R^d$,

$$
f(y)\ge f(x)+\langle\nabla f(x),y-x\rangle
       +\frac q2\|y-x\|^2,
\qquad
\|\nabla f(y)-\nabla f(x)\|\le\|y-x\|.
$$

Strong convexity and continuity imply existence of a unique minimizer $x_*$; write $f_*=f(x_*)$. The normalized algorithm is

$$
x_{t+1}=x_t-a\nabla f(x_t)+b(x_t-x_{t-1}).
\tag{HB}
$$

The dimension is any finite $d\ge1$, and the initial pair $(x_{-1},x_0)$ is arbitrary. The objective and parameters remain fixed throughout the trajectory. We assume neither Hessian continuity nor bounded iterates, and do not restrict initialization to $x_{-1}=x_0$.

The parameter domain is

$$
\mathcal D=\{(q,a,b):0<q<1,\ 0\le b<1,\ 0<a<2(1+b)\}.
$$

This already excludes elementary instability on scalar quadratics. For $f(x)=\lambda x^2/2$, the characteristic polynomial is

$$
r^2-(1+b-a\lambda)r+b.
$$

In the nonnegative-momentum regime, its roots are inside the unit disk precisely when $b<1$ and $0<a\lambda<2(1+b)$. Stability on quadratics, however, does not settle stability over the larger function class.

### 1.2 What exactly is a certificate?

For a state $(u,v)$, define the four-vector record

$$
s_f(u,v)=\big(u-x_*,\nabla f(u),v-x_*,\nabla f(v)\big).
$$

The prescribed certificate has the form

$$
\begin{aligned}
V_f(u,v)={}&c_0(f(v)-f_*)+c_1(f(u)-f_*)\\
&+\sum_{i,j=1}^4 Q_{ij}\langle s_i,s_j\rangle,
\qquad Q\in\mathbb S^4.
\end{aligned}
\tag{L-form}
$$

The coefficients $c_0,c_1,Q$ may depend on the parameters, but the same coefficients must work for every admissible objective, dimension, and initial pair. The matrix $Q$ need not itself be positive semidefinite.

If $w=(1+b)v-bu-a\nabla f(v)$, the requirements are

$$
f(w)-f_*\le V_f(v,w)\le V_f(u,v).
\tag{L}
$$

The first inequality makes the energy control an objective gap; the second makes it nonincreasing. Denote existence of such coefficients by $\mathsf L(q,a,b)$. This is the $\rho=1$ test, which by itself does not assert asymptotic convergence. Automated searches within prescribed state templates are developed in [Taylor–Van Scoy–Lessard, 2018](https://proceedings.mlr.press/v80/taylor18a.html).

Let $\mathsf C(q,a,b)$ mean that some finite dimension, some fixed $f\in\mathcal F_{q,1}$, and some integer $K\ge2$ admit a nonconstant $K$-periodic HB trajectory. All finite periods and all orbit shapes are included.

The existence question is

$$
\exists(q,a,b)\in\mathcal D:
\qquad\neg\mathsf L(q,a,b)\ \land\ \neg\mathsf C(q,a,b).
\tag{E}
$$

One rigorous witness settles (E). Classifying that witness's infinite-time dynamics is a further mathematical question.

## 2. Main results

<div class="theorem">

**Theorem A — An exact separation witness.** At

$$
(q_*,a_*,b_*)=\left(\frac1{100},\frac{113}{50},\frac35\right),
$$

both $\neg\mathsf L(q_*,a_*,b_*)$ and $\neg\mathsf C(q_*,a_*,b_*)$ hold. The first statement excludes every coefficient choice in (L-form). The second excludes every nonconstant finite cycle, in every finite dimension, over the entire admissible function class.

</div>

<div class="theorem">

**Theorem B — Uniform global linear convergence.** Define

$$
B=\left\{(q,a,b):
\begin{aligned}
 |q-q_*|&\le10^{-5},\\
 |a-a_*|&\le10^{-5},\\
 |b-b_*|&\le10^{-5}
\end{aligned}\right\}.
$$

For every $(q,a,b)\in B$, every finite $d\ge1$, every $f\in\mathcal F_{q,1}(\mathbb R^d)$, every initial pair, and every integer $t\ge0$,

$$
\begin{aligned}
\|x_t-x_*\|&\le10^7(1-10^{-14})^{t/2}\\[-2pt]
&\qquad\cdot\sqrt{\|x_{-1}-x_*\|^2+\|x_0-x_*\|^2}.
\end{aligned}
\tag{G}
$$

</div>

The constants are deliberately conservative. They provide a fully explicit uniform guarantee, rather than a sharp worst-case rate. This is not an acceleration claim as the condition number varies.

Theorem B also rules out nonconstant finite cycles throughout $B$: a convergent periodic sequence must be constant. We nevertheless prove the cycle part of Theorem A independently. Its shorter argument makes the role of longer-range interpolation constraints transparent.

The proof has three stages: build four samples that defeat every prescribed certificate; turn all possible finite periods into a single polynomial positivity problem; and extend the same structure to infinite time without assuming convergence along the way.

<div class="proof-guide">

**Reading the proof.** The finite construction in Sections 3–4 proves impossibility of a common certificate. Section 5 proves cycle exclusion independently. For convergence, Section 6.2 first derives an inequality for square-summable test sequences; Section 6.3 supplies its strict frequency margin; Section 6.4 then proves that the actual trajectory is square summable. Sections 6.5–6.6 turn that qualitative statement into the explicit estimate (G). In particular, the argument never deduces convergence merely from the absence of cycles.

</div>

## 3. A tool: realizing finite data by a global function

Suppose we prescribe positions, gradients, and values $(x_i,g_i,F_i)$. They cannot be chosen independently if they are to belong to one smooth strongly convex objective.

Define the interpolation residual

$$
\begin{aligned}
I_{ij}={}&F_i-F_j-\langle g_j,x_i-x_j\rangle\\
&-\frac{\|g_i-g_j\|^2+q\|x_i-x_j\|^2
-2q\langle g_i-g_j,x_i-x_j\rangle}{2(1-q)}.
\end{aligned}
\tag{I}
$$

The finite dataset is realizable by a function in $\mathcal F_{q,1}$ if and only if $I_{ij}\ge0$ for every ordered pair. This is the normalized [smooth strongly convex interpolation theorem](https://arxiv.org/abs/1502.05666v6). We include the argument needed here, so global admissibility of our construction is explicit.

### 3.1 Necessity by subtracting a quadratic

**Lemma 3.1 (interpolation necessity).** Every finite collection of samples from a function in $\mathcal F_{q,1}$ satisfies (I). The following proof reduces the claim to the descent estimate for a convex smooth function.

Set

$$
\ell=1-q,\qquad
\psi(x)=f(x)-\frac q2\|x\|^2,\qquad p(x)=\nabla\psi(x).
$$

Strong convexity makes $\psi$ convex. Subtracting the quadratic from the smooth upper bound for $f$ gives

$$
\psi(y)\le\psi(x)+\langle p(x),y-x\rangle
                 +\frac\ell2\|y-x\|^2.
$$

Fix $x_j$ and consider $\varphi(x)=\psi(x)-\langle p(x_j),x\rangle$. Its gradient vanishes at $x_j$, so convexity makes $x_j$ a global minimizer. A gradient step of length $1/\ell$ from $x_i$ gives

$$
\begin{aligned}
\varphi(x_j)
&\le\varphi\!\left(x_i-\frac{\nabla\varphi(x_i)}\ell\right)\\
&\le\varphi(x_i)-\frac1{2\ell}\|p(x_i)-p(x_j)\|^2.
\end{aligned}
$$

Rearranging,

$$
\psi(x_i)-\psi(x_j)
\ge\langle p(x_j),x_i-x_j\rangle
  +\frac1{2\ell}\|p(x_i)-p(x_j)\|^2.
\tag{CI}
$$

Substitute $p_i=g_i-qx_i$ and expand to obtain $I_{ij}\ge0$. No Hessian assumption is used. Adding (CI) to its reversed version yields

$$
\|p_i-p_j\|^2\le\ell\langle p_i-p_j,x_i-x_j\rangle.
\tag{Co}
$$

This is the cocoercivity inequality. Cauchy–Schwarz then makes $p$ $\ell$-Lipschitz, a fact used again in the convergence proof.

### 3.2 Sufficiency through an explicit conjugate

**Lemma 3.2 (global realization).** Every nonempty finite dataset satisfying (I) is realized by the globally defined function (Interp). This includes the starred minimizer sample; no extension outside a bounded plotting window is needed.

Assume all $I_{ij}\ge0$, and write

$$
p_i=g_i-qx_i,\qquad h_i=F_i-\frac q2\|x_i\|^2.
$$

Construct

$$
\begin{aligned}
H(p)&=\max_i\left\{\langle p,x_i\rangle-h_i
                     +\frac{\|p-p_i\|^2}{2\ell}\right\},\\
f(x)&=H^*(x)+\frac q2\|x\|^2,
\end{aligned}
\tag{Interp}
$$

where $H^*(x)=\sup_p\{\langle x,p\rangle-H(p)\}$ is the convex conjugate. Geometrically, we place quadratic surfaces of the same curvature in gradient space, take their maximum, and return to the original space by conjugacy.

Let $H_i$ be the $i$th expression inside the maximum. Direct calculation gives

$$
H_i(p_i)-H_j(p_i)=I_{ji}\ge0.
$$

Thus the $i$th piece is active at $p_i$, and $\nabla H_i(p_i)=x_i$. It follows that $x_i\in\partial H(p_i)$, even if several pieces tie. Conjugacy implies

$$
H^*(x_i)=h_i,\qquad\nabla H^*(x_i)=p_i,
$$

so $f(x_i)=F_i$ and $\nabla f(x_i)=g_i$.

Global smoothness follows directly. Each $H_i(p)-\|p\|^2/(2\ell)$ is affine, so $H$ is $1/\ell$-strongly convex. For every $x$, the coercive function $H(p)-\langle x,p\rangle$ has a unique minimizer $P(x)$. Adding its two strong subgradient inequalities gives

$$
\langle x-y,P(x)-P(y)\rangle
\ge\frac1\ell\|P(x)-P(y)\|^2.
$$

Hence $P$ is $\ell$-Lipschitz. The two maximizing inequalities defining the conjugate give

$$
\begin{aligned}
0&\le H^*(x+v)-H^*(x)-\langle P(x),v\rangle\\
 &\le\langle P(x+v)-P(x),v\rangle\le\ell\|v\|^2.
\end{aligned}
$$

Therefore $H^*$ is globally differentiable with gradient $P$. The function in (Interp) is $q$-strongly convex and has gradient Lipschitz constant at most $\ell+q=1$. Our finite data come from a globally admissible objective.

## 4. No certificate: one step defeats every coefficient

Fix the central parameters. Identify $\mathbb R^2$ with $\mathbb C$, with real inner product $\langle u,v\rangle=\operatorname{Re}(\overline u v)$. Set

$$
z=\frac{23+199\mathrm i}{200},\qquad
R=|z|^2=\frac{4013}{4000}>1,\qquad F=\frac{41}{100},
$$

$$
\eta=\frac{1+b-z-b/z}{a}
      =\frac{1136661-320987\mathrm i}{1813876}.
$$

Use a starred sample for the minimizer and three other samples:

$$
\begin{gathered}
x_*=0,\quad x_0=z^{-1},\quad x_1=1,\quad x_2=z,\\
g_j=\eta x_j,\qquad F_j=F|x_j|^2.
\end{gathered}
\tag{Data}
$$

At the starred point, $g_*=0$ and $F_*=0$. The three nonzero samples are related by multiplication by $z$: the same rotation and a dilation by $\sqrt R$.

<figure>
<img src="assets/similarity.svg" alt="The complex samples z inverse, 1, and z, related by a common expanding similarity.">
<figcaption>Figure 1. (a) Three samples related by a rotation and dilation; the dashed circle has radius one. The dilation is only about 0.16%, so its magnitude is specified exactly. (b) The same successor decomposed into momentum (rose), negative gradient (blue), and net update (black), following the vector convention of Figure 7 in Goujaud–Taylor–Dieuleveut. All coordinates are computed from our witness. Only the transition from (u,v) to (v,w) is asserted.</figcaption>
</figure>

### 4.1 Are the samples realizable?

Substitution into (I) gives twelve strictly positive off-diagonal residuals and zero diagonal residuals. The smallest is

$$
\min_{i\ne j}I_{ij}
=\frac{1775394252563}{1017888963106950}>0.
$$

Section 3 constructs one fixed, globally admissible two-dimensional function realizing them. The starred sample makes its unique minimizer and minimum zero.

<details>
<summary>Arithmetic detail: all twelve interpolation residuals</summary>

The indices $(*,0,1,2)$ refer to $(0,z^{-1},1,z)$. All ordered pairs are needed: adjacent pairs alone would not establish global realizability.

| $(i,j)$ | $I_{ij}$ |
|---|---|
| $(*,0)$ | $76785548080/20357779262139$ |
| $(*,1)$ | $959819351/253647885150$ |
| $(*,2)$ | $959819351/252826200000$ |
| $(0,*)$ | $4000260206920/20357779262139$ |
| $(0,1)$ | $1775394252563/1017888963106950$ |
| $(0,2)$ | $1447646143705644319/4071555852427800000$ |
| $(1,*)$ | $100006505173/507295770300$ |
| $(1,0)$ | $719411350000249/2035777926213900$ |
| $(1,2)$ | $1775394252563/1014591540600000$ |
| $(2,*)$ | $100006505173/505652400000$ |
| $(2,0)$ | $3562928495857226237/8143111704855600000$ |
| $(2,1)$ | $719411350000249/2029183081200000$ |

The [rational checker](checks/verify_recovery_similarity.py) recomputes the table and all conjugate-piece activity identities.

</details>

### 4.2 Does the step obey Heavy-Ball?

Set $u=z^{-1}$, $v=1$, and $w=z$. The definition of $\eta$ gives exactly

$$
(1+b)v-bu-a\nabla f(v)=1+b-b/z-a\eta=z=w.
$$

This is a legal HB transition. Arbitrary initialization allows us to start from $(u,v)$.

### 4.3 Why do all coefficients fail at once?

The four state features satisfy the componentwise identity

$$
s_f(v,w)=z\,s_f(u,v).
$$

Multiplication by the same complex number multiplies every real inner product by $R$. Both sampled function values also multiply by $R$. Consequently, for every choice of $c_0,c_1,Q$,

$$
V_f(v,w)=R\,V_f(u,v).
\tag{Scale}
$$

If (L) held, monotonicity would imply $(R-1)V_f(u,v)\le0$, hence $V_f(u,v)\le0$. But objective-gap domination would give

$$
0<FR=f(w)-f_*
\le V_f(v,w)=R V_f(u,v)\le0,
$$

a contradiction. This proves $\neg\mathsf L(q_*,a_*,b_*)$.

The argument is an exact obstruction to the whole family; it does not rely on a failed numerical SDP. Nor does it identify the global gradient with $x\mapsto\eta x$. That relation is imposed only at the finite samples. The global objective is the conjugate interpolant.

## 5. No cycles: a single inequality covers every period

The certificate obstruction used only a short segment. To exclude cycles, we instead exploit the fact that *every* pair of observations on one objective satisfies interpolation.

### 5.1 Sum interpolation around a hypothetical cycle

Suppose a $K$-periodic trajectory $y_i\in\mathbb R^d$ exists, with $g_i=\nabla f(y_i)$. Read indices modulo $K$. For any signed lag $k$, apply $I_{i+k,i}\ge0$ and sum over $i$. Function values cancel, leaving

$$
\begin{aligned}
\sum_i\Bigg[&\langle g_i,y_{i+k}-y_i\rangle\\
&+\frac{\|g_{i+k}-g_i\|^2+q\|y_{i+k}-y_i\|^2
-2q\langle g_{i+k}-g_i,y_{i+k}-y_i\rangle}{2(1-q)}
\Bigg]\le0.
\end{aligned}
\tag{Lag}
$$

The lag may be negative or exceed the period. The inequality remains valid, including when some shifted indices coincide. Crucially, we can add these inequalities with nonnegative weights.

### 5.2 Fourier coordinates separate the oscillations

**Why Fourier coordinates?** On a periodic sequence, shifting every index by one is a linear operation whose eigenvectors are discrete oscillations. The HB recurrence and every lag difference use only such shifts. The same change of coordinates therefore diagonalizes all of them, reducing a vector inequality over a whole orbit to one real scalar coefficient for each frequency.

Use the unitary discrete Fourier transform

$$
\widehat y_j=\frac1{\sqrt K}\sum_{i=0}^{K-1}y_i e^{-2\pi\mathrm i ji/K},
\qquad \theta_j=\frac{2\pi j}K.
$$

The recurrence implies

$$
a\widehat g_j=
\big(1+b-e^{\mathrm i\theta_j}-be^{-\mathrm i\theta_j}\big)\widehat y_j.
$$

Indeed, changing index in the finite sum gives $\widehat{y_{i+k}}_j=e^{\mathrm i k\theta_j}\widehat y_j$. Separating the real and imaginary parts gives

$$
\widehat g_j=\mathcal H(\theta_j)\widehat y_j,
\qquad \mathcal H(\theta)=U-\mathrm i V,
$$

where

$$
U=\frac{(1+b)(1-\cos\theta)}a,
\qquad V=\frac{(1-b)\sin\theta}a.
$$

Parseval's identity turns the left side of (Lag) into

$$
\sum_{j=0}^{K-1}\|\widehat y_j\|^2\tau_k(\theta_j),
$$

with

$$
\tau_k(\theta)=
\frac{U^2+V^2-(1+q)U+q}{1-q}(1-\cos k\theta)
-V\sin k\theta.
\tag{Symbol}
$$

Here the squared Fourier norm is the sum of squared complex moduli over the $d$ coordinates. Thus the calculation includes arbitrary vector-valued, multimode cycles; it does not assume a regular polygon or a single oscillatory mode.

To see the sign in (Symbol), the first inner product contributes

$$
\operatorname{Re}\big((U+\mathrm i V)(e^{\mathrm i k\theta}-1)\big)
=-U(1-\cos k\theta)-V\sin k\theta.
$$

The squared differences contribute

$$
\frac{U^2+V^2+q-2qU}{1-q}(1-\cos k\theta),
$$

which gives the stated expression when added.

### 5.3 Two lags suffice

Write $c=\cos\theta$ and define

$$
\begin{aligned}
J(c)={}&2(1-c)(1+b^2-2bc)\\
&-a(1+q)(1+b)(1-c)+a^2q,\\
A={}&a(1-q)(1-b),\\
S(c)={}&1+\frac{32}{25}c^2(1+c),\\
K(c)={}&(1+c)\left(1+\frac{16}{25}c-\frac{32}{25}c^3\right),\\
W(c)={}&S(c)J(c)+K(c)A.
\end{aligned}
\tag{W}
$$

Using $\cos4\theta=8c^4-8c^2+1$ and $\sin4\theta=(8c^3-4c)\sin\theta$, substitution into (Symbol) gives

$$
\tau_{-1}(\theta)+\frac4{25}\tau_4(\theta)
=\frac{1-c}{a^2(1-q)}W(c).
\tag{Two-lags}
$$

For clarity, the factors arise from

$$
\begin{aligned}
(1-c)+\frac4{25}(1-\cos4\theta)&=(1-c)S(c),\\
(1+c)\left(1-\frac4{25}(8c^3-4c)\right)&=K(c).
\end{aligned}
$$

At our central parameters, expansion gives $W_*(c)=P(c)/6250000$, where

$$
\begin{aligned}
P(c)={}&19200000c^5+297600c^4-25951072c^3\\
&+11531168c^2-660c+86725.
\end{aligned}
\tag{P}
$$

It remains to prove this polynomial strictly positive on $[-1,1]$.

### 5.4 An exact positivity certificate

On each interval $[l,r]$, express the polynomial in the Bernstein basis:

$$
P(l+(r-l)t)=\sum_{j=0}^5 B_j\binom5j t^j(1-t)^{5-j},
\qquad 0\le t\le1.
$$

Each basis function is nonnegative and their sum is one. Hence the polynomial is at least the smallest $B_j$. This reduces positivity on an entire interval to six exact numbers.

The conversion can also be checked by hand. If
$P(l+(r-l)t)=\sum_{m=0}^5 d_m t^m$, then

$$
B_j=\sum_{m=0}^j d_m\frac{\binom jm}{\binom5m},
\qquad j=0,\ldots,5.
$$

This follows by substituting
$t^m=\sum_{j=m}^5\frac{\binom jm}{\binom5m}\binom5j t^j(1-t)^{5-j}$
and using the binomial theorem. Thus each row below is an exact polynomial identity followed by a convex-combination bound, rather than a test of a few sampled values.

The four intervals $[-1,0]$, $[0,1/2]$, $[1/2,3/4]$, and $[3/4,1]$ have strictly positive coefficient rows. The smallest coefficient across all rows is $557731/10$. Therefore

$$
P(c)\ge\frac{557731}{10}>0,
\qquad
W_*(c)\ge\frac{557731}{62500000}
\quad(-1\le c\le1).
\tag{Positive}
$$

<details>
<summary>Arithmetic detail: the complete Bernstein certificate</summary>

Each row lists coefficient numerators, followed by a common positive denominator. The table is split into two parts to remain legible in print.

| Interval | $B_0$ numerator | $B_1$ numerator | $B_2$ numerator | Denominator |
|---|---:|---:|---:|---:|
| $[-1,0]$ | 93336125 | 87229513 | 30707893 | 5 |
| $[0,1/2]$ | 433625 | 433295 | 1874361 | 5 |
| $[1/2,3/4]$ | 6878060 | 5094064 | 2941438 | 20 |
| $[3/4,1]$ | 5496320 | 9877178 | 18651243 | 20 |

| Interval | $B_3$ numerator | $B_4$ numerator | $B_5$ numerator | Denominator |
|---|---:|---:|---:|---:|
| $[-1,0]$ | 6200529 | 434285 | 433625 | 5 |
| $[0,1/2]$ | 3134881 | 2611513 | 1719515 | 5 |
| $[1/2,3/4]$ | 1127811 | 1115462 | 5496320 | 20 |
| $[3/4,1]$ | 34410444 | 60876360 | 103275220 | 20 |

These rows are checked by exact expansion in [verify_cycle_certificate.py](checks/verify_cycle_certificate.py). Both the polynomial identity and the signs are verified using rational arithmetic.

</details>

<figure>
<img src="assets/frequency_margin.svg" alt="The positive polynomial margin over minus one to one, with the exact Bernstein lower bound and a magnified small-margin region.">
<figcaption>Figure 2. The curve illustrates the polynomial's shape; the finite Bernstein certificate proves positivity over every frequency. Vertical lines mark the four certified intervals. Numerical sampling is not used to infer the sign.</figcaption>
</figure>

Now add (Lag) at lags $-1$ and $4$ with weights $1$ and $4/25$. The result is nonpositive. Yet (Two-lags) and (Positive) make each nonzero Fourier mode contribute a strictly positive multiple of $\|\widehat y_j\|^2$. The zero mode contributes zero. All nonzero modes must therefore vanish, making the trajectory constant. This proves $\neg\mathsf C(q_*,a_*,b_*)$ and completes Theorem A.

More explicitly, for $j=1,\ldots,K-1$ we have $1-\cos(2\pi j/K)>0$, and hence

$$
0\ge\sum_{j=1}^{K-1}
\frac{(1-\cos\theta_j)W_*(\cos\theta_j)}{a^2(1-q)}
\|\widehat y_j\|^2\ge0.
$$

Every summand is nonnegative and its coefficient is strictly positive. Thus $\widehat y_j=0$ for every $j\ne0$. The inverse transform gives $y_i=\widehat y_0/\sqrt K$, independently of $i$. Substituting this constant sequence into HB also gives $a\nabla f(y_i)=0$, so its value must be $x_*$. This covers periods two, three, and four as well: repeated or zero lag differences modulo the period are already included in the same identity.

## 6. Convergence: from finite cycles to infinite time

Absence of finite cycles does not by itself force convergence. We now prove Theorem B directly. The delicate point is that an infinite sum cannot be applied to the physical trajectory until its summability has been established.

### 6.1 Separate the linear dynamics from the gradient

Translate the minimizer and minimum to zero. Write

$$
\ell=1-q,\qquad\psi(x)=f(x)-\frac q2\|x\|^2,
\qquad D(x)=\nabla\psi(x).
$$

Section 3 gives convexity of $\psi$, $D(0)=0$, and $\|D(x)-D(y)\|\le\ell\|x-y\|$. The recurrence is

$$
x_{t+1}=(1+b-aq)x_t-bx_{t-1}-aD(x_t).
$$

Its stable linear input/output operator has transfer function

$$
G(z)=\frac{-az}{z^2-(1+b-aq)z+b}.
\tag{Plant}
$$

Our Fourier convention is $\widehat x(\theta)=\sum_t x_t e^{-\mathrm i t\theta}$, so $z^k$ means advance by $k$ time steps. The operator $G$ is **strictly causal**: its output at time $t$ depends only on inputs at earlier times. Let $e$ be the homogeneous response carrying the arbitrary initial pair. Variation of constants gives

$$
x=e+GD(x).
\tag{Loop}
$$

Stability follows from $b<1$ and $0<aq<2(1+b)$ throughout $B$. Quantitative bounds for the poles and free response will be supplied in Section 6.5.

### 6.2 Longer-range interpolation gives a supply inequality

**Lemma 6.1 (the supply inequality).** For every $\tau\in[0,1]$ and every square-summable test sequence, (Supply) holds. At this stage the sequence is a test input, not a trajectory whose convergence is being assumed.

For any $\tau\in[0,1]$, the convex function $F=\tau\psi$ satisfies the same upper smoothness inequality with constant $\ell$. Its gradient is $p=\tau D(x)$. The corresponding objective $q\|x\|^2/2+\tau\psi(x)$ remains in $\mathcal F_{q,1}$. Thus scaling the nonlinearity preserves admissibility.

For now, take any sequence $x\in\ell_2(\mathbb N;\mathbb R^d)$ and extend it by zero to negative times. Define, on all integers,

$$
p_t=\tau D(x_t),\qquad s_t=\ell x_t-p_t,
\qquad \Phi_t=\ell F(x_t)-\frac12\|p_t\|^2.
$$

Here $\ell_2$ means that the sum of squared norms is finite. Rearranging (CI) gives

$$
\Phi_i-\Phi_j\ge\langle p_j,s_i-s_j\rangle.
$$

Since $0\le F(x)\le\ell\|x\|^2/2$, the sequence $\Phi$ is absolutely summable, while $p,s$ are square summable. Summing with $(i,j)=(t+k,t)$ and shifting indices is therefore legitimate:

$$
\sum_{t\in\mathbb Z}\langle p_t,s_t-s_{t+k}\rangle\ge0
\qquad(k\in\mathbb Z).
$$

Here are the estimates behind that passage. Lipschitz continuity and $p(0)=0$ give $\|p_t\|\le\ell\|x_t\|$ and $\|s_t\|\le2\ell\|x_t\|$, while

$$
|\Phi_t|\le\ell F(x_t)+\tfrac12\|p_t\|^2
\le\ell^2\|x_t\|^2.
$$

Consequently $\sum_t|\Phi_t|<\infty$ and
$\sum_t|\langle p_t,s_{t+k}\rangle|\le\|p\|_2\|s\|_2<\infty$.
Absolute convergence permits the reindexing
$\sum_t\Phi_{t+k}=\sum_t\Phi_t$ for either sign of $k$. This is why the potential differences cancel with no boundary remainder.

Cocoercivity against zero also gives $\langle p_t,s_t\rangle\ge0$. Take the same lags as before, add a small positive constant, and define

$$
M(z)=\varepsilon+(1-z^{-1})+\frac4{25}(1-z^4),
\qquad\varepsilon=10^{-5}.
\tag{Multiplier}
$$

Then

$$
\langle p,M(\ell x-p)\rangle\ge0,
\qquad p=\tau D(x),\quad x\in\ell_2.
\tag{Supply}
$$

The inner product is the sum over all integer times. Its terms are absolutely summable by Cauchy–Schwarz. In particular, the advanced lag $z^4$ does not introduce an ignored terminal term.

This is a finite-lag, noncausal multiplier of the type studied in [Zhang–Seiler–Carrasco, 2019](https://arxiv.org/abs/1902.09473). The inequality itself has just been proved from interpolation. We will also prove the stability step directly, rather than importing an external stability theorem.

### 6.3 A strict frequency margin on the whole box

We first extend (Positive) from the center to every point of $B$. All line segments from the center to the box lie inside

$$
\frac{99}{10000}<q<\frac{11}{1000},\quad
\frac94<a<\frac{23}{10},\quad
\frac{59}{100}<b<\frac{61}{100}.
\tag{Ranges}
$$

For $|c|\le1$, direct differentiation of (W) gives

$$
\begin{gathered}
|J_q|<13,\quad |J_a|<4,\quad |J_b|<18,\\
|A_q|<1,\quad |A_a|<\tfrac12,\quad |A_b|<\tfrac52,
\qquad |S|<4,\quad |K|<6.
\end{gathered}
$$

Indeed, valid bounds for the first row are respectively

$$
\begin{aligned}
|J_q|&\le2a(1+b)+a^2,\\
|J_a|&\le2(1+q)(1+b)+2aq,\\
|J_b|&\le8(b+1)+2a(1+q).
\end{aligned}
$$

Using $W=SJ+KA$, integrating along a center-to-box segment gives

$$
\begin{aligned}
|W(c)-W_*(c)|
&<10^{-5}\left[4(13+4+18)+6(1+\tfrac12+\tfrac52)\right]\\
&=\frac{41}{25000}<\frac1{500}.
\end{aligned}
$$

Combining with (Positive), uniformly on the closed box,

$$
W(c)>\frac{557731}{62500000}-\frac1{500}>\frac3{500}.
\tag{Box-margin}
$$

Next put $z=e^{\mathrm i\theta}$, $c=\cos\theta$, $r=1-c$, and

$$
h=\frac{1+b-z-bz^{-1}}a.
$$

Then $G=1/(h-q)$ and $\ell G-1=(1-h)/(h-q)$. Define the real polynomials

$$
\begin{aligned}
d(c)&=-a^2q+\{a(1+q)(1+b)-2(1-b)^2\}r-4br^2,\\
T(c)&=a^2q^2+\{2(1-b)^2-2aq(1+b)\}r+4br^2.
\end{aligned}
$$

Here $T=a^2|h-q|^2>0$, because the stable plant has no unit-circle pole. Direct calculation yields

$$
\operatorname{Re}\{M(z)(\ell G(z)-1)\}
=\frac{-rW(c)+\varepsilon d(c)}{T(c)}.
\tag{Frequency}
$$

One can check the sign without relying on a software simplification: $d=-J$, $\operatorname{Re}M=\varepsilon+rS(c)$, and

$$
\operatorname{Im}M=\sin\theta\left(1-\frac4{25}(8c^3-4c)\right).
$$

After multiplication by $T$, the imaginary part of $\ell G-1$ is $A\sin\theta$. Taking the real part of the product therefore gives $\varepsilon d-rSJ-rKA=\varepsilon d-rW$.

The ranges above imply

$$
\begin{gathered}
a(1+q)(1+b)<4,\qquad a^2q>\frac1{20},\\
a^2q^2<\frac1{1000},\qquad 2(1-b)^2+8b<6.
\end{gathered}
$$

Since $0\le r\le2$, these give $d<4r-1/20$ and $T<6r+1/1000$. If $N=-rW+\varepsilon d$, then

$$
\begin{aligned}
-N&>\frac{149}{25000}r+\frac1{2000000}\\
&\ge\frac1{2000}\left(6r+\frac1{1000}\right)
>\frac T{2000}.
\end{aligned}
$$

Consequently

$$
\operatorname{Re}\{M(z)(\ell G(z)-1)\}\le-\delta_0,
\qquad\delta_0=\frac1{2000},\quad |z|=1.
\tag{Strict}
$$

The small constant $\varepsilon$ handles zero frequency, where pure lag differences vanish. This margin is uniform over the entire closed box and independent of dimension.

### 6.4 Establish summability before using it

**Lemma 6.2 (causal continuation).** For every $\tau\in[0,1]$ and every one-sided input $e\in\ell_2$, the recursively defined loop $x=e+G\tau D(x)$ has a unique trajectory in $\ell_2$ and satisfies (Conditional). The proof has two parts: an estimate conditional on finite energy, followed by a finite continuation argument that establishes finite energy.

Let $g=\|G\|_{\ell_2\to\ell_2}$ and $m=\|M\|_{\ell_2\to\ell_2}$. The shifts have norm one, so $m\le\varepsilon+2+8/25<3$.

First suppose a solution of

$$
x=e+Gp,\qquad p=\tau D(x),\quad\tau\in[0,1]
$$

is already square summable. Combining (Supply), Parseval, and (Strict) gives

$$
\begin{aligned}
0&\le\langle p,M((\ell G-I)p+\ell e)\rangle\\
 &\le-\delta_0\|p\|_2^2+\ell m\|p\|_2\|e\|_2.
\end{aligned}
$$

For completeness, the frequency-domain step is the identity

$$
\begin{aligned}
&\langle p,M(\ell G-I)p\rangle\\
&\quad=\frac1{2\pi}\int_{-\pi}^{\pi}
\operatorname{Re}\{M(e^{\mathrm i\theta})(\ell G(e^{\mathrm i\theta})-1)\}
\|\widehat p(\theta)\|^2\,d\theta\\
&\quad\le-\delta_0\|p\|_2^2.
\end{aligned}
$$

For an $\ell_2$ sequence, the Fourier transform is understood as the $L_2$ limit of the transforms of finite truncations; pointwise convergence of its Fourier series is unnecessary. The filters are bounded on $\ell_2$, so Parseval and this identity extend from finite sequences by continuity. Since all coordinates have the same scalar filter, the vector-valued formula follows by summing over coordinates. The forcing term is bounded by
$|\ell\langle p,Me\rangle|\le\ell m\|p\|_2\|e\|_2$.

Dividing when $p\ne0$, with the zero case immediate, proves

$$
\|p\|_2\le\frac{\ell m}{\delta_0}\|e\|_2,
\qquad
\|x\|_2\le C_0\|e\|_2,
\quad C_0=1+\frac{g\ell m}{\delta_0}.
\tag{Conditional}
$$

This is still a conditional estimate. To remove the condition, start at $\tau=0$, where every square-summable input has output $x=e$. Suppose square summability for every input has been established at some $\tau$. Increase the gain to $\tau+\Delta\le1$, with

$$
C_0\Delta g\ell\le\frac12.
$$

Strict causality defines the new output $x$ recursively at every finite time, even before we know whether $x\in\ell_2$. Let $P_n$ keep only times $0,\ldots,n$. Feed the old $\tau$-loop the input

$$
e^{(n)}=e+\Delta G(P_nD(x)).
$$

It is square summable because the truncated sequence has finite support and $G$ is stable. The induction hypothesis gives a square-summable old-loop output $y^{(n)}$. Causality implies

$$
P_ny^{(n)}=P_nx.
$$

Indeed, up to time $n$, the extra forcing supplies exactly the missing $\Delta D(x)$ term; induction in time identifies the two prefixes.

To spell out that induction, write $(Gv)_t=\sum_{j=0}^{t-1}G_{t-j}v_j$. Both outputs equal $e_0$ at time zero because this sum is empty. If $y_j^{(n)}=x_j$ for $j<t\le n$, then

$$
\begin{aligned}
y_t^{(n)}
&=e_t+\Delta\sum_{j=0}^{t-1}G_{t-j}D(x_j)
       +\tau\sum_{j=0}^{t-1}G_{t-j}D(y_j^{(n)})\\
&=e_t+(\tau+\Delta)\sum_{j=0}^{t-1}G_{t-j}D(x_j)=x_t.
\end{aligned}
$$

The same recursion proves uniqueness at every finite time. No inverse of a nonlinear operator and no contraction assumption on the full HB update is needed. Now (Conditional) applied to $y^{(n)}$ gives

$$
\begin{aligned}
\|P_nx\|_2
&\le C_0\|e^{(n)}\|_2\\
&\le C_0\|e\|_2+C_0\Delta g\ell\|P_nx\|_2,
\end{aligned}
$$

so every prefix obeys $\|P_nx\|_2\le2C_0\|e\|_2$. The partial sums of squared norms are increasing and bounded. Therefore $x\in\ell_2$.

Only now do we apply (Conditional) to the full new loop, sharpening its gain back to $C_0$. Taking a finite number of equal steps, with an integer $J\ge\max\{1,2C_0g\ell\}$ and $\Delta=1/J$, reaches $\tau=1$. Thus the actual HB trajectory is square summable and satisfies (Conditional).

The continuation is a proof device. The physical trajectory still uses one fixed objective and fixed parameters. The argument requires no incremental stability estimate between different trajectories.

### 6.5 Arbitrary initialization and explicit constants

Set $\alpha=1+b-aq$. The wider bounds (Ranges) imply

$$
\alpha>\frac{15647}{10000}>0,
\qquad
\alpha^2-4b>\frac{828609}{10^8}>0.
$$

The two characteristic roots are real and positive. Their product is $b<1$, and the polynomial at one is $aq>0$, so both are below one.

Let $k_{-1}=0$, $k_0=1$, and $k_{t+1}=\alpha k_t-bk_{t-1}$. For roots $r_1>r_2>0$,

$$
k_t=\frac{r_1^{t+1}-r_2^{t+1}}{r_1-r_2}\ge0.
$$

Summing the recurrence, or its geometric-series expression, gives $\sum_{t\ge0}k_t=1/(aq)$. The impulse response of $G$ is $-ak_t$ with a one-step delay. Its absolute sum bounds the induced $\ell_2$ norm, hence

$$
g\le a\sum_{t\ge0}k_t=\frac1q<101.
$$

Using $\ell<1$, $m<3$, and $\delta_0^{-1}=2000$, (Conditional) gives

$$
\|x\|_2\le610000\|e\|_2.
\tag{Gain}
$$

The free response from the arbitrary initial pair is

$$
e_t=k_tx_0-bk_{t-1}x_{-1}.
$$

To bound its energy, put $R_k=\sum_{t\ge0}k_t^2$ and $R_1=\sum_{t\ge1}k_tk_{t-1}$. Multiplying the recurrence by $k_t$ and summing gives $(1+b)R_1=\alpha R_k$. Squaring the recurrence and summing gives

$$
R_k-1=(\alpha^2+b^2)R_k-2\alpha bR_1.
$$

Solving,

$$
R_k=\frac{1+b}{(1-b)aq[2(1+b)-aq]}.
$$

All sums already converge because the roots lie inside the unit disk. From (Ranges), $aq>11/500$ and $2(1+b)-aq>63/20$, so

$$
R_k<\frac{161/100}{(39/100)(11/500)(63/20)}<60.
$$

Cauchy–Schwarz on the two coefficients of $x_0,x_{-1}$ now gives

$$
\begin{aligned}
\|e\|_2^2
&\le R_k(1+b^2)(\|x_{-1}\|^2+\|x_0\|^2)\\
&\le100(\|x_{-1}\|^2+\|x_0\|^2).
\end{aligned}
$$

This explicitly includes unequal initial points. The earlier zero extension was a convention for signals in the Fourier argument; it did not require the physical $x_{-1}$ to be zero.

### 6.6 From total energy to a linear rate

**Lemma 6.3 (energy-to-rate estimate).** Suppose an autonomous recurrence satisfies $\sum_{j\ge0}\|Y_j\|^2\le C\|Y_0\|^2$ for every initial state, with the same $C>1$. Then $\|Y_t\|^2\le C(1-C^{-1})^t\|Y_0\|^2$. The essential hypothesis is that the energy estimate also applies after restarting at any later state.

Let $Y_t=(x_{t-1},x_t)$. Combining the preceding bounds,

$$
\begin{aligned}
\sum_{t\ge0}\|Y_t\|^2
&=\|x_{-1}\|^2+2\sum_{t\ge0}\|x_t\|^2\\
&\le(1+200\cdot610000^2)\|Y_0\|^2\\
&\le C\|Y_0\|^2,\qquad C=10^{14}.
\end{aligned}
\tag{Energy}
$$

Every tail of the trajectory is the same autonomous recurrence with another admissible initial pair. For the finite tail energy

$$
\mathcal S_t=\sum_{j=t}^{\infty}\|Y_j\|^2,
$$

(Energy) therefore gives $\mathcal S_t\le C\|Y_t\|^2$.

The direction of this inequality matters: it says that the current state accounts for at least a fraction $1/C$ of all remaining energy, namely $\|Y_t\|^2\ge\mathcal S_t/C$. Removing that current term therefore removes a fixed fraction of the tail. In equations,

$$
\mathcal S_{t+1}=\mathcal S_t-\|Y_t\|^2
\le(1-C^{-1})\mathcal S_t.
$$

Iteration yields

$$
\|Y_t\|^2\le\mathcal S_t
\le C(1-C^{-1})^t\|Y_0\|^2.
$$

Taking square roots, using $\|x_t\|\le\|Y_t\|$, and undoing translation proves exactly (G). All constants are uniform over $B$, all finite dimensions, all objectives, and all initial pairs. This completes Theorem B.

<figure>
<img src="assets/fixed_objective_trajectory.svg" alt="A numerical trajectory on the explicitly constructed fixed interpolant, with a first expanding step followed by decreasing state norms.">
<figcaption>Figure 3. A numerical illustration on the exact conjugate interpolant of Section 4, initialized at (z inverse,1). The left panel shows the initial trajectory over objective contours. The right shows the state norm relative to its initial value. The first squared-state ratio is exactly 4013/4000; the universal convergence guarantee comes from Theorem B, not from this simulation.</figcaption>
</figure>

## 7. A stronger obstruction: the information in two points

The argument in Section 4 used homogeneity of a quadratic formula. There is a stronger statement: at the witness, even an arbitrary finite-valued function of the full two-point record cannot supply one common monotone energy controlling the next objective gap.

To state the distinction precisely, define

$$
\begin{aligned}
\mathcal O_f(u,v)=\big(&u-x_*,\nabla f(u),v-x_*,\nabla f(v),\\
&f(u)-f_*,f(v)-f_*\big).
\end{aligned}
$$

A candidate common energy would be a map $\Phi$ of these six entries. It may be nonlinear or discontinuous and may depend on the fixed parameters and dimension. It must take a finite real value on every record and must be the same map for every objective. It has no access to the objective beyond the displayed record.

<div class="theorem">

**Theorem C — No common two-point record energy.** At the central parameters, already in dimension two, no such $\Phi$ satisfies

$$
f(w)-f_*\le\Phi(\mathcal O_f(v,w))
             \le\Phi(\mathcal O_f(u,v))
$$

for every admissible objective and every initial pair, with $w$ the HB successor.

</div>

### 7.1 Join identical records across scaled objectives

Let $S$ be the real matrix for multiplication by the complex number $z$ from Section 4. Then $S^{\mathsf T}S=RI$ and the samples satisfy

$$
x_{j+1}=Sx_j,\quad g_{j+1}=Sg_j,\quad F_{j+1}=RF_j
\quad(j=0,1),\qquad F_0>0.
$$

Let $f_0$ be their normalized global interpolant. For each integer $n\ge0$, define a different objective

$$
f_n(x)=R^n f_0(S^{-n}x).
$$

The scaling preserves the exact function class. Indeed, $\|S^nv\|=R^{n/2}\|v\|$ and $R^n(S^{-n})^{\mathsf T}=S^n$, so

$$
\nabla f_n(x)=S^n\nabla f_0(S^{-n}x).
$$

The gradient Lipschitz factors cancel. Multiplying the strong-convexity inequality for $f_0$ by $R^n$ also leaves its constant $q$ unchanged. Each objective still has minimizer and minimum zero.

For $f_n$, the initial state $(S^nx_0,S^nx_1)$ has successor $S^nx_2$. Define its predecessor record

$$
A_n=\big(S^nx_0,S^ng_0,S^nx_1,S^ng_1,R^nF_0,R^nF_1\big).
$$

The successor record for $f_n$ equals $A_{n+1}$ exactly, component by component. Therefore a common $\Phi$ would have to satisfy

$$
R^nF_2\le\Phi(A_{n+1})\le\Phi(A_n)
\qquad(n\ge0).
$$

Chaining finitely many inequalities gives $R^nF_2\le\Phi(A_0)$ for every $n$. Since $R>1$ and $F_2>0$, the left side is unbounded while the right side is a single finite number. This is impossible.

Each inequality concerns one fixed admissible objective and one legal step. Joining the inequalities is justified by equality of records and by the requirement that $\Phi$ be common across objectives. The proof does **not** construct a divergent trajectory on one objective. It proves an information restriction on a common energy. The general conditional form of this obstruction and its rational application received a [separate review](evidence/common_record_review.md).

### 7.2 Why convergence still permits a Lyapunov function

For each fixed objective, let $T_f$ be the centered two-state update and define

$$
E_f(Y)=\sum_{j=0}^{\infty}\|T_f^jY\|^2.
$$

The proof of Theorem B establishes

$$
\|Y\|^2\le E_f(Y)\le C\|Y\|^2,\qquad C=10^{14}.
$$

Shifting the sum gives

$$
E_f(T_fY)=E_f(Y)-\|Y\|^2
\le(1-C^{-1})E_f(Y).
$$

Thus every fixed objective has a strictly decreasing state energy. The tail after $N$ terms is at most $C(1-C^{-1})^N\|Y\|^2$, by the tail-energy argument in Section 6.6. The continuous partial sums converge uniformly on bounded sets, so $E_f$ is continuous.

There is no contradiction with Theorem C. The definition of $E_f$ uses the objective through its future trajectory. Two objectives having the same current two-point record may have different future behavior and different values of $E_f$. Theorem C excludes one formula using only that record, not objective-dependent energies with access to more information.

## 8. What the result settles, and what remains

Theorems A and B settle the existence question for the prescribed certificate family and classify the dynamics at the exhibited witness. There are parameters outside that family for which every fixed-objective trajectory nevertheless converges. Theorem C sharpens the explanation: at the witness, the obstruction persists for every finite-valued common formula of the full displayed two-point record.

The separation is robust. All off-diagonal interpolation residuals at the center are strict. Keeping the sample locations and values fixed while varying

$$
\eta(q,a,b)=\frac{1+b-z-b/z}{a}
$$

preserves them in some open neighborhood. The same similarity argument then excludes the prescribed family there. Intersecting that neighborhood with the interior of $B$ produces a nonempty open region of convergent parameters with the obstruction. The source package also gives explicit rational interval bounds for the full-box obstruction; this strengthening is not needed for the two main theorems above.

Several questions remain distinct:

- **Global classification.** What happens at all the other parameters in $\mathcal D$? The present results classify a specific region, not every blank region in a numerical plot.
- **Cycles versus failure of convergence.** Does every parameter triple failing universal convergence admit some finite-cycle counterexample? No global implication of this kind is proved here.
- **Sharper guarantees.** How large can the convergence region be made, and what is its sharp worst-case rate?
- **The information needed by common energies.** How much additional history or objective information suffices for a compact, useful certificate?

The interpolation and multiplier frameworks are established methods. The contribution documented here is their combination with an exact impossibility witness and a full dynamical classification of that witness. A bounded [prior-art review](evidence/prior_art_20260909.md) did not locate a matching complete separation statement, but does not establish priority over all published or unpublished work.

## 9. Reproduction and verification

These notes reorganize the saved mathematical proofs; they do not change their assumptions or quantifiers. The research workflow used AI for exploration, derivation, and separate mathematical review. It produced target-specific terminal decisions, preserved in the accompanying evidence snapshot.

| Result | Reviewed scope | Terminal decision, September 9, 2026 (UTC+8) |
|---|---|---|
| Theorem A / HB-R2-E | Exact point; prescribed-family impossibility; all finite periods and dimensions | PROVED, 18:35 |
| Theorem C / record obstruction | General conditional obstruction and the rational application | PROVED, 18:53 |
| Theorem B / HB-R2-G | Entire closed box; exact constants; all functions, dimensions, initial pairs, and times | PROVED, 19:25 |

Theorem B also received a separate direct review at 19:21. Neither convergence review infers convergence from cycle exclusion. Both examine the signed frequency identity, the box margin, the causal continuation, arbitrary initialization, and the final rate constants. The [verdict snapshot](evidence/verdicts.json) retains the exact target digests and decisions; the [full convergence review](evidence/convergence_terminal_review.md) contains the analytical checks.

These are mathematical text reviews with exact arithmetic support. **This project does not currently supply a Lean kernel-checked formalization of these theorems.** The checks below certify finite identities and inequalities; the analytical and quantified arguments are given in the text. Publication review and priority assessment remain separate from the internal terminal decisions.

### 9.1 Run the exact arithmetic checks

From this notes directory, run:

```bash
python -B checks/verify_submission.py
```

Only the Python standard library is needed. The script checks all twelve interpolation residuals, the conjugate-piece identities, the exact HB transition, every Gram scaling entry, the lag polynomial, every Bernstein coefficient, interval bounds on the parameter box, the general signed frequency identity, and the constants in the convergence estimate.

The additional finite-horizon arithmetic at the end of that script belongs to a supplemental construction in the source package; it is not needed for Theorems A or B. A complete successful run is preserved in [exact_checks.txt](validation/exact_checks.txt).

### 9.2 Reproduce the illustrations

```bash
python scripts/make_figures.py
```

The figure script uses NumPy and Matplotlib. Figures 1 and 2 visualize the exact geometric data and polynomial. Figure 3 numerically evaluates the same fixed conjugate interpolant, by minimizing a quadratic over a four-weight simplex and enumerating its active supports. No objective is switched during the simulated trajectory.

The numerical evaluator reproduces the prescribed values and gradients to floating-point accuracy and checks the first transition. Its output is an illustration, not an additional premise of the universal theorems. The sampled trajectory is saved in [trajectory_data.json](assets/trajectory_data.json). Each figure is available as SVG, PDF, and PNG.

### 9.3 Evidence and versions

The [original root proof](evidence/root_proof.md), [dynamics proof](evidence/submission_dynamics.md), and [independent convergence review](evidence/convergence_independent_review.md) are copied into the bundle. Their historical wording is retained; passages saying “pending verification” precede the later decisions listed above. File hashes and the source location are recorded in [snapshot.json](evidence/snapshot.json).

The HTML contains its mathematical typesetting, fonts, and figures inline and can be read offline. The PDF uses the same mathematical content, expands all calculation details, and adds print pagination. Accompanying source and evidence links are resolved within the full downloadable bundle.

## References

1. Baptiste Goujaud, Adrien Taylor, and Aymeric Dieuleveut. [*Open Problem: Two Riddles in Heavy-Ball Dynamics*](https://arxiv.org/abs/2502.19916v1). 2025. The source of the second riddle and its specified certificate family.

2. Konstantinos Fotopoulos, Michael Helcig, Karl Deck, and Jannis Alsbach. [*Cycling and Non-Acceleration of the Heavy-Ball Method in One Dimension*](https://odi.inf.ethz.ch/blog/heavy-ball-one-dimension/). ODI Blog, July 7, 2026. Expository reference for the companion first riddle.

3. Adrien B. Taylor, Julien M. Hendrickx, and François Glineur. [*Smooth Strongly Convex Interpolation and Exact Worst-case Performance of First-order Methods*](https://arxiv.org/abs/1502.05666v6). Mathematical Programming, 2017. Finite interpolation and global realization.

4. Adrien Taylor, Bryan Van Scoy, and Laurent Lessard. [*Lyapunov Functions for First-Order Methods: Tight Automated Convergence Guarantees*](https://proceedings.mlr.press/v80/taylor18a.html). ICML, 2018. Automated certificates for prescribed state templates.

5. Baptiste Goujaud, Adrien Taylor, and Aymeric Dieuleveut. [*Provable non-accelerations of the heavy-ball method*](https://arxiv.org/abs/2307.11291v2). Mathematical Programming, 2025. Prior cycling and non-acceleration results.

6. Jingfan Zhang, Peter Seiler, and Joaquin Carrasco. [*Noncausal FIR Zames-Falb Multiplier Search for Exponential Convergence Rate*](https://arxiv.org/abs/1902.09473). 2019. Related noncausal finite-lag multiplier methodology.
