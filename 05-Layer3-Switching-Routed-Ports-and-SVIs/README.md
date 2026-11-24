# Project 05: Layer 3 Switching – Routed Ports and SVIs

## Overview

This project demonstrates two methods of Layer 3 routing using a Cisco Multilayer Switch (Cisco 3560) in Cisco Packet Tracer.

The project explores how a multilayer switch can perform routing between different networks without relying on an external router.

Two approaches are implemented:

1. **Routed Physical Interfaces:** Converting physical switch ports into Layer 3 interfaces using `no switchport` and assigning IP addresses.
2. **Switched Virtual Interfaces (SVIs):** Creating virtual VLAN interfaces to act as default gateways for different VLANs.

Both methods demonstrate how a multilayer switch can handle Layer 2 switching and Layer 3 routing.

## Objectives

- Create and configure multiple VLANs.
- Assign switch ports to their respective VLANs.
- Configure physical interfaces as Layer 3 routed ports.
- Create and configure Switched Virtual Interfaces (SVIs).
- Enable IPv4 routing using `ip routing`.
- Understand the differences between Routed Ports and SVIs.
- Verify network connectivity between different networks.

## Devices Used

- Cisco Catalyst 3560 Multilayer Switch.
- PCs.
- Cisco Packet Tracer.

---

## Method 1: Layer 3 Routing Using Physical Interfaces

### Network Overview

This topology uses two physical Layer 3 interfaces to connect two different networks.

| Network | Interface | Default Gateway | PC Address |
|---|---|---|---|
| 192.168.10.0/24 | Fa0/3 | 192.168.10.1 | 192.168.10.3 |
| 192.168.20.0/24 | Fa0/15 | 192.168.20.1 | 192.168.20.15 |

### Configuration

**1. Create VLANs**

```cisco
vlan 10
 name SC
exit

vlan 20
 name SC
exit
```

**2. Configure Access Ports**

```cisco
interface range fa0/1 - 12
 switchport mode access
 switchport access vlan 10
exit

interface range fa0/13 - 20
 switchport mode access
 switchport access vlan 20
exit
```

**3. Configure Layer 3 Routed Interfaces**

```cisco
interface fa0/3
 no switchport
 ip address 192.168.10.1 255.255.255.0
 no shutdown
exit

interface fa0/15
 no switchport
 ip address 192.168.20.1 255.255.255.0
 no shutdown
exit
```

**4. Enable IP Routing**

```cisco
ip routing
```

### Key Concept

The `no switchport` command converts a physical switch interface from Layer 2 switching to Layer 3 routing.

Each routed interface receives an IP address and can act as a gateway for its connected network.

---

## Method 2: Inter-VLAN Routing Using SVIs

### Network Overview

This topology uses three VLANs, with an SVI configured for each VLAN to provide its default gateway.

| VLAN | Network | Default Gateway | PC Addresses |
|---|---|---|---|
| VLAN 10 | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.3, 192.168.10.4 |
| VLAN 20 | 192.168.20.0/24 | 192.168.20.1 | 192.168.20.12, 192.168.20.13 |
| VLAN 30 | 192.168.30.0/24 | 192.168.30.1 | 192.168.30.17, 192.168.30.18 |

### Configuration

**1. Create VLANs**

```cisco
vlan 10
 name CS
exit

vlan 20
 name SC
exit

vlan 30
 name IT
exit
```

**2. Assign Access Ports**

```cisco
interface range fa0/1 - 8
 switchport mode access
 switchport access vlan 10
exit

interface range fa0/9 - 15
 switchport mode access
 switchport access vlan 20
exit

interface range fa0/16 - 20
 switchport mode access
 switchport access vlan 30
exit
```

**3. Configure Switched Virtual Interfaces (SVIs)**

```cisco
interface vlan 10
 ip address 192.168.10.1 255.255.255.0
 no shutdown
exit

interface vlan 20
 ip address 192.168.20.1 255.255.255.0
 no shutdown
exit

interface vlan 30
 ip address 192.168.30.1 255.255.255.0
 no shutdown
exit
```

**4. Enable IP Routing**

```cisco
ip routing
```

### Key Concept

An SVI is a virtual Layer 3 interface associated with a VLAN.

Each SVI provides a default gateway for devices within its VLAN, allowing the multilayer switch to route traffic between different VLANs.

---

## Verification and Connectivity Testing

All configuration and connectivity tests were successfully completed in both methods.

### 1. Verification Commands

The following commands were used to verify the network configuration:

**Check VLAN Configuration**

```cisco
show vlan brief
```

**Check Interface Status and IP Addresses**

```cisco
show ip interface brief
```

**Check the Routing Table**

```cisco
show ip route
```

**Check Running Configuration**

```cisco
show running-config
```

### 2. Connectivity Testing

Ping tests were performed between devices in different networks to verify successful communication.

Example Ping tests for Method 2:

```text
ping 192.168.10.1
ping 192.168.20.12
ping 192.168.30.17
```

### Test Results

- All devices successfully reached their default gateways.
- Devices in different VLANs successfully communicated with each other.
- The multilayer switch successfully routed traffic between the configured networks.
- Both Routed Physical Interfaces and SVI-based routing worked as expected.

**Result: All connectivity tests passed successfully in both methods.**

---

## Comparison: Routed Ports vs SVIs

| Feature | Routed Physical Ports | SVIs |
|---|---|---|
| Interface Type | Physical Interface | Virtual Interface |
| Configuration | `no switchport` | `interface vlan` |
| IP Assignment | Physical Port | VLAN Interface |
| Common Use | Dedicated Layer 3 Links | VLAN Default Gateways |
| Routing | `ip routing` | `ip routing` |

## Key Takeaways

Through this project, I gained practical experience with:

- Creating and configuring VLANs.
- Assigning access ports to different VLANs.
- Converting Layer 2 switch ports into Layer 3 routed interfaces.
- Configuring SVIs for different VLANs.
- Enabling IPv4 routing on a multilayer switch.
- Understanding the differences between Routed Ports and SVIs.
- Verifying interface status and routing tables.
- Testing connectivity between different networks.

## Project Files

- Cisco Packet Tracer topology (`.pkt`).
- Network topology screenshots.
- Configuration commands and verification details.

---

**Project 05/30 – 30 Projects in 30 Days**

*Learn. Practice. Build.*