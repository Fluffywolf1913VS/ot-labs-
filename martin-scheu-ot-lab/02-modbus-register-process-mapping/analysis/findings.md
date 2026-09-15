# Findings

## Network roles

- `172.18.1.30` behaved as the HMI / Modbus client.
- `172.18.1.21:502` behaved as SCP-1 / Modbus server.
- The HMI polled a 28-word holding-register block once per second in the observed sessions.

## Confirmed write semantics

### Register 2 — Level SP

```text
HMI: 60 % → 61 %
FC06: Register 2 = 61
```

### Register 16 — Outlet Flow SP

```text
HMI: 200 L/s → 201 L/s
FC06: Register 16 = 201
```

### Register 3 — Inlet valve position/command

```text
Open  → 100
Close → 0
```

During FC03 polling the same register tracked intermediate values around the HMI position (for example 46–51%).

### Register 26 — Inlet valve Stop/Hold

```text
Stop → 1
```

### Register 4 — Outlet valve position/command

```text
Open  → 100
Close → 0
```

### Register 27 — Outlet valve Stop/Hold

```text
Stop → 1
```

## Strong FC03 correlations

A representative read response showed:

```text
R0 = 60
R1 = 1
R2 = 60
R3 = 46
R4 = 40
R5 = 207
R6 = 201
```

At approximately the same time, the HMI displayed:

```text
Tank level        ≈ 60
Level SP           = 60 %
Inlet valve        ≈ 46–51 %
Outlet valve       = 40 %
Inlet flow         ≈ 200 L/s
Outlet flow        = 201 L/s
```

This strongly supports:

- `R0` → Tank level
- `R5` → Inlet flow (FT)
- `R6` → Outlet flow (FT)

These are retained as **strong correlations**, not hard-confirmed controlled mappings.

## Unmapped area

The baseline FC03 request reads raw addresses `0–27`. Only a subset has been assigned semantics. Registers not listed in the map should remain `Unknown` until validated with additional controlled observations.
