# Adaptive Cruise Control Using a Sugeno Fuzzy Logic Controller

![MATLAB](https://img.shields.io/badge/MATLAB-R2024b-orange)
![Simulink](https://img.shields.io/badge/Simulink-Control%20Systems-blue)
![Fuzzy Logic](https://img.shields.io/badge/Fuzzy%20Logic-Sugeno-green)
![Project](https://img.shields.io/badge/Status-Completed-brightgreen)

---

## Overview

This project presents the design, implementation, and simulation of an **Adaptive Cruise Control (ACC)** system using a **Zero-Order Sugeno Fuzzy Logic Controller** developed in **MATLAB**, **Simulink**, and the **Fuzzy Logic Toolbox**.

The controller regulates an ego vehicle's longitudinal motion by maintaining a safe following distance behind a lead vehicle. Unlike traditional PID controllers, the fuzzy controller uses expert driving knowledge through linguistic rules based on **distance error** and **relative velocity**, producing smooth acceleration and braking commands under varying driving conditions.

The controller was evaluated under two different vehicle models with varying aerodynamic drag to demonstrate stability, robustness, and safe vehicle behavior.

---

# System Overview

<p align="center">
<img src="images/01-system-overview.png" width="1000">
</p>

The Adaptive Cruise Control system consists of:

- Lead Vehicle Model
- Ego Vehicle Dynamics
- Sugeno Fuzzy Controller
- Actuator Lag Model
- Aerodynamic Drag Model
- Vehicle Dynamics
- Closed-Loop Feedback

---

# Project Highlights

- Designed a Zero-Order Sugeno Fuzzy Logic Controller
- Built a nonlinear Adaptive Cruise Control model in Simulink
- Implemented actuator lag and aerodynamic drag models
- Designed custom fuzzy membership functions
- Developed a 15-rule fuzzy inference system
- Simulated realistic acceleration, braking, and re-acceleration events
- Compared controller performance under multiple vehicle configurations
- Achieved stable speed tracking with safe vehicle spacing

---

# Software Used

- MATLAB
- Simulink
- Fuzzy Logic Toolbox

---

# Controller Inputs

The fuzzy controller uses two input variables.

## Distance Error Membership Functions

Distance Error represents the difference between the desired safe following distance and the measured vehicle spacing.

<p align="center">
<img src="images/02-distance-mf.png" width="700">
</p>

Membership Functions:

- Very Close
- Close
- Safe
- Far
- Very Far

---

## Relative Velocity Membership Functions

Relative Velocity measures the speed difference between the lead vehicle and the ego vehicle.

<p align="center">
<img src="images/03-velocity-mf.png" width="700">
</p>

Membership Functions:

- Approaching
- Stable
- Moving Away

---

# Controller Output

The Sugeno controller outputs one of five acceleration commands.

| Output | Acceleration |
|---------|-------------:|
| Brake Hard | -4.0 m/s² |
| Brake Light | -0.8 m/s² |
| Maintain | 0.0 m/s² |
| Accelerate Light | 0.5 m/s² |
| Accelerate Hard | 3.0 m/s² (Case 1) / 2.5 m/s² (Case 2) |

---

# Fuzzy Rule Base

The controller consists of **15 expert driving rules** that determine throttle and braking behavior based on distance error and relative velocity.

Example rules include:

- If Distance is **Very Close** and Relative Velocity is **Approaching**, then **Brake Hard**
- If Distance is **Close** and Relative Velocity is **Stable**, then **Brake Light**
- If Distance is **Safe** and Relative Velocity is **Stable**, then **Maintain Speed**
- If Distance is **Far** and Relative Velocity is **Moving Away**, then **Accelerate Hard**
- If Distance is **Very Far** and Relative Velocity is **Moving Away**, then **Accelerate Hard**

These rules emulate human driving behavior while minimizing oscillations and maintaining safe vehicle spacing.

---

# Simulation Scenarios

Two different vehicle configurations were simulated to evaluate controller robustness.

---

# Case 1 – High Aerodynamic Drag

Vehicle Parameters

- Drag Coefficient: **0.003**
- Maximum Acceleration: **3.0 m/s²**

### Velocity Response

<p align="center">
<img src="images/04-velocity-case1.png" width="850">
</p>

The controller smoothly tracks the lead vehicle while maintaining stable behavior with minimal overshoot.

---

### Distance Response

<p align="center">
<img src="images/06-distance-case1.png" width="850">
</p>

The controller maintains a safe following distance throughout acceleration, braking, and re-acceleration events.

---

### Acceleration Response

<p align="center">
<img src="images/08-acceleration-case1.png" width="850">
</p>

The controller generates realistic acceleration and braking commands while respecting actuator limits.

---

# Case 2 – Low Aerodynamic Drag

Vehicle Parameters

- Drag Coefficient: **0.0004**
- Maximum Acceleration: **2.5 m/s²**

### Velocity Response

<p align="center">
<img src="images/05-velocity-case2.png" width="850">
</p>

The reduced aerodynamic drag results in faster acceleration and slightly larger overshoot while maintaining overall stability.

---

### Distance Response

<p align="center">
<img src="images/07-distance_case2.png" width="850">
</p>

Although the system experiences larger spacing variations, the controller successfully prevents unsafe following distances.

---

### Acceleration Response

<p align="center">
<img src="images/09-acceleration-case2.png" width="850">
</p>

Acceleration commands remain smooth and bounded while compensating for the reduced aerodynamic damping.

---

# Performance Comparison

| Performance Metric | Case 1 | Case 2 |
|--------------------|--------|--------|
| Velocity Overshoot | Low | Moderate |
| Settling Time | Moderate | Faster |
| Oscillation | Minimal | Slight |
| Ride Comfort | Excellent | Good |
| Tracking Accuracy | Excellent | Excellent |
| Safety | Excellent | Excellent |

---

# Skills Demonstrated

This project demonstrates practical experience with:

- MATLAB Programming
- Simulink Modeling
- Fuzzy Logic Control
- Sugeno Inference Systems
- Control Systems
- Vehicle Dynamics
- Adaptive Cruise Control
- Nonlinear Dynamic Systems
- Closed-Loop Feedback Control
- Engineering Simulation
- System Modeling
- Engineering Design

---

# Repository Structure

```
Adaptive-Cruise-Control-Fuzzy-Logic/
│
├── README.md
├── LICENSE
│
├── images/
│   ├── 01-system-overview.png
│   ├── 02-distance-mf.png
│   ├── 03-velocity-mf.png
│   ├── 04-velocity-case1.png
│   ├── 05-velocity_case2.png
│   ├── 06-distance_case1.png
│   ├── 07-distance_case2.png
│   ├── 08-acceleration_case1.png
│   └── 09-acceleration_case2.png
│
├── matlab/
│   ├── ACC_Controller.slx
│   ├── ACC_Fuzzy.fis
│   ├── createFIS.m
│   └── runSimulation.m
│
└── report/
    └── Adaptive_Cruise_Control_Report.pdf
```

---

# Running the Project

1. Open MATLAB.
2. Launch Simulink.
3. Open **ACC_Controller.slx**.
4. Ensure the **ACC_Fuzzy.fis** file is located in the project directory.
5. Run the simulation.
6. View the generated scope outputs for velocity, distance, error, and acceleration responses.

---

# Future Improvements

Potential future enhancements include:

- Sensor fusion using radar and LiDAR
- Model Predictive Control (MPC) comparison
- Adaptive membership function tuning
- Automatic rule optimization
- Hardware-in-the-loop (HIL) testing
- Real-time embedded implementation
- Lane keeping integration
- Autonomous vehicle path planning

---

# Report

A detailed technical report describing the controller design, fuzzy rule base, vehicle model, simulation setup, and performance evaluation is included in the **report/** directory.

---

# Author

**Nehorai Bachur**

Electrical Engineering Graduate

California State University, Northridge

---

## License

This project is licensed under the MIT License.
