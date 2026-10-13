## EV Regenerative Braking System (RBS) Simulation

A beginner-friendly, proof-of-concept simulation model built in MATLAB/Simulink that demonstrates energy recovery dynamics in Electric Vehicles (EVs).

---

## 🏎️ What This Project Describes
This project simulates the **dynamic energy flow** inside an electric vehicle during two distinct phases of operation: driving and stopping. 

Instead of treating vehicle braking as purely mechanical waste (where energy is lost as heat through traditional brake pads), this model illustrates the principle of **energy conservation**. It tracks how a vehicle can reuse its own momentum to extend driving range, acting as a baseline reference tool for understanding modern EV powertrain efficiency.

---

## ⚙️ How the Application Works
The simulation mimics real-world automotive control logic over a 15-second timeline using sequential operating blocks:

1. **The Motoring Phase (0 to 5 seconds):** 
   The application simulates a vehicle cruising at a constant speed of **100 km/h**. The braking command signal is idle (`0`), meaning the battery is strictly providing energy or the vehicle is maintaining its state.

2. **The Braking Phase (5 to 10 seconds):** 
   At exactly 5 seconds, a simulated driver steps on the brake pedal (`Step block` triggers to `1`). The control system (`Switch block`) immediately cuts off the cruise signal and forces the vehicle into a steady deceleration ramp, dropping the speed by **16.2 km/h every second** until the vehicle stops.

3. **The Regenerative Energy Capture:** 
   While the car slows down, the algorithm combines the vehicle’s remaining speed and the active brake pressure (`Product block`). This calculated kinetic power is routed through an **85% efficiency factor** to simulate losses in the inverter and motor coils.

4. **Battery Recharging Pipeline:** 
   The recovered energy is continuously fed into a mathematical accumulator (`Integrator block`). This causes the battery's **State of Charge (SoC%)** curve to reverse direction and slope upwards, visually demonstrating the battery recovering charge out on the road.

---

## 📊 Core Architecture & Parameters

### Block Parameter Checklist

| Block Name | Dialog Parameter Field | Exact Input Value | Units / Operational Purpose |
| :--- | :--- | :--- | :--- |
| **Constant** | `Value` | `100.0` | km/h (Initial cruise speed) |
| **Step** | `Time` \| `Before` \| `After` | `5.0` \| `0.0` \| `1.0` | s \| Boolean braking command |
| **Ramp** | `Slope` \| `Start` \| `Initial` | `-16.2` \| `5.0` \| `100.0` | km/h/s \| s \| km/h |
| **Switch** | `Criteria` \| `Threshold` | `u2 >= Threshold` \| `0.5` | Logic Select \| Threshold |
| **Gain** | `Gain` | `0.85` | p.u. (85% recovery efficiency) |
| **Integrator** | `Initial` \| `Limit output` <br> `Upper` \| `Lower` | `50.0` \| Check `on` <br> `100.0` \| `0.0` | % SoC \| Saturation logic limits |

### Solver Environment Settings
- **Simulation Stop Time:** `15.0` seconds
- **Solver Type:** `Fixed-step`
- **Solver Algorithm:** `ode4 (Runge-Kutta)`
- **Fixed-step size:** `0.001` (1 millisecond resolution data logging)

---

## 🚀 How to Run
1. Download the `EV_Regen_Braking_Model.slx` file from this repository.
2. Launch **MATLAB** and open the **Simulink** interface.
3. Open the downloaded model file.
4. Click the green **Run** button on the top toolbar.
5. Double-click the **Scope** block to see the real-time interaction between the falling velocity curve and the rising battery percentage curve!


