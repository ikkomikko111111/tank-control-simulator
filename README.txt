TANK LEVEL CONTROL AND FAULT MONITORING SIMULATOR

PROJECT OVERVIEW
A browser-based simulation of tank filling and pump control.
It demonstrates automatic/manual operation, protective
interlocks, fault handling, and event logging.

TECHNOLOGIES
HTML, CSS, JavaScript.

HOW TO RUN
Open index.html in a modern web browser.
No installation or internet connection is required.

CONTROL LOGIC
Automatic mode:
- Pump starts when tank level is below 30%.
- Pump stops when tank level reaches or exceeds 80%.
- Between these limits, the pump retains its previous state.

Manual mode:
- Operator starts and stops the pump.
- Protective interlocks remain active.

PROTECTION FEATURES
- High-high level: trips at 90% or above.
- Source tank empty: stops the pump to simulate dry-run prevention.
- Sensor failure: displays INVALID and stops the pump.
- All faults latch a trip.
- Reset is rejected while any fault remains active.
- After faults clear, the operator must reset the trip.
- In automatic mode, the pump may restart after reset if level
  is below 30%.
- In manual mode, a fresh start command is required.

SIMULATION MODEL
- Pump inflow: 5 percentage points per simulated second.
- Open-outlet outflow: 2 percentage points per simulated second.
- Update interval: 0.2 simulated seconds.
- Level is limited to 0–100%.
- Pause freezes time and water movement; controls remain active.
- The high-high switch uses simulated physical level independently
  of the main level sensor's fault state.

MANUAL TEST RESULTS
The following checks passed during user-operated testing:

1. Automatic hysteresis:
   At 20%, 50%, 80%, then 50%, pump states were
   ON, ON, OFF, OFF.

2. Manual-mode overflow protection:
   At 95%, the pump stopped and reset was rejected.
   Lowering the level and resetting cleared the trip.
   A new manual start command restarted the pump.

3. Source-empty protection:
   The fault stopped the pump and blocked reset.
   Clearing the fault, resetting, and issuing a manual start
   restored operation.

4. Sensor-failure protection:
   Sensor displayed INVALID and the pump stopped.
   Reset was blocked until the fault was cleared.

5. Combined faults in automatic mode:
   Both faults stopped the pump.
   Clearing only one fault did not permit reset.
   Clearing both and resetting at 20% restarted the pump.

PROJECT FILES
- index.html: simulator source code and interface.
- tank_control_event_log.csv: exported simulation events.
- README.txt: project description and test summary.
- Screenshot(s): interface evidence.

LIMITATIONS
This is an educational browser simulation, not a PLC program.
It does not connect to physical sensors, pumps, or industrial systems.
Faults are manually injected rather than detected from real hardware.
Simulated results do not establish real-world accuracy or safety.
Browser timing may differ from real elapsed time.

DEVELOPMENT APPROACH
Built with AI-assisted code generation and guidance.
Manually executed and checked against the scenarios listed above.