# README Lane–Emden Equation Solver (RK4) 
Astrophysics II FY3451

Numerical solver for the Lane–Emden equation using a custom 4th-order Runge–Kutta (RK4) integrator, with validation against known analytical solutions for selected polytropic indices.

## What this repo demonstrates
- Implementing a custom ODE solver (RK4) from scratch (no black-box solver)
- Working with coupled first-order systems derived from a second-order ODE
- Numerical stability considerations (handling the singular point at ξ = 0)
- Validation: comparing numerical results to analytical solutions for `n = 0, 1, 5`
- Scientific plotting and reproducible computation (NumPy + Matplotlib)
- Optional performance optimization using Numba JIT

## Problem background
The Lane–Emden equation describes the dimensionless structure of polytropic stellar models:

- `n = 1.5` is commonly used as an approximation for adiabatic/convective transport in main-sequence stars  
- `n = 3` is commonly used as an approximation for radiative transport  

This script computes numerical solutions for `n = 1.5` and `n = 3`, and plots them together with analytical solutions for:
- `n = 0`:  θ(ξ) = 1 − ξ²/6  
- `n = 1`:  θ(ξ) = sin(ξ)/ξ  
- `n = 5`:  θ(ξ) = 1 / sqrt(1 + ξ²/3)

## Implementation details
### ODE formulation
The Lane–Emden equation is written as a first-order system:

- `w[0] = θ(ξ)`
- `w[1] = dθ/dξ`

with derivative function `f_vector(ξ, w, n)`.

### Numerical method
- RK4 stepper: `RK4(w0, f_vector, dt, n, xi_end)`
- Uses a small non-zero start value `ξ₀ = 1e-4` to avoid division by zero in the derivative term.

## How to run
This code was originally written in a Jupyter/interactive style.

### Option A: Run in Jupyter
1. Open a notebook and paste/run the script cells
2. Ensure dependencies are installed:
```bash
pip install numpy matplotlib scipy numba
```

### Option B: Run as a Python script

If you convert it into a .py file, remove the Jupyter magic line:

```bash
delete %matplotlib inline
```

Then run:
```bash
python lane_emden_rk4.py
```

## Output

The script produces a plot titled “Solutions to Lane-Emden equation” comparing:
* analytical solutions for n = 0, 1, 5 (dashed)
* numerical RK4 solutions for n = 1.5, 3

## Notes / limitations

The plotting parameters are tuned for large figures and presentation-style readability. SciPy is imported but the main solver is intentionally not solve_ivp — the goal is to demonstrate a custom RK4 integrator.

## Course context

This implementation was created as part of FY3451 Astrophysics II (Home Exam, Sep–Oct 2023), specifically the task:

> Implement an ODE solver (e.g. Runge–Kutta) and solve the Lane–Emden equation for n = 1.5 and 3, and compare to analytical solutions for n = 0, 1, 5.
