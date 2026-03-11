# Aircraft Longitudinal Control System Design

This repository contains the implementation of a longitudinal flight control system for a fighter aircraft similar to the **Mirage III class**. The project was developed as part of the **Aircraft Control course at IPSA**.

The objective is to model the aircraft dynamics, analyze the natural flight modes, and design an autopilot composed of several feedback control loops.

## Author

Gabriel Casarotto  
IPSA – Institut Polytechnique des Sciences Avancées  
Academic year 2025–2026

## Project Overview

The project focuses on the **longitudinal dynamics of an aircraft** under the following assumptions:

- Symmetrical flight in the vertical plane
- No sideslip or roll motion
- Thrust aligned with the aircraft longitudinal axis
- Perfect auto-throttle maintaining constant speed

The aircraft considered has characteristics comparable to a **Mirage III fighter aircraft**, with aerodynamic coefficients depending on the Mach number.

## Objectives

The main objectives of the project are:

1. Determine the **equilibrium flight conditions** for a given operating point.
2. Derive the **linearized state-space model** of the aircraft.
3. Analyze the **open-loop dynamic modes**:
   - Short-period mode
   - Phugoid mode
4. Design a **multi-loop autopilot controller**.
5. Simulate flight phases such as ascent, cruise, and descent.

## Aircraft Dynamic Model

The aircraft dynamics are modeled using a **linear state-space representation** around the equilibrium point.

Initial state vector: X = (V, γ, α, q, θ, z)

After introducing a perfect auto-throttle, the velocity state is removed and the system becomes: X = (γ, α, q, θ, z)

Control input: U = δm

where δm represents the control surface deflection.

## Control System Architecture

The autopilot is designed progressively using three feedback loops.

### 1. Pitch Rate Control (q feedback)

A gyrometric feedback loop is introduced to stabilize the aircraft and increase damping of the short-period mode.

The gain **Kr** is tuned to obtain a damping ratio: ξ = 0.65

### 2. Flight Path Angle Control (γ feedback)

A second feedback loop controls the **flight path angle γ**.

The controller gain **Kγ** is tuned to achieve:

- Gain margin ≥ 7 dB
- Phase margin ≥ 30°
- Overshoot ≤ 5%
- Settling time optimized

### 3. Altitude Control (z feedback)

A third feedback loop regulates the **aircraft altitude** using the altitude sensor model.

The controller gain **Kz** is chosen to obtain:

- Overshoot ≤ 5%
- Well-damped pseudo-periodic modes
- Optimized settling time

## Saturation Analysis

A saturation is introduced on the flight path angle command.

The maximum admissible flight path angle is determined by limiting the **maximum load factor**: Δnz = 3 g

A **bisection method** is used to determine the maximum command input ensuring that the incidence angle does not exceed the allowed limit.

## Flight Management Simulation

A final simulation script links several flight phases:

1. **Climb phase** using flight path angle control
2. **Cruise phase** with altitude hold
3. **Descent phase**
4. **Final flare and level flight**

Different command profiles are tested:

- Step commands
- Ramp commands
- Exponential flare profiles

## Tools and Libraries

The implementation uses Python and the control systems ecosystem:

- `numpy`
- `matplotlib`
- `python-control`
- `slycot`

The **sisotool functionality** is used to tune controller gains.

## Academic Context

This project was completed during the **Aircraft Control course at IPSA**, focusing on aircraft longitudinal dynamics and autopilot design.
