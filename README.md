# Physics-Informed Neural Networks (PINNs) for Parameter Estimation in Nonlinear Differential Equations

## 📘 Project Overview

This project applies **Physics-Informed Neural Networks (PINNs)** to solve nonlinear differential equations and estimate system parameters, with a primary focus on the **damped harmonic oscillator** problem.

PINNs are neural networks that incorporate governing physical laws (differential equations) into their training loss. This approach offers a modern alternative to traditional numerical methods, which often require heavy computation and abundant clean data.

By embedding the physical laws directly into the learning process, PINNs produce models that are both **data-efficient** and **physically consistent**.

In this thesis-based project, we demonstrate how an *inverse PINN* can learn unknown parameters (like damping and stiffness in an oscillator) directly from trajectory data, yielding accurate solutions even with limited or noisy data.

## 🧠 Key Contributions

- **Inverse PINN for Parameter Estimation**  
  Developed an **inverse PINN** approach to estimate parameters of a nonlinear dynamical system (damped mass-spring-damper oscillator) directly from data. The PINN treats physical parameters (damping coefficient μ, stiffness k) as trainable variables.

- **High Accuracy and Robustness**  
  Accurately recovered oscillator parameters with errors below 6%. Achieved **RMSE ≈ 0.00285** on predictions, including generalization to future time ranges. Maintained performance even under moderate noise levels.

- **Superior Generalization vs. Baselines**  
  Outperformed both **forward PINNs** and the **Multiple Shooting Method** in predicting system behavior outside the training interval. Inverse PINNs generalize better due to their embedded physics.

- **Demonstrated Data Efficiency**  
  Achieved high accuracy with very limited training data. Inverse PINNs needed fewer samples compared to traditional methods and forward models.

- **Case Studies and Realistic Scenarios**  
  Validated the approach on both simple nonlinear ODEs and realistic damped oscillators (including non-homogeneous systems with external forcing), showing adaptability to real-world dynamics.

 ## 🏗️ Architecture and Methods

### 🔧 Neural Network Architecture
- Fully-connected feedforward neural network.
- Input: scalar time `t`; Output: scalar displacement `x(t)`.
- Architecture: 5 hidden layers with **Tanh** activation functions.
- Built using **PyTorch**, leveraging automatic differentiation for computing derivatives.

### 🧮 Physics-Informed Loss Function
The total loss combines three components:

- **Physics Loss (`L_physics`)**:  
  Penalizes violations of the governing ODE:  
  `m * d²x/dt² + μ * dx/dt + k * x = 0`

- **Data Loss (`L_data`)**:  
  Measures the mean squared error between predicted and observed displacement values.

- **Initial Condition Loss (`L_initial`)**:  
  Ensures the network satisfies known initial displacement and velocity values.

- **Total Loss Function**:  
  `L_total = λ1 * L_physics + λ2 * L_data + λ3 * L_initial`

### ⚙️ Optimization
- Optimizer: **Adam**
- Techniques: Learning rate scheduling, early stopping, and weight decay.
- Input normalization and gradient clipping used for stability.
- Physical parameters `μ` and `k` are trainable during optimization.

### 🧪 Two-Input Architecture
- For non-homogeneous systems, an additional input (e.g., `sin(t)`) is added.
- Helps model systems with external forcing like:  
  `m * d²x/dt² + μ * dx/dt + k * x = A * sin(ωt)`



