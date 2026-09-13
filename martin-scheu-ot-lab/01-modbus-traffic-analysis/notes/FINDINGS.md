# Findings

## Finding 1 — Normal HMI polling is easy to baseline

The FUXA HMI repeatedly uses Modbus FC03 to read 28 holding registers from SCP-1.

This creates a stable pattern that can be used as an OT network baseline.

## Finding 2 — Operator writes are distinguishable from polling

Normal traffic:

```text
FC03 — Read Holding Registers
```

Operator control actions:

```text
FC06 — Write Single Register
```

This distinction is useful for detection engineering.

## Finding 3 — Process semantics can be inferred from packet captures

By changing one HMI value at a time and capturing the resulting network traffic, register meanings were reconstructed without relying on a pre-existing register map.

Examples:

```text
Register 2  = Level Setpoint
Register 16 = Outlet Flow Setpoint
Register 4  = Outlet Valve Position / Command
```

## Finding 4 — Modbus TCP exposes control intent in cleartext

The analyzed traffic exposes register addresses and values directly.

This reinforces the importance of:

- segmentation
- strict allow-listing
- passive monitoring
- alerts for writes
- engineering-workstation access control
