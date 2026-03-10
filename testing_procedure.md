# Testing Procedure

## Test Environment

I verified the control logic using simulated tag values within **Studio 5000 Logix Designer**. Since the project does not use physical I/O hardware, I manually adjusted Boolean tag values in the program tag table to simulate pushbutton inputs and overload conditions.

The following tags were used to simulate system inputs:

* `PB_Start`
* `PB_Stop`
* `OL_OK`

The system outputs monitored during testing included:

* `Mtr_Permissive`
* `Mtr_RunCmd`
* `Mtr_Starter`
* `PL_Run`
* `PL_Fault`

---

# Test 1: Normal Healthy System State

### Objective

Verify the controller correctly recognizes healthy operating conditions before the motor is started.

### Procedure

I set the simulated input values to represent a normal system condition.

```
PB_Stop = 1
OL_OK   = 1
PB_Start = 0
```

### Expected Result

```
Mtr_Permissive = 1
Mtr_RunCmd     = 0
Mtr_Starter    = 0
PL_Run         = 0
PL_Fault       = 0
```

### Result

The controller correctly generated the motor permissive signal while keeping the motor stopped.

---

# Test 2: Motor Start Operation

### Objective

Verify that the motor starts when the start pushbutton is pressed.

### Procedure

I simulated pressing the start pushbutton.

```
PB_Start = 1
```

### Expected Result

```
Mtr_RunCmd  = 1
Mtr_Starter = 1
PL_Run      = 1
```

### Result

The motor run command energized successfully, the motor starter output activated, and the run pilot light turned on.

---

# Test 3: Seal-In Circuit Verification

### Objective

Verify that the run command remains active after the start pushbutton is released.

### Procedure

I released the start pushbutton.

```
PB_Start = 0
```

### Expected Result

```
Mtr_RunCmd  = 1
Mtr_Starter = 1
PL_Run      = 1
```

### Result

The motor continued running due to the seal-in contact within the ladder logic. This confirmed the latch behavior was functioning correctly.

---

# Test 4: Stop Pushbutton Operation

### Objective

Verify that the motor stops when the stop pushbutton is activated.

### Procedure

I simulated pressing the stop pushbutton.

```
PB_Stop = 0
```

### Expected Result

```
Mtr_Permissive = 0
Mtr_RunCmd     = 0
Mtr_Starter    = 0
PL_Run         = 0
```

### Result

The motor command immediately dropped out and the motor starter output de-energized.

---

# Test 5: Overload Fault Condition

### Objective

Verify that the system responds correctly to an overload condition.

### Procedure

I simulated an overload fault.

```
OL_OK = 0
```

### Expected Result

```
Mtr_Permissive = 0
Mtr_RunCmd     = 0
Mtr_Starter    = 0
PL_Fault       = 1
```

### Result

The system correctly removed the permissive signal, stopped the motor, and activated the fault pilot light.

---

# Test 6: System Recovery

### Objective

Verify the system can return to a normal operating state after a fault condition is cleared.

### Procedure

I restored the overload signal.

```
OL_OK = 1
```

### Expected Result

```
Mtr_Permissive = 1
Motor remains stopped until start is pressed
```

### Result

The system returned to a normal ready state and required the start pushbutton to be pressed before the motor could run again.

---

# Testing Summary

All functional tests confirmed that the ladder logic program correctly implements a standard **3-wire motor starter control system**. The program successfully handled:

* Normal operating conditions
* Motor start and stop commands
* Seal-in run command behavior
* Overload fault protection
* System recovery after faults


---

# Lessons Learned / Engineering Notes

## Importance of Permissive Logic

One key takeaway from this project was the importance of **separating permissive logic from the motor start command**.

By creating a dedicated permissive signal (`Mtr_Permissive`), the control logic becomes easier to maintain and expand. Additional safety or operational conditions can be added without modifying the motor start logic.

This modular approach is commonly used in industrial control systems to simplify troubleshooting and improve system reliability.

---

## Seal-In Circuits Replicate Real Industrial Control

The use of a **seal-in circuit** allowed the motor run command to remain active after the start pushbutton was released.

This method closely replicates traditional **electromechanical motor control circuits** that use auxiliary contacts on motor starters to maintain coil energization.

Understanding this concept is important because many modern PLC control systems are designed to mimic these proven industrial control patterns.

---

## Importance of Input Signal Polarity

During development, I had to carefully consider the polarity of simulated input signals when using ladder logic instructions such as:

* **XIC (Examine If Closed)**
* **XIO (Examine If Open)**

Correct instruction selection ensures that the ladder logic accurately reflects the behavior of real field devices such as normally closed stop pushbuttons or overload contacts.

This highlighted the importance of understanding how field devices are wired and how their signals appear to the PLC.

---

## Value of Status Indication

Adding run and fault pilot lights improved the clarity of the control system.

Visual indicators provide immediate feedback about system operation and are commonly used in industrial control panels to help operators and maintenance personnel quickly identify system states.

Including status indication in the design also improves troubleshooting capability.

---

## Importance of Structured Ladder Logic

Organizing the ladder logic into clearly defined functional sections helped make the program easier to understand and maintain.

Separating the program into logical steps such as:

* Permissive evaluation
* Start/stop control
* Motor output control
* Status indication

makes the control system easier to troubleshoot and extend.

This structure is commonly used in larger automation projects where multiple control conditions must be managed.

---

# Future Improvements

Several improvements could be implemented to expand the system functionality and more closely resemble a real industrial control application:

* Hand / Off / Auto selector switch
* Motor auxiliary feedback input
* Fault reset pushbutton
* Restart delay timer after faults
* Operator HMI interface
* Alarm logging and diagnostics

These additions would provide additional safety and control capabilities while demonstrating more advanced PLC programming concepts.

---

# Final Result

This project successfully demonstrates the design and testing of a basic **industrial motor starter control system** using ladder logic in Studio 5000.

The project highlights several fundamental automation engineering concepts, including:

* 3-wire motor control
* permissive logic
* seal-in circuits
* fault handling
* structured ladder programming
* system testing and documentation

