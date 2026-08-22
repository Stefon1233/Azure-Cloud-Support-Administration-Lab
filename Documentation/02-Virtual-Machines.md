# Azure Virtual Machines

## Overview

This section documents the planned deployment, administration, and 
troubleshooting of a Windows virtual machine within the Azure Cloud Support & 
Administration Lab.

The virtual machine will provide a realistic cloud-hosted Windows system for 
practicing remote administration, networking, monitoring, access control, and 
help-desk troubleshooting.

## Objectives

The objectives of this portion of the lab are to:

- Deploy a Windows virtual machine in Microsoft Azure
- Configure VM networking
- Review VM sizing and resource configuration
- Understand public and private IP addressing
- Configure remote administrative access
- Connect to the VM using Remote Desktop Protocol
- Perform VM lifecycle operations
- Review VM resource information
- Troubleshoot VM connectivity and availability issues
- Document support scenarios involving Azure virtual machines

## Planned Virtual Machine

- **VM Name:** VM-ITSupport-01
- **Resource Group:** RG-IT-Support-Lab
- **Operating System:** Windows
- **Region:** To be determined during deployment
- **VM Size:** To be selected based on lab requirements and cost
- **Virtual Network:** VNET-IT-Support
- **Subnet:** SNET-Workstations
- **Network Security Group:** NSG-IT-Support
- **Private IP:** To be assigned during deployment
- **Public IP:** To be determined during deployment

## Virtual Machine Deployment

The VM will be deployed through the Microsoft Azure portal.

Deployment configuration will include:

1. Selecting the correct Azure subscription
2. Selecting RG-IT-Support-Lab
3. Creating VM-ITSupport-01
4. Selecting an appropriate Windows image
5. Selecting a cost-conscious VM size
6. Configuring administrator authentication
7. Connecting the VM to VNET-IT-Support
8. Connecting the VM to SNET-Workstations
9. Configuring network access
10. Reviewing the deployment before creation

Actual deployment settings will be recorded after the VM has been created.

## VM Networking

The virtual machine will use an Azure network interface connected to the lab 
virtual network.

The networking configuration will be reviewed for:

- Network interface
- Virtual Network
- Subnet
- Private IP address
- Public IP configuration
- Network Security Group
- Inbound security rules
- Outbound connectivity

## Remote Administration

Remote Desktop Protocol will be used as one method of administering the 
Windows virtual machine.

The planned troubleshooting process for RDP includes checking:

1. VM power state
2. VM IP configuration
3. Network interface status
4. Network Security Group rules
5. TCP port 3389 access
6. Source restrictions
7. Windows Remote Desktop configuration
8. Authentication
9. Connectivity from the client system

RDP access will only be enabled when required for the lab.

## VM Lifecycle Management

The lab will demonstrate common Azure VM administrative operations including:

- Start
- Restart
- Stop
- Deallocate
- Review status
- Review configuration
- Review networking
- Review disks
- Review monitoring information

The difference between a running, stopped, and deallocated VM will be 
documented after testing.

## Planned Support Scenarios

The virtual machine will support several help-desk scenarios.

### RDP Connection Failure

A user will report that they cannot establish an RDP session with the Azure 
VM.

The investigation will include:

- VM state
- IP addressing
- NSG rules
- Port configuration
- RDP configuration
- Authentication
- Connectivity testing

### VM Unavailable

A user will report that the Azure-hosted system is unavailable.

The investigation will include:

- VM power state
- Resource status
- Azure Activity Log
- Network configuration
- Recent administrative changes

### VM Performance Issue

A user will report poor performance.

The investigation will include:

- CPU metrics
- Disk activity
- Network activity
- VM configuration
- Azure Monitor
- Recent changes
- Workload behavior

## Security Considerations

The VM configuration will follow basic security practices including:

- Avoid unnecessary inbound ports
- Restrict remote administrative access
- Use appropriate authentication
- Apply least privilege
- Avoid publishing credentials
- Avoid exposing sensitive IP or account information in screenshots
- Stop or deallocate resources when they are not required

## Validation Plan

After deployment, verify:

- VM exists in RG-IT-Support-Lab
- VM reaches the expected power state
- Network interface is attached
- Private IP is assigned
- VM is connected to the correct VNet and subnet
- Required network rules are configured
- Administrative connectivity works when intentionally permitted
- VM can be restarted
- VM can be stopped and started
- Monitoring information is available

## Screenshot Evidence

Planned screenshots:

- VM overview
- VM deployment/configuration
- VM networking
- VM power state
- Successful RDP session
- VM monitoring information
- VM troubleshooting scenario

Screenshots will be added after the Azure environment is configured.

## Skills Demonstrated

- Microsoft Azure
- Azure Virtual Machines
- Windows administration
- Remote Desktop Protocol
- VM lifecycle management
- Azure networking
- Cloud administration
- Connectivity troubleshooting
- Technical documentation

