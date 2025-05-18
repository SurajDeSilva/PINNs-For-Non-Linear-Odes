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

## 🔬 Experiments and Case Studies

This project includes several experiments to test the performance, accuracy, and generalization of the PINN approach.

### 1️⃣ Simple Nonlinear ODE
- Solved `dy/dt = α*y² - β*y` using inverse PINN.
- Demonstrated that the network can learn unknown parameters (`α`, `β`) from sparse, synthetic data.
- Compared PINN predictions with analytical and numerical solutions.

### 2️⃣ Damped Harmonic Oscillator (Main Case Study)
- Solved `m * d²x/dt² + μ * dx/dt + k * x = 0` using inverse PINN.
- Objective: estimate damping coefficient (`μ`) and stiffness (`k`) directly from displacement data.
- Two scenarios tested:
  - **Homogeneous** system (no external forcing).
  - **Non-homogeneous** system with external sinusoidal forcing: `A * sin(ωt)`.

### 🔁 In-Range vs. Out-of-Range Testing
- **In-range**: PINN trained and tested on the same time domain (e.g., `t = 0–30s`).
- **Out-of-range**: Trained on initial range (e.g., `t = 0–30s`), tested on future range (`t = 30–60s`).
- Inverse PINN generalized well to future time intervals, while forward PINN did not.

### 🧪 Sensitivity to Noise and Sample Size
- Evaluated performance under increasing levels of Gaussian noise in the training data.
- Tested model accuracy across varying numbers of training samples.
- Observed that inverse PINNs remain robust and accurate with small data and mild noise.

### ⚖️ Comparison with Traditional Method
- Benchmarked against the **Multiple Shooting Method (MSM)** for parameter estimation.
- PINN outperformed MSM in noisy and sparse data scenarios, offering better generalization and requiring fewer assumptions.

## 📊 Results Summary

### ✅ Parameter Estimation Accuracy
- Inverse PINN estimated system parameters with **< 2% error**.
- Achieved **RMSE ≈ 0.00285** on test data, even for future time intervals not included in training.

### 🔮 Generalization Ability
- Inverse PINN accurately predicted system behavior **outside the training range**.
- Forward PINN failed to extrapolate effectively (RMSE ≈ 0.42 in out-of-range testing).

### 🧱 Robustness to Noise
- Maintained strong performance with **moderate Gaussian noise** in training data.
- At low noise levels (≤ 0.02), parameter estimates remained stable.
- Performance degraded gracefully with increasing noise, especially in damping coefficient (μ).

### 📉 Data Efficiency
- High accuracy achieved with **very limited training data** (as few as ~10 samples).
- Forward PINN required significantly more data and still failed to generalize.

### ⚖️ Comparison with Multiple Shooting Method
- Inverse PINN matched or outperformed MSM in clean-data scenarios.
- Under noisy or sparse data conditions, **PINN was more robust and stable**.
- MSM required good initial guesses and more tuning; PINN was more adaptable.

### 🌐 Complex System Handling
- Successfully modeled a **non-homogeneous damped oscillator** with external forcing.
- Demonstrated flexibility of PINNs in real-world, time-dependent, and non-linear systems.

## 🧾 Conclusion

This project demonstrates the potential of **Physics-Informed Neural Networks (PINNs)** as a powerful tool for solving nonlinear differential equations and estimating physical parameters in dynamical systems.

By embedding physical laws directly into the learning process, PINNs achieve strong generalization, high accuracy, and robustness—even with limited or noisy data. The successful estimation of parameters like damping and stiffness in a damped harmonic oscillator shows that PINNs can outperform traditional methods such as the Multiple Shooting Method.

With their ability to handle inverse problems, extrapolate beyond training data, and operate efficiently with small datasets, PINNs offer a modern approach for real-world engineering, physics, and system identification challenges.

This work highlights the promise of PINNs for future applications in scientific computing, modeling, and digital twin systems.


