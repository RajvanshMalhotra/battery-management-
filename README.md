## Abstract

This project develops a **Physics-Informed Neural Network (PINN)** to estimate the **State of Charge (SoC)** of a battery system using time-series IoT sensor data. The core motivation is to go beyond purely data-driven approaches by embedding known physical laws of battery behaviour directly into the model's learning objective, improving both accuracy and physical consistency of predictions.

---

## Problem Statement

Accurate SoC estimation is critical in battery-powered IoT systems. Traditional Coulomb counting methods accumulate error over time, while pure machine learning models lack physical interpretability and may produce physically implausible outputs (e.g., SoC > 100%). This work addresses both limitations by combining data-driven learning with physics-based constraints.

---

## Dataset

The model is trained on IoT sensor data (`saved_iot_new_data.csv`) containing the following features:

| Feature | Description |
|---|---|
| `current` | Instantaneous battery current (A) |
| `voltage` | Terminal voltage (V) |
| `temp` | Battery temperature |
| `dt_hours` | Time step duration (hours) |
| `ah_consumed` | Ampere-hours consumed in step |
| `total_ah_used` | Cumulative Ah drawn |
| `True_SoC` | Ground truth State of Charge (%) — target variable |

The data is normalized using `MinMaxScaler` and split into training (70%), validation (15%), and test (15%) sets.

---

## Model Architecture

A fully connected feedforward neural network with the following configuration:

- **Input layer**: 6 features
- **Hidden layers**: 2 × 32 neurons with ReLU activations
- **Output layer**: 1 neuron (predicted SoC)
- **Optimizer**: AdamW (lr=0.03, weight_decay=0.1)
- **Epochs**: 100 | **Batch size**: 64

---

## Physics Integration

The governing physical equation used is **Coulomb Counting**:

$$\frac{d(\text{SoC})}{dt} = -\frac{I}{Q_{\text{nominal}}} \times 100$$

Where `I` is current (A) and `Q_nominal = 16 Ah` is the assumed nominal battery capacity.

The **physics-informed loss** penalises:
1. **ODE residual**: violation of the Coulomb counting equation, computed via `torch.autograd.grad` on the `dt_hours` input
2. **Boundary constraints**: predictions outside the physical range [0%, 100%]

The total loss function is:

$$\mathcal{L}_{\text{total}} = \mathcal{L}_{\text{data}} + \lambda \cdot \mathcal{L}_{\text{physics}}$$

with `λ = 0.1`.

---



## Results

Model performance is evaluated on the held-out test set using MSE, MAE, and R² score, alongside visualisation of predicted vs. true SoC trajectories and decomposed physics loss components.

---

## Tech Stack

`Python` · `PyTorch` · `scikit-learn` · `pandas` · `matplotlib` · Google Colab

---

## Note: I have added two file ipynb and the py file 
