---
type: page
title: "Resources"
footnotes: true
mathjax: true
---

On this page I will keep a running list of computation/programming projects I work on from time to time.

When it comes to coding, my interests range from estimation of nonlinear moment condition models, approximate bayesian inference, large optimization problems,
high-performance computing in econometrics and finance, and big data application to time time series econometrics.  Below you will find a list of package I have developed recently. For details on each packages visit my [github](http://github.com/gragusa) and/or visit the package page. For code related to publish paper, visit the publication section.

# Julia Packages

Notice that some of the Julia packages are "registered", meaning that you can install them from Julia by `Pkg.add`-ing them. Others are at an early stage and are not yet registered. To install these packages use `Pkg.clone`.

## [`CovarianceMatrices.jl`](http:://github.com/gragusa/CovarianceMatrices.jl)

[![license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/gragusa/CovarianceMatrices.jl/master/LICENSE.md)  [![CovarianceMatrices](http://pkg.julialang.org/badges/CovarianceMatrices_0.5.svg)](http://pkg.julialang.org/?pkg=CovarianceMatrices&ver=0.5) [![Build Status](https://travis-ci.org/gragusa/CovarianceMatrices.jl.svg?branch=master)](https://travis-ci.org/gragusa/CovarianceMatrices.jl) [![Coverage Status](https://coveralls.io/repos/gragusa/CovarianceMatrices.jl/badge.svg?branch=master&service=github)](https://coveralls.io/github/gragusa/CovarianceMatrices.jl?branch=master)

`CovarianceMatrices` is a package for estimating variance covariance matrices in situations where the standard assumptions of independence is violated. It provides heteroskedasticity consistent (HC); heteroskedasticity and autocorrelation consistent (HAC); and cluster robust (CRVE) estimators of the variance matrices. An interface for `GLM.jl` is given so that they can be integrated easily  into standard regression analysis. It is also easy to integrated these estimators into new inferential procedures or applications.


{{< highlight julia "style=native" >}}
using CovarianceMatrices
## Simulated AR(1) and estimate it using OLS
srand(1)
y = zeros(Float64, 100)
rho = 0.8
y[1] = randn()
for j = 2:100
  y[j] = rho * y[j-1] + randn()
end

data = DataFrame(y = y[2:100], yl = y[1:99])
AR1  = fit(GeneralizedLinearModel, y~yl, data, Normal())

## Truncated Kernel with optimal bandwidth
vcov(AR1, TruncatedKernel())

{{< /highlight >}}


## [`Divergences.jl`](http://github.com/gragusa/Divergences.jl)
[![license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/gragusa/Divergences.jl/master/LICENSE.md) [![Pkg](http://pkg.julialang.org/badges/Divergences_0.5.svg)](http://pkg.julialang.org/detail/Divergences.html) [![Build Status](https://travis-ci.org/gragusa/Divergences.jl.svg?branch=master)](https://travis-ci.org/gragusa/Divergences.jl) [![Coverage Status](https://coveralls.io/repos/github/gragusa/Divergences.jl/badge.svg?branch=master)](https://coveralls.io/github/gragusa/Divergences.jl?branch=master)

`Divergences` is a Julia package that makes it easy to evaluate divergence measures between two vectors. The package allows calculating the gradient and the diagonal of the Hessian of several divergences.

- Komunjer, I.; Ragusa, G. "Existence and characterization of conditional density projections." Econometric Theory 2016, 32, 947–987.

<!--
A divergence between two vectors of probabilities; $p := (p\_1, p\_2,\ldots,p\_n)$ and $q := (q\_1, q\_2,\ldots,q\_n)$ is defined as
$$ D(p,q)= \sum\_{i=1}^{n} \phi \left(\frac{p\_{i}}{q\_{i}}\right)p\_{i} $$ where $\phi$ is function that satisfies the following:

1. is twice continuously differentiable on `$ (0, +\infty) $`;
2. is strictly convex on $(0, +\infty)$;
3. $\phi(1) = \phi'(1) = 0$;
4. $\lim\_{u->0^+} \phi'(u) < 0$;
5. $\lim\_{u->+\infty} \phi'(u) > 0$.

An very general family of divergences is the Cressie-Read family[^1]. The class is indexed by a real parameter $\alpha$ and it is defined as
<div>
$$
\phi\_{\alpha}(u)=\begin{cases}
\frac{u^{\alpha+1}-1}{a(a+1)}-\frac{1}{a}u+\frac{1}{a} \& u>0 \\\\[2ex]
\frac{1}{a+1} \& u=0
\end{cases}.
$$
</div>

The package defines a `Divergence` type with the following suptypes:

* Kullback-Leibler divergence `KullbackLeibler`
* Chi-square distance `ChiSquared`
* Reverse Kullback-Leibler divergence `ReverseKullbackLeibler`
* Cressie-Read divergences `CressieRead`

These divergences differ from the equivalent ones defined in the `Distances` package because they are normalized. Also, the package provides methods for calculating their gradient and the (diagonal elements of the) Hessian matrix.

The constructors for the types above are straightforward
```julia
KullbackLeibler()
ChiSqaured()
ReverseKullbackLeibler()
```
The constructor for `CressieRead` is
```julia
CR(::Real)
```
The Hellinger divergence is obtained by `CR(-1/2)`. For a certain value of `alpha`, `CressieRead` correspond to a divergence that has a specific type defined. For instance `CR(1)` is equivalent to `ChiSquared` although the underlying code for evaluation and calculation of the gradient and Hessian are different. -->

{{< highlight julia "style=native" >}}
using Divergences
p = rand(20)
q = rand(20)
scale!(p, 1/sum(p))
scale!(q, 1/sum(q))
evaluate(CressieRead(-.5), p, q)
{{< /highlight >}}


## [`Genoud.jl`](http://github.org/gragusa/Genoud.jl)
[![](https://img.shields.io/badge/license-GPL3.0+-blue.svg)](https://raw.githubusercontent.com/gragusa/Genoud.jl/master/LICENSE.md) [![](https://img.shields.io/badge/Julia-unregistered-red.svg)](code/)

GENetic Optimization Using Derivative.

<div class="units-row">

<div class="unit-65">


{{< highlight julia "style=native" >}}
using Genoud
using Calculus
function f8(xx)
    x, y = xx
    -x*sin(√abs(x)) - y*sin(√abs(y))
end

function gr!(x, stor)  
    stor[:] = Calculus.gradient(f8, x)
end

dom = Genoud.Domain([-500  500.;
                     -500. 500.])
out = Genoud.genoud(f8, [1.0, -1.0],
                    sizepop = 5000,
                    sense = :Min,
                    domains = dom)
{{< /highlight >}}

</div>

<div class="unit-35">

<figure>
    <img src="fig/f8.png"  />
    <figcaption>
        <h4>Surface plot of $$f(x_1, x_2) = -\sum_{i=1}^2 x_i \sin(\sqrt{|x_i|}).$$ This function is minimized at $x_1^*  \approx 420.968$ and $x_2^* \approx 420.968$. At the minima, $f(x_1^*, x_2^*) = -837.9$.
        <p></p>
        Source: Yao, Xin, Yong Liu, and Guangming Lin. "Evolutionary programming made faster." IEEE Transactions on Evolutionary computation 3, no. 2 (1999): 82-102.</h4>
    </figcaption>
</figure>


</div>
</div>

{{< highlight julia "style=native" >}}
Results of Genoud Optimization Algorithm
 * Minimizer: [420.96874636091724,420.9687462145861]
 * Minimum: -8.379658e+02
 * Pick generation: 20
 * Convergence: true
   * |f(x) - f(x')| / |f(x)| < 1.0e-03: true
   * Number of Generations: 27
{{< /highlight >}}


## [`CsminWel.jl`](http://github.org/gragusa/CsminWel.jl)
[![](https://img.shields.io/badge/license-BSD3-blue.svg)](https://raw.githubusercontent.com/gragusa/CsminWel.jl/master/LICENSE.md) [![](https://img.shields.io/badge/Julia-unregistered-red.svg)](code/) [![](https://img.shields.io/badge/Julia-unregistered-red.svg)](code/) [![Build Status](https://travis-ci.org/gragusa/CsminWel.jl.svg?branch=master)](https://travis-ci.org/gragusa/CsminWel.jl) [![Coverage Status](https://coveralls.io/repos/gragusa/CsminWel.jl/badge.svg?branch=master&service=github)](https://coveralls.io/github/gragusa/CsminWel.jl?branch=master) [![codecov.io](http://codecov.io/github/gragusa/CsminWel.jl/coverage.svg?branch=master)](http://codecov.io/github/gragusa/CsminWel.jl?branch=master)


This package provides an interface to Chris Sims' `csminwel` optimization code. The code borrows from [DSGE.jl](https://github.com/FRBNY-DSGE/DSGE.jl), but it is adapted to be compatibles with the [Optim.jl](https://github.com/JuliaOpt/Optim.jl)'s API. When the derivative of the minimand is not supply either Finite Difference of Forward Automatic Differentiation derivatives are automatically supplied to the underlying code.


From the original author:
> Uses a quasi-Newton method with BFGS update of the estimated inverse hessian. It is robust against certain pathologies common on likelihood functions. It attempts to be robust against "cliffs", i.e. hyperplane discontinuities, though it is not really clear whether what it does in such cases succeeds reliably.

Differently from the solvers in `Optim.jl`, `Csminwel` returns an estimate of the inverse of the Hessian at the solution which may be used for standard errors calculations and/or to scale a Monte Carlo sampler.

{{< highlight julia "style=native" >}}
#=
Maximizing loglikelihood of logistic models
=#
using CsminWel
using StatsFuns
## Generate fake data (true coefficient = 0)
srand(1)
x = [ones(200) randn(200,4)]
y = [rand() < 0.5 ? 1. : 0. for j in 1:200]

## log-likelihood
function loglik(beta)
    xb = x*beta
    sum(-y.*xb + log1pexp.(xb))
end

## Derivative of loglikelihood
function dloglik(beta)
    xb = x*beta
    px = logistic.(xb)
    -x'*(y.-px)
end

## Optim uses a mutating function for deriv
function fg!(beta, stor)
    stor[:] = dloglik(beta)
end

## With analytical derivative
res1 = optimize(loglik, fg!, zeros(5), BFGS())
res2 = optimize(loglik, fg!, zeros(5), Csminwel())

## With finite-difference derivative
res3 = optimize(loglik, zeros(5), Csminwel())

## With forward AD derivative
res4 = optimize(loglik, zeros(5), Csminwel(), OptimizationOptions(autodiff=true))

## Use approximation to the inverse Hessian for standard errors of estimated parameters
stderr = √diag(res2.invH)
{{< /highlight >}}



[^1]: Cressie, Noel, and Timothy RC Read. "Multinomial goodness-of-fit tests." Journal of the Royal Statistical Society. Series B (Methodological) (1984): 440-464.
