# Azure Monitoring, Governance, and Observability

## Overview

This section documents the Azure monitoring, alerting, governance, logging, health, cost-management, and observability work completed in the Azure Cloud Support & Administration Lab.

The monitoring environment progressed beyond basic Azure Portal monitoring and included:

- Azure Activity Log
- Azure Monitor alerts
- Action groups
- Email alert notifications
- Cost Management budgets
- Azure Policy
- Resource Health
- Azure Advisor
- Azure Service Health
- Log Analytics
- Diagnostic settings
- Kusto Query Language (KQL)
- Azure Monitor Workbooks

These services were configured and tested to demonstrate how cloud-support technicians can identify configuration changes, receive proactive alerts, investigate platform activity, evaluate resource health, control cost, and centralize operational data.

---

## Objectives Completed

The monitoring portion of the lab demonstrated:

- Azure Activity Log investigation
- Administrative event review
- Azure Monitor alert-rule creation
- Action-group configuration
- Email alert notification
- Fired-alert investigation
- Cost budget configuration
- Budget threshold configuration
- Azure Policy assignment
- Policy compliance verification
- Resource Health monitoring
- Azure Advisor review
- Advisor alerting
- Azure Service Health alerting
- Service Health troubleshooting
- Log Analytics workspace deployment
- Activity Log diagnostic settings
- Centralized log ingestion
- KQL querying
- Administrative activity investigation
- KQL summarization
- Azure Monitor Workbook creation
- Operational dashboard development
- Cloud observability
- Technical documentation

---

## Monitoring Architecture

The completed monitoring workflow can be summarized as:

Azure resources and subscription activity

→ Azure Activity Log

→ Azure Monitor

→ Alert rules and action groups

→ Log Analytics

→ KQL

→ Azure Monitor Workbooks

Additional operational signals were provided through:

- Resource Health
- Service Health
- Azure Advisor
- Azure Policy
- Cost Management

Together, these tools created a layered monitoring and governance environment.

---

## Azure Activity Log

Azure Activity Log was used to review subscription-level administrative activity.

The Activity Log is particularly useful when investigating questions such as:

- Who changed a resource?
- What operation occurred?
- When did the change occur?
- Did the operation succeed or fail?
- Which resource was affected?
- Which resource group was involved?

This makes Activity Log an important source of evidence during Azure support investigations.

---

## Resource Group Activity Log

Activity associated with the lab resource group was reviewed through Azure.

Evidence:

`../Screenshots/Monitoring/01-Resource-Group-Activity-Log.png`

The Activity Log provided an audit trail of Azure control-plane operations affecting the environment.

---

## RBAC Activity Monitoring

RBAC changes were also visible through Azure activity records.

A successful role assignment was captured and reviewed.

Evidence:

`../Screenshots/Monitoring/02-RBAC-Role-Assignment-Succeeded.png`

Detailed information for the role-assignment operation was then inspected.

Evidence:

`../Screenshots/Monitoring/03-RBAC-Role-Assignment-Details.png`

This demonstrated how Azure Activity Log can support identity and access investigations.

---

## Administrative Activity Alert

An Azure Monitor alert rule was configured to detect administrative activity.

The purpose was to demonstrate proactive monitoring of control-plane changes rather than relying only on manual Activity Log review.

Evidence:

`../Screenshots/Monitoring/04-Administrative-Activity-Alert-Rule-Enabled.png`

---

## Action Group

Azure Monitor action groups provide notification and automation targets for alerts.

The lab used an action group to deliver monitoring notifications.

One action group used during the monitoring scenarios was:

`ag-it-support-alerts`

The action group supported alert notification for the IT support lab.

Sensitive notification addresses should be obscured before screenshots are published.

---

## Alert Notification

The configured Azure Monitor alert successfully generated an email notification.

Evidence:

`../Screenshots/Monitoring/05-Azure-Monitor-Alert-Fired-Email-Notification.png`

This provided evidence that the monitoring workflow extended beyond alert-rule configuration and successfully delivered a notification.

---

## Fired Alerts

The Azure Monitor Fired Alerts interface was reviewed after the alert triggered.

Evidence:

`../Screenshots/Monitoring/06-Azure-Monitor-Fired-Alerts.png`

The individual alert details were also inspected.

Evidence:

`../Screenshots/Monitoring/07-Azure-Monitor-Fired-Alert-Details.png`

This demonstrated the workflow:

Configuration change

→ Activity event

→ Alert condition

→ Fired alert

→ Notification

→ Investigation

---

## Cost Management

Cloud administration also requires cost awareness.

A technically valid Azure configuration may still be inappropriate if it creates unnecessary recurring cost.

Cost Management was therefore included as part of the lab.

---

## Monthly Budget

A monthly Azure budget was configured.

Budget name:

`IT-Support-Lab-Monthly-Budget`

Budget amount:

`$10`

Budget period:

Monthly

The budget was configured across an approximately 12-month period.

Evidence:

`../Screenshots/Monitoring/08-Monthly-Cost-Budget-Configured.png`

---

## Budget Overview

The Azure Cost Management budget overview was reviewed after configuration.

Evidence:

`../Screenshots/Monitoring/09-Monthly-Budget-Overview.png`

The budget provides visibility into spending relative to the defined lab threshold.

---

## Budget Alerts

Budget thresholds were configured to provide proactive notification as spending approaches the configured limit.

The configuration included threshold-based notification behavior for actual and/or forecasted spending.

Evidence:

`../Screenshots/Monitoring/10-Budget-Alert-Configuration.png`

This demonstrated that cost monitoring should be proactive rather than performed only after unexpected charges appear.

---

## Cost-Aware VM Decision

Cost awareness also influenced the virtual-machine portion of the lab.

Low-cost B-series VM sizes were unavailable for the lab subscription in the tested regions.

A larger D-series VM option was available, but deploying it solely to generate portfolio screenshots was not justified.

The VM deployment was therefore intentionally deferred.

This decision demonstrated an important cloud-administration principle:

A resource should not be deployed simply because it is technically available.

Cost, business need, lab objectives, and operational value should also be considered.

---

## Azure Policy

Azure Policy was configured to demonstrate resource governance.

The built-in policy definition:

`Require a tag on resource groups`

was assigned.

The policy assignment was named:

`Require-Environment-Tag`

The assignment targeted the lab resource-group governance requirement.

---

## Policy Purpose

The policy was configured to require the:

`Environment`

tag on resource groups.

The assignment description documented the purpose as requiring the Environment tag on the IT Support Lab resource group to demonstrate Azure Policy governance and resource compliance.

---

## Policy Assignment

The Azure Policy assignment was successfully created.

Evidence:

`../Screenshots/Monitoring/11-Azure-Policy-Assignment-Created.png`

---

## Policy Overview

The policy assignment was reviewed after creation.

Evidence:

`../Screenshots/Monitoring/12-Azure-Policy-Assignment-Overview.png`

---

## Policy Compliance

The lab resource group already contained:

`Environment = Lab`

The policy compliance state was reviewed and verified.

Evidence:

`../Screenshots/Monitoring/13-Azure-Policy-Compliance-Verified.png`

This demonstrated the relationship between:

- Governance requirements
- Resource tags
- Azure Policy
- Compliance evaluation

---

## Governance Tags

The lab used governance tags including:

- `Environment = Lab`
- `Department = IT`
- `Purpose = Cloud-Support-Training`
- `Owner = IT-Support`

These tags improved organization and provided a configuration that Azure Policy could evaluate.

---

## Resource Health

Azure Resource Health was reviewed to understand the current health of Azure resources.

Resource Health helps distinguish between:

- Azure platform problems
- Resource-specific problems
- Configuration problems
- User-access problems

This distinction is valuable during incident investigation.

---

## Storage Resource Health

The storage environment was reviewed through Resource Health.

The storage resources were shown as healthy during the completed review.

This provided evidence that troubleshooting scenarios involving access and permissions were not necessarily Azure platform outages.

---

## Resource Health Alert

A Resource Health alert was configured for:

`stitsupportlab002`

Alert name:

`ALERT-Storage-Resource-Health`

The alert was designed to detect degraded or unavailable resource-health states.

The description documented its purpose as notifying IT support when the Azure storage account becomes degraded or unavailable.

The alert used:

`ag-it-support-alerts`

for notification.

Evidence:

`../Screenshots/Monitoring/14-Resource-Health-Alert-Created.png`

---

## Resource Health Investigation Principle

When a user reports that an Azure service is unavailable, a support technician should not immediately assume the problem is:

- RBAC
- Networking
- Authentication
- Application configuration

Resource Health should also be reviewed to determine whether Azure reports a platform or resource-health issue.

---

## Azure Advisor

Azure Advisor was reviewed to identify recommendations related to the lab environment.

Advisor provides recommendations across areas such as:

- Reliability
- Security
- Performance
- Operational excellence
- Cost

Evidence:

`../Screenshots/Monitoring/16-Azure-Advisor-Overview.png`

---

## Advisor Reliability Score

The Advisor overview showed a Reliability score of approximately:

`94%`

The environment contained active reliability recommendations.

This demonstrated that a functioning Azure environment can still have opportunities for improvement.

---

## Reliability Recommendations

Advisor reliability recommendations were reviewed.

Evidence:

`../Screenshots/Monitoring/17-Azure-Advisor-Reliability-Recommendations.png`

Recommendations included items related to service-health alerting and outbound connectivity architecture.

---

## Service Health Recommendation

Azure Advisor recommended creating an Azure Service Health alert.

Evidence:

`../Screenshots/Monitoring/18-Azure-Advisor-Service-Health-Recommendation.png`

This recommendation was selected for implementation because Service Health alerting provides useful operational value without requiring an unnecessary workload deployment.

---

## NAT Gateway Recommendation

Azure Advisor also presented a recommendation related to NAT Gateway and outbound connectivity.

The recommendation was reviewed but not implemented.

A NAT Gateway was not required for the completed lab architecture and could introduce unnecessary cost.

This demonstrated that Advisor recommendations should be evaluated in context rather than automatically implemented.

---

## Advisor Alert

An Azure Advisor alert was configured to detect high-impact reliability recommendations.

Alert name:

`ALERT-Advisor-High-Reliability`

The alert targeted:

- Category: Reliability
- Impact: High

The description documented its purpose as alerting IT support when Azure Advisor generates a new high-impact reliability recommendation.

The alert used:

`ag-it-support-alerts`

Evidence:

`../Screenshots/Monitoring/19-Azure-Advisor-Reliability-Alert-Created.png`

---

## Azure Service Health

Azure Service Health provides information about Azure service issues that may affect a subscription.

It complements Resource Health.

Resource Health focuses on individual Azure resources.

Service Health focuses on Azure service incidents, planned maintenance, advisories, and other subscription-relevant platform information.

---

## Initial Service Health Alert Failure

The first Service Health alert configuration attempt failed.

Azure returned an error indicating that:

Service Health rules support action groups on the Global location only.

This was an important troubleshooting event because the existing action group was not suitable for the Service Health alert configuration.

Evidence:

`../Screenshots/Troubleshooting/Monitoring-Logs/03-Service-Health-Alert-Action-Group-Error.png`

Any Activity ID, account information, or other sensitive identifiers visible in this screenshot should be obscured before publication.

---

## Service Health Root Cause

The alert-rule failure was not caused by:

- Missing Azure permissions
- An invalid subscription
- A Service Health outage
- Incorrect event selection

The issue was the action-group location requirement.

Service Health required an action group using the:

`Global`

region.

---

## Global Action Group

A new action group was created specifically for Service Health.

Action group:

`ag-service-health-alerts`

Display name:

`ServiceHlth`

Region:

`Global`

The shorter display name was used to remain within the Azure display-name length requirement.

The action group used the same general governance tagging approach as the rest of the lab.

---

## Service Health Alert

After creating the Global action group, the Service Health alert was configured successfully.

Alert name:

`ALERT-Azure-Service-Health`

The alert targeted the Azure subscription and monitored applicable Service Health events.

The final configuration showed:

- Event types: All
- Resource type: Subscription
- Status: Enabled

Evidence:

`../Screenshots/Monitoring/20-Azure-Service-Health-Alert-Created.png`

---

## Service Health Alert Enabled

The completed alert was verified as enabled.

Evidence:

`../Screenshots/Monitoring/21-Azure-Service-Health-Alert-Enabled.png`

This completed the Service Health troubleshooting workflow:

Advisor recommendation

→ Alert configuration attempt

→ Azure error

→ Requirement investigation

→ Global action group

→ Alert creation

→ Enabled alert verification

---

## Advisor Reevaluation

Azure Advisor may not immediately remove a recommendation after the underlying configuration is changed.

The Azure interface indicated that recommendation updates may require additional time for reevaluation.

The lab therefore did not repeatedly recreate the Service Health configuration simply because Advisor had not yet refreshed the recommendation.

This reflects an important support principle:

Allow platform evaluation and propagation processes reasonable time before making unnecessary additional changes.

---

## Log Analytics

Azure Log Analytics was configured to centralize operational activity for investigation.

A Log Analytics workspace was created:

`LAW-IT-Support-Lab`

Resource group:

`RG-IT-Support-Lab`

Region:

North Central US

The workspace used the lab governance tagging structure.

Evidence:

`../Screenshots/Monitoring/22-Log-Analytics-Workspace-Created.png`

Workspace IDs and subscription identifiers should be obscured if visible in public screenshots.

---

## Diagnostic Settings

Azure Activity Log data was configured for export to the Log Analytics workspace.

Diagnostic setting:

`Activity-Log-to-LAW`

Destination:

`LAW-IT-Support-Lab`

The diagnostic configuration included Activity Log categories used for operational investigation.

---

## Activity Log Categories

The diagnostic setting included:

- Administrative
- Security
- ServiceHealth
- Alert
- Recommendation
- Policy
- Autoscale
- ResourceHealth

Evidence:

`../Screenshots/Monitoring/23-Activity-Log-Diagnostic-Setting.png`

This allowed subscription activity to be centralized in Log Analytics.

---

## Log Ingestion

After the diagnostic setting was enabled, Azure Activity data required time to appear in the workspace.

This demonstrated an important logging concept:

Telemetry ingestion is not always instantaneous.

A newly configured workspace may initially return no records even when the configuration is correct.

---

## Initial KQL Query

Azure Activity data was tested using Kusto Query Language.

An initial query used the `AzureActivity` table to confirm ingestion.

Example:

    AzureActivity
    | take 20

This query was useful for quickly verifying that records were reaching the workspace.

---

## Activity Investigation Query

A more focused query was then used:

    AzureActivity
    | where TimeGenerated > ago(1h)
    | project TimeGenerated, OperationNameValue, ActivityStatusValue, CategoryValue, ResourceGroup
    | sort by TimeGenerated desc
    | take 20

The query selected useful troubleshooting fields and displayed recent Azure activity.

Evidence:

`../Screenshots/Monitoring/24-Log-Analytics-Azure-Activity-Query.png`

---

## Failed Operation Investigation

A query was tested for failed operations.

At the time of the investigation, no matching failed operations were returned from the newly configured workspace.

This was not treated as a logging failure.

The workspace was new, and only activity ingested after configuration was expected to be available for the tested period.

---

## Generating Administrative Activity

To verify that administrative events were being ingested, a controlled resource-group tag change was performed.

A temporary tag value was changed from:

`KQL-Ingestion-Test`

to:

`KQL-Admin-Test`

This generated an administrative control-plane event that could be detected through Log Analytics.

---

## Administrative Event Ingestion

After allowing time for ingestion, Administrative tag-write activity appeared in Log Analytics.

The operation included Azure resource tag write activity.

This confirmed that:

- Activity Log export was configured
- Diagnostic settings were functioning
- Log Analytics was receiving Azure Activity records
- Administrative operations could be queried

---

## Activity Summary Query

A KQL summary query was used to aggregate events by category and status:

    AzureActivity
    | where TimeGenerated > ago(24h)
    | summarize EventCount=count() by CategoryValue, ActivityStatusValue
    | sort by EventCount desc

Evidence:

`../Screenshots/Monitoring/25-KQL-Activity-Summary.png`

This transformed raw Azure activity records into a concise operational summary.

---

## KQL Skills Demonstrated

The Log Analytics portion of the lab demonstrated KQL operations including:

- Table selection
- Time filtering
- Field projection
- Sorting
- Result limiting
- Category filtering
- Aggregation
- Counting
- Grouping by fields

These are useful foundational skills for Azure support, cloud operations, and security investigations.

---

## Azure Monitor Workbooks

Azure Monitor Workbooks were used to convert Log Analytics data into a reusable monitoring view.

Workbook name:

`IT-Support-Monitoring-Workbook`

The workbook used:

`LAW-IT-Support-Lab`

as its Log Analytics data source.

The primary time range used was:

Last 24 hours

---

## Workbook Component 1

The first workbook component was titled:

`Azure Activity Summary`

The query summarized Azure activity by category and status:

    AzureActivity
    | summarize EventCount=count() by CategoryValue, ActivityStatusValue
    | sort by EventCount desc

The results were displayed as a grid.

Evidence:

`../Screenshots/Monitoring/26-Azure-Monitor-Workbook-Activity-Summary.png`

---

## Workbook Component 2

The second component was titled:

`Administrative Activity Details`

The query focused specifically on Administrative activity:

    AzureActivity
    | where CategoryValue == "Administrative"
    | project TimeGenerated, OperationNameValue, ActivityStatusValue, ResourceGroup
    | sort by TimeGenerated desc

The resulting grid displayed administrative operations including Azure tag-write activity.

Evidence:

`../Screenshots/Monitoring/27-Azure-Monitor-Workbook-Activity-Details.png`

---

## Workbook Component 3

A third component was created:

`Recent Azure Activity`

The query displayed recent activity:

    AzureActivity
    | project TimeGenerated, CategoryValue, OperationNameValue, ActivityStatusValue, ResourceGroup
    | sort by TimeGenerated desc
    | take 20

This provided a broader recent-activity view for operational investigation.

---

## Workbook Value

The workbook demonstrated how a support technician can move from individual log queries to a reusable monitoring interface.

Instead of manually rebuilding every query during an incident, a workbook can provide organized operational views for:

- Administrative activity
- Alert activity
- Recent events
- Activity status
- Resource-group changes

---

## Monitoring Troubleshooting Methodology

A structured monitoring workflow was used throughout the lab.

### 1. Identify the Reported Problem

Determine whether the issue involves:

- Availability
- Access
- Configuration
- Performance
- Platform health
- Cost
- Governance

### 2. Review Resource State

Confirm that the affected Azure resource exists and is available.

### 3. Review Activity Log

Look for:

- Recent changes
- Failed operations
- Role assignments
- Policy activity
- Administrative events

### 4. Review Azure Monitor

Check:

- Alert rules
- Fired alerts
- Alert details
- Action groups

### 5. Review Resource Health

Determine whether Azure reports a resource-specific health problem.

### 6. Review Service Health

Determine whether a broader Azure platform event may affect the subscription.

### 7. Review Advisor

Check for reliability or operational recommendations related to the environment.

### 8. Review Log Analytics

Use centralized telemetry to investigate activity over time.

### 9. Use KQL

Filter and summarize relevant operational data.

### 10. Verify Resolution

Confirm the corrective action worked and avoid unnecessary unrelated changes.

---

## Monitoring vs Troubleshooting

Monitoring and troubleshooting are closely related but not identical.

Monitoring provides:

- Visibility
- Alerts
- Telemetry
- Trends
- Audit records

Troubleshooting uses that information to:

- Reproduce a problem
- Narrow the cause
- Identify the responsible layer
- Apply a corrective action
- Verify the outcome

The lab demonstrated both functions.

---

## VM Monitoring Scope

A Windows virtual machine was originally planned for the lab.

Low-cost B-series VM sizes were unavailable under the lab subscription in the tested regions.

A larger VM option was available, but deployment was intentionally deferred to avoid unnecessary cost.

Because a Windows VM was not deployed, VM-specific performance metrics were not collected.

No CPU, disk, network, or VM availability metrics are presented as completed evidence.

---

## Future VM Monitoring Methodology

If a Windows VM is added later, relevant Azure Monitor metrics could include:

- CPU percentage
- Disk read activity
- Disk write activity
- Network inbound traffic
- Network outbound traffic
- Availability information
- Additional VM metrics exposed through Azure Monitor

Those metrics could be correlated with:

- Activity Log
- Resource Health
- NSG configuration
- User-reported symptoms
- Log Analytics
- Azure Monitor alerts

This is documented as future methodology rather than completed lab evidence.

---

## Monitoring Security

Monitoring systems may expose operational and identity information.

Before publishing monitoring screenshots, review them for:

- Email addresses
- Subscription IDs
- Tenant IDs
- Object IDs
- Workspace IDs
- Account identifiers
- IP addresses
- Correlation IDs
- Activity IDs
- Request IDs

Credentials and secrets must never be published.

---

## Monitoring Screenshot Evidence

Completed monitoring screenshots include:

- `../Screenshots/Monitoring/01-Resource-Group-Activity-Log.png`
- `../Screenshots/Monitoring/02-RBAC-Role-Assignment-Succeeded.png`
- `../Screenshots/Monitoring/03-RBAC-Role-Assignment-Details.png`
- `../Screenshots/Monitoring/04-Administrative-Activity-Alert-Rule-Enabled.png`
- `../Screenshots/Monitoring/05-Azure-Monitor-Alert-Fired-Email-Notification.png`
- `../Screenshots/Monitoring/06-Azure-Monitor-Fired-Alerts.png`
- `../Screenshots/Monitoring/07-Azure-Monitor-Fired-Alert-Details.png`
- `../Screenshots/Monitoring/08-Monthly-Cost-Budget-Configured.png`
- `../Screenshots/Monitoring/09-Monthly-Budget-Overview.png`
- `../Screenshots/Monitoring/10-Budget-Alert-Configuration.png`
- `../Screenshots/Monitoring/11-Azure-Policy-Assignment-Created.png`
- `../Screenshots/Monitoring/12-Azure-Policy-Assignment-Overview.png`
- `../Screenshots/Monitoring/13-Azure-Policy-Compliance-Verified.png`
- `../Screenshots/Monitoring/14-Resource-Health-Alert-Created.png`
- `../Screenshots/Monitoring/16-Azure-Advisor-Overview.png`
- `../Screenshots/Monitoring/17-Azure-Advisor-Reliability-Recommendations.png`
- `../Screenshots/Monitoring/18-Azure-Advisor-Service-Health-Recommendation.png`
- `../Screenshots/Monitoring/19-Azure-Advisor-Reliability-Alert-Created.png`
- `../Screenshots/Monitoring/20-Azure-Service-Health-Alert-Created.png`
- `../Screenshots/Monitoring/21-Azure-Service-Health-Alert-Enabled.png`
- `../Screenshots/Monitoring/22-Log-Analytics-Workspace-Created.png`
- `../Screenshots/Monitoring/23-Activity-Log-Diagnostic-Setting.png`
- `../Screenshots/Monitoring/24-Log-Analytics-Azure-Activity-Query.png`
- `../Screenshots/Monitoring/25-KQL-Activity-Summary.png`
- `../Screenshots/Monitoring/26-Azure-Monitor-Workbook-Activity-Summary.png`
- `../Screenshots/Monitoring/27-Azure-Monitor-Workbook-Activity-Details.png`

Screenshot number 15 is intentionally unused.

---

## Troubleshooting Evidence

Monitoring-related troubleshooting evidence includes:

- `../Screenshots/Troubleshooting/Monitoring-Logs/01-Activity-Log-Investigation.png`
- `../Screenshots/Troubleshooting/Monitoring-Logs/02-Activity-Log-JSON-Details.png`
- `../Screenshots/Troubleshooting/Monitoring-Logs/03-Service-Health-Alert-Action-Group-Error.png`

---

## Related Help-Desk Tickets

Monitoring work is documented in:

- `../Help-Desk-Tickets/Ticket-002-Azure-Monitor-Administrative-Alert.md`
- `../Help-Desk-Tickets/Ticket-009-Service-Health-Alert-Configuration-Failure.md`
- `../Help-Desk-Tickets/Ticket-010-Log-Analytics-Activity-Investigation.md`

These tickets demonstrate alerting, troubleshooting, log investigation, and monitoring verification.

---

## Skills Demonstrated

- Microsoft Azure
- Azure Monitor
- Azure Activity Log
- Azure alert rules
- Action groups
- Resource Health
- Azure Service Health
- Azure Advisor
- Azure Policy
- Cost Management
- Azure budgets
- Log Analytics
- Diagnostic settings
- Kusto Query Language
- KQL filtering
- KQL aggregation
- Azure Monitor Workbooks
- Cloud monitoring
- Cloud governance
- Cloud observability
- Incident investigation
- Root-cause analysis
- Cost awareness
- Technical documentation

---

## Outcome

The monitoring portion of the Azure Cloud Support & Administration Lab developed into a layered cloud-observability environment.

Azure Activity Log was used to investigate administrative changes.

Azure Monitor alerts and action groups provided proactive notification.

Cost Management provided spending controls.

Azure Policy demonstrated governance and compliance.

Resource Health and Service Health provided health visibility at different Azure layers.

Azure Advisor identified reliability recommendations.

Log Analytics centralized Azure Activity records.

KQL was used to investigate and summarize telemetry.

Azure Monitor Workbooks converted collected logs into reusable operational views.

A real Service Health configuration failure was also diagnosed and corrected by identifying the requirement for a Global action group.

The completed monitoring work provides portfolio evidence of Azure monitoring, governance, logging, KQL, alerting, troubleshooting, observability, and cost-aware cloud administration.
