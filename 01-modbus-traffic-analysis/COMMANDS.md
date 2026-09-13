# Commands Used

## WSL2

PowerShell as Administrator:

```powershell
wsl --install -d Ubuntu
```

Verify:

```powershell
wsl --status
wsl -l -v
```

## Ubuntu Preparation

```bash
sudo apt update
sudo apt install -y git curl ca-certificates
mkdir -p ~/Labs
cd ~/Labs
```

## Clone Martin Scheu OT Lab

```bash
git clone https://gitlab.switch.ch/martin.scheu/ot-lab.git
cd ot-lab
```

Inspect:

```bash
ls -la
sed -n '1,220p' README.md
sed -n '221,440p' README.md
sed -n '1,200p' install.sh
```

## Check KVM and systemd

```bash
ls -l /dev/kvm
if [ -e /dev/kvm ]; then echo "KVM OK"; else echo "KVM ABSENT"; fi
systemctl is-system-running
```

## Install

```bash
sudo -E bash install.sh
```

## Service Management

```bash
systemctl status ot-lab --no-pager
sudo systemctl restart ot-lab
sudo systemctl stop ot-lab
journalctl -u ot-lab -n 80
docker ps --filter name=clab-ot-
```

## Find Current WSL IP

```bash
hostname -I
```

Open:

```text
http://<WSL-IP>:3000/
```

## Packet Capture Settings Used

```text
NODE:                sw-distribution
INTERFACE:           eth4
PORT:                502
DESTINATION / HOST:  172.18.1.21
PACKET COUNT:        20 / 50 / 100
```

## Wireshark

Primary filter:

```text
modbus
```

Alternative:

```text
tcp.port == 502
```

Look for:

```text
Func: 3 — Read Holding Registers
Func: 6 — Write Single Register
```

## Portfolio Repository Commands

```bash
git clone https://github.com/Fluffywolf1913VS/ot-labs-.git
cd ot-labs-
git status
git add .
git commit -m "Add Modbus TCP traffic analysis lab"
git push origin main
```
