# Azure Cloud Support Lab Architecture

## Architecture Overview

The following diagram represents the Azure services and administrative components configured during the Azure Cloud Support & Administration Lab.

```mermaid
flowchart TB

    ADMIN["Azure Administrator"]
    USER["Microsoft Entra Test User"]

    subgraph AZURE["Microsoft Azure Subscription"]

        RG["RG-IT-Support-Lab<br/>Resource Group"]

        subgraph IDENTITY["Identity & Access"]
            ENTRA["Microsoft Entra ID"]
            RBAC["Azure RBAC<br/>Reader<br/>Storage Blob Data Reader"]
        end

        subgraph NETWORK["Networking"]
            VNET["VNET-IT-Support"]
            SUBNET["SNET-Workstations"]
            NSG["NSG-IT-Support<br/>Security Rules"]
        end

        subgraph STORAGE["Azure Storage"]
            SA["stitsupportlab002<br/>Storage Account"]
            BLOB["Blob Containers"]
            LIFECYCLE["Lifecycle Management"]
            PROTECTION["Soft Delete<br/>Versioning"]
            LOCK["Delete Resource Lock"]
        end

        subgraph GOVERNANCE["Governance & Cost"]
            POLICY["Azure Policy<br/>Require Environment Tag"]
            TAGS["Governance Tags"]
            BUDGET["Cost Management<br/>Monthly Budget"]
            ADVISOR["Azure Advisor"]
        end

        subgraph MONITORING["Monitoring & Observability"]
            ACTIVITY["Azure Activity Log"]
            MONITOR["Azure Monitor"]
            ALERTS["Alert Rules"]
            ACTIONS["Action Groups"]
            HEALTH["Resource Health"]
            SERVICE["Azure Service Health"]
            LAW["LAW-IT-Support-Lab<br/>Log Analytics"]
            KQL["KQL Queries"]
            WORKBOOK["IT-Support-Monitoring-Workbook"]
        end
    end

    ADMIN --> RG
    USER --> ENTRA

    RG --> ENTRA
    ENTRA --> RBAC
    RBAC --> SA

    RG --> VNET
    VNET --> SUBNET
    SUBNET --> NSG

    RG --> SA
    SA --> BLOB
    SA --> LIFECYCLE
    SA --> PROTECTION
    SA --> LOCK

    RG --> POLICY
    RG --> TAGS
    RG --> BUDGET
    ADVISOR --> RG

    RG --> ACTIVITY
    ACTIVITY --> MONITOR
    MONITOR --> ALERTS
    ALERTS --> ACTIONS

    RG --> HEALTH
    SERVICE --> ALERTS

    ACTIVITY --> LAW
    LAW --> KQL
    KQL --> WORKBOOK
```---

## Architecture Components

### Identity and Access

Microsoft Entra ID provided identity services for the lab.

Azure RBAC controlled access through built-in roles including:

- Reader
- Storage Blob Data Reader

The lab demonstrated management-plane and data-plane permission differences and least-privilege access.

### Networking

The networking environment included:

- `VNET-IT-Support`
- `SNET-Workstations`
- `NSG-IT-Support`

Network Security Group rules were used to demonstrate controlled TCP port 3389 troubleshooting.

### Storage

`stitsupportlab002` provided Azure Blob Storage for administration and troubleshooting scenarios.

Storage controls included:

- Private blob access
- Lifecycle management
- Blob soft delete
- Container soft delete
- Blob versioning
- Network-access controls
- Delete resource lock
### Governance

Azure governance components included:

- Azure Policy
- Resource tags
- Cost Management budget
- Azure Advisor

These services demonstrated compliance, organization, cost awareness, and reliability recommendations.

### Monitoring and Observability

The monitoring environment included:

- Azure Activity Log
- Azure Monitor
- Alert rules
- Action groups
- Resource Health
- Azure Service Health
- Log Analytics
- KQL
- Azure Monitor Workbooks

Activity Log data was exported to `LAW-IT-Support-Lab`, queried with KQL, and displayed through the `IT-Support-Monitoring-Workbook`.

---

## Troubleshooting Coverage

The architecture supported troubleshooting scenarios involving:

- Blob Storage access
- RBAC permissions
- Resource visibility
- Storage networking
- Network Security Groups
- Resource locks
- Blob recovery
- Container recovery
- Azure Monitor alerts
- Service Health alerts
- Activity Log
- Log Analytics
- KQL

Ten structured help-desk tickets document these scenarios in the repository.
---

## Virtual Machine Scope

A Windows Azure VM was evaluated but intentionally not deployed.

Low-cost B-series VM sizes were unavailable under the lab subscription in the tested Azure regions, while the available larger VM option was not justified for the remaining lab objectives.

The networking environment and NSG troubleshooting scenario were completed independently.

The repository therefore does not represent a VM or successful RDP session as completed lab evidence.

---

## Architecture Outcome

The completed architecture demonstrates an Azure cloud-support environment combining:

**Identity → Networking → Storage → Governance → Monitoring → Troubleshooting**

The environment emphasizes least privilege, layered security, proactive monitoring, data protection, cost awareness, and evidence-based troubleshooting.
