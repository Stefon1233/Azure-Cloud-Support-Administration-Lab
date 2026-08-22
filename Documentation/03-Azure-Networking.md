# Azure Networking

## Overview

This section documents the planned networking architecture for the Azure 
Cloud Support & Administration Lab.

The network will provide connectivity for Azure resources while demonstrating 
Virtual Networks, subnets, Network Security Groups, IP addressing, security 
rules, DNS, and structured connectivity troubleshooting.

## Objectives

- Create an Azure Virtual Network
- Configure an IPv4 address space
- Create a subnet
- Connect Azure resources to the subnet
- Configure a Network Security Group
- Review inbound and outbound security rules
- Understand private and public IP addressing
- Test network connectivity
- Troubleshoot blocked traffic
- Troubleshoot DNS and network configuration issues

## Planned Network Architecture

### Virtual Network

- **Name:** VNET-IT-Support
- **Resource Group:** RG-IT-Support-Lab
- **Region:** To be determined
- **Address Space:** To be configured

### Subnet

- **Name:** SNET-Workstations
- **Address Range:** To be configured

### Network Security Group

- **Name:** NSG-IT-Support
- **Purpose:** Control network traffic to lab resources

## Virtual Network

VNET-IT-Support will provide the private network used by Azure resources in 
the lab.

The VNet configuration will include:

- IPv4 address space
- Subnet
- Connected network interfaces
- DNS configuration
- Security configuration

## Subnet

SNET-Workstations will provide a logical network segment for the lab virtual 
machine.

The subnet configuration will be reviewed for:

- Address range
- Available addresses
- Connected resources
- Network Security Group association
- Routing behavior

## Network Security Group

NSG-IT-Support will be used to control allowed and denied network traffic.

The lab will review:

- Inbound security rules
- Outbound security rules
- Rule priority
- Source
- Source port
- Destination
- Destination port
- Protocol
- Allow/Deny action

## Planned Security Rules

Actual values will be documented after configuration.

| Priority | Rule | Source | Destination | Port | Protocol | Action |
|---|---|---|---|---|---|---|
| TBD | Administrative Access | TBD | VM | TBD | TCP | Allow |
| TBD | Test Deny Rule | TBD | VM | TBD | TBD | Deny |

## Private IP Addressing

The Azure VM will receive a private IP address from its subnet.

Private addressing will be used to demonstrate:

- Internal resource communication
- Subnet membership
- Network interface configuration
- Azure private networking

## Public IP Addressing

A public IP may be used when required for remote administration.

The lab will document:

- Why a public IP is required
- How it is associated
- Security considerations
- How access is restricted
- When it can be removed

## DNS

DNS troubleshooting will be included in the lab.

The investigation process will distinguish between:

- IP connectivity
- DNS resolution
- Hostname resolution
- Azure VNet DNS configuration
- Client DNS configuration

A system that can reach an IP address but cannot reach the same service by 
hostname will be treated as a potential DNS-resolution problem.

## Connectivity Troubleshooting Methodology

When network connectivity fails, troubleshooting will proceed systematically.

### Layer 1 — Resource State

Verify the Azure resource is running and available.

### Layer 2 — Network Interface

Verify:

- NIC exists
- NIC is attached
- IP configuration is correct

### Layer 3 — Virtual Network

Verify:

- Correct VNet
- Correct subnet
- Correct address range

### Layer 4 — Security

Verify:

- NSG association
- Inbound rules
- Outbound rules
- Priority
- Source
- Destination
- Port
- Protocol
- Allow/Deny action

### Layer 5 — Name Resolution

Verify DNS only after basic IP connectivity has been evaluated.

### Layer 6 — Application or Service

Verify that the destination service is actually listening and available.

## Planned Troubleshooting Scenarios

### NSG Connectivity Failure

A required connection will be intentionally prevented by network security 
configuration.

The investigation will review:

- NSG association
- Rule priority
- Source
- Destination
- Required port
- Allow/Deny action

### DNS Connectivity Failure

A scenario will demonstrate the difference between basic network connectivity 
and hostname resolution.

### Incorrect Network Configuration

A network configuration issue will be investigated using:

- NIC
- IP configuration
- VNet
- Subnet
- NSG
- DNS
- Routes
- Destination
- Required service port

## Validation Plan

Verify:

- VNET-IT-Support exists
- SNET-Workstations exists
- Address ranges do not conflict
- VM uses the correct subnet
- NSG is associated correctly
- Required traffic is allowed
- Unnecessary traffic remains restricted
- DNS behavior can be tested
- Network configuration can be systematically troubleshot

## Screenshot Evidence

Planned screenshots:

- VNet overview
- Address space
- Subnet
- NSG overview
- Security rules
- VM network interface
- IP configuration
- Failed connectivity scenario
- Corrected connectivity scenario

## Skills Demonstrated

- Azure Virtual Networks
- Azure subnets
- Network Security Groups
- IPv4 addressing
- Firewall rules
- DNS
- Network troubleshooting
- Connectivity testing
- Cloud networking
