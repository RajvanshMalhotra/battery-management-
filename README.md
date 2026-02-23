---

# **Battery Management System with Machine Learning**

**Abstract**
Lead-acid batteries power the critical starting systems of over a billion vehicles worldwide, yet conventional voltage-based monitoring often fails to detect internal degradation until a sudden no start failure occurs. Addressing this gap, we present a low-cost, edge-native TinyML framework that performs accurate battery diagnostics directly on an ESP32 microcontroller  eliminating cloud dependency and enabling fully offline inference.

Our approach leverages a Physics block on top of a neural network to estimate State of Charge (SOC) and dynamically forecast Time-to-Empty (TTE) using real-time voltage, current, and temperature sensor data. By integrating physics-based constraints with data-driven learning, the model ensures both predictive accuracy and physical consistency.

A key innovation of this work is the introduction of a novel Virtual Cranking mechanism, which estimates internal resistance in real time and simulates a 200A engine start event to proactively predict potential no-crank failures. This safety-aware diagnostic layer enables pre-emptive alerts before critical battery failure occurs.

The deployed TinyML model achieves an R² score of 99.7%, demonstrating near-perfect alignment with true degradation patterns while remaining computationally efficient for resource-constrained embedded systems.

This work bridges the gap between physics-based battery diagnostics and edge-deployed machine learning, offering a scalable, energy-efficient, and production-ready solution for next-generation battery health monitoring.

---
