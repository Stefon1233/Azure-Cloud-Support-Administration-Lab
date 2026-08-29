# Ticket 009 - Azure Service Health Alert Configuration Failure

## Ticket Summary

**Category:** Azure Monitoring / Service Health  
**Service:** Azure Service Health / Azure Monitor  
**Priority:** Medium  
**Status:** Resolved  

An Azure Service Health alert rule failed during configuration because the notification configuration used an incompatible action group location. Azure reported that Service Health alert rules require action groups configured in the Global location.

The error was investigated, a new Global action group was created, and the Service Health alert was successfully deployed and verified as enabled.

---

## User Report

The objective was to configure proactive monitoring for Azure service incidents that could affect the lab subscription.

The alert was intended to notify IT support when Azure reported Service Health incidents affecting subscribed Azure services.

During creation of the alert rule, Azure rejected the configuration.

---

## Environment

- Microsoft Azure
- Azure Service Health
- Azure Monitor
- Azure Monitor Alerts
- Azure Action Groups
- Resource Group: `RG-IT-Support-Lab`
- Subscription: Azure subscription 1
- Alert Rule: `ALERT-Azure-Service-Health`
- Action Group: `ag-service-health-alerts`

---

## Initial Configuration

The Service Health alert was configured at the subscription scope.

The configuration included:

- Azure subscription scope
- Azure services
- Azure regions
- Service Health event monitoring
- Resource group: `RG-IT-Support-Lab`
- Alert rule name: `ALERT-Azure-Service-Health`

The objective was to create a centralized notification mechanism for Azure platform incidents.

---

## Error Encountered

When the alert rule was submitted, Azure returned an error indicating:

`Service Health rules support action groups on global location only.`

The alert rule was not created successfully.

This provided a specific configuration clue for the investigation.

---

## Initial Investigation

I reviewed the failed alert configuration and focused on the notification/action-group requirement identified by Azure.

The error indicated that the problem was not related to:

- The Azure subscription
- Service selection
- Region selection
- RBAC authorization
- The Service Health service itself

Instead, the failure was associated with the action group configuration.

---

## Root Cause

Azure Service Health alert rules require compatible Azure Monitor action groups configured with the **Global** location.

The notification configuration being used during the initial attempt did not meet this requirement.

As a result, Azure rejected the Service Health alert rule.

---

## Resolution

I created a dedicated action group for Service Health notifications.

The action group was configured as:

**Action Group Name:** `ag-service-health-alerts`

**Display Name:** `ServiceHlth`

**Region:** `Global`

**Resource Group:** `RG-IT-Support-Lab`

The Global region was selected specifically to satisfy the requirement identified in the Azure error message.

---

## Governance Tags

The action group and related monitoring resources were configured using the lab's governance tags where supported:

- `Environment = Lab`
- `Department = IT`
- `Purpose = Cloud-Support-Training`
- `Owner = IT-Support`

This maintained consistent resource organization across the Azure environment.

---

## Alert Rule Configuration

After correcting the action-group configuration, I recreated the Azure Service Health alert.

The alert rule was configured as:

**Alert Rule Name:** `ALERT-Azure-Service-Health`

**Scope:** Azure subscription 1

**Services:** All selected services

**Regions:** All selected regions

**Service Health Events:** Service Health monitoring

**Action Group:** `ag-service-health-alerts`

The alert was enabled when created.

---

## Alert Description

The alert was documented with the following operational purpose:

Alerts IT support when Azure Service Health reports service issues affecting the subscription, enabling proactive investigation and response.

This provides a clear explanation of why the alert exists and how it supports IT operations.

---

## Verification

After correcting the configuration:

1. The Global action group was created successfully.
2. The Service Health alert rule was submitted again.
3. Azure confirmed successful alert-rule creation.
4. The Health alerts page displayed the new alert.
5. The alert showed an Enabled status.
6. The subscription was listed as the target scope.
7. Services and regions were configured for broad monitoring coverage.

The successful deployment confirmed that the action-group location had caused the original failure.

---

## Troubleshooting Process

The investigation followed this sequence:

1. Attempt to create the Azure Service Health alert.
2. Capture the Azure configuration error.
3. Read the error details rather than repeatedly submitting the same configuration.
4. Identify the Global action-group requirement.
5. Review the notification configuration.
6. Create a dedicated Global action group.
7. Configure the required notification destination.
8. Recreate the Service Health alert.
9. Verify successful creation.
10. Confirm that the alert was enabled.

---

## Azure Advisor Context

Azure Advisor had previously identified a reliability recommendation to create an Azure Service Health alert.

The recommendation was classified as a high-impact reliability recommendation.

This Service Health configuration was implemented as part of improving the lab's proactive monitoring and reliability posture.

Azure Advisor can require additional time to reevaluate recommendations after the recommended configuration is implemented.

---

## Monitoring Significance

Service Health alerts provide proactive awareness of Azure platform events that may affect workloads.

These events can be different from resource-level monitoring.

For example:

- Azure Monitor can detect resource metrics and activity.
- Resource Health can report the health of individual Azure resources.
- Service Health provides information about Azure platform events affecting subscriptions and services.

Using these tools together provides broader operational visibility.

---

## Production Considerations

In a production environment, Service Health alerts should be routed to monitored notification channels or incident-management systems.

Organizations may configure notifications for:

- Service issues
- Planned maintenance
- Health advisories
- Security advisories

Action groups may route notifications through supported channels such as:

- Email
- SMS
- Push notifications
- Webhooks
- Automation workflows
- IT service-management integrations

Notification configuration should match the organization's escalation and incident-response procedures.

---

## Security and Privacy

Before publishing screenshots from the Azure Portal, sensitive information should be reviewed and redacted where necessary.

Examples include:

- User email addresses
- Subscription IDs
- Tenant IDs
- Correlation IDs
- Activity IDs
- Other unique Azure identifiers

This preserves useful technical evidence without exposing unnecessary account information.

---

## Screenshots

Troubleshooting evidence:

- `../Screenshots/Troubleshooting/Monitoring-Logs/03-Service-Health-Alert-Action-Group-Error.png`

Successful configuration evidence:

- `../Screenshots/Monitoring/18-Azure-Advisor-Service-Health-Recommendation.png`
- `../Screenshots/Monitoring/20-Azure-Service-Health-Alert-Created.png`
- `../Screenshots/Monitoring/21-Azure-Service-Health-Alert-Enabled.png`

---

## Skills Demonstrated

This incident demonstrates experience with:

- Azure Service Health
- Azure Monitor alerts
- Azure Action Groups
- Monitoring configuration
- Error-message analysis
- Root-cause identification
- Azure reliability monitoring
- Alert validation
- Cloud troubleshooting
- Governance tagging
- Technical documentation

---

## Support Notes

The most important troubleshooting clue was contained directly in the Azure error message.

Rather than treating the failed alert as a general Azure Portal problem, the error was used to isolate the incompatible action-group configuration.

Creating a dedicated Global action group resolved the issue without unnecessary changes to the subscription, monitoring scope, or Azure RBAC configuration.

---

## Resolution Summary

**Issue:** Azure Service Health alert creation failed.

**Error:** Service Health rules required an action group using the Global location.

**Cause:** The original notification/action-group configuration did not meet the Service Health Global-location requirement.

**Fix:** Created `ag-service-health-alerts` using the Global region and used it for the Service Health alert.

**Result:** `ALERT-Azure-Service-Health` was successfully created and verified as enabled.

**Status:** Resolved
