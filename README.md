# Azure Cloud Support & Administration Lab

## Enterprise Azure Administration, Security, Monitoring, and Troubleshooting Portfolio

This project demonstrates hands-on Microsoft Azure cloud administration and technical support in a simulated IT environment.

The lab was built around practical cloud-support responsibilities rather than simply deploying Azure resources. It includes identity and access management, Azure RBAC, networking, storage administration, governance, monitoring, logging, KQL, cost management, data 
protection, and structured troubleshooting.

Controlled failures were intentionally introduced throughout the environment and investigated using Azure Portal tools, Activity Log, Azure Monitor, Log Analytics, KQL, Microsoft Entra ID, RBAC, Resource Health, Service Health, and configuration analysis.

The repository includes **10 documented help-desk incidents**, extensive screenshot evidence, detailed technical documentation, and an Azure architecture diagram.

---

## Project Highlights

- Configured a structured Microsoft Azure support lab
- Administered Microsoft Entra ID and Azure RBAC
- Implemented least-privilege access controls
- Distinguished management-plane and data-plane permissions
- Configured Azure Virtual Network, subnet, and Network Security Group
- Administered Azure Blob Storage
- Configured storage lifecycle management
- Enabled blob and container soft delete
- Enabled Blob Storage versioning
- Implemented Azure resource locks
- Recovered deleted Azure Storage data
- Configured Azure Monitor alerts and action groups
- Generated and investigated Azure monitoring alerts
- Configured Azure Cost Management budget alerts
- Implemented Azure Policy governance
- Reviewed Azure Resource Health
- Reviewed and acted on Azure Advisor recommendations
- Configured Azure Service Health alerting
- Deployed a Log Analytics workspace
- Exported Azure Activity Log through diagnostic settings
- Queried Azure activity using KQL
- Created an Azure Monitor Workbook
- Completed 10 structured cloud-support tickets
- Documented troubleshooting, root cause, remediation, and verification

---

## Technologies and Azure Services

| Area | Technologies |
|---|---|
| Cloud Platform | Microsoft Azure |
| Identity | Microsoft Entra ID |
| Access Control | Azure RBAC |
| Networking | Azure Virtual Network, Subnet, Network Security Groups |
| Storage | Azure Storage, Blob Storage |
| Security | RBAC, NSGs, Resource Locks, Private Blob Access |
| Data Protection | Blob Soft Delete, Container Soft Delete, Blob Versioning |
| Governance | Azure Policy, Resource Tags |
| Cost Management | Azure Budgets and Budget Alerts |
| Monitoring | Azure Monitor, Activity Log, Alert Rules |
| Health | Resource Health, Azure Service Health |
| Optimization | Azure Advisor |
| Logging | Log Analytics |
| Query Language | Kusto Query Language (KQL) |
| Visualization | Azure Monitor Workbooks |
| Documentation | Markdown, Git, GitHub |

---

## Architecture

The lab combines Azure identity, networking, storage, governance, monitoring, and troubleshooting services into a cloud-support environment.

[View the complete Azure architecture diagram](Diagrams/Azure-Lab-Architecture.md)

The architecture includes:

**Microsoft Entra ID → Azure RBAC → Networking → Storage → Governance → Azure Monitor → Log Analytics → KQL → Workbooks**

---

## Core Azure Environment

### Resource Group

Primary lab resource group:

`RG-IT-Support-Lab`

Governance tags were applied to organize and classify resources.

Examples included:

- `Environment = Lab`
- `Department = IT`
- `Purpose = Cloud-Support-Training`
- `Owner = IT-Support`

### Networking

The network environment included:

- `VNET-IT-Support`
- `SNET-Workstations`
- `NSG-IT-Support`

A controlled NSG rule was used to simulate an RDP-related network failure on TCP port 3389.

### Azure Storage

Primary storage account:

`stitsupportlab002`

The storage environment was used for access-control, networking, lifecycle, resource-protection, and recovery scenarios.
---

## Identity and Azure RBAC

Microsoft Entra ID and Azure RBAC were used to reproduce practical user-access problems.

The lab demonstrated the difference between:

- Authentication
- Authorization
- Management-plane permissions
- Data-plane permissions
- Resource-level scope
- Resource-group scope

Built-in roles used during testing included:

- `Reader`
- `Storage Blob Data Reader`

One scenario demonstrated that a user could have Blob Storage data permissions while lacking the management-plane visibility required for the expected Azure Portal workflow.

The final least-privilege configuration combined Reader with Storage Blob Data Reader.

Verification demonstrated:

- Required Azure resource visibility succeeded
- Required blob read access succeeded
- Unauthorized blob write access remained denied
- Resource-group administrative changes remained denied for Reader

[View Identity and RBAC documentation](Documentation/05-Identity-RBAC.md)

---

## Azure Storage Administration

The storage portion of the lab covered both normal administration and controlled failure scenarios.

Completed work included:

- Storage account deployment
- Private blob container configuration
- Blob upload
- Microsoft Entra authenticated access
- RBAC data access
- Storage network controls
- Lifecycle management
- Blob soft delete
- Container soft delete
- Blob versioning
- Resource locks
- Blob recovery
- Container recovery

A lifecycle rule named:

`Archive-Old-Support-Files`

was configured to transition eligible data based on age.

The data-protection configuration included:

- Blob soft delete: 7 days
- Container soft delete: 7 days
- Blob versioning: Enabled
- Previous-version cleanup: 30 days

A Delete lock named:

`Protect-Storage-Account`

was also used to demonstrate protection against accidental deletion.

[View Azure Storage documentation](Documentation/04-Storage.md)

---

## Azure Networking

Azure networking components were configured independently of a virtual-machine deployment.

The environment included:

- Virtual Network
- Subnet
- Network Security Group
- Inbound security rules

A controlled rule named:

`Deny-RDP-Test`

was configured to deny:

`TCP 3389`

The rule was investigated as a simulated RDP connectivity problem and then removed.

This demonstrated how an IT support technician can identify an NSG as the source of a blocked network path.

No live Azure VM or RDP session is represented as completed evidence.

[View Azure Networking documentation](Documentation/03-Azure-Networking.md)

---

## Azure Monitoring

Azure Monitor and Activity Log were used to provide visibility into administrative activity.

Completed monitoring work included:

- Resource-group Activity Log review
- RBAC operation investigation
- Administrative activity alert
- Action-group configuration
- Fired-alert investigation
- Email alert notification

The completed workflow demonstrated:

**Administrative Change → Activity Log → Azure Monitor → Alert → Action Group → Notification → Investigation**

[View Monitoring documentation](Documentation/06-Monitoring.md)

---

## Cost Management

A monthly Azure budget was configured to demonstrate proactive cloud-cost management.

Budget:

`IT-Support-Lab-Monthly-Budget`

Monthly threshold:

`$10`

Budget alerts were configured to provide notification as spending approached the defined threshold.

Cost awareness also influenced the decision not to deploy an unnecessarily large Azure VM solely for portfolio evidence.

---

## Azure Policy and Governance

Azure Policy was configured to demonstrate cloud governance.

Policy:

`Require a tag on resource groups`

Assignment:

`Require-Environment-Tag`

Required tag:

`Environment`

The lab resource group contained:

`Environment = Lab`

Policy compliance was then verified through Azure.

This demonstrated the relationship between resource organization, governance requirements, Azure Policy, and compliance.
---

## Resource Health, Advisor, and Service Health

Azure Resource Health was reviewed to distinguish resource-specific health problems from configuration or access problems.

Azure Advisor was also reviewed for reliability recommendations.

The Advisor environment identified recommendations including Azure Service Health alerting.

A high-impact reliability Advisor alert was configured:

`ALERT-Advisor-High-Reliability`

### Service Health Troubleshooting

The first Service Health alert configuration attempt failed because Service Health alert rules required an action group in the Global location.

The Azure error was investigated and the root cause identified.

A new Global action group was created:

`ag-service-health-alerts`

The Service Health alert was then successfully configured:

`ALERT-Azure-Service-Health`

This scenario became one of the documented support tickets in the repository.

---

## Log Analytics and KQL

A Log Analytics workspace was deployed:

`LAW-IT-Support-Lab`

Azure Activity Log data was exported to the workspace using:

`Activity-Log-to-LAW`

Diagnostic categories included:

- Administrative
- Security
- ServiceHealth
- Alert
- Recommendation
- Policy
- Autoscale
- ResourceHealth

KQL was then used to investigate Azure Activity data.

Example activity query:

    AzureActivity
    | where TimeGenerated > ago(1h)
    | project TimeGenerated, OperationNameValue, ActivityStatusValue, CategoryValue, ResourceGroup
    | sort by TimeGenerated desc
    | take 20

A summary query was also created:

    AzureActivity
    | where TimeGenerated > ago(24h)
    | summarize EventCount=count() by CategoryValue, ActivityStatusValue
    | sort by EventCount desc

This demonstrated foundational KQL skills including filtering, projection, sorting, aggregation, grouping, and event investigation.

---

## Azure Monitor Workbook

A reusable monitoring workbook was created:

`IT-Support-Monitoring-Workbook`

The workbook used data from:

`LAW-IT-Support-Lab`

Workbook views included:

### Azure Activity Summary

Aggregated Azure Activity events by category and status.

### Administrative Activity Details

Displayed detailed administrative control-plane operations.

### Recent Azure Activity

Provided a recent operational activity view.

The workbook converted raw Log Analytics data into a reusable cloud-support monitoring interface.

---

# Help-Desk Troubleshooting Portfolio

The lab includes **10 structured Azure support tickets**.

| # | Support Scenario |
|---|---|
| 001 | Blob Storage Access Denied |
| 002 | Azure Monitor Administrative Alert |
| 003 | NSG RDP Connectivity Issue |
| 004 | RBAC Resource Visibility Issue |
| 005 | Storage Network Access Failure |
| 006 | Resource Lock Preventing Deletion |
| 007 | Azure Blob Soft-Delete Recovery |
| 008 | Resource Group Reader Write Denied |
| 009 | Service Health Alert Configuration Failure |
| 010 | Log Analytics Activity Investigation |

### Ticket Documentation

- [Ticket 001 — Blob Storage Access Denied](Help-Desk-Tickets/Ticket-001-Blob-Storage-Access-Denied.md)
- [Ticket 002 — Azure Monitor Administrative Alert](Help-Desk-Tickets/Ticket-002-Azure-Monitor-Administrative-Alert.md)
- [Ticket 003 — NSG RDP Connectivity Issue](Help-Desk-Tickets/Ticket-003-NSG-RDP-Connectivity-Issue.md)
- [Ticket 004 — RBAC Resource Visibility Issue](Help-Desk-Tickets/Ticket-004-RBAC-Resource-Visibility-Issue.md)
- [Ticket 005 — Storage Network Access Failure](Help-Desk-Tickets/Ticket-005-Storage-Network-Access-Failure.md)
- [Ticket 006 — Resource Lock Preventing Deletion](Help-Desk-Tickets/Ticket-006-Resource-Lock-Preventing-Deletion.md)
- [Ticket 007 — Azure Blob Soft-Delete Recovery](Help-Desk-Tickets/Ticket-007-Azure-Blob-Soft-Delete-Recovery.md)
- [Ticket 008 — Resource Group Reader Write Denied](Help-Desk-Tickets/Ticket-008-Resource-Group-Reader-Write-Denied.md)
- [Ticket 009 — Service Health Alert Configuration Failure](Help-Desk-Tickets/Ticket-009-Service-Health-Alert-Configuration-Failure.md)
- [Ticket 010 — Log Analytics Activity Investigation](Help-Desk-Tickets/Ticket-010-Log-Analytics-Activity-Investigation.md)

---

## Troubleshooting Methodology

The lab used a structured support workflow:

1. Identify the symptom
2. Identify the affected resource and identity
3. Reproduce the problem
4. Capture the Azure error
5. Determine the affected technical layer
6. Review configuration and logs
7. Identify root cause
8. Apply the smallest corrective action
9. Retest required functionality
10. Verify security boundaries
11. Document the resolution

This approach helped distinguish between identity, RBAC, networking, storage, governance, monitoring, and platform-health problems.
---

# Documentation

Detailed technical documentation is available throughout the repository.

| Document | Topic |
|---|---|
| [01 — Azure Environment Setup](Documentation/01-Azure-Environment-Setup.md) | Azure environment and resource-group setup |
| [02 — Virtual Machines](Documentation/02-Virtual-Machines.md) | VM deployment feasibility and support planning |
| [03 — Azure Networking](Documentation/03-Azure-Networking.md) | VNet, subnet, NSG, and network troubleshooting |
| [04 — Azure Storage](Documentation/04-Storage.md) | Storage administration, security, lifecycle, and recovery |
| [05 — Identity & RBAC](Documentation/05-Identity-RBAC.md) | Microsoft Entra ID, RBAC, scope, and least privilege |
| [06 — Monitoring](Documentation/06-Monitoring.md) | Azure Monitor, governance, Log Analytics, KQL, and Workbooks |
| [07 — Troubleshooting](Documentation/07-Troubleshooting.md) | Completed Azure troubleshooting scenarios |

---

# Screenshot Evidence

Screenshot evidence is organized by technology and troubleshooting area.

    Screenshots/
    ├── Identity/
    ├── Monitoring/
    ├── Networking/
    ├── Resource-Groups/
    ├── Storage/
    └── Troubleshooting/
        ├── Azure-Storage/
        ├── Identity-Access/
        ├── Monitoring-Logs/
        └── Networking/

Screenshots demonstrate both successful configurations and controlled failures.

This allows the repository to show the complete support process:

**Issue → Investigation → Root Cause → Resolution → Verification**

---

# Virtual Machine Scope

A Windows Azure virtual machine was evaluated as part of the original lab design.

Low-cost B-series VM sizes were unavailable for the lab subscription in the tested Azure regions.

A larger D-series option was available, but deploying a higher-cost VM solely for portfolio screenshots was not justified.

The VM deployment was therefore intentionally deferred.

The repository does **not** claim:

- A deployed Azure Windows VM
- A successful Azure RDP session
- A failed live RDP session
- VM performance-monitoring results

The networking and NSG troubleshooting portions were completed independently.

This decision also demonstrates cost-aware Azure administration.

---

# Security and Privacy

Sensitive Azure information should not be stored in a public repository.

Screenshots are reviewed for information including:

- Personal email addresses
- User principal names
- Subscription IDs
- Tenant IDs
- Object IDs
- Principal IDs
- Workspace IDs
- Public/private IP addresses
- Activity IDs
- Correlation IDs
- Request IDs

Credentials, passwords, storage access keys, SAS tokens, and other secrets should never be committed.

---

# Skills Demonstrated

- Microsoft Azure Administration
- Cloud Technical Support
- Microsoft Entra ID
- Identity and Access Management
- Azure RBAC
- Least-Privilege Security
- Azure Virtual Networks
- Network Security Groups
- Azure Storage
- Blob Storage
- Storage Lifecycle Management
- Soft-Delete Recovery
- Resource Locks
- Azure Policy
- Azure Cost Management
- Azure Monitor
- Azure Activity Log
- Alert Rules
- Action Groups
- Resource Health
- Azure Service Health
- Azure Advisor
- Log Analytics
- Diagnostic Settings
- Kusto Query Language
- Azure Monitor Workbooks
- Root-Cause Analysis
- Incident Troubleshooting
- Help-Desk Documentation
- Technical Documentation
- Git
- GitHub

---

# Project Outcome

This project demonstrates a practical Azure cloud-support environment built around administration, security, monitoring, troubleshooting, and documentation.

Rather than presenting only successful Azure configuration screens, the lab includes controlled failures involving RBAC, networking, storage, resource protection, monitoring, and logging.

Each major troubleshooting scenario was investigated, corrected where appropriate, verified, and documented as a support ticket.

The completed project provides portfolio evidence relevant to roles such as:

- IT Support Specialist
- Help Desk Technician
- Cloud Support Associate
- Azure Support Technician
- Technical Support Specialist
- Junior Cloud Administrator
- Microsoft 365 / Azure Support Specialist

The strongest areas demonstrated by the lab are **Azure RBAC, Azure Storage, troubleshooting, monitoring, Log Analytics, KQL, governance, and technical support documentation**.
