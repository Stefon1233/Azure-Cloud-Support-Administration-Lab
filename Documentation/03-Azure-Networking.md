# Azure Networking

## Overview

This section documents the Azure networking configuration and troubleshooting work completed in the Azure Cloud Support & Administration Lab.

The networking portion of the lab focused on Azure Virtual Networks, subnets, Network Security Groups (NSGs), security-rule evaluation, port-based access control, and structured connectivity troubleshooting.

A controlled RDP-related networking scenario was performed by intentionally creating an NSG rule that denied TCP port 3389. The rule was investigated, identified as the source of the simulated connectivity problem, and removed.

Because a Windows virtual machine was not ultimately deployed, this documentation does not claim an actual RDP connection failure or successful RDP session.

---

## Objectives Completed

The networking portion of the lab demonstrated:

- Azure Virtual Network administration
- Subnet configuration
- Network Security Group administration
- NSG-to-subnet association
- Inbound security-rule review
- Default NSG rule analysis
- Security-rule priority analysis
- TCP port troubleshooting
- Allow and deny rule evaluation
- Controlled configuration changes
- Connectivity troubleshooting methodology
- Azure networking documentation

---

## Network Architecture

The lab networking environment included:

### Virtual Network

- **Name:** `VNET-IT-Support`
- **Resource Group:** `RG-IT-Support-Lab`
- **Purpose:** Provide private Azure networking for the IT support lab

### Subnet

- **Name:** `SNET-Workstations`
- **Purpose:** Provide a logical network segment for supported lab resources

### Network Security Group

- **Name:** `NSG-IT-Support`
- **Purpose:** Control allowed and denied network traffic for the lab environment

---

## Virtual Network

`VNET-IT-Support` was configured as the primary Azure Virtual Network for the lab.

The VNet provided the networking foundation for demonstrating:

- Azure private networking
- Subnet organization
- NSG association
- Network security
- Future workload connectivity

The VNet configuration was reviewed through the Azure Portal and documented with screenshot evidence.

---

## Subnet

`SNET-Workstations` was configured as a subnet within the lab Virtual Network.

The subnet provided a logical network segment for resources that could be added to the environment.

The subnet configuration was reviewed for:

- VNet membership
- Address allocation
- Security association
- Network organization

The subnet was associated with `NSG-IT-Support`.

---

## Network Security Group

`NSG-IT-Support` was used to demonstrate Azure network traffic filtering.

The NSG configuration was reviewed for:

- Inbound security rules
- Default inbound rules
- Rule priorities
- Source
- Destination
- Destination port
- Protocol
- Allow/Deny action
- Subnet association

Understanding these properties is important because Azure evaluates NSG rules according to priority.

Lower priority numbers are evaluated before higher priority numbers.

A matching higher-priority deny rule can therefore block traffic before a lower-priority allow rule is evaluated.

---

## Default Inbound Security Rules

The default inbound NSG rules were reviewed as part of the networking investigation.

This demonstrated that Azure NSGs contain default behavior in addition to custom administrator-created rules.

When troubleshooting connectivity, both custom and default rules should be considered.

A technician should evaluate:

1. Rule priority
2. Source
3. Destination
4. Protocol
5. Destination port
6. Allow or Deny action
7. NSG association

This prevents troubleshooting from focusing only on whether an allow rule exists.

---

## Controlled RDP Blocking Scenario

A controlled networking problem was created to demonstrate NSG troubleshooting.

A custom inbound security rule named:

`Deny-RDP-Test`

was created.

The rule targeted:

- **Protocol:** TCP
- **Destination Port:** 3389
- **Action:** Deny
- **Priority:** 300

TCP port 3389 is commonly associated with Windows Remote Desktop Protocol.

The purpose of the rule was to simulate the network-layer conditions that could prevent RDP connectivity to an Azure Windows system.

No actual Azure VM or RDP session was required to demonstrate the NSG rule investigation.

---

## Initial State

Before introducing the test rule, the existing inbound NSG configuration was reviewed and documented.

This established a baseline before the troubleshooting scenario.

The baseline screenshot allowed the configuration before and after the change to be compared.

Evidence:

`../Screenshots/Troubleshooting/Networking/01-NSG-Inbound-Rules-Before-Change.png`

---

## Introducing the Failure

The `Deny-RDP-Test` rule was added to `NSG-IT-Support`.

The rule denied TCP traffic destined for port 3389.

This intentionally created a configuration that would block RDP traffic if an applicable Windows workload were attached behind the NSG.

Evidence:

`../Screenshots/Troubleshooting/Networking/02-NSG-Deny-RDP-Rule.png`

---

## Investigation

The NSG rules were reviewed to determine why TCP 3389 traffic would be blocked.

The investigation focused on:

- NSG association
- Custom inbound rules
- Rule priority
- Protocol
- Destination port
- Allow/Deny action

The `Deny-RDP-Test` rule was identified as the configuration responsible for the simulated RDP network restriction.

This demonstrated why rule priority and matching conditions must be reviewed during Azure connectivity troubleshooting.

Evidence:

`../Screenshots/Troubleshooting/Networking/03-NSG-RDP-Blocking-Rule-Diagnosed.png`

---

## Root Cause

The root cause of the simulated connectivity problem was:

`Deny-RDP-Test`

The rule explicitly denied TCP traffic on destination port 3389.

This represented a network-security configuration issue rather than:

- A Windows authentication problem
- A VM performance problem
- A DNS problem
- An Azure platform outage
- An application problem

Correctly identifying the troubleshooting layer prevents unnecessary changes elsewhere in the environment.

---

## Resolution

After identifying the test rule as the cause, `Deny-RDP-Test` was removed.

The NSG configuration was then reviewed again to verify that the intentional blocking rule was no longer present.

Evidence:

`../Screenshots/Troubleshooting/Networking/04-NSG-Blocking-Rule-Removed.png`

This completed the controlled NSG troubleshooting scenario.

---

## Verification

The resolution was verified by confirming that:

- `NSG-IT-Support` remained available
- The subnet association remained intact
- `Deny-RDP-Test` was removed
- The intentional TCP 3389 deny condition was no longer present

An actual RDP reconnection is not presented as verification evidence because a Windows VM was not deployed.

The verified result was the correction of the NSG configuration itself.

---

## Connectivity Troubleshooting Methodology

The lab used a structured approach for evaluating Azure network problems.

### 1. Resource State

Determine whether the affected Azure resource exists and is available.

### 2. Network Association

Determine which:

- VNet
- Subnet
- NIC
- NSG

apply to the affected workload.

### 3. IP Configuration

Review:

- Private addressing
- Public addressing where applicable
- Address assignment
- Subnet membership

### 4. Network Security

Review:

- NSG association
- Inbound rules
- Outbound rules
- Rule priority
- Source
- Destination
- Protocol
- Destination port
- Allow/Deny action

### 5. Routing

Determine whether routing configuration affects the network path.

### 6. DNS

If IP connectivity works but hostname-based connectivity does not, investigate name resolution.

### 7. Application or Service

After the Azure network path has been evaluated, verify whether the destination operating system, application, or service is actually listening and available.

This approach helps avoid changing unrelated configurations during troubleshooting.

---

## RDP Troubleshooting Methodology

For a future Azure Windows VM, an RDP support incident would include checking:

1. VM power and provisioning state
2. Network interface configuration
3. Private and public IP configuration
4. VNet and subnet membership
5. Associated NSGs
6. Effective security rules
7. TCP port 3389
8. Rule priorities
9. Source restrictions
10. Windows RDP configuration
11. Authentication
12. Azure Activity Log
13. Resource Health
14. Azure Monitor

The current lab directly demonstrated the NSG and TCP 3389 portions of this workflow.

---

## DNS Scope

DNS troubleshooting methodology was reviewed as part of the overall networking support process.

However, a dedicated DNS failure scenario was not completed during this lab.

Therefore, this repository does not present DNS resolution testing as completed hands-on evidence.

A future DNS investigation could compare:

- IP connectivity
- Hostname connectivity
- Azure-provided DNS
- Custom DNS configuration
- Client DNS configuration
- Name-resolution results

This remains a possible future extension of the lab.

---

## Public and Private IP Scope

Private and public IP concepts were considered as part of the network architecture.

Because the planned Windows VM was not deployed, the lab does not claim assignment or testing of a VM public or private IP address.

Future workload deployment could extend this section with:

- NIC IP configuration
- Dynamic or static private addressing
- Public IP configuration
- Source restrictions
- Remote administration
- IP-based connectivity testing

---

## Security Considerations

The networking configuration followed several cloud-security principles.

These included:

- Avoid unnecessary inbound access
- Understand NSG rule priority
- Review both allow and deny rules
- Limit administrative ports
- Remove temporary troubleshooting rules
- Avoid exposing unnecessary public services
- Document security changes
- Verify configuration after remediation

Temporary test configurations should not remain enabled after troubleshooting is complete.

The `Deny-RDP-Test` rule was therefore removed after the scenario.

---

## Production Considerations

In a production Azure environment, additional networking controls could include:

- Azure Bastion
- Just-in-Time VM access
- VPN connectivity
- Private endpoints
- Azure Firewall
- Network Watcher
- Network Security Group flow logs
- Centralized DNS
- User-defined routes
- Load balancing
- Application Gateway
- Network monitoring and alerting

These services were outside the completed scope of this lab and are not presented as implemented features.

---

## Validation

The networking portion of the lab was validated by confirming:

- `VNET-IT-Support` was configured
- `SNET-Workstations` was configured
- `NSG-IT-Support` was configured
- The NSG was associated with the subnet
- Default inbound rules were reviewed
- A controlled TCP 3389 deny rule was created
- Rule priority and action were investigated
- The blocking rule was identified
- The blocking rule was removed
- The corrected NSG configuration was verified

---

## Screenshot Evidence

### Azure Networking

- `../Screenshots/Networking/01-Virtual-Network-Overview.png`
- `../Screenshots/Networking/02-NSG-Subnet-Association.png`
- `../Screenshots/Networking/03-NSG-Default-Inbound-Rules.png`

### NSG Troubleshooting

- `../Screenshots/Troubleshooting/Networking/01-NSG-Inbound-Rules-Before-Change.png`
- `../Screenshots/Troubleshooting/Networking/02-NSG-Deny-RDP-Rule.png`
- `../Screenshots/Troubleshooting/Networking/03-NSG-RDP-Blocking-Rule-Diagnosed.png`
- `../Screenshots/Troubleshooting/Networking/04-NSG-Blocking-Rule-Removed.png`

---

## Related Help-Desk Ticket

The completed NSG troubleshooting scenario is documented in:

`../Help-Desk-Tickets/Ticket-003-NSG-RDP-Connectivity-Issue.md`

The ticket records:

- Initial configuration
- Controlled failure
- Investigation
- Root cause
- Remediation
- Verification
- Support considerations

---

## Skills Demonstrated

- Microsoft Azure
- Azure Virtual Networks
- Azure subnets
- Network Security Groups
- NSG rule analysis
- Rule priority
- TCP/IP
- Port-based troubleshooting
- RDP network troubleshooting methodology
- Cloud networking
- Connectivity troubleshooting
- Security configuration
- Root-cause analysis
- Technical documentation

---

## Outcome

The Azure networking environment was successfully configured and used to demonstrate network-security troubleshooting.

The strongest hands-on scenario involved intentionally denying TCP port 3389 through `NSG-IT-Support`, investigating the resulting configuration, identifying the blocking rule, and removing it.

The lab demonstrates practical Azure networking and support methodology without claiming an actual VM or RDP session that was not performed.
