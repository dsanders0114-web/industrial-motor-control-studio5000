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

# Skills Demonstrated

This project demonstrates practical skills in:

* Rockwell Studio 5000 Logix Designer
* PLC ladder logic programming
* Industrial motor control circuits
* Control system documentation
* Automation troubleshooting methodology

