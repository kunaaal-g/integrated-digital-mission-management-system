# Integrated Digital Mission Management System Using TTL Logic

### A Simplified Launch-Vehicle Mission Computer Realised Entirely in Discrete Digital Logic

![Project Schematic]
<img width="2200" height="1700" alt="iddms-1" src="https://github.com/user-attachments/assets/e703be2d-4ad6-4c4a-bd13-22ff8640d3f1" />


---

## 📌 Overview

The **Integrated Digital Mission Management System** is a simplified digital mission-management architecture developed using **74LS-series TTL (Transistor-Transistor Logic) integrated circuits**.

The project demonstrates how fundamental digital logic circuits can be integrated to perform simplified mission-management functions such as:

* Mission timing
* Sequential mission-phase control
* Sensor-status monitoring
* Redundant sensor decision-making
* Majority voting
* Mission decision logic
* Fault detection
* Fault memory
* Digital mission-status indication

Unlike modern mission computers that rely on microprocessors, microcontrollers, FPGAs, and embedded software, this project implements the core logic using **discrete TTL digital ICs**.

The system was designed and simulated using **NI Multisim** as an educational demonstration of how complex control-oriented functions can be constructed from fundamental digital logic blocks.

> **Note:** This project is an academic simulation and is not a flight-qualified or safety-critical mission computer.

---

# 🎯 Project Objectives

The main objectives of this project are:

1. Design a simplified mission-management system using discrete TTL logic.
2. Understand the practical operation of counters, decoders, logic gates, and flip-flops.
3. Implement a sequential mission-control architecture.
4. Demonstrate **2-out-of-3 (2oo3) majority voting** for redundant sensor inputs.
5. Implement mission decision and fault-detection logic.
6. Demonstrate digital fault-memory functionality.
7. Provide visual mission-status indication through a telemetry panel.
8. Simulate and verify the complete digital architecture using **NI Multisim**.

---

# 🏗️ System Architecture

The complete system is divided into six major functional sections:

```text
                 ┌─────────────────────────┐
                 │      Mission Timer      │
                 │        74LS93           │
                 └────────────┬────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │    Mission Sequencer    │
                 │        74LS154          │
                 └────────────┬────────────┘
                              │
                              ▼
              ┌────────────────────────────────┐
              │        Mission States          │
              │                                │
              │ Launch / Abort / Frozen        │
              │ Stage Separation / Deployment  │
              └───────────────┬────────────────┘
                              │
                              ▼
       ┌────────────────────────────────────────────┐
       │             Sensor Monitoring              │
       │                                            │
       │ GPS │ Gyroscope │ Accelerometer            │
       │ Battery │ Temperature │ Communication      │
       └──────────────────────┬─────────────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │    Majority Voter       │
                 │        2-out-of-3       │
                 └────────────┬────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │     Decision Logic      │
                 │        74LS74           │
                 └────────────┬────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │     Fault Detection     │
                 │      Fault Memory       │
                 └────────────┬────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │     Telemetry Panel     │
                 │    Mission Indicators   │
                 └─────────────────────────┘
```

---

# ⏱️ Phase 1 — Mission Timer

The mission timer generates the digital timing sequence used to progress through different mission states.

A **74LS93 binary counter** is used with a digital clock source to generate sequential binary states.

### Main Components

* 74LS93 binary counter
* 5 Hz clock source
* Reset logic
* TTL logic

The counter output provides the digital timing information required by the mission sequencer.

---

# 🔢 Phase 2 — Mission Sequencer

The mission sequencer converts the binary counter states into individual mission-phase signals.

A **74LS154 4-to-16 line decoder** is used to decode the counter outputs into individual digital states.

The decoded states represent simplified mission events such as:

* Ready to Launch
* Power On
* Self Test
* Navigation
* Mission Launch
* Mission Abort
* Mission Frozen
* Stage Separation
* Payload Deployment

This demonstrates the fundamental concept of converting a binary state representation into individual control signals.

---

# 📡 Phase 3 — Sensor Monitoring

The sensor-monitoring section evaluates simulated mission-critical sensor inputs.

The project includes simulated inputs representing:

* GPS
* Gyroscope
* Accelerometer
* Battery
* Temperature
* Communication

Digital logic gates are used to combine and evaluate the sensor states.

A key feature of this section is **redundant sensor decision-making using majority voting**.

---

# 🔁 Triple Redundancy Majority Voting

Three redundant sensor channels are used to demonstrate a basic **2-out-of-3 (2oo3) voting architecture**.

The majority-voting equation is:

$$
M = AB + AC + BC
$$

Where:

* \(A\) = Sensor Channel A
* \(B\) = Sensor Channel B
* \(C\) = Sensor Channel C
* \(M\) = Majority-voter output
* \(+\) = OR operation
* Juxtaposition = AND operation

The output becomes HIGH when **at least two of the three sensor channels are HIGH**.

### Truth Table

| A | B | C | Majority Output |
| - | - | - | --------------- |
| 0 | 0 | 0 | 0               |
| 0 | 0 | 1 | 0               |
| 0 | 1 | 0 | 0               |
| 0 | 1 | 1 | 1               |
| 1 | 0 | 0 | 0               |
| 1 | 0 | 1 | 1               |
| 1 | 1 | 0 | 1               |
| 1 | 1 | 1 | 1               |

This illustrates the basic principle of **redundancy-based decision-making**, where one disagreeing channel does not necessarily determine the final decision.

---

# 🧠 Phase 4 — Decision Logic

The decision-logic section combines information from:

* Mission sequence
* Sensor status
* Majority-voter output
* Control conditions

The resulting logic determines whether the simplified mission sequence can proceed or whether a corresponding mission-state signal should be generated.

**74LS74 D-type flip-flops** are used to provide sequential behavior and state retention where required.

This demonstrates the difference between:

* **Combinational logic** — output depends on present inputs.
* **Sequential logic** — output can depend on previous system state.

---

# ⚠️ Phase 5 — Fault Detection

The fault-detection subsystem monitors abnormal digital conditions and stores the detected fault state.

**74LS74 D-type flip-flops** are used as digital storage elements to implement a basic **Fault Memory** function.

Once a fault condition is detected, the fault indication can be retained as a digital state rather than disappearing immediately when the original input condition changes.

This demonstrates the basic principle of **latched fault indication** used in digital monitoring and control systems.

---

# 📊 Phase 6 — Telemetry Panel

The telemetry panel provides visual indication of the simulated mission state.

The project includes digital outputs representing the following mission-status signals:

| Output | Mission Status   |
| ------ | ---------------- |
| X1     | Ready to Launch  |
| X2     | Power On         |
| X3     | Self Test        |
| X4     | Navigation       |
| X5     | Mission Launch   |
| X6     | Mission Abort    |
| X7     | Mission Frozen   |
| X8     | Stage Separation |
| X9     | Payload Deploy   |
| X10    | Navigation OK    |
| X11    | Fault Memory     |
| X12    | Power On         |
| X13    | Self Test        |
| X14    | Navigation       |
| X15    | Ready to Launch  |
| X16    | Mission Launch   |
| X17    | Mission Abort    |
| X18    | Mission Frozen   |
| X19    | Stage Separation |
| X20    | Payload Deploy   |
| X21    | Fault Memory     |

The outputs are represented using digital indicators within the Multisim simulation.

---

# 🔧 Hardware / Logic Components

The design primarily uses components from the **74LS TTL logic family**.

| IC          | Function                                 |
| ----------- | ---------------------------------------- |
| **74LS93**  | Binary counter / mission timer           |
| **74LS154** | 4-to-16 line decoder / mission sequencer |
| **74LS08**  | Quad 2-input AND gate                    |
| **74LS32**  | Quad 2-input OR gate                     |
| **74LS04**  | Hex inverter                             |
| **74LS74**  | Dual D-type flip-flop                    |

### Additional Components

* Digital clock source
* Logic power supplies
* Digital switches
* Simulated sensor inputs
* LEDs / digital indicators
* Ground connections
* TTL logic interconnections

---

# 🖥️ Simulation

The complete digital architecture was designed and simulated using:

### NI Multisim

The simulation demonstrates the interaction between:

```text
Mission Timer
      ↓
Mission Sequencer
      ↓
Mission States
      ↓
Sensor Monitoring
      ↓
Majority Voting
      ↓
Decision Logic
      ↓
Fault Detection
      ↓
Telemetry
```

The simulation allows the behavior of the digital mission-management architecture to be observed without requiring physical hardware.

---

# 📁 Repository Contents

This repository intentionally contains only the essential project files.

```text
Integrated-Digital-Mission-Management-System/
│
├── Integrated_Digital_Mission_Management_System.ms8
├── Project_Documentation.docx
├── Mission_Management_System.png
└── README.md
```

| File                                                | Description                                  |
| --------------------------------------------------- | -------------------------------------------- |
| `Integrated_Digital_Mission_Management_System.ms8` | Complete NI Multisim circuit simulation      |
| `Project_Documentation.docx`                        | Detailed project documentation               |
| `Mission_Management_System.png`                     | Complete circuit schematic                   |
| `README.md`                                         | Project overview and technical documentation |

---

# 🧩 Key Concepts Demonstrated

This project combines several important concepts from digital electronics and control-oriented systems:

* TTL digital logic
* Binary counting
* Frequency division
* Digital decoding
* Combinational logic
* Sequential logic
* Sensor redundancy
* 2-out-of-3 majority voting
* Mission sequencing
* Fault detection
* Fault memory
* Flip-flop-based state storage
* Digital decision-making
* Digital telemetry
* System-level logic integration

---

# 🚀 Engineering Significance

Although this project is an **educational simulation**, its architecture introduces concepts that are relevant to aerospace, robotics, industrial automation, and safety-oriented digital systems.

Modern aerospace systems use substantially more advanced technologies, including:

* Radiation-tolerant electronics
* High-reliability processors
* FPGA-based digital logic
* Real-time operating systems
* Watchdog systems
* Built-in test systems
* Fault-tolerant architectures
* Redundant computing
* Hardware-in-the-loop testing
* Formal verification
* Safety and reliability analysis

The present project provides a simplified foundation for understanding how **timing, state sequencing, redundancy, decision logic, and fault memory** can be implemented at the digital-logic level.

---

# 🎓 Learning Outcomes

After completing this project, the following concepts can be understood more practically:

1. How digital counters generate sequential states.
2. How frequency division can be obtained from binary counters.
3. How decoders convert binary states into individual control signals.
4. How logic gates implement digital decision-making.
5. How redundant sensor information can be combined using majority voting.
6. How flip-flops provide digital state storage.
7. How fault information can be latched and retained.
8. How multiple digital subsystems can be integrated into a larger architecture.
9. How a simplified mission sequence can be represented using discrete digital logic.
10. How digital logic concepts can be applied to aerospace-oriented system architectures.

---

# 🔮 Future Improvements

The current system can be extended in several directions:

### Hardware

* Build a physical prototype using 74LS-series ICs.
* Add real sensors and signal-conditioning circuits.
* Interface physical indicators and switches.
* Develop a dedicated power and reset subsystem.

### Digital Architecture

* Replace discrete TTL logic with FPGA implementation.
* Add watchdog and timeout logic.
* Implement more advanced fault-management architecture.
* Introduce additional redundant processing channels.
* Implement automated fault-injection testing.

### Software / Interface

* Interface the system with a microcontroller or FPGA.
* Develop a graphical telemetry interface.
* Log mission states and fault events.
* Perform automated simulation-based verification.

### Advanced Development

A future version could evolve from discrete digital logic toward an **FPGA-based mission-management architecture**, allowing more sophisticated state machines, fault handling, timing control, and telemetry processing.

---

# 📚 Project Classification

| Category                | Details                                              |
| ----------------------- | ---------------------------------------------------- |
| **Project Type**        | Academic / Educational Project                       |
| **Domain**              | Digital Electronics, Mechatronics, Aerospace Systems |
| **Application Area**    | Mission Management / Digital Control                 |
| **Simulation Platform** | NI Multisim                                          |
| **Logic Technology**    | 74LS TTL                                             |
| **Architecture**        | Sequential + Combinational Digital Logic             |
| **Primary Focus**       | Mission Sequencing, Redundancy & Fault Detection     |

---

# 👨‍💻 Author

**Kunal Nitin Gadhave**

Mechatronics Engineering
SVPM's College of Engineering, Malegaon (Bk.), Baramati
Academic Year: **2026–2027**

---

# ⚠️ Disclaimer

This project is developed strictly for **academic and educational purposes**.

The system is a simplified digital simulation intended to demonstrate concepts related to:

* Digital logic
* Mission sequencing
* Redundancy
* Decision-making
* Fault detection
* Fault memory
* Digital telemetry

It is **not intended for use in an actual launch vehicle, spacecraft, aircraft, industrial safety system, or other safety-critical application**.

The architecture presented here is not flight-qualified and does not represent the design standards, verification processes, reliability requirements, redundancy management, or safety certification applicable to real aerospace mission computers.

---

# 📄 License

This project is provided for **educational and academic reference**.

If you use, modify, or build upon this project, please provide appropriate credit to the original author.

---

## ⭐ Project Status

**Completed — Simulation Verified in NI Multisim**

> A small-scale digital-logic implementation demonstrating how fundamental TTL building blocks can be integrated into a simplified mission-management architecture.
