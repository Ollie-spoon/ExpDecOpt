# Exponential Decay Fitting with JIT-Optimized Solvers

This repository contains a single Python file designed for efficient fitting of multi-exponential decay models to patient data from NMR scans of skeletal muscles. The code includes JIT-compiled solvers for optimization and a JIT-compiled bootstrapping method for calculating confidence intervals.

## Features
- **Efficient Optimization**: Implements BFGS, a quasi-Newton optimization method, to handle the wide trough-like loss landscapes common in exponential decay fitting.
- **Hierarchical Fitting**: Uses a progressive approach, starting with a single decay, then leveraging those results to fit bi-exponential and multi-exponential models.
- **Sampling-Based Global Optimization**: Employs a local sampling strategy to identify candidate starting points, ensuring convergence to the global minimum.
- **Bootstrapping for Confidence Intervals**: Generates robust confidence intervals using a JIT-compiled bootstrapping method, providing statistical reliability to the fitted parameters.

## Why This Approach?
Newton and quasi-Newton methods excel in minimizing loss functions with wide, trough-like landscapes, such as:

```math
f(x, y) = x^2 + \frac{y^2}{1000}
```

However, these methods are local optimizers and may converge to suboptimal minima without good initial guesses. By sampling starting points:
- Begin with a single decay, which typically has a single minimum.
- Use the results to generate starting points for bi-exponential fitting.
- Extend to tri-exponential fitting, using the results iteratively.

The physical constraints of NMR data (e.g., all amplitudes and decay constants must be positive) make this hierarchical sampling approach particularly effective.
