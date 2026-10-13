# EV Regenerative Braking System (RBS) Simulation

A simple, beginner-friendly proof-of-concept simulation model built in MATLAB/Simulink.

## Project Overview
This model demonstrates how kinetic energy is captured during vehicle deceleration and converted back into electrical energy to recharge an EV battery.

## Block Parameter Settings
- **Cruising Speed:** 100 km/h
- **Brake Event Time:** 5.0 seconds
- **Deceleration Rate:** -16.2 km/h/s
- **System Efficiency:** 85%
- **Initial Battery State of Charge (SoC):** 50%

## How to Run
1. Download the `EV_Regen_Braking_Model.slx` file.
2. Open it in MATLAB/Simulink.
3. Set the simulation stop time to `15.0` seconds and click **Run**.
4. Open the **Scope** block to view the speed drop and battery charging curves.

