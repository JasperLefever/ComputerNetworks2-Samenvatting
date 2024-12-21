# Module 1: Basic Device Configuration

## Configure a Switch with Initial Settings

### Switch Management Access

> Remote access requires a management IP address and a default gateway to reach other networks. This interface on a switch is called a **Switch Virtual Interface (SVI)**. This interface is configured using a console connection.

> Default management interface is VLAN 1. It is recommended to change the management interface to a different VLAN.

## Configure Switch Ports

### Duplex Communication

- **Half-Duplex**: Devices can only send or receive data at a time. Collisions can occur in half-duplex communication.

- **Full-Duplex**: Devices can send and receive data simultaneously. No collisions occur in full-duplex communication.

### Auto-MDIX

- **Auto-MDIX**: Automatically detects the type of cable connected to the switch port and configures the port accordingly.

> Switches without Auto-MDIX require a crossover cable to connect to another switch. Switches with Auto-MDIX can use a straight-through cable to connect to another switch.

- **Enabled by default on most switches.**

## Secure remote access

> Telnet is an insecure protocol. Use SSH for secure remote access.

## Basic router configuration

- Secure with password on console and exec mode.
- Configure a banner to warn unauthorized access.
- Configure a hostname for the router.
- Encrypt all passwords.

### Dual Stack Configuration

- **Dual Stack**: Running both IPv4 and IPv6 on the same network.

## Verify Directly Connected Networks

- Use the `show ip route` command to verify directly connected networks.

Meaning of the output:

- **C**: Directly connected network.
- **L**: Local interface.
- **S**: Static route.
- **R**: RIP route.
- **M**: Mobile route.
- **B**: BGP route.
