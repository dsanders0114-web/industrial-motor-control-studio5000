# Studio 5000 Motor Starter Control

## Overview

This project demonstrates the development and testing of a basic **industrial motor starter control routine** using **Studio 5000 Logix Designer** and ladder logic programming.

The control system simulates a standard **3-wire motor starter circuit** using a start pushbutton, stop pushbutton, and overload permissive condition to control a motor starter output.

The program includes sealed run command logic, status indication through pilot lights, and simulated testing of system behavior under normal and fault conditions.

This project was developed as part of a **PLC automation portfolio** to demonstrate practical ladder logic programming, system documentation, and troubleshooting procedures.

---

# System Architecture

| Component            | Description                      |
| -------------------- | -------------------------------- |
| Controller Platform  | Rockwell Logix 5000 Architecture |
| Development Software | Studio 5000 Logix Designer       |
| Programming Language | Ladder Logic                     |
| Control Method       | 3-Wire Motor Starter Control     |
| Testing Method       | Simulated tag inputs             |

---

# Control Features

The control routine includes the following functionality:

* Start pushbutton motor control
* Stop pushbutton motor shutdown
* Overload permissive protection
* Seal-in (latching) motor run command
* Run pilot light indication
* Fault pilot light indication
* Simulated testing procedure

These features replicate the behavior of a typical **industrial motor starter control circuit**.

---

# I/O List

| Tag Name       | Type | Description                 |
| -------------- | ---- | --------------------------- |
| PB_Start       | BOOL | Start pushbutton input      |
| PB_Stop        | BOOL | Stop pushbutton input       |
| OL_OK          | BOOL | Overload healthy permissive |
| Mtr_Permissive | BOOL | Motor permissive signal     |
| Mtr_RunCmd     | BOOL | Sealed motor run command    |
| Mtr_Starter    | BOOL | Motor starter output        |
| PL_Run         | BOOL | Run pilot light             |
| PL_Fault       | BOOL | Fault pilot light           |

---

# Ladder Logic Structure

The ladder logic routine is divided into several functional sections:

1. **Permissive Logic**
   Ensures the stop circuit and overload condition are healthy before allowing motor operation.

2. **Motor Start / Seal-In Logic**
   Implements a sealed run command using a start pushbutton and internal latch contact.

3. **Motor Output Control**
   Energizes the motor starter output when the run command is active.

4. **Run Status Indication**
   Activates the run pilot light when the motor is operating.

5. **Fault Indication**
   Activates the fault pilot light when the overload condition is not healthy.

---

# Project Objectives

The purpose of this project was to demonstrate the following automation engineering concepts:

* PLC ladder logic development
* Industrial motor control design patterns
* Use of permissive and interlock conditions
* Implementation of seal-in control circuits
* Documentation of control system operation
* Simulation-based system testing

---

# Repository Structure

```text
studio5000-motor-starter
│
├── README.md
├── sequence_of_operation.md
├── testing_procedure.md
├── screenshots
│   ├── ladder_logic.png
│   ├── motor_running.png
│   └── overload_fault.png
└── motor_starter.ACD
```

---

Good. This section helps show that you **understand the engineering behind the logic**, not just how to draw rungs. Hiring managers and controls engineers like seeing this.

You can place this **near the end of your README**.

---

# Engineering Concepts Demonstrated

## 3-Wire Motor Control

This project implements a **3-wire motor control circuit**, which is one of the most common motor control methods used in industrial automation systems.

The system uses:

* A **momentary start pushbutton**
* A **normally closed stop pushbutton**
* A **sealed run command**

This control method prevents a motor from automatically restarting after a power loss or fault condition. The operator must intentionally press the start pushbutton to restart the motor.

This design improves both **operator safety and equipment protection**.

---

## Permissive Logic

Permissive logic is used to ensure that required operating conditions are satisfied before a machine or device is allowed to start.

In this project, the motor is only allowed to run when:

* The **stop circuit is healthy**
* The **overload protection is healthy**

These conditions are evaluated in the **permissive rung**, which generates the `Mtr_Permissive` signal.

Separating permissive logic from the start logic allows additional safety or interlock conditions to be added easily in future system expansions.

Examples of additional permissive conditions might include:

* Emergency stop circuits
* Safety relay status
* Equipment interlocks
* Process conditions

---

## Seal-In (Latching) Circuits

A **seal-in circuit** is used to maintain a command after a momentary input has been released.

When the start pushbutton is pressed, the controller energizes the motor run command (`Mtr_RunCmd`).

A parallel branch using the run command contact then maintains the rung condition even after the start pushbutton returns to its normal state.

This behavior replicates traditional **electromechanical relay circuits** commonly used in industrial motor control panels.

---

## Interlock Protection

The overload permissive (`OL_OK`) functions as a protective interlock.

If an overload condition occurs, the permissive signal is removed and the motor run command is immediately dropped.

This ensures the motor cannot continue operating under a fault condition and prevents equipment damage.

---

## Status Indication

Pilot lights were included in the design to provide visual system feedback.

### Run Pilot Light

The run pilot light (`PL_Run`) indicates that the motor starter output is energized and the motor is operating.

### Fault Pilot Light

The fault pilot light (`PL_Fault`) indicates that the overload protection has been triggered and the motor is not permitted to run.

Status indication is commonly used in industrial control panels to help operators quickly understand system conditions.

---

## Modular Ladder Logic Design

The ladder logic was structured to separate different system functions into individual rungs:

* Permissive logic
* Start / seal-in logic
* Motor output control
* Run indication
* Fault indication

This modular structure improves program readability and makes the system easier to troubleshoot and expand.

---

# Possible System Extensions

This control system could be expanded with additional automation features, including:

* Hand / Off / Auto selector switch
* Motor auxiliary feedback contact
* Fault reset pushbutton
* Restart delay timer after fault conditions
* Alarm notification system
* HMI operator interface
![Screenshot 2026-03-10 140156](https://github.com/user-attachments/assets/a60035ff-a30b-4a7e-ab79-0d6022ae2436)
![Screenshot 2026-03-10 140340](https://github.com/user-attachments/assets/9a7cfa79-daeb-4ae9-83ee-02a13ef03926)
![Screenshot 2026-03-10 140513](https://github.com/user-attachments/assets/24ef13c3-45fb-420c-99c3-8cf99405d386)
![Screenshot 2026-03-10 140018](https://github.com/user-attachments/assets/47455afa-35cc-46ce-80fb-20f267389193)

