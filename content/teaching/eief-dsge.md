---
title: Econometrics of DSGE models
date: "2017-02-16T00:00:00+11:00"
enddate: "2017-03-30T00:00:00+11:00"
publishdate: "2016-03-24"
host: "EIEF"
duration: 7776000
---

This is a course on the econometric techniques used in the estimation of dynamic
macroeconomic models (DSGE models). The aim of the course is mostly theoretical, but applications are also presented using [Julia](http://julialang.org).


<!--more-->

### Topics

1. Motivation: DSGE models and their applications
2. Approximating and solving DSGE models

    a.  State space representation
    b.  Constructing (log-)linear approximation

3. Time series properties of the model and data
4. Classical estimation of DSGE models

    a.  Generalized Method of Moments (GMM)

    b.  Simulated Method of Moments (SMM) and Indirect Inference (IF)

    c.  Impulse response functions matching

5. Bayesian estimation of DSGE models

    a.  (log-)linear models

    b.  Non linear models

6.  The twilight zone of DSGE estimation

    a.  Identification

    b.  Feasible non linear estimation

    c.  VAR and DSGE

    d.  Limited information estimation


### Readings

This is a list of readings. This is by no means comprehensive --- it
simply reflects the source that are closely related with the topics
covered in lectures.

#### Books:

-   Canova, F. (2007), Methods for Applied Macroeconomic Research,
    Princeton: Princeton University Press.
-   Dejong, D.N. and C. Dave (2007), Structural Macroeconomics,
    Princeton: Princeton University Press

#### Papers:

-   An and Schoerfheide (2007) Bayesian Analysis of DSGE Models,
    Econometric Reviews, 26(2-4), 2007, 113-172.
    [Download](http://www.tandfonline.com/doi/abs/10.1080/07474930701220071)
-   Fernández-Villaverde, Jesús. "The econometrics of DSGE models."
    SERIEs 1.1-2 (2010): 3-49.
    [Download](http://link.springer.com/article/10.1007/s13209-009-0014-7)
-   Schorfheide, Frank. "Loss function-based evaluation of DSGE models."
    Journal of Applied Econometrics 15.6 (2000): 645-670.
    [Download](http://onlinelibrary.wiley.com/doi/10.1002/jae.582/full)
-   Arulampalam, M. Sanjeev, et al. "A tutorial on particle filters for
    online nonlinear/non-Gaussian Bayesian tracking." Signal Processing,
    IEEE Transactions on 50.2 (2002): 174-188.
    [Download](http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=978374)
-   Doucet, Arnaud, and Adam M. Johansen. "A tutorial on particle
    filtering and smoothing: Fifteen years later." Handbook of Nonlinear
    Filtering 12.656-704 (2009): 3.
    [Download](http://automatica.dei.unipd.it/tl_files/utenti/lucaschenato/Classes/PSC10_11/Tutorial_PF_doucet_johansen.pdf)
-   Andrieu, Christophe, Arnaud Doucet, and Roman Holenstein. "Particle
    markov chain monte carlo methods." Journal of the Royal Statistical
    Society: Series B (Statistical Methodology) 72.3 (2010): 269-342.
    [Download](http://onlinelibrary.wiley.com/doi/10.1111/j.1467-9868.2009.00736.x/full)
-   Gallant, A. Ronald, Raffaella Giacomini, and Giuseppe Ragusa. Bayesian
    estimation of state space models using moment conditions. Technical
    report, 2015. [Download](http://www.aronaldg.org/papers/bliml.pdf)
-   Giacomini, Raffaella. "The relationship between DSGE and VAR models."
    Advances in Econometrics 31 (2013).
    [Download](http://www.emeraldinsight.com/doi/abs/10.1108/S0731-9053(2013)0000031001)
-   Komunjer, Ivana, and Serena Ng. "Dynamic identification of
    stochastic general equilibrium models." Econometrica 79.6
    (2011):1995-2032.
    [Download](http://www.columbia.edu/~sn2294/pub/ecta11.pdf)
-   Del Negro, Marco, and Frank Schorfheide. "Bayesian
    macroeconometrics." The Oxford handbook of Bayesian econometrics 293
    (2011): 389.
    [Download](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.414.4871&rep=rep1&type=pdf)

### Julia

[Julia](http://julialang.org) is a high-level, high-performance dynamic
programming language for technical computing, with syntax that is
familiar to users of other technical computing environments. In
particular, its syntax is similar to Matlab. The similarity of the
syntax means that a lot of Matlab code will run almost unmodified.

`Julia` has many advantages over other languages and for this reason is
being extensively used in industries and in research.

Recently, the [Federal Reserve of New York](https://www.newyorkfed.org/) has
open sourced its macroeconomic model (used for producing forecast about key
variables and to conduct policy experiment). The code is written in Julia. You
can read about
it
[here](http://libertystreeteconomics.newyorkfed.org/2015/12/the-frbny-dsge-model-meets-julia.html).
The code is [here](https://github.com/FRBNY-DSGE/DSGE.jl).


[Programming in Julia](http://quant-econ.net/jl/learning_julia.html) in an
excellent tutorial is written by Thomas J. Sargent and John Stachurski. Along
with being a very good introduction to the language, this is also a complete macroeconomic textbook with concept illustrated in Julia.
.
