# Physics-Informed Neural Networks (PINNs) for Parameter Estimation in Nonlinear Differential Equations

## 📘 Project Overview

This project applies **Physics-Informed Neural Networks (PINNs)** to solve nonlinear differential equations and estimate system parameters, with a primary focus on the **damped harmonic oscillator** problem.

PINNs are neural networks that incorporate governing physical laws (differential equations) into their training loss. This approach offers a modern alternative to traditional numerical methods, which often require heavy computation and abundant clean data.

By embedding the physical laws directly into the learning process, PINNs produce models that are both **data-efficient** and **physically consistent**.

In this thesis-based project, we demonstrate how an *inverse PINN* can learn unknown parameters (like damping and stiffness in an oscillator) directly from trajectory data, yielding accurate solutions even with limited or noisy data.
