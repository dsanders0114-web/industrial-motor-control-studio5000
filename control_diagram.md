# Motor Control Diagram

```text
Ladder Logic Control Concept

        +-------------------+      +-------------------+
        |   Start PB        |      |    Stop PB        |
        |   PB_Start        |      |    PB_Stop        |
        |   Momentary NO    |      |    Healthy = TRUE |
        +---------+---------+      +---------+---------+
                  |                          |
                  +------------+-------------+
                               |
                               v
                     +---------------------+
                     |   Permissive Logic  |
                     |  PB_Stop AND OL_OK  |
                     +----------+----------+
                                |
                                v
                     +---------------------+
                     |   Run Command Logic |
                     |  Start + Seal-In    |
                     |    Mtr_RunCmd       |
                     +----------+----------+
                                |
                                v
                     +---------------------+
                     |  Motor Starter Coil |
                     |    Mtr_Starter      |
                     +----+-----------+----+
                          |           |
                          |           |
                          v           v
               +----------------+   +----------------+
               |   Run Light    |   |  Fault Light   |
               |    PL_Run      |   |   PL_Fault     |
               +----------------+   +----------------+

Overload Input:
OL_OK = Healthy overload condition required for motor operation
If OL_OK goes false:
- permissive drops
- motor stops
- fault light turns on
```

# Simplified Sequence Flow

```text
Healthy Stop + Healthy Overload
            ↓
      Permissive True
            ↓
       Start Pressed
            ↓
     Run Command Latches
            ↓
   Motor Starter Energizes
            ↓
      Run Light Turns On

If Stop Pressed or Overload Trips:
            ↓
     Permissive Becomes False
            ↓
      Run Command Drops Out
            ↓
   Motor Starter De-Energizes
            ↓
   Run Light Off / Fault Light On
```

# I/O Table

Use this as your table in the README:

| Tag Name         | Type | Role     | Description                                             |
| ---------------- | ---- | -------- | ------------------------------------------------------- |
| `PB_Start`       | BOOL | Input    | Start pushbutton, momentary normally open               |
| `PB_Stop`        | BOOL | Input    | Stop pushbutton status, healthy state allows operation  |
| `OL_OK`          | BOOL | Input    | Overload healthy permissive                             |
| `Mtr_Permissive` | BOOL | Internal | True only when stop and overload conditions are healthy |
| `Mtr_RunCmd`     | BOOL | Internal | Sealed motor run command                                |
| `Mtr_Starter`    | BOOL | Output   | Motor starter coil output                               |
| `PL_Run`         | BOOL | Output   | Run pilot light                                         |
| `PL_Fault`       | BOOL | Output   | Fault pilot light                                       |

## Control Narrative

This control routine uses permissive logic to verify the stop circuit and overload condition are healthy before allowing motor operation. When I press the start pushbutton, the motor run command energizes and seals itself in through an internal holding branch. That run command drives the motor starter output and turns on the run pilot light. If I press the stop pushbutton or simulate an overload fault, the permissive is removed, the motor command drops out, the starter de-energizes, and the fault light indicates the abnormal condition.


