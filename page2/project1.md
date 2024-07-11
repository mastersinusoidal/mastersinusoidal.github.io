# Introduction: Rosenbrock

Welcome to the first AeroSandbox tutorial!

AeroSandbox is a tool for solving design optimization problems for
large, multidisciplinary engineered systems. The most important part of
AeroSandbox is its `Opti()` stack, which allows you formulate and solve
an optimization problem in natural mathematical syntax.

The `Opti` class extends the `Opti` class of CasADi (the library
AeroSandbox uses for automatic differentiation), adding many new
features tailored specifically for engineering design. We\'ll explore
more of these advanced features later!

For now, let\'s solve the \"Hello World!\" of optimization problems:
[the Rosenbrock
problem](https://en.wikipedia.org/wiki/Rosenbrock_function).
Mathematically, it is stated as:

$$ \underset{x, y}{\text{minimize }}(1-x)^2 + 100(y-x^2)^2 $$

In code:
:::

::: {.cell .code execution_count="1" ExecuteTime="{\"end_time\":\"2024-04-05T23:36:38.738497Z\",\"start_time\":\"2024-04-05T23:36:38.729472Z\"}" collapsed="false"}
``` python
def rosenbrock(x, y):
    return (1 - x) ** 2 + 100 * (y - x ** 2) ** 2
```
:::

::: {.cell .markdown collapsed="false"}
It\'s a good test case, because the minimum lies at the bottom of a
shallow, curving valley:
:::

::: {.cell .code execution_count="2" ExecuteTime="{\"end_time\":\"2024-04-05T23:36:41.714041Z\",\"start_time\":\"2024-04-05T23:36:38.739504Z\"}" collapsed="false"}
``` python
### Don't worry about this code block; this is just here to visualize the Rosenbrock function.
from aerosandbox.tools.pretty_plots import plt, show_plot, contour, mpl, equal
import aerosandbox.numpy as np

fig, ax = plt.subplots(figsize=(7.5, 6), dpi=200)
X, Y = np.meshgrid(np.linspace(-1, 2, 300), np.linspace(-1, 2, 300))
contour(X, Y, rosenbrock(X, Y), z_log_scale=True, linelabels_fontsize=8)
plt.clim(vmin=1e-1); equal()
show_plot("The Rosenbrock Function", "$x$", "$y$")
```

::: {.output .display_data}
![](vertopal_c880935963c84ca592351e716a7b4a3a/cbdcd3b5e762f041bf524dd444afebfe50394287.png)
:::
:::

::: {.cell .markdown collapsed="false"}
As it turns out, a good number of engineering design optimization
problems are pretty mathematically similar to the Rosenbrock problem (of
course, there are plenty of exceptions). Specifically, many engineering
design problems are:

-   Continuous: all design variables are continuous inputs (as opposed
    to being discrete).
-   [Nonlinear](https://en.wikipedia.org/wiki/Nonlinear_system): the
    sensitivity of performance with respect to inputs changes throughout
    the design space.
-   Nonconvex: doesn\'t satisfy the [convex
    inequality](https://en.wikipedia.org/wiki/Convex_function#Definition).
    Speaking loosely, convexity means the objective function is always
    \"curving up\" and that the boundary of the feasible design space
    doesn\'t have any concave regions.
-   Poorly-scaled, i.e. Hessian has a large condition number (e.g. for
    Rosenbrock, $\text{cond}(H)\approx 2500$ at the optimum)
-   [Constrained](https://en.wikipedia.org/wiki/Constrained_optimization):
    most engineering problems are constrained. The Rosenbrock problem is
    unconstrained out-of-the-box, but we\'ll add a constraint in the
    next tutorial.

For now, let\'s optimize and find the minimum of the Rosenbrock
function! First, we set up the problem:
:::

::: {.cell .code execution_count="3" ExecuteTime="{\"end_time\":\"2024-04-05T23:36:42.219460Z\",\"start_time\":\"2024-04-05T23:36:41.715055Z\"}" collapsed="false"}
``` python
import aerosandbox as asb  # This is the standard AeroSandbox import convention

opti = asb.Opti()  # Initialize a new optimization environment; convention is to name it `opti`.

### Define your optimization variables
x = opti.variable(init_guess=0)  # You must provide initial guesses.
y = opti.variable(init_guess=0)

### Define your objective
f = (1 - x) ** 2 + 100 * (y - x ** 2) ** 2  # You can construct nonlinear functions of variables...
opti.minimize(f)  # ...and then optimize them.
```
:::

::: {.cell .markdown collapsed="false"}
Then, we solve the problem. The solver will spit out lots of helpful
info as it solves; we can ignore this for now (and later we\'ll learn
how to suppress it if desired).
:::

::: {.cell .code execution_count="4" ExecuteTime="{\"end_time\":\"2024-04-05T23:36:42.240265Z\",\"start_time\":\"2024-04-05T23:36:42.220467Z\"}" collapsed="false"}
``` python
### Optimize
sol = opti.solve()  # This is the conventional syntax to solve the optimization problem.
```

::: {.output .stream .stdout}
    This is Ipopt version 3.14.11, running with linear solver MUMPS 5.4.1.

    Number of nonzeros in equality constraint Jacobian...:        0
    Number of nonzeros in inequality constraint Jacobian.:        0
    Number of nonzeros in Lagrangian Hessian.............:        3

    Total number of variables............................:        2
                         variables with only lower bounds:        0
                    variables with lower and upper bounds:        0
                         variables with only upper bounds:        0
    Total number of equality constraints.................:        0
    Total number of inequality constraints...............:        0
            inequality constraints with only lower bounds:        0
       inequality constraints with lower and upper bounds:        0
            inequality constraints with only upper bounds:        0

    iter    objective    inf_pr   inf_du lg(mu)  ||d||  lg(rg) alpha_du alpha_pr  ls
       0  1.0000000e+00 0.00e+00 2.00e+00   0.0 0.00e+00    -  0.00e+00 0.00e+00   0
       1  9.5312500e-01 0.00e+00 1.25e+01 -11.0 1.00e+00    -  1.00e+00 2.50e-01f  3
       2  4.8320569e-01 0.00e+00 1.01e+00 -11.0 9.03e-02    -  1.00e+00 1.00e+00f  1
       3  4.5708829e-01 0.00e+00 9.53e+00 -11.0 4.29e-01    -  1.00e+00 5.00e-01f  2
       4  1.8894205e-01 0.00e+00 4.15e-01 -11.0 9.51e-02    -  1.00e+00 1.00e+00f  1
       5  1.3918726e-01 0.00e+00 6.51e+00 -11.0 3.49e-01    -  1.00e+00 5.00e-01f  2
       6  5.4940990e-02 0.00e+00 4.51e-01 -11.0 9.29e-02    -  1.00e+00 1.00e+00f  1
       7  2.9144630e-02 0.00e+00 2.27e+00 -11.0 2.49e-01    -  1.00e+00 5.00e-01f  2
       8  9.8586451e-03 0.00e+00 1.15e+00 -11.0 1.10e-01    -  1.00e+00 1.00e+00f  1
       9  2.3237475e-03 0.00e+00 1.00e+00 -11.0 1.00e-01    -  1.00e+00 1.00e+00f  1
    iter    objective    inf_pr   inf_du lg(mu)  ||d||  lg(rg) alpha_du alpha_pr  ls
      10  2.3797236e-04 0.00e+00 2.19e-01 -11.0 5.09e-02    -  1.00e+00 1.00e+00f  1
      11  4.9267371e-06 0.00e+00 5.95e-02 -11.0 2.53e-02    -  1.00e+00 1.00e+00f  1
      12  2.8189505e-09 0.00e+00 8.31e-04 -11.0 3.20e-03    -  1.00e+00 1.00e+00f  1
      13  1.0095040e-15 0.00e+00 8.68e-07 -11.0 9.78e-05    -  1.00e+00 1.00e+00f  1
      14  1.3288608e-28 0.00e+00 2.02e-13 -11.0 4.65e-08    -  1.00e+00 1.00e+00f  1

    Number of Iterations....: 14

                                       (scaled)                 (unscaled)
    Objective...............:   1.3288608467480825e-28    1.3288608467480825e-28
    Dual infeasibility......:   2.0183854587685121e-13    2.0183854587685121e-13
    Constraint violation....:   0.0000000000000000e+00    0.0000000000000000e+00
    Variable bound violation:   0.0000000000000000e+00    0.0000000000000000e+00
    Complementarity.........:   0.0000000000000000e+00    0.0000000000000000e+00
    Overall NLP error.......:   2.0183854587685121e-13    2.0183854587685121e-13


    Number of objective function evaluations             = 36
    Number of objective gradient evaluations             = 15
    Number of equality constraint evaluations            = 0
    Number of inequality constraint evaluations          = 0
    Number of equality constraint Jacobian evaluations   = 0
    Number of inequality constraint Jacobian evaluations = 0
    Number of Lagrangian Hessian evaluations             = 14
    Total seconds in IPOPT                               = 0.008

    EXIT: Optimal Solution Found.
          solver  :   t_proc      (avg)   t_wall      (avg)    n_eval
           nlp_f  |   1.00ms ( 27.78us)  53.00us (  1.47us)        36
      nlp_grad_f  |        0 (       0) 134.00us (  8.37us)        16
      nlp_hess_l  |        0 (       0)  49.00us (  3.50us)        14
           total  |   9.00ms (  9.00ms)   8.03ms (  8.03ms)         1
:::
:::

::: {.cell .markdown collapsed="false"}
Finally, we can look at the optimal values of our optimization
variables:
:::

::: {.cell .code execution_count="5" ExecuteTime="{\"end_time\":\"2024-04-05T23:36:42.247932Z\",\"start_time\":\"2024-04-05T23:36:42.242274Z\"}" collapsed="false"}
``` python
### Extract values at the optimum
x_opt = sol(x)  # Evaluates x at the point where the solver converged.
y_opt = sol(y)

### Print values
print(f"x = {x_opt}")
print(f"y = {y_opt}")
```

::: {.output .stream .stdout}
    x = 0.9999999999999899
    y = 0.9999999999999792
:::
:::

::: {.cell .markdown collapsed="false"}
The solution is found to be $(1, 1)$, which can be proven to be the
optimal value via hand calculations.
:::
