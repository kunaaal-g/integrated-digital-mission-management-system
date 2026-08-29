# Integrated Digital Mission Management System

A digital logic-based mission management system designed to demonstrate how mission sequencing, sensor validation, decision-making, fault detection, and telemetry indication can be implemented using conventional 74xx-series digital logic ICs.

The system is organized into six functional phases, beginning with a mission timing signal and progressing through mission-state generation, sensor validation, decision logic, fault detection, and telemetry indication.

---

## 📌 Project Overview

The **Integrated Digital Mission Management System** is a sequential and combinational digital logic architecture that models the control flow of a mission-management system.

Instead of using a microcontroller or processor, the system uses discrete TTL logic ICs to implement:

- Mission timing
- Mission-state sequencing
- Sensor condition monitoring
- Boolean decision logic
- State memory
- Fault detection and memory
- Mission-status indication

The project demonstrates the integration of **counters, decoders, logic gates, and flip-flops** into a single coordinated digital system.

> **Note:** This project is an educational digital-logic model and is not intended for use as an actual aerospace flight-control or safety-critical system.

---

## 🎯 Objectives

The main objectives of this project are:

1. Generate a controlled mission timing sequence.
2. Decode timing states into individual mission events.
3. Monitor multiple simulated subsystem conditions.
4. Determine whether required mission conditions are satisfied.
5. Implement sequential decision logic.
6. Detect and retain fault conditions.
7. Display mission status through a telemetry panel.
8. Demonstrate the integration of combinational and sequential digital logic.

---

## 🏗️ System Architecture

The complete system is divided into six functional phases:
                    ┌─────────────────────┐
                    │   Mission Clock     │
                    │       5 Hz          │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Phase 1             │
                    │ Mission Timer       │
                    │ 74LS93              │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Phase 2             │
                    │ Mission Sequencer   │
                    │ 74154               │
                    └──────────┬──────────┘
                               │
                 ┌─────────────┴─────────────┐
                 │                           │
                 ▼                           ▼
       ┌─────────────────────┐     ┌─────────────────────┐
       │ Phase 3             │     │ Mission State       │
       │ Sensor Monitoring   │     │ Information         │
       │                     │     │                     │
       │ GPS                 │     └──────────┬──────────┘
       │ Gyroscope           │                │
       │ Accelerometer       │                │
       │ Battery             │                │
       │ Temperature         │                │
       │ Communication       │                │
       └──────────┬──────────┘                │
                  │                           │
                  └─────────────┬─────────────┘
                                ▼
                    ┌─────────────────────┐
                    │ Phase 4             │
                    │ Decision Logic      │
                    │ 74LS74 / 74LS04     │
                    │ 74LS08              │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Phase 5             │
                    │ Fault Detection     │
                    │ & Fault Memory      │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Phase 6             │
                    │ Telemetry Panel     │
                    └─────────────────────┘
🔹 Phase 1 — Mission Timer

The first stage generates the timing sequence used by the mission-management system.

A 74LS93 binary counter is used to count the incoming clock pulses.

Main components
5 Hz clock source
74LS93 binary counter
Reset circuitry

The counter generates binary state information that is passed to the mission sequencer.

Purpose

The mission timer provides a deterministic sequence that can be used to represent the progression of different mission events.

🔹 Phase 2 — Mission Sequencer

The mission sequencer converts the binary counter output into individual mission-state signals.

A 74154 4-to-16 line decoder is used for state decoding.

The decoded outputs represent different mission events.

Mission states
Output	Mission State
X2	POWER ON
X3	SELF TEST
X4	NAVIGATION
X5	MISSION LAUNCH
X6	MISSION ABORT
X7	MISSION FROZEN
X8	STAGE SEPARATION
X9	PAYLOAD DEPLOY

Additional telemetry outputs are used for system-status indication.

The decoder allows a binary state to be converted into a one-of-many mission event representation.

🔹 Phase 3 — Sensor Monitoring

The sensor-monitoring subsystem evaluates multiple simulated system conditions.

The monitored inputs include:

GPS
Gyroscope
Accelerometer
Battery
Temperature
Communication

Logic gates are used to combine these signals and determine whether the required conditions are satisfied.

Logic components
74LS08 — Quad 2-input AND gate
74LS32 — Quad 2-input OR gate

The sensor conditions are combined to generate system-level status signals such as:

GPS
 │
 ▼
GPS condition ─────┐
                   │
Gyroscope ─────────┤
                   │
Accelerometer ─────┤
                   ├──► Sensor Validation
Battery ───────────┤
                   │
Temperature ───────┤
                   │
Communication ─────┘

The resulting sensor-status logic is used by the decision-making stage.

🔹 Phase 4 — Decision Logic

The decision-logic subsystem combines:

Mission-state information
Sensor-status information
Control conditions
Stored state information

The subsystem uses sequential logic to maintain decision states.

Main components
74LS74 — Dual D-type flip-flop
74LS04 — Hex inverter
74LS08 — Quad 2-input AND gate

The flip-flops provide state memory, allowing the system to retain information beyond a single combinational logic evaluation.

This stage is responsible for determining conditions such as:

Mission State
      │
      ├───────────────┐
      │               │
      ▼               ▼
Sensor Status     Control Logic
      │               │
      └───────┬───────┘
              ▼
       Decision Logic
              │
              ▼
       Stored Decision
🔹 Phase 5 — Fault Detection

The fault-detection stage monitors system conditions and provides a mechanism for retaining a detected fault.

A fault condition can be represented by a digital logic signal and stored using sequential logic.

Fault-memory concept
Fault Condition
      │
      ▼
Fault Detection
      │
      ▼
Fault Memory
      │
      ├──────────────► FAULT MEMORY
      │
      ▼
Mission Decision Logic

The fault-memory mechanism allows the system to retain a fault indication until the appropriate reset condition is applied.

This demonstrates the concept of fault latching, which is commonly used in digital control and monitoring systems.

🔹 Phase 6 — Telemetry Panel

The final stage provides visual mission-status outputs.

The telemetry panel represents the current state of the mission-management system.

Telemetry outputs
Signal	Indication
X12	POWER ON
X13	SELF TEST
X14	NAVIGATION
X15	READY TO LAUNCH
X16	MISSION LAUNCH
X17	MISSION ABORT
X18	MISSION FROZEN
X19	STAGE SEPARATION
X20	PAYLOAD DEPLOY
X21	FAULT MEMORY

These outputs provide a simple human-readable representation of the internal digital state of the system.

🧩 Major Components
IC / Component	Function
74LS93	Binary counter / mission timer
74154	4-to-16 line decoder
74LS08	AND logic
74LS32	OR logic
74LS04	NOT / inversion logic
74LS74	D-type flip-flop / state memory
Clock Source	Mission timing
5 V Supply	TTL logic power
Indicators	Mission telemetry
📐 Digital Logic Concepts Demonstrated

This project combines several fundamental concepts of digital electronics:

Combinational Logic
AND gates
OR gates
NOT gates
Boolean decision logic
Sensor-condition validation
Sequential Logic
Binary counters
State sequencing
D-type flip-flops
State memory
Fault latching
System-Level Concepts
Event sequencing
State decoding
Condition monitoring
Decision making
Fault detection
Telemetry indication
🔄 Mission Sequence

The overall conceptual sequence is:

POWER ON
   │
   ▼
SELF TEST
   │
   ▼
NAVIGATION
   │
   ▼
READY TO LAUNCH
   │
   ▼
MISSION LAUNCH
   │
   ├──────────────► MISSION ABORT
   │
   ▼
STAGE SEPARATION
   │
   ▼
PAYLOAD DEPLOY

Abnormal conditions can result in alternate states such as:

                ┌──► MISSION ABORT
                │
Mission State ──┼──► MISSION FROZEN
                │
                └──► FAULT MEMORY

The exact state transition depends on the implemented logic conditions.

🖥️ Complete Schematic

The complete integrated digital circuit is shown below.

🧪 Testing Strategy

The system can be tested phase-by-phase rather than testing the complete circuit simultaneously.

Test 1 — Clock and Counter

Verify that the 74LS93 produces the expected binary count sequence.

Test 2 — State Decoder

Verify that the 74154 activates the expected decoded state for each counter condition.

Test 3 — Sensor Logic

Apply different combinations of sensor inputs and verify the resulting sensor-status outputs.

Test 4 — Decision Logic

Verify that the correct decision is generated for valid and invalid mission conditions.

Test 5 — Fault Detection

Introduce a fault condition and verify that the fault-memory output responds correctly.

Test 6 — Telemetry

Verify that each mission state produces the corresponding telemetry indication.

📊 Expected System Behavior

Under normal operating conditions, the system should progress through its predefined mission states according to the generated timing sequence.

When the required sensor conditions are satisfied:

Valid Conditions
       │
       ▼
Sensor Validation
       │
       ▼
Decision Logic
       │
       ▼
Next Mission State

When an abnormal condition is detected:

Abnormal Condition
       │
       ▼
Fault Detection
       │
       ▼
Fault Memory
       │
       ▼
Mission Status / Decision
📁 Repository Structure
integrated-digital-mission-management-system/
│
├── README.md
│
├── schematic/
│   └── integrated-mission-management-system.png
│
├── documentation/
│   ├── phase-1-mission-timer.md
│   ├── phase-2-mission-sequencer.md
│   ├── phase-3-sensor-monitoring.md
│   ├── phase-4-decision-logic.md
│   ├── phase-5-fault-detection.md
│   └── phase-6-telemetry-panel.md
│
├── simulation/
│   ├── multisim/
│   └── screenshots/
│
├── testing/
│   ├── test-cases.md
│   └── truth-tables.md
│
└── images/
    └── system-overview.png
🚀 Future Improvements

The system can be further developed by adding:

Formal Boolean-equation analysis
Complete truth tables
Timing-diagram analysis
Fault-injection testing
Automated test cases
Hardware implementation
PCB implementation
FPGA implementation
Microcontroller-based comparison
Mission-state logging
More detailed telemetry
Hardware-in-the-loop testing
🎓 Learning Outcomes

Through this project, the following concepts are demonstrated:

Digital system architecture
TTL logic families
Combinational logic design
Sequential logic design
Counters
Decoders
Flip-flops
Boolean logic
Sensor-condition validation
Fault-memory circuits
State-based system design
System integration
Digital testing and debugging
🛠️ Technology

Hardware / Digital Logic

74LS93
74154
74LS08
74LS32
74LS04
74LS74
5 V TTL logic

Design / Simulation

Digital circuit simulation
Logic analysis
Timing analysis
👨‍💻 Author

Kunal Nitin Gadhave

Mechatronics Engineering
SVPM's College of Engineering, Malegaon (Bk.), Baramati, Maharashtra, India

📜 License

This project is intended for educational, academic, and experimental purposes.

⭐ Project Status

Status: In Development

The digital architecture and major functional phases have been designed. Further work includes detailed verification, simulation validation, test-case documentation, and hardware-level validation.

Keywords

Digital Electronics Digital Logic 74LS93 74154 74LS74 TTL Logic Mission Management Fault Detection Telemetry Sequential Logic Combinational Logic Sensor Monitoring Mechatronics Control Systems Embedded Systems
