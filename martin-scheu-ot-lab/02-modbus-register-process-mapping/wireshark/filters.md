# Wireshark Filters

## All Modbus/TCP on default port

```text
tcp.port == 502
```

## All decoded Modbus traffic

```text
modbus
```

## FC03 — Read Holding Registers

```text
modbus.func_code == 3
```

## FC03 responses from SCP-1

```text
modbus.func_code == 3 && ip.src == 172.18.1.21
```

## FC06 — Write Single Register

```text
modbus.func_code == 6
```

## FC06 requests from the HMI only

```text
modbus.func_code == 6 && ip.src == 172.18.1.30
```

## Traffic between HMI and SCP-1

```text
(ip.addr == 172.18.1.30 && ip.addr == 172.18.1.21) && tcp.port == 502
```
