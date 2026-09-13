# Modbus Register Map

## Confirmed

| Register | Function | Values Observed | Evidence |
|---:|---|---|---|
| `2` | Tank Level Setpoint | `60`, `65` | FC06 operator setpoint change |
| `4` | Outlet Valve Position / Command | `0`, `100` | FC06 Close/Open |
| `16` | Outlet Flow Setpoint | `200`, `220` | FC06 operator setpoint change |

## Probable

| Register | Function | Values Observed | Why Probable |
|---:|---|---|---|
| `1` | Operating Mode | `0` | Observed when switching to Manual; reverse transition not yet captured |

## Baseline FC03 Values Observed

One FC03 response included:

```text
Register 0  = 60
Register 1  = 1
Register 2  = 60
Register 3  = 47
Register 4  = 40
Register 5  = 198
Register 6  = 200
Register 7  = 0
Register 8  = 1
Register 9  = 17
```

Only mappings backed by controlled operator-action tests are marked Confirmed.
