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
Switch# show ipv6 route
Switch# show vlan
Switch# show vlan brief
Switch# show interfaces trunk
Switch# show interfaces status
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
