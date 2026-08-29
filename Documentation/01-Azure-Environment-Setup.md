# Azure Environment Setup

## Overview

This document describes the completed initial configuration and organization of the Azure Cloud Support & Administration Lab.

The environment was designed to simulate practical Azure administration and cloud-support responsibilities while maintaining a controlled, cost-conscious lab scope.

The lab established the resource organization, naming standards, governance tags, regional configuration, and administrative foundation used throughout the remainder of the project.

The environment later supported hands-on work involving:

- Microsoft Entra ID
- Azure RBAC
- Azure Virtual Network
- Network Security Groups
- Azure Storage
- Azure Policy
- Azure Cost Management
- Azure Monitor
- Azure Activity Log
- Resource Health
- Azure Advisor
- Azure Service Health
- Log Analytics
- KQL
- Azure Monitor Workbooks
- Cloud troubleshooting
- Help-desk incident documentation

---

## Objectives

The environment setup focused on the following objectives:

- Establish an organized Azure lab environment
- Configure a dedicated resource group
- Apply consistent resource naming
- Implement governance tags
- Maintain clear resource ownership and purpose
- Support least-privilege access testing
- Prepare networking and storage resources
- Support monitoring and logging
- Provide an environment for controlled troubleshooting
- Maintain cost awareness throughout the lab
- Document configuration decisions and limitations

---

# Azure Resource Organization

Azure resources were organized around a dedicated resource group:

`RG-IT-Support-Lab`

The resource group served as the primary administrative boundary for the cloud-support lab.

It provided a centralized location for managing and reviewing:

- Networking resources
- Storage resources
- Monitoring resources
- Log Analytics
- Alerting
- Governance
- Access control
- Resource health
- Diagnostic configuration

Using a dedicated resource group also made it easier to apply RBAC, tags, Azure Policy, monitoring, and troubleshooting practices at a consistent scope.

---

## Resource Group

### Name

`RG-IT-Support-Lab`

### Purpose

The resource group was created as the centralized resource container for the Azure Cloud Support & Administration Lab.

Its purpose was to separate lab resources from unrelated Azure resources while providing a realistic administrative scope for:

- Resource deployment
- Access management
- Governance
- Monitoring
- Troubleshooting
- Cost review

---

# Naming Convention

A consistent naming convention was used to make Azure resources easier to identify and administer.

Major resource names included:

- `RG-IT-Support-Lab`
- `VNET-IT-Support`
- `SNET-Workstations`
- `NSG-IT-Support`
- `stitsupportlab002`
- `LAW-IT-Support-Lab`

Additional named resources created during the project included:

- `Activity-Log-to-LAW`
- `IT-Support-Monitoring-Workbook`
- `IT-Support-Lab-Monthly-Budget`
- `Require-Environment-Tag`
- `Protect-Storage-Account`
- `ag-it-support-alerts`
- `ag-service-health-alerts`
- `ALERT-Storage-Resource-Health`
- `ALERT-Advisor-High-Reliability`
- `ALERT-Azure-Service-Health`

The naming convention emphasized:

- Resource purpose
- Technology or service type
- Lab ownership
- Administrative readability
- Consistency across Azure services

---

# Resource Tags

Governance tags were applied to identify the purpose and ownership of lab resources.

The primary tag structure used during the completed lab included:

- `Environment = Lab`
- `Department = IT`
- `Purpose = Cloud-Support-Training`
- `Owner = IT-Support`

These tags provided a consistent method for classifying resources.

They also supported later governance work involving Azure Policy.
---

# Initial Environment Configuration

## Step 1 — Verify Azure Access

The Azure portal was accessed using an administrative account with permission to configure resources required for the lab.

Before creating resources, the available Azure subscription and resource-deployment capabilities were reviewed.

The subscription provided access to the Azure services required for the majority of the project.

Subscription-specific identifiers are intentionally excluded from this public documentation.

---

## Step 2 — Create the Resource Group

The primary resource group was configured as:

`RG-IT-Support-Lab`

The resource group became the central scope for the Azure support environment.

After creation, the resource group was verified through the Azure portal.

### Validation

The following were confirmed:

- The resource group existed
- The correct Azure subscription was selected
- The resource group was available for resource deployment
- Resources could be organized under the lab scope
- Access-control configuration could be applied
- Monitoring data could be reviewed
- Governance configuration could be applied

---

# Resource Group Evidence

Screenshot evidence was captured for the resource group configuration.

### Resource Group Overview

`Screenshots/Resource-Groups/01-Azure-Resource-Group.png`

This screenshot documents the Azure resource group used for the lab.

### Resource Group Resources

`Screenshots/Resource-Groups/02-Resource-Group-Resources.png`

This screenshot demonstrates resources organized within the lab resource group.

### Governance Tags

`Screenshots/Resource-Groups/03-Resource-Group-Governance-Tags.png`

This screenshot demonstrates the governance tags applied to the resource group.

---

# Step 3 — Configure Governance Tags

Tags were applied to the lab environment to provide resource classification and administrative context.

The completed tag structure included:

`Environment = Lab`

`Department = IT`

`Purpose = Cloud-Support-Training`

`Owner = IT-Support`

The tags established a consistent governance model that could later be validated through Azure Policy.

---

# Azure Policy Integration

The environment setup later supported Azure Policy configuration.

The built-in policy:

`Require a tag on resource groups`

was assigned to the lab scope.

The assignment was named:

`Require-Environment-Tag`

The required tag was:

`Environment`

Because `RG-IT-Support-Lab` contained:

`Environment = Lab`

the resource group could be evaluated against the governance requirement.

This extended the initial tagging strategy into a practical Azure governance exercise.

---

# Networking Foundation

The environment included a dedicated Azure networking structure.

Configured resources included:

- `VNET-IT-Support`
- `SNET-Workstations`
- `NSG-IT-Support`

These resources established the networking foundation for the lab.

The Network Security Group was later used in a controlled troubleshooting scenario involving TCP port 3389.

A temporary deny rule was introduced, investigated, and removed to demonstrate NSG troubleshooting.

Detailed networking configuration is documented in:

`Documentation/03-Azure-Networking.md`

---

# Storage Foundation

Azure Storage became one of the primary services used throughout the support lab.

The primary completed storage account was:

`stitsupportlab002`

The storage environment supported exercises involving:

- Private blob access
- Microsoft Entra authentication
- Azure RBAC
- Management-plane access
- Data-plane access
- Storage networking
- Lifecycle management
- Blob soft delete
- Container soft delete
- Blob versioning
- Resource locks
- Blob recovery
- Container recovery

Detailed storage configuration is documented in:

`Documentation/04-Storage.md`
---

# Identity and Access Foundation

Microsoft Entra ID and Azure RBAC were incorporated into the environment to provide realistic identity and access-management scenarios.

A test identity was used to investigate access behavior under different RBAC configurations.

Roles used during the lab included:

- Reader
- Storage Blob Data Reader

This allowed the environment to demonstrate the distinction between:

- Authentication and authorization
- Management-plane permissions and data-plane permissions
- Resource-level access and resource-group access
- Required permissions and excessive permissions

The identity environment later supported multiple documented troubleshooting incidents.

Detailed identity and RBAC configuration is available in:

`Documentation/05-Identity-RBAC.md`

---

# Monitoring Foundation

The Azure environment was extended with monitoring and observability services.

Monitoring components included:

- Azure Activity Log
- Azure Monitor
- Alert rules
- Action groups
- Resource Health
- Azure Advisor
- Azure Service Health
- Log Analytics
- Diagnostic settings
- KQL
- Azure Monitor Workbooks

A Log Analytics workspace was created:

`LAW-IT-Support-Lab`

Azure Activity Log data was exported through the diagnostic setting:

`Activity-Log-to-LAW`

This created the foundation for centralized activity investigation using KQL.

Detailed monitoring configuration is documented in:

`Documentation/06-Monitoring.md`

---

# Cost Management

Cost awareness was incorporated into the environment instead of treating the Azure subscription as an unlimited lab environment.

A monthly budget was configured:

`IT-Support-Lab-Monthly-Budget`

Budget amount:

`$10`

The budget demonstrated basic Azure Cost Management practices and proactive spending awareness.

Cost considerations also influenced the virtual-machine deployment decision.

---

# Virtual Machine Deployment Evaluation

A Windows Azure virtual machine was evaluated during the project but intentionally not deployed.

The original design considered a VM named:

`VM-ITSupport-01`

During deployment evaluation, low-cost B-series VM sizes were unavailable for the lab subscription in the tested Azure regions.

A larger D-series option was available, but its additional cost was not justified for the remaining support-lab objectives.

Rather than deploying a larger VM solely to generate portfolio screenshots, the VM deployment was deferred.

This means the repository does not represent the following as completed work:

- A deployed Windows Azure VM
- A successful Azure RDP session
- A failed live RDP session
- VM performance monitoring
- VM operating-system administration

Networking and NSG troubleshooting were completed independently without claiming that a live VM existed.

The complete VM feasibility assessment is documented in:

`Documentation/02-Virtual-Machines.md`

---

# Environment Validation

After the environment was established, the configuration was validated through subsequent administrative and troubleshooting work.

Validation included confirming that:

- `RG-IT-Support-Lab` existed
- Azure resources could be deployed into the lab environment
- Governance tags were applied
- Azure Policy could evaluate the resource group
- RBAC assignments could be configured
- Least-privilege access behavior could be tested
- Virtual networking could be configured
- NSG rules could be modified and investigated
- Azure Storage could be deployed
- Blob access could be tested
- Storage networking controls could be modified
- Resource locks could protect resources
- Deleted storage data could be recovered
- Activity Log captured administrative operations
- Azure Monitor alerts could be configured
- Action groups could deliver notifications
- Log Analytics could ingest Azure Activity data
- KQL could query ingested activity
- Azure Monitor Workbooks could visualize operational data

These validations demonstrated that the environment functioned as a practical Azure cloud-support lab rather than only a collection of deployed resources.
---

# Troubleshooting Integration

The Azure environment was intentionally used to create controlled support scenarios.

The completed project contains 10 structured help-desk tickets covering:

1. Blob Storage Access Denied
2. Azure Monitor Administrative Alert
3. NSG RDP Connectivity Issue
4. RBAC Resource Visibility Issue
5. Storage Network Access Failure
6. Resource Lock Preventing Deletion
7. Azure Blob Soft-Delete Recovery
8. Resource Group Reader Write Denied
9. Service Health Alert Configuration Failure
10. Log Analytics Activity Investigation

These scenarios required investigation across multiple Azure technical layers.

The troubleshooting process included:

- Reproducing symptoms
- Reviewing Azure configuration
- Reviewing RBAC scope
- Investigating management-plane permissions
- Investigating data-plane permissions
- Reviewing network controls
- Reviewing Activity Log
- Reviewing Azure Monitor
- Investigating service configuration errors
- Querying Log Analytics
- Applying corrective actions
- Retesting functionality
- Verifying security boundaries
- Documenting root cause and resolution

Detailed troubleshooting documentation is available in:

`Documentation/07-Troubleshooting.md`

---

# Security and Privacy

The lab used non-production resources and test data.

Sensitive Azure identifiers are intentionally excluded from the written documentation where they are not required to demonstrate the technical work.

Public repository content should not expose:

- Personal email addresses
- User principal names
- Subscription IDs
- Tenant IDs
- Object IDs
- Principal IDs
- Workspace IDs
- Public or private IP addresses
- Activity IDs
- Correlation IDs
- Request IDs
- Access keys
- SAS tokens
- Passwords
- Authentication tokens
- Connection strings

Screenshots should be reviewed before publication and sensitive identifiers obscured where necessary.

No credentials, passwords, access keys, or authentication secrets should be committed to the repository.

---

# Documentation Structure

The completed Azure documentation set includes:

- `01-Azure-Environment-Setup.md`
- `02-Virtual-Machines.md`
- `03-Azure-Networking.md`
- `04-Storage.md`
- `05-Identity-RBAC.md`
- `06-Monitoring.md`
- `07-Troubleshooting.md`

Together, these documents provide technical evidence covering environment setup, deployment decisions, networking, storage, identity, monitoring, governance, and troubleshooting.

---

# Skills Demonstrated

This portion of the project demonstrates experience with:

- Microsoft Azure
- Azure Portal
- Azure resource organization
- Resource groups
- Resource naming
- Resource tagging
- Microsoft Entra ID
- Azure RBAC
- Least-privilege access
- Azure Virtual Network
- Azure Subnets
- Network Security Groups
- Azure Storage
- Azure Policy
- Azure Cost Management
- Azure Monitor
- Azure Activity Log
- Azure Service Health
- Azure Advisor
- Resource Health
- Log Analytics
- KQL
- Azure Monitor Workbooks
- Cloud governance
- Cloud troubleshooting
- Cost-aware administration
- Technical documentation

---

# Environment Outcome

The initial Azure environment developed into a complete cloud-support and administration lab.

The final environment provided hands-on experience across:

**Resource Organization → Identity → Networking → Storage → Governance → Monitoring → Troubleshooting**

The project demonstrates how Azure services interact during practical administration and technical-support scenarios.

Rather than focusing only on resource deployment, the environment was used to demonstrate:

- Least-privilege access
- Security boundaries
- Controlled failure testing
- Root-cause analysis
- Resource protection
- Data recovery
- Monitoring
- Logging
- Governance
- Cost awareness
- Support-ticket documentation

The resulting environment provides a documented foundation for entry-level Azure cloud support, IT support, and junior cloud administration portfolio work.
