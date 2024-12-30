# CheetSheet Computer Networks 2 - Cisco SRWE

## IPV6 On a Switch

```bash
sdm prefer dual-ipv4-and-ipv6 default

reload
```

## Show Commands

```bash
Switch# show running-config
Switch# show flash
Switch# show mac address-table
Switch# show ip interface brief
Switch# show ipv6 interface brief
Switch# show interfaces
Switch# show interfaces <interface>
Switch# show ipv6 interface brief
Switch# show ip route
Switch# show ip route static
Switch# show ipv6 route
Switch# show vlan
Switch# show vlan brief
Switch# show interfaces trunk
Switch# show interfaces status
Switch# show etherchannel summary
Switch# show etherchannel port-channel
Switch# show interfaces port-channel <number>
Switch# show ip dhcp binding
Switch# show ip dhcp server statistics
Switch# show ipv6 dhcp pool
```

## SVI Configuration

```bash
Switch> enable
Switch# configure terminal
Switch(config)# interface vlan <vlan of management interface>
Switch(config-if)# ip address <ip address> <subnet mask>
Switch(config-if)# no shutdown
Switch(config-if)# description "Management Interface"
Switch(config-if)# end
Switch# copy running-config startup-config

# Setting default gateway
Switch> enable
Switch# configure terminal
Switch(config)# ip default-gateway <ip address>
Switch(config)# end
Switch# copy running-config startup-config
```

## Configure SSH

```bash
Switch> enable
Switch# show ip ssh # Check if SSH is supported
Switch# ip domain-name <domain name>
Switch# crypto key generate rsa
Switch# username <username> secret <password>
Switch# line vty 0 15
Switch(config-line)# transport input ssh
Switch(config-line)# login local
Switch(config-line)# exit
Switch(config)# ip ssh version 2
Switch(config)# end
Switch# copy running-config startup-config
```

## Change Full-Duplex

```bash
Switch> enable
Switch# configure terminal
Switch(config)# interface <interface>
Switch(config-if)# duplex <full/half>
Switch(config-if)# speed <10/100/1000/10000>
Switch(config-if)# end
Switch# copy running-config startup-config
```

## Set password for console

```bash
Switch> enable
Switch# configure terminal
Switch(config)# line console 0
Switch(config-line)# password <password>
Switch(config-line)# login
Switch(config-line)# end
Switch# copy running-config startup-config
```

## Password for exec mode

```bash
Switch> enable
Switch# configure terminal
Switch(config)# enable secret <password>
Switch(config)# end
Switch# copy running-config startup-config
```

## Encrypt Passwords

```bash
Switch> enable
Switch# configure terminal
Switch(config)# service password-encryption
Switch(config)# end
Switch# copy running-config startup-config
```

## Set hostname

```bash
Switch> enable
Switch# configure terminal
Switch(config)# hostname <hostname>
Switch(config)# end
Switch# copy running-config startup-config
```

## Set banner

```bash
Switch> enable
Switch# configure terminal
Switch(config)# banner motd <banner>
Switch(config)# end
Switch# copy running-config startup-config
```

## Interface Configuration

```bash
Switch> enable
Switch# configure terminal
Switch(config)# interface <interface>
Switch(config-if)# ip address <ip address> <subnet mask>
Switch(config-if)# ipv6 address <ipv6 address>/<prefix length>
Switch(config-if)# no shutdown
Switch(config-if)# description <description>
# Possible  VLAN configuration
```

## Loopback Interface

> Loopback interfaces are virtual interfaces that are always up and running. They are used for testing and troubleshooting.

```bash
Switch> enable
Switch# configure terminal
Switch(config)# interface loopback <number>
Switch(config-if)# ip address <ip address> <subnet mask>
Switch(config-if)# end
Switch# copy running-config startup-config
```

## Enable ipv6 routing

```bash
Router> enable
Router# configure terminal
Router(config)# ipv6 unicast-routing
Router(config)# end
Router# copy running-config startup-config
```

## Static Routes

On directly connected networks use the exit interface as the next-hop option.

### ipv4

```bash
Router> enable
Router# configure terminal
Router(config)# ip route <destination network> <subnet mask> <next-hop ip address> | <exit interface>
# Fully specified route
#Router(config)# ip route <destination network> <subnet mask> <interface> <next-hop ip address>
Router(config)# end
Router# copy running-config startup-config
```

### ipv6

```bash
Router> enable
Router# configure terminal
Router# ipv6 unicast-routing
Router(config)# ipv6 route <destination network>/<prefix length> <next-hop ip address> | <exit interface>
Router(config)# end
```

## Default Static Routes

```bash
Router> enable
Router# configure terminal
Router(config)# ip route 0.0.0.0 0.0.0.0 <next-hop ip address> | <exit interface>
Router(config)# end
Router# copy running-config startup-config
```

```bash
Router> enable
Router# configure terminal
Router(config)# ipv6 route ::/0 <next-hop ip address> | <exit interface>
Router(config)# end
Router# copy running-config startup-config
```

## Floating Static Routes

```bash
Router> enable
Router# configure terminal
Router(config)# ip route <destination network> <subnet mask> <next-hop ip address> <administrative distance mostly 5>
Router(config)# end
Router# copy running-config startup-config
```

## VLAN Config

### Switch

#### Create VLAN

```bash
Switch> enable
Switch# configure terminal
Switch(config)# vlan <vlan number>
Switch(config-vlan)# name <vlan name>
Switch(config-vlan)# end
```

#### Assign VLAN to Interface

```bash
Switch> enable
Switch# configure terminal
Switch(config)# interface <interface>
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan <vlan number>
Switch(config-if)# end
```

#### Assign VLAN to Trunk

```bash
Switch> enable
Switch# configure terminal
Switch(config)# interface <interface>
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk native vlan <native vlan number>
Switch(config-if)# switchport trunk allowed vlan <vlan number>
Switch(config-if)# end
```

#### Delete VLAN

```bash
Switch> enable
Switch# configure terminal
Switch(config)# no vlan <vlan number>
Switch(config)# end
```

### Router

#### Assign VLAN to subinterface

```bash
Router> enable
Router# configure terminal
Router(config)# interface <interface>.<vlan number>
Router(config-subif)# description <description>
Router(config-subif)# no shutdown
Router(config-subif)# encapsulation dot1Q <vlan number>
Router(config-subif)# ip address <ip address> <subnet mask>
Router(config-subif)# end
```

### Layer 3 Switch

#### Assign VLAN to SVI

```bash
Switch> enable
Switch# configure terminal
Switch(config)# interface vlan <vlan number>
Switch(config-if)# description <description>
Switch(config-if)# ip address <ip address> <subnet mask>
Switch(config-if)# no shutdown
Switch(config-if)# end
```

#### Routing configuration to other Layer 3 Device

```bash
Switch> enable
Switch# configure terminal
Switch(config)# interface <interface>
Switch(config-if)# no switchport
Switch(config-if)# ip address <ip address> <subnet mask>
Switch(config-if)# end
Switch(config)# ip route <destination network> <subnet mask> <next-hop ip address> | <exit interface>
Switch(config)# end
```

## EtherChannel with LACP

```bash
Switch> enable
Switch# configure terminal
Switch(config)# interface range <interface1> - <interface2>
Switch(config-if-range)# channel-group <number> mode active
Switch(config-if-range)# exit
Switch(config)# interface port-channel <number>
Switch(config-if)# description <description>
Switch(config-if)# no shutdown
## All other configurations like VLAN, IP, etc.
```

## DHCPv4

```bash
Router> enable
Router# configure terminal
Router(config)# ip dhcp excluded-address <start ip address> <end ip address>
### Create new pool
Router(config)# ip dhcp pool <pool name>
Router(dhcp-config)# network <network> <subnet mask>
Router(dhcp-config)# default-router <default gateway>
Router(dhcp-config)# dns-server <dns server>
##Router(dhcp-config)# domain-name <domain name>
Router(dhcp-config)# lease <days> <hours> <minutes>
##Router(dhcp-config)# netbios-name-server <netbios server>
```

### DHCPv4 Relay

```bash
Router> enable
Router# configure terminal
Router(config)# interface <interface>
Router(config-if)# ip helper-address <ip address of DHCP server>
Router(config-if)# end
```

### DHCPv4 Client

```bash
Router> enable
Router# configure terminal
Router(config)# interface <interface>
Router(config-if)# ip address dhcp
Router(config-if)# end
```

## DHCPv6

### Stateless DHCPv6 server

```bash
Router> enable
Router# configure terminal
Router(config)# ipv6 unicast-routing
Router(config)# ipv6 dhcp pool <pool name>
Router(config-dhcp)# dns-server <dns server>
Router(config-dhcp)# domain-name <domain name>
Router(config-dhcp)# ipv6 dhcp server <pool name>
Router(config-dhcp)# ipv6 nd other-config-flag
Router(config-dhcp)# end
```

### Stateless DHCPv6 client

```bash
Router> enable
Router# configure terminal
Router# ipv6 unicast-routing
Router(config)# interface <interface>
Router(config-if)# ipv6 enable
Router(config-if)# ipv6 address autoconfig
Router(config-if)# end
```

### Stateful DHCPv6 server

```bash
Router> enable
Router# configure terminal
Router(config)# ipv6 unicast-routing
Router(config)# ipv6 dhcp pool <pool name>
Router(config-dhcp)# address prefix <prefix> <prefix length>
Router(config-dhcp)# dns-server <dns server>
Router(config-dhcp)# domain-name <domain name>
Router(config-dhcp)# ipv6 dhcp server <pool name>
Router(config-dhcp)# ipv6 nd managed-config-flag
Router(config-dhcp)# ipv6 nd prefix default no-autoconfig
Router(config-dhcp)# end
```

### Stateful DHCPv6 client

```bash
Router> enable
Router# configure terminal
Router# ipv6 unicast-routing
Router(config)# interface <interface>
Router(config-if)# ipv6 enable
Router(config-if)# ipv6 address dhcp
Router(config-if)# end
```

### DHCPv6 Relay

```bash
Router> enable
Router# configure terminal
Router(config)# interface <interface>
Router(config-if)# ipv6 dhcp relay destination <ip address of DHCP server> <interface>
```
