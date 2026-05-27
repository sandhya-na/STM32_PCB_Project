# STM32_PCB_Project
This project contains the complete hardware design files for a custom 2-layer development board built around the STM32F103C8T6 microcontroller. I designed this entire board in KiCad.  My main goal for this project was to focus on real-world board performance—making sure the power lines are stable, the clock signal doesn't pick up electrical noise, and the ground layout is solid enough to prevent signal problems. This board is ready to be used as a reliable core module for robotics or automation setups.
# Design Choices & Technical Details. 
## 1. Power Supply Layout
For the power stage, I used an **AMS1117-3.3V** linear regulator to drop the incoming +5V power down to the +3.3V needed by the STM32 chip. Since these regulators can get pretty hot when running, I spent extra time planning the layout around it.
   - **Cooling Copper Zones**: I poured large areas of copper directly connected to the regulator's ground tab. This acts like a built-in heatsink to keep the regulator cool so it doesn't overheat.
   - **Thicker Power Traces**: I routed the main 3.3V and 5V lines using a wide 0.5mm track width instead of thin signal lines. This keeps the voltage steady and prevents drops when the chip draws sudden bursts of power.
   - **Decoupling Capacitor Placement**: I placed the 100 nF decoupling capacitors as close as physically possible to the STM32's VDD pins. I routed the tracks so that power flows into the capacitor pad first, and then into the chip pin, which helps filter out electrical noise perfectly.
## 2. Crystal Oscillator (Clock) Circuit
The external 8 MHz crystal acts as the heartbeat of the microcontroller. If this part of the circuit picks up noise, the whole chip can freeze or misbehave.
   - **Symmetrical Tracks**: I routed the two lines connecting the crystal to the chip with equal lengths and matching shapes. This ensures the clock signals stay perfectly in sync.
   - **Noise Isolation**: I kept this entire area clear of any other switching digital lines. I didn't route any other tracks underneath the crystal on either layer to prevent noise from leaking into the clock signal.
## 3. Ground Plane & Return Paths
In high-frequency digital circuits, current needs a quick, clean path to travel back to the ground. If the ground path is long and winding, it acts like an antenna and creates a lot of electrical noise.
    - **Solid Bottom Ground Plane**: I used a continuous, unbroken copper pour on the Bottom Layer (B.Cu) to act as a massive ground shield under the whole board.
    - **Dedicated Vias**: Instead of running long ground tracks on the top layer, every ground pad drops immediately down to the bottom ground plane using its own small via. This keeps the connections incredibly short and clean.
# What I Learned
  - **Manual Routing Control**: Hand-routing 100% of the tracks allowed me to plan exactly where current flows, ensuring my bottom ground plane didn't get chopped into pieces by crossing traces.
  - **Handling Bottlenecks**: I learned how to deal with tight spaces around small 0805 components by smoothly narrowing down traces just to pass the bottleneck, and then widening them back out for power capacity.
  - **Fixing DRC Errors**: Running the final Design Rules Check taught me how to fix real manufacturing issues, like snapping open edges on the board outline layer and clearing up solder mask alerts near the crystal pads.
