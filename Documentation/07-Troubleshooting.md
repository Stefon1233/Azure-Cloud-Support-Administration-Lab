# Azure Troubleshooting and Support Methodology

## Overview

This section documents the troubleshooting methodology and completed support scenarios from the Azure Cloud Support & Administration Lab.

The lab was designed to demonstrate more than successful Azure configuration.

Controlled failures were intentionally introduced so they could be investigated, documented, corrected, and verified using a structured cloud-support workflow.

Completed troubleshooting areas included:

- Azure Storage deployment
- Storage network access
- Blob access permissions
- Azure RBAC
- Resource visibility
- Reader write restrictions
- Network Security Groups
- Resource locks
- Blob soft-delete recovery
- Container soft-delete recovery
- Azure Monitor
- Service Health alerting
- Activity Log
- Log Analytics
- KQL investigation

The environment provided practical examples of how Azure support incidents can originate from different layers even when the user-facing symptom appears similar.

---

## Objectives Completed

The troubleshooting portion of the lab demonstrated:

- Incident reproduction
- Azure Portal investigation
- Error-message analysis
- Root-cause identification
- Least-privilege remediation
- Configuration rollback
- Access verification
- Network troubleshooting
- RBAC troubleshooting
- Storage troubleshooting
- Resource-lock troubleshooting
- Data recovery
- Alert troubleshooting
- Log investigation
- KQL analysis
- Support documentation
- Customer-oriented incident summaries

---

## Troubleshooting Philosophy

Azure support problems should be approached systematically.

A user reporting that they "cannot access Azure" does not identify the actual cause.

Possible causes may include:

- Authentication
- Authorization
- RBAC scope
- Management-plane permissions
- Data-plane permissions
- Network restrictions
- Network Security Groups
- Resource locks
- Azure Policy
- Resource Health
- Service Health
- Resource configuration
- Data deletion
- Logging delays
- Alert configuration
- Platform requirements

The purpose of structured troubleshooting is to isolate the correct layer before making changes.

---

## Core Troubleshooting Workflow

The general workflow used throughout the lab was:

1. Identify the reported symptom
2. Identify the affected resource
3. Confirm the affected identity
4. Reproduce the problem
5. Record the Azure error
6. Determine the likely troubleshooting layer
7. Review recent configuration
8. Review Azure logs where applicable
9. Identify the root cause
10. Apply the smallest corrective action
11. Retest the required operation
12. Confirm unauthorized operations remain restricted
13. Document the final result

This reduced the risk of making unnecessary changes.

---

## Evidence-Based Troubleshooting

The lab emphasized evidence rather than assumptions.

Useful Azure evidence included:

- Portal error messages
- IAM role assignments
- Activity Log events
- Resource configuration
- NSG rules
- Resource-lock status
- Soft-delete status
- Fired alerts
- Resource Health
- Service Health
- Log Analytics results
- KQL output
- Azure Monitor Workbooks

A troubleshooting conclusion should be supported by observable configuration or event data whenever possible.

---

# Scenario 1 — Blob Storage Access Denied

## User Impact

A test user could authenticate to Azure but could not access the required Blob Storage data.

This demonstrated that successful sign-in does not guarantee authorization.

---

## Investigation

The investigation reviewed:

- Correct identity
- Correct storage account
- Blob container
- Azure IAM
- Existing role assignments
- Role scope
- Data-plane permissions
- Authentication method

The test identity did not initially have the required Blob Storage data permission.

---

## Root Cause

The identity lacked the appropriate Azure Blob Storage data role.

The issue was authorization rather than authentication.

---

## Resolution

The built-in Azure role:

`Storage Blob Data Reader`

was assigned.

This provided read access without unnecessary Blob Storage write permissions.

---

## Verification

Required Blob Storage access was restored.

Evidence:

- `../Screenshots/Troubleshooting/Identity-Access/01-Storage-Access-Issue.png`
- `../Screenshots/Troubleshooting/Identity-Access/02-RBAC-Permissions-Investigation.png`
- `../Screenshots/Troubleshooting/Identity-Access/03-Entra-Blob-Access-Permission-Denied.png`
- `../Screenshots/Troubleshooting/Identity-Access/04-Storage-Blob-Data-Reader-Role-Assigned.png`
- `../Screenshots/Troubleshooting/Identity-Access/05-Storage-Blob-Access-Restored.png`

Related ticket:

`../Help-Desk-Tickets/Ticket-001-Blob-Storage-Access-Denied.md`

---

# Scenario 2 — Azure Monitor Administrative Alert

## Support Goal

Administrative Azure activity needed to generate proactive monitoring evidence.

Azure Activity Log and Azure Monitor were used to demonstrate detection and notification.

---

## Investigation and Configuration

The lab reviewed administrative activity and configured an Azure Monitor alert rule.

An action group was associated with the alert.

---

## Verification

The alert fired successfully and generated an email notification.

The Fired Alerts interface and alert details were reviewed.

Evidence:

- `../Screenshots/Monitoring/01-Resource-Group-Activity-Log.png`
- `../Screenshots/Monitoring/04-Administrative-Activity-Alert-Rule-Enabled.png`
- `../Screenshots/Monitoring/05-Azure-Monitor-Alert-Fired-Email-Notification.png`
- `../Screenshots/Monitoring/06-Azure-Monitor-Fired-Alerts.png`
- `../Screenshots/Monitoring/07-Azure-Monitor-Fired-Alert-Details.png`

Related ticket:

`../Help-Desk-Tickets/Ticket-002-Azure-Monitor-Administrative-Alert.md`

---

# Scenario 3 — NSG RDP Connectivity Issue

## Support Scenario

A controlled Network Security Group rule was introduced to simulate a condition that would block RDP traffic.

The rule was named:

`Deny-RDP-Test`

It denied:

- Protocol: TCP
- Destination port: 3389
- Priority: 300

---

## Investigation

The NSG configuration was reviewed for:

- Association
- Inbound rules
- Rule priority
- Destination port
- Allow/Deny action

The custom deny rule was identified as the source of the simulated network restriction.

---

## Root Cause

`Deny-RDP-Test` explicitly denied TCP port 3389.

---

## Resolution

The test rule was removed.

---

## Verification

The NSG was reviewed again and the blocking rule was confirmed absent.

An actual Azure VM and RDP session were not used as verification evidence because the VM deployment was intentionally deferred.

The verified result was correction of the NSG configuration.

Evidence:

- `../Screenshots/Troubleshooting/Networking/01-NSG-Inbound-Rules-Before-Change.png`
- `../Screenshots/Troubleshooting/Networking/02-NSG-Deny-RDP-Rule.png`
- `../Screenshots/Troubleshooting/Networking/03-NSG-RDP-Blocking-Rule-Diagnosed.png`
- `../Screenshots/Troubleshooting/Networking/04-NSG-Blocking-Rule-Removed.png`

Related ticket:

`../Help-Desk-Tickets/Ticket-003-NSG-RDP-Connectivity-Issue.md`

---

# Scenario 4 — RBAC Resource Visibility Issue

## User Impact

A test identity had Blob Storage data permissions but could not properly navigate to or view the storage account through the expected Azure Portal workflow.

---

## Investigation

The assigned role was:

`Storage Blob Data Reader`

The investigation determined that the identity had data-plane read permissions but lacked the necessary management-plane visibility.

---

## Root Cause

The permission issue involved the difference between:

- Data-plane access
- Management-plane access

Storage Blob Data Reader did not provide all of the Azure resource visibility required for the intended workflow.

---

## Resolution

The built-in Azure:

`Reader`

role was added.

The final access model used:

- Reader
- Storage Blob Data Reader

---

## Verification

The test identity could view the resource and read Blob Storage data.

An attempted write operation remained denied.

This confirmed least-privilege behavior.

Evidence:

- `../Screenshots/Troubleshooting/Identity-Access/06-RBAC-Reader-Assignment.png`
- `../Screenshots/Troubleshooting/Identity-Access/07-RBAC-Storage-Account-Not-Visible.png`
- `../Screenshots/Troubleshooting/Identity-Access/08-RBAC-Reader-And-Blob-Reader-Roles.png`
- `../Screenshots/Troubleshooting/Identity-Access/09-RBAC-Read-Allowed-Write-Denied.png`
- `../Screenshots/Troubleshooting/Identity-Access/10-RBAC-Blob-Read-Success.png`

Related ticket:

`../Help-Desk-Tickets/Ticket-004-RBAC-Resource-Visibility-Issue.md`

---

# Scenario 5 — Storage Network Access Failure

## User Impact

Storage access failed after a controlled network-access configuration change.

---

## Investigation

The troubleshooting process reviewed:

- Storage account state
- Network configuration
- Public network access
- Existing authentication
- Existing RBAC
- Error behavior

The issue was investigated as a networking problem rather than immediately changing identity permissions.

---

## Root Cause

A restrictive storage networking configuration prevented the intended access.

---

## Resolution

The storage network-access configuration was corrected.

---

## Verification

Access was restored after the network restriction was addressed.

Evidence:

- `../Screenshots/Troubleshooting/Azure-Storage/06-Storage-Network-Access-Before.png`
- `../Screenshots/Troubleshooting/Azure-Storage/07-Storage-Network-Access-Failure.png`
- `../Screenshots/Troubleshooting/Azure-Storage/08-Storage-Network-Access-Restored.png`

Related ticket:

`../Help-Desk-Tickets/Ticket-005-Storage-Network-Access-Failure.md`

---

# Scenario 6 — Resource Lock Preventing Deletion

## Support Scenario

A Delete resource lock was configured on the Azure Storage environment.

Lock name:

`Protect-Storage-Account`

Lock type:

`Delete`

---

## Investigation

A deletion operation was attempted while the lock was active.

Azure blocked the operation.

The investigation reviewed the storage account and management-lock configuration.

---

## Root Cause

The Delete resource lock intentionally prevented the deletion operation.

---

## Resolution

For the controlled recovery exercise, the lock was temporarily removed.

This was a deliberate administrative action and not a permanent removal of the protection.

---

## Verification

The required test operation could proceed after the lock was removed.

The lock was later restored.

Evidence:

- `../Screenshots/Troubleshooting/Azure-Storage/09-Storage-Resource-Lock.png`
- `../Screenshots/Troubleshooting/Azure-Storage/10-Resource-Lock-Deletion-Blocked.png`
- `../Screenshots/Troubleshooting/Azure-Storage/20-Storage-Delete-Lock-Restored.png`

Related ticket:

`../Help-Desk-Tickets/Ticket-006-Resource-Lock-Preventing-Deletion.md`

---

# Scenario 7 — Blob Soft-Delete Recovery

## User Impact

A test blob was intentionally deleted to simulate accidental data removal.

Test blob:

`Recovery-Test.txt`

Container:

`rbac-test`

---

## Investigation

Blob soft delete had already been enabled.

The deleted-object view was used to determine whether the blob remained recoverable.

---

## Root Cause

The data was deleted, but it remained inside the configured soft-delete retention period.

---

## Resolution

The deleted blob was restored.

---

## Verification

The blob appeared again after recovery.

Evidence:

- `../Screenshots/Troubleshooting/Azure-Storage/11-Blob-Before-Soft-Delete.png`
- `../Screenshots/Troubleshooting/Azure-Storage/12-Blob-Deleted-Soft-Delete-Test.png`
- `../Screenshots/Troubleshooting/Azure-Storage/13-Soft-Deleted-Blob-Detected.png`
- `../Screenshots/Troubleshooting/Azure-Storage/14-Soft-Deleted-Blob-Restored.png`

Related ticket:

`../Help-Desk-Tickets/Ticket-007-Azure-Blob-Soft-Delete-Recovery.md`

---

# Additional Container Recovery Exercise

A separate container-level recovery exercise was also completed.

Test container:

`recovery-container-test`

Test file:

`Container-Recovery-Test.txt`

The first container-deletion attempt was blocked by the active Delete lock.

After temporarily removing the lock, the container was deleted.

Because container soft delete was enabled, the deleted container remained recoverable.

The container was then restored.

Finally, the Delete lock was restored.

Evidence:

- `../Screenshots/Troubleshooting/Azure-Storage/15-Container-Before-Deletion.png`
- `../Screenshots/Troubleshooting/Azure-Storage/16-Container-Deletion-Blocked-By-Resource-Lock.png`
- `../Screenshots/Troubleshooting/Azure-Storage/17-Container-Deletion-Succeeded-After-Lock-Removal.png`
- `../Screenshots/Troubleshooting/Azure-Storage/18-Soft-Deleted-Container-Detected.png`
- `../Screenshots/Troubleshooting/Azure-Storage/19-Soft-Deleted-Container-Restored.png`
- `../Screenshots/Troubleshooting/Azure-Storage/20-Storage-Delete-Lock-Restored.png`

---

# Scenario 8 — Resource Group Reader Write Denied

## User Impact

A test identity had Reader access at the resource-group scope but could not perform administrative changes.

---

## Investigation

The Reader role assignment was reviewed.

Reader is intended to provide visibility without resource modification.

Two write-oriented tests were performed.

---

## Test 1 — Resource Lock Administration

The test identity could not edit resource locks.

Evidence:

`../Screenshots/Troubleshooting/Identity-Access/11-Resource-Group-Reader-Write-Denied.png`

---

## Test 2 — Tag Modification

The test identity attempted to modify resource-group tags.

Azure returned an authorization failure.

Evidence:

`../Screenshots/Troubleshooting/Identity-Access/12-Reader-Tag-Modification-Denied.png`

---

## Root Cause

There was no misconfiguration.

The denied operations were expected because the identity had Reader rather than a write-capable role.

---

## Resolution

No additional role was assigned.

Granting a broader role would have violated the access requirement.

---

## Verification

The user retained required read access while unauthorized changes remained blocked.

This demonstrated least privilege.

Related ticket:

`../Help-Desk-Tickets/Ticket-008-Resource-Group-Reader-Write-Denied.md`

---

# Scenario 9 — Service Health Alert Configuration Failure

## Support Goal

Azure Advisor recommended creating a Service Health alert.

The recommendation was selected for implementation.

---

## Initial Failure

The first alert configuration attempt failed.

Azure reported that Service Health rules support action groups in the Global location only.

Evidence:

`../Screenshots/Troubleshooting/Monitoring-Logs/03-Service-Health-Alert-Action-Group-Error.png`

---

## Investigation

The existing action group was reviewed.

The failure was traced to an Azure Service Health requirement rather than an identity, subscription, or event-selection problem.

---

## Root Cause

The action group used for the initial configuration was not in the Global location required by Service Health alert rules.

---

## Resolution

A new Global action group was created:

`ag-service-health-alerts`

Display name:

`ServiceHlth`

Region:

`Global`

The Service Health alert was then recreated.

Alert name:

`ALERT-Azure-Service-Health`

---

## Verification

The Service Health alert was successfully created and displayed as enabled.

Evidence:

- `../Screenshots/Monitoring/18-Azure-Advisor-Service-Health-Recommendation.png`
- `../Screenshots/Monitoring/20-Azure-Service-Health-Alert-Created.png`
- `../Screenshots/Monitoring/21-Azure-Service-Health-Alert-Enabled.png`

Related ticket:

`../Help-Desk-Tickets/Ticket-009-Service-Health-Alert-Configuration-Failure.md`

---

# Scenario 10 — Log Analytics Activity Investigation

## Support Goal

Azure administrative activity needed to be centralized and queried using Log Analytics.

---

## Workspace Configuration

A Log Analytics workspace was created:

`LAW-IT-Support-Lab`

Azure Activity Log data was then exported to the workspace through the diagnostic setting:

`Activity-Log-to-LAW`

---

## Diagnostic Categories

The configuration included:

- Administrative
- Security
- ServiceHealth
- Alert
- Recommendation
- Policy
- Autoscale
- ResourceHealth

Evidence:

- `../Screenshots/Monitoring/22-Log-Analytics-Workspace-Created.png`
- `../Screenshots/Monitoring/23-Activity-Log-Diagnostic-Setting.png`

---

## Initial Investigation

The `AzureActivity` table was queried.

A basic validation query included:

    AzureActivity
    | take 20

A more focused query included:

    AzureActivity
    | where TimeGenerated > ago(1h)
    | project TimeGenerated, OperationNameValue, ActivityStatusValue, CategoryValue, ResourceGroup
    | sort by TimeGenerated desc
    | take 20

Evidence:

`../Screenshots/Monitoring/24-Log-Analytics-Azure-Activity-Query.png`

---

## Ingestion Delay

The newly configured workspace did not immediately contain every expected event.

This was investigated as a possible ingestion-timing issue.

The absence of immediate results was not treated as proof that the diagnostic setting had failed.

---

## Controlled Administrative Event

A resource-group tag value was changed to generate fresh administrative activity.

The controlled change provided an event that could be searched for after ingestion.

---

## Verification

Administrative activity appeared in Log Analytics after ingestion.

A summary query was then used:

    AzureActivity
    | where TimeGenerated > ago(24h)
    | summarize EventCount=count() by CategoryValue, ActivityStatusValue
    | sort by EventCount desc

Evidence:

`../Screenshots/Monitoring/25-KQL-Activity-Summary.png`

---

## Workbook Verification

The Log Analytics data was also visualized through:

`IT-Support-Monitoring-Workbook`

Evidence:

- `../Screenshots/Monitoring/26-Azure-Monitor-Workbook-Activity-Summary.png`
- `../Screenshots/Monitoring/27-Azure-Monitor-Workbook-Activity-Details.png`

This completed the monitoring investigation from raw Azure activity through reusable workbook visualization.

Related ticket:

`../Help-Desk-Tickets/Ticket-010-Log-Analytics-Activity-Investigation.md`

---

# Activity Log Investigation

Azure Activity Log was also used directly during troubleshooting.

Evidence:

- `../Screenshots/Troubleshooting/Monitoring-Logs/01-Activity-Log-Investigation.png`
- `../Screenshots/Troubleshooting/Monitoring-Logs/02-Activity-Log-JSON-Details.png`

Detailed activity information can help identify:

- Operation
- Status
- Timestamp
- Resource
- Caller
- Event category
- Correlation information

Sensitive identifiers should be obscured before screenshots are published.

---

# Storage Deployment Troubleshooting

An Azure Storage account naming/deployment issue was also investigated during environment setup.

The original storage-account deployment attempt encountered validation errors.

The Azure error information was reviewed and the account name was corrected.

The final storage account:

`stitsupportlab002`

was successfully deployed and verified.

Evidence:

- `../Screenshots/Troubleshooting/Azure-Storage/01-Storage-Account-Invalid-Name-Error.png`
- `../Screenshots/Troubleshooting/Azure-Storage/02-Storage-Account-Validation-Failed.png`
- `../Screenshots/Troubleshooting/Azure-Storage/03-Storage-Account-Name-Corrected.png`
- `../Screenshots/Troubleshooting/Azure-Storage/04-Storage-Account-Deployment-Succeeded.png`
- `../Screenshots/Troubleshooting/Azure-Storage/05-Storage-Account-Deployment-Verified.png`

This reinforced the importance of reading Azure validation messages before retrying deployment.

---

# Troubleshooting by Layer

A useful Azure support approach is to classify an incident by layer.

## Identity Layer

Questions:

- Is the correct account signed in?
- Is authentication successful?
- Is the identity enabled?
- Is the correct tenant being used?

---

## Authorization Layer

Questions:

- Which RBAC roles are assigned?
- At what scope?
- Is the required operation management plane or data plane?
- Is the identity using a read-only role?

---

## Network Layer

Questions:

- Is the network path permitted?
- Is an NSG blocking the port?
- Is storage networking restricted?
- Is the correct subnet involved?
- Is public access restricted?

---

## Governance Layer

Questions:

- Is Azure Policy affecting configuration?
- Is a resource lock preventing the operation?
- Are required tags present?

---

## Resource Layer

Questions:

- Does the resource exist?
- Is the correct resource selected?
- Is Azure reporting the resource as healthy?
- Was the resource deleted?

---

## Monitoring Layer

Questions:

- What does Activity Log show?
- Did an alert fire?
- Are diagnostic settings enabled?
- Has telemetry reached Log Analytics?
- What does KQL show?

---

## Platform Layer

Questions:

- Is Resource Health reporting an issue?
- Is Service Health reporting an Azure service problem?
- Is Azure Advisor reporting a reliability concern?

---

# Authentication vs Authorization

The lab repeatedly demonstrated the difference between these concepts.

Authentication answers:

"Who are you?"

Authorization answers:

"What are you allowed to do?"

A user can successfully authenticate but still receive:

- Access denied
- AuthorizationFailed
- Write denied
- Resource not visible

Troubleshooting should identify which stage is failing.

---

# Management Plane vs Data Plane

Azure Storage provided the clearest example of this distinction.

Management-plane permissions affect the Azure resource.

Data-plane permissions affect the data inside the service.

The lab demonstrated a user with Blob data access who still required Reader for the desired Azure Portal resource visibility.

This prevented the troubleshooting process from incorrectly treating all Storage permissions as one permission layer.

---

# Expected Denials

Not every denied operation represents a support failure.

Examples from the lab included:

- Reader unable to edit tags
- Reader unable to modify resource locks
- Storage Blob Data Reader unable to upload/write blobs

These denied operations were expected.

They confirmed that least-privilege controls were working.

A technician should not escalate permissions when the blocked operation is outside the user's required responsibilities.

---

# Least-Privilege Remediation

Corrective actions should provide only the permissions required.

The lab avoided resolving RBAC issues by assigning powerful roles such as:

- Owner
- Contributor

when narrower roles were sufficient.

Instead, the tested configuration used combinations such as:

- Reader
- Storage Blob Data Reader

This allowed required operations without unnecessary write access.

---

# Change Control

Controlled failures were introduced deliberately.

Examples included:

- NSG deny rule
- Storage networking restriction
- Blob deletion
- Container deletion
- Temporary tag change
- Temporary resource-lock removal

Temporary changes were documented and reversed where appropriate.

This reflects basic change-management discipline.

---

# Resolution Verification

Every completed troubleshooting scenario included evidence that the corrective action produced the expected result.

Verification methods used throughout the lab included:

- Successful Azure Storage access
- Correct RBAC role assignment
- Read access allowed while unauthorized write access remained denied
- Storage network access restored
- NSG blocking rule identified and removed
- Resource lock behavior verified
- Soft-deleted blob restored
- Soft-deleted container restored
- Azure Monitor alert enabled
- Service Health alert successfully configured
- Azure Activity records ingested into Log Analytics
- KQL queries returning expected activity
- Azure Monitor Workbook displaying collected activity

The NSG scenario demonstrated RDP-related network troubleshooting by intentionally configuring and removing a rule that denied TCP port 3389.

An actual Azure VM and RDP session were not used as verification evidence because VM deployment was intentionally deferred.

---

# Customer Communication

Technical resolution should be translated into clear support communication.

A useful customer-facing update should explain:

- What was affected
- What caused the issue
- What was changed
- Whether access or service was restored
- Whether the user needs to take additional action
- Whether monitoring or follow-up is required

Technical detail should be adjusted for the intended audience.

---

# Help-Desk Ticket Documentation

The repository includes ten completed Azure support tickets:

1. `Ticket-001-Blob-Storage-Access-Denied.md`
2. `Ticket-002-Azure-Monitor-Administrative-Alert.md`
3. `Ticket-003-NSG-RDP-Connectivity-Issue.md`
4. `Ticket-004-RBAC-Resource-Visibility-Issue.md`
5. `Ticket-005-Storage-Network-Access-Failure.md`
6. `Ticket-006-Resource-Lock-Preventing-Deletion.md`
7. `Ticket-007-Azure-Blob-Soft-Delete-Recovery.md`
8. `Ticket-008-Resource-Group-Reader-Write-Denied.md`
9. `Ticket-009-Service-Health-Alert-Configuration-Failure.md`
10. `Ticket-010-Log-Analytics-Activity-Investigation.md`

Each ticket provides structured support evidence for the lab.

---

# Ticket Structure

Completed help-desk documentation may include:

- Ticket summary
- User impact
- Environment
- Reported issue
- Investigation
- Troubleshooting steps
- Root cause
- Resolution
- Verification
- Evidence
- Security considerations
- Customer communication
- Lessons learned

This structure makes the repository easier for recruiters and technical reviewers to evaluate.

---

# Screenshot Evidence by Troubleshooting Area

## Identity and Access

- `../Screenshots/Troubleshooting/Identity-Access/01-Storage-Access-Issue.png`
- `../Screenshots/Troubleshooting/Identity-Access/02-RBAC-Permissions-Investigation.png`
- `../Screenshots/Troubleshooting/Identity-Access/03-Entra-Blob-Access-Permission-Denied.png`
- `../Screenshots/Troubleshooting/Identity-Access/04-Storage-Blob-Data-Reader-Role-Assigned.png`
- `../Screenshots/Troubleshooting/Identity-Access/05-Storage-Blob-Access-Restored.png`
- `../Screenshots/Troubleshooting/Identity-Access/06-RBAC-Reader-Assignment.png`
- `../Screenshots/Troubleshooting/Identity-Access/07-RBAC-Storage-Account-Not-Visible.png`
- `../Screenshots/Troubleshooting/Identity-Access/08-RBAC-Reader-And-Blob-Reader-Roles.png`
- `../Screenshots/Troubleshooting/Identity-Access/09-RBAC-Read-Allowed-Write-Denied.png`
- `../Screenshots/Troubleshooting/Identity-Access/10-RBAC-Blob-Read-Success.png`
- `../Screenshots/Troubleshooting/Identity-Access/11-Resource-Group-Reader-Write-Denied.png`
- `../Screenshots/Troubleshooting/Identity-Access/12-Reader-Tag-Modification-Denied.png`

---

## Azure Storage

- `../Screenshots/Troubleshooting/Azure-Storage/01-Storage-Account-Invalid-Name-Error.png`
- `../Screenshots/Troubleshooting/Azure-Storage/02-Storage-Account-Validation-Failed.png`
- `../Screenshots/Troubleshooting/Azure-Storage/03-Storage-Account-Name-Corrected.png`
- `../Screenshots/Troubleshooting/Azure-Storage/04-Storage-Account-Deployment-Succeeded.png`
- `../Screenshots/Troubleshooting/Azure-Storage/05-Storage-Account-Deployment-Verified.png`
- `../Screenshots/Troubleshooting/Azure-Storage/06-Storage-Network-Access-Before.png`
- `../Screenshots/Troubleshooting/Azure-Storage/07-Storage-Network-Access-Failure.png`
- `../Screenshots/Troubleshooting/Azure-Storage/08-Storage-Network-Access-Restored.png`
- `../Screenshots/Troubleshooting/Azure-Storage/09-Storage-Resource-Lock.png`
- `../Screenshots/Troubleshooting/Azure-Storage/10-Resource-Lock-Deletion-Blocked.png`
- `../Screenshots/Troubleshooting/Azure-Storage/11-Blob-Before-Soft-Delete.png`
- `../Screenshots/Troubleshooting/Azure-Storage/12-Blob-Deleted-Soft-Delete-Test.png`
- `../Screenshots/Troubleshooting/Azure-Storage/13-Soft-Deleted-Blob-Detected.png`
- `../Screenshots/Troubleshooting/Azure-Storage/14-Soft-Deleted-Blob-Restored.png`
- `../Screenshots/Troubleshooting/Azure-Storage/15-Container-Before-Deletion.png`
- `../Screenshots/Troubleshooting/Azure-Storage/16-Container-Deletion-Blocked-By-Resource-Lock.png`
- `../Screenshots/Troubleshooting/Azure-Storage/17-Container-Deletion-Succeeded-After-Lock-Removal.png`
- `../Screenshots/Troubleshooting/Azure-Storage/18-Soft-Deleted-Container-Detected.png`
- `../Screenshots/Troubleshooting/Azure-Storage/19-Soft-Deleted-Container-Restored.png`
- `../Screenshots/Troubleshooting/Azure-Storage/20-Storage-Delete-Lock-Restored.png`

---

## Networking

- `../Screenshots/Troubleshooting/Networking/01-NSG-Inbound-Rules-Before-Change.png`
- `../Screenshots/Troubleshooting/Networking/02-NSG-Deny-RDP-Rule.png`
- `../Screenshots/Troubleshooting/Networking/03-NSG-RDP-Blocking-Rule-Diagnosed.png`
- `../Screenshots/Troubleshooting/Networking/04-NSG-Blocking-Rule-Removed.png`

---

## Monitoring and Logs

- `../Screenshots/Troubleshooting/Monitoring-Logs/01-Activity-Log-Investigation.png`
- `../Screenshots/Troubleshooting/Monitoring-Logs/02-Activity-Log-JSON-Details.png`
- `../Screenshots/Troubleshooting/Monitoring-Logs/03-Service-Health-Alert-Action-Group-Error.png`

---

# Sensitive Information Review

Before publishing screenshots or ticket evidence, review for:

- Personal email addresses
- User principal names
- Subscription IDs
- Tenant IDs
- Object IDs
- Principal IDs
- Workspace IDs
- IP addresses
- Activity IDs
- Correlation IDs
- Request IDs
- Access keys
- SAS tokens
- Credentials

Secrets must never be stored in the repository.

---

# Troubleshooting Anti-Patterns

The lab avoided several common support mistakes.

## Assigning Administrator Access Immediately

Broad permissions may make an error disappear while creating a security problem.

The lab used least-privilege roles instead.

---

## Changing Multiple Settings at Once

Changing several variables makes it difficult to determine which change solved the problem.

Controlled scenarios used targeted configuration changes.

---

## Ignoring Azure Error Messages

Azure validation and authorization errors often contain useful troubleshooting information.

The storage naming and Service Health scenarios both depended on reading Azure's error details.

---

## Assuming Every Access Problem Is RBAC

Storage network restrictions and resource locks demonstrated that access failures can originate outside RBAC.

---

## Treating Expected Denials as Failures

Read-only roles should deny write operations.

The Reader and Storage Blob Data Reader tests demonstrated this intentionally.

---

## Ignoring Propagation and Ingestion Delays

Azure services may require time to:

- Propagate RBAC
- Evaluate Advisor
- Process Policy
- Ingest telemetry
- Update monitoring views

Unnecessary repeated changes can make troubleshooting harder.

---

# Production Support Considerations

In a production Azure environment, troubleshooting may additionally involve:

- Change-management systems
- ServiceNow or another ITSM platform
- Escalation procedures
- Azure CLI
- Azure PowerShell
- Azure Resource Graph
- Network Watcher
- Application Insights
- Microsoft Sentinel
- Centralized identity governance
- Privileged Identity Management
- Azure Bastion
- Backup and disaster recovery
- Formal incident severity
- SLA tracking

These items were outside the completed lab scope and are not presented as implemented features.

---

# VM Troubleshooting Scope

A Windows Azure VM was originally planned.

Low-cost B-series VM sizes were unavailable under the lab subscription in the tested Azure regions.

A larger D-series VM could have been deployed, but the cost was not justified for the remaining portfolio objectives.

VM deployment was therefore intentionally deferred.

No documentation in this repository should be interpreted as evidence of:

- A deployed Windows VM
- A successful Azure RDP session
- A failed live RDP session
- Collected VM performance metrics

The NSG RDP scenario demonstrated the network-security configuration associated with TCP port 3389 without claiming a live VM connection.

---

# Future VM Troubleshooting Methodology

If an Azure Windows VM is added later, a structured investigation could review:

1. VM power state
2. Provisioning state
3. Resource Health
4. Network interface
5. VNet
6. Subnet
7. NSG
8. Effective security rules
9. Public/private IP configuration
10. TCP port 3389
11. Windows RDP settings
12. Authentication
13. Azure Activity Log
14. Azure Monitor
15. Log Analytics

This is future methodology rather than completed evidence.

---

# Skills Demonstrated

- Microsoft Azure
- Azure troubleshooting
- Cloud support
- Root-cause analysis
- Microsoft Entra ID
- Azure RBAC
- Least privilege
- Azure Storage
- Blob Storage
- Storage networking
- Network Security Groups
- TCP/IP
- RDP network troubleshooting
- Resource locks
- Soft-delete recovery
- Azure Monitor
- Azure Activity Log
- Service Health
- Resource Health
- Azure Advisor
- Log Analytics
- KQL
- Azure Monitor Workbooks
- Error-message analysis
- Incident documentation
- Help-desk support
- Change control
- Technical communication

---

# Outcome

The troubleshooting portion of the Azure Cloud Support & Administration Lab demonstrates a practical support workflow rather than a collection of successful configuration screenshots.

Ten completed help-desk tickets document real or controlled Azure scenarios involving permissions, networking, storage, monitoring, recovery, and logging.

The strongest outcome of the lab is the ability to distinguish between different Azure troubleshooting layers.

The completed scenarios demonstrate that similar user symptoms can originate from:

- Identity
- RBAC
- Data-plane permissions
- Management-plane permissions
- Networking
- Resource locks
- Data deletion
- Alert configuration
- Logging and ingestion timing

Each scenario was investigated using the smallest appropriate corrective action and verified using Azure evidence.

The resulting repository provides portfolio evidence of Azure cloud support, administration, troubleshooting, incident analysis, least-privilege security, monitoring, and technical documentation.
