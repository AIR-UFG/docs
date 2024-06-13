# Self-Driving Car - eno1 fix

## General information
### Udev description
udev (userspace /dev) is a device manager for the Linux kernel. udev primarily manages device nodes in the /dev directory. At the same time, udev also handles all user space events raised when hardware devices are added into the system or removed from it, including firmware loading as required by certain devices. (from [wikipedia](https://en.wikipedia.org/wiki/Udev))

### Useful commands
Show pci slots and their names:
```
lshw -class network -businfo
```
Show info about pci devices:
```
lspci -vv
```

udev rule to disable a pci device (added to /etc/udev/rules.d/10-network.rules)
```
ACTION=="add", KERNEL=="0000:00:03.0", SUBSYSTEM=="pci", RUN+="/bin/sh -c 'echo 1 > /sys/bus/pci/devices/0000:00:03.0/remove'"
```

## The Problem
Whenever the LiDAR or another device like a router connects to the eno1 network adapter, it stops working. The network adapter a device is connected to is assigned dynamically, so sometimes it's assigned to eno1, and sometimes it is assigned to a working adapter e.g. enp2s0.
## The Solution
We created a new file on /etc/udev/rules.d/ named 10-network.rules

`air@twizy:~$ cat /etc/udev/rules.d/10-network.rules`
```bash
# Set LiDAR network adapter name to eth_lidar
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="d0:4c:c1:06:05:b3", NAME="eth_lidar"

# Disable eno1 network adapter
ACTION=="add", KERNEL=="0000:00:1f.6", SUBSYSTEM=="pci", RUN+="/bin/sh -c 'echo 1 > /sys/bus/pci/devices/0000:00:1f.6/remove'"
```

The first line, `SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="d0:4c:c1:06:05:b3", NAME="eth_lidar"` renames whichever network adapter the LiDAR is assigned to *eth_lidar*. We do this by creating a rule that looks at the device's MAC address, and if it is the LiDAR's MAC address, it is renamed. While not an issue, having a consistent name for the network adapter of our LiDAR device may prove useful in the future.

The second line, `ACTION=="add", KERNEL=="0000:00:1f.6", SUBSYSTEM=="pci", RUN+="/bin/sh -c 'echo 1 > /sys/bus/pci/devices/0000:00:1f.6/remove'"`, if the address of a pci device is `0000:00:1f.6`, the eno1 adapter, we execute a bash script `/bin/sh -c 'echo 1 > /sys/bus/pci/devices/0000:00:1f.6/remove` that shuts it down.

## PCI Ports
![Pasted%20image%2020240612160309.png](images/Pasted%20image%2020240612160309.png)
## eno1 Network Adapter Information
![Pasted%20image%2020240612160401.png](images/Pasted%20image%2020240612160401.png)

## LiDAR Network Information
![Pasted%20image%2020240612160500.png](images/Pasted%20image%2020240612160500.png)

## Before
![Captura%20de%20tela%20de%202024-06-12%2015-46-31.png](images/Captura%20de%20tela%20de%202024-06-12%2015-46-31.png)
## After
![Captura%20de%20tela%20de%202024-06-12%2015-48-26.png](images/Captura%20de%20tela%20de%202024-06-12%2015-48-26.png)
