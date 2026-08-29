# Azure Virtual Machines - Deployment Feasibility and Support Planning

## Overview

This section documents the evaluation of Azure Virtual Machine deployment options within the Azure Cloud Support & Administration Lab.

A Windows virtual machine was originally planned as part of the environment to provide hands-on experience with Windows administration, Remote Desktop Protocol (RDP), VM lifecycle management, networking, monitoring, and troubleshooting.

During deployment planning, suitable low-cost B-series virtual machine sizes were unavailable for the lab subscription in the tested Azure regions.

Rather than deploying a larger and more expensive virtual machine solely to satisfy the original lab design, the deployment was intentionally deferred.

The investigation itself demonstrates an important cloud-support skill: evaluating Azure resource availability, subscription constraints, regional availability, and cost before deploying infrastructure.

---

## Original Deployment Objective

The planned virtual machine was:

- **VM Name:** `VM-ITSupport-01`
- **Resource Group:** `RG-IT-Support-Lab`
- **Operating System:** Windows
- **Virtual Network:** `VNET-IT-Support`
- **Subnet:** `SNET-Workstations`
- **Network Security Group:** `NSG-IT-Support`

The VM was intended to support:

- Windows administration
- Azure VM configuration
- Azure networking
- RDP troubleshooting
- VM lifecycle management
- Azure Monitor
- Activity Log investigations
- Help-desk troubleshooting scenarios

---

## Deployment Evaluation

Before deploying the virtual machine, I reviewed available Azure VM sizes with the goal of selecting a low-cost SKU appropriate for a temporary training environment.

The preferred approach was to use a small B-series virtual machine because the lab did not require production-level compute capacity.

Small B-series options were investigated in multiple Azure regions.

The tested regions included:

- North Central US
- East US

Suitable small B-series VM sizes were not available for the subscription during the deployment attempt.

A larger VM size such as a D-series option was available, but deploying a higher-cost VM was not justified for the objectives of this lab.

---

## Deployment Decision

The virtual machine deployment was intentionally deferred.

This decision was based on:

1. Subscription and SKU availability
2. Regional VM availability
3. Cost control
4. Actual lab requirements
5. Availability of other Azure services for demonstrating cloud-support skills

Deploying a larger VM would have added unnecessary cost without materially improving the portfolio.

This reflects a practical cloud-administration principle:

> Resources should be deployed based on technical requirements, availability, and cost rather than simply because they were included in an initial design.

---

## Troubleshooting Approach

When the preferred VM sizes were unavailable, the deployment issue was evaluated as a resource-availability and subscription constraint rather than a general Azure failure.

The investigation considered:

- Azure region
- Available VM SKUs
- Subscription limitations
- VM sizing
- Cost
- Alternative regions
- Whether the workload required a larger VM

Testing another region did not provide a suitable low-cost deployment option.

The available larger VM option was therefore not deployed.

---

## Cost Management Consideration

Cost management was an important part of the decision.

Cloud administrators should avoid provisioning oversized resources when a workload does not require them.

For a temporary IT support training environment, deploying a larger VM would introduce unnecessary compute charges.

Instead, the lab prioritized Azure services that could demonstrate relevant cloud-support capabilities without unnecessary infrastructure cost.

These included:

- Azure Storage
- Azure RBAC
- Microsoft Entra ID
- Azure Monitor
- Azure Activity Log
- Log Analytics
- Azure Monitor Workbooks
- Azure Policy
- Azure Advisor
- Azure Service Health
- Resource Health
- Cost Management

---

## Azure Networking Preparation

Although the Windows VM was not deployed, Azure networking was still configured and tested independently.

The networking environment included:

- Virtual Network
- Subnet
- Network Security Group
- Inbound security rules

The lab also included a simulated RDP-related NSG troubleshooting scenario.

A deny rule for TCP port `3389` was intentionally configured to demonstrate how Network Security Group rules can prevent Remote Desktop connectivity.

The configuration was investigated and the blocking rule was removed after troubleshooting.

This allowed RDP-related network troubleshooting concepts to be demonstrated without claiming that an actual VM RDP session occurred.

---

## Planned VM Networking Model

If `VM-ITSupport-01` were deployed, the intended network path would be:

`VM-ITSupport-01`

→ Azure Network Interface

→ `SNET-Workstations`

→ `VNET-IT-Support`

→ `NSG-IT-Support`

The NSG would control permitted inbound and outbound network traffic.

Remote administration would require evaluation of TCP port `3389`, source restrictions, IP configuration, NSG rules, operating-system configuration, and authentication.

---

## RDP Troubleshooting Methodology

For a future Azure Windows VM support incident, an RDP investigation would include:

1. Verify VM power state
2. Verify VM provisioning status
3. Review network interface configuration
4. Verify private and public IP configuration
5. Review subnet configuration
6. Review associated NSGs
7. Review effective security rules
8. Check TCP port `3389`
9. Check rule priorities
10. Verify source restrictions
11. Review Windows RDP configuration
12. Verify authentication
13. Review Azure Activity Log for recent changes
14. Review Azure Monitor and Resource Health

This methodology was incorporated into the networking portion of the lab even though the VM itself was not provisioned.

---

## Network Security Group Troubleshooting Scenario

A controlled NSG troubleshooting scenario was performed.

An inbound rule named:

`Deny-RDP-Test`

was configured to deny TCP traffic on port:

`3389`

The rule used a priority that caused the deny rule to be evaluated before a potential lower-priority allow rule.

The NSG configuration was reviewed to identify the blocking rule.

After identifying the cause, the test rule was removed.

This demonstrated:

- NSG rule evaluation
- Port-based troubleshooting
- Rule priority analysis
- RDP connectivity troubleshooting methodology
- Controlled configuration changes
- Verification after remediation

Supporting screenshots are stored in:

`../Screenshots/Troubleshooting/Networking/`

---

## VM Lifecycle Knowledge

Although lifecycle operations were not performed on an actual VM in this lab, the planned support workflow included:

- Start
- Restart
- Stop
- Deallocate
- Review status
- Review configuration
- Review networking
- Review disks
- Review monitoring information

An important Azure cost-management distinction is the difference between stopping an operating system and deallocating the Azure VM resource.

VM lifecycle management remains an important area for future expansion of the lab when an appropriate low-cost VM SKU is available.

---

## Security Considerations

A future VM deployment would follow basic cloud security practices.

These include:

- Avoid unnecessary inbound ports
- Restrict administrative access
- Apply least privilege
- Use appropriate authentication
- Review NSG rules
- Avoid exposing credentials
- Avoid exposing sensitive IP information
- Monitor administrative changes
- Stop or deallocate unnecessary compute resources
- Avoid oversized infrastructure

The networking portion of the current lab demonstrates several of these principles without requiring an active VM.

---

## Support Decision

The VM deployment limitation was not treated as a reason to abandon the Azure lab.

Instead, the lab scope was adjusted.

Hands-on work continued across:

- Storage administration
- Identity and access management
- Azure RBAC
- Resource-group RBAC
- Azure networking
- Network Security Groups
- Resource locks
- Blob recovery
- Container recovery
- Azure Monitor
- Alert rules
- Action Groups
- Azure Policy
- Azure Advisor
- Resource Health
- Service Health
- Log Analytics
- KQL
- Azure Monitor Workbooks
- Cost Management

This allowed the environment to demonstrate cloud-support and administration skills while maintaining cost awareness.

---

## Future Expansion

If a suitable low-cost VM SKU becomes available, the lab can be expanded with:

- Windows Server or Windows client VM deployment
- Network interface configuration
- Private IP configuration
- Controlled public IP configuration
- RDP administration
- VM start/restart/deallocate operations
- VM metrics
- Boot diagnostics
- VM-specific Azure Monitor alerts
- Windows Event Log collection
- Log Analytics agent integration
- VM performance troubleshooting
- VM availability troubleshooting

These would be treated as future enhancements rather than completed tasks.

---

## Validation

The VM portion of the lab is considered complete as a deployment feasibility and support-planning exercise.

Validated outcomes include:

- Evaluated Azure VM deployment requirements
- Reviewed available VM sizes
- Considered multiple Azure regions
- Identified low-cost SKU availability limitations
- Evaluated a larger available VM option
- Chose not to deploy unnecessarily expensive compute
- Maintained cost-conscious cloud administration
- Configured the supporting Azure network environment
- Demonstrated NSG troubleshooting concepts
- Documented future VM troubleshooting methodology
- Continued the lab using other Azure services

---

## Screenshot Evidence

The strongest related evidence is contained in the networking and troubleshooting sections of the repository.

Relevant screenshots include:

- `../Screenshots/Networking/01-Virtual-Network-Overview.png`
- `../Screenshots/Networking/02-NSG-Subnet-Association.png`
- `../Screenshots/Networking/03-NSG-Default-Inbound-Rules.png`
- `../Screenshots/Troubleshooting/Networking/01-NSG-Inbound-Rules-Before-Change.png`
- `../Screenshots/Troubleshooting/Networking/02-NSG-Deny-RDP-Rule.png`
- `../Screenshots/Troubleshooting/Networking/03-NSG-RDP-Blocking-Rule-Diagnosed.png`
- `../Screenshots/Troubleshooting/Networking/04-NSG-Blocking-Rule-Removed.png`

No screenshots are presented as evidence of an actual VM deployment or successful RDP session because those actions were not completed.

---

## Skills Demonstrated

- Microsoft Azure
- Azure resource planning
- VM sizing evaluation
- Cloud cost awareness
- Regional resource availability analysis
- Subscription constraint troubleshooting
- Azure networking
- Network Security Groups
- RDP troubleshooting methodology
- Azure resource governance
- Technical decision-making
- Cloud support documentation

---

## Outcome

The original plan called for deployment of a Windows Azure VM.

Suitable low-cost VM SKUs were not available under the lab subscription in the tested regions. A larger VM option was available, but deploying it would have introduced unnecessary cost.

The VM deployment was therefore intentionally deferred.

Rather than presenting an incomplete deployment as completed work, this documentation records the actual technical investigation, deployment decision, networking preparation, troubleshooting methodology, and cost-management considerations.

The lab remains suitable for demonstrating Azure cloud-support and administration skills while accurately representing the work performed.
