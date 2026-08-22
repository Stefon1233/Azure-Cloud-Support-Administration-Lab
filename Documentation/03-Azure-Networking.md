# Azure Networking

## Overview

This document covers the Azure networking components supporting the IT support lab.

## Objectives

- Create a Virtual Network
- Configure a subnet
- Configure a Network Security Group
- Understand private and public IP addressing
- Configure inbound rules
- Test connectivity
- Troubleshoot blocked network traffic

## Virtual Network

- Name: VNET-IT-Support
- Resource Group: RG-IT-Support-Lab
- Region:
- Address Space:

## Subnet

- Name: SNET-Workstations
- Address Range:

## Network Security Group

- Name: NSG-IT-Support

## Security Rules

Document configured rules:

| Priority | Name | Port | Protocol | Source | Destination | Action |
|---|---|---|---|---|---|---|
| | | | | | | |

## IP Addressing

### Private IP

Document the private address assigned to the VM.

### Public IP

Document whether a public IP is used and its purpose.

Do not publish unnecessary sensitive connection information in screenshots.

## Connectivity Testing

Test:

- VM network status
- RDP connectivity
- DNS resolution
- Internet connectivity
- NSG behavior

## Troubleshooting Scenario

Intentionally test how an NSG rule can prevent connectivity and document the troubleshooting process.

## Validation

Verify:

- VNet exists
- Subnet exists
- VM is attached to the correct subnet
- NSG is associated correctly
- Required traffic is permitted
- Unwanted traffic is restricted

## Screenshots

Add networking screenshots after configuration.

## Skills Demonstrated

- Azure Virtual Networks
- Subnets
- Network Security Groups
- IP addressing
- Firewall rules
- Network troubleshooting
- Connectivity testing
