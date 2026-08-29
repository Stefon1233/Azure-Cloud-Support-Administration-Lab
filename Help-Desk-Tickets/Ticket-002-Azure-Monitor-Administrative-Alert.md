# Ticket 002 – Azure Monitor Administrative Activity Alert

## Ticket Information

- **Ticket ID:** AZ-002
- **Category:** Azure Monitor / Monitoring & Alerting
- **Priority:** Medium
- **Status:** Resolved
- **Environment:** Microsoft Azure
- **Affected Service:** Azure Monitor
- **Resource Group:** RG-IT-Support-Lab
- **Alert Rule:** ALERT-Administrative-Activity
- **Action Group:** AG-IT-Support-Alerts
- **Notification Method:** Email
- **Signal Type:** Activity Log

---

## Issue Summary

The IT support environment required monitoring for administrative changes occurring within the Azure lab environment.

Without an alerting mechanism, administrative operations could occur without proactively notifying the support team.

An Azure Monitor Activity Log alert was configured to detect administrative activity and automatically send an email notification through an Azure Monitor action group.

---

## Support Request

Configure monitoring for administrative operations within the Azure IT support lab.

The monitoring solution should:

- Detect administrative Activity Log events
- Monitor the RG-IT-Support-Lab environment
- Generate an Azure Monitor alert
- Notify IT support by email
- Provide information that can be used to investigate the event

---

## Initial Investigation

Azure Monitor was reviewed to determine the appropriate monitoring method.

Because the requirement involved Azure administrative operations rather than application performance or resource utilization, an Activity Log alert was selected.

The alert would monitor the Administrative event category.

---

## Configuration

### Step 1 – Configure Alert Scope

The alert was configured for the Azure lab environment containing:

`RG-IT-Support-Lab`

This allowed administrative operations associated with the lab environment to be monitored.

---

### Step 2 – Configure Alert Condition

The Azure Monitor condition was configured with:

- **Signal name:** All Administrative operations
- **Category:** Administrative
- **Signal source:** Azure Activity Log

The condition was configured to trigger when an administrative event was recorded.

The Azure portal displayed recent administrative events during configuration, confirming that Activity Log data was available for monitoring.

---

### Step 3 – Create Action Group

A dedicated Azure Monitor action group was created.

Configuration:

- **Action group name:** AG-IT-Support-Alerts
- **Display name:** ITSupport
- **Resource group:** RG-IT-Support-Lab
- **Notification type:** Email/SMS message/Push/Voice
- **Notification method used:** Email
- **Notification name:** IT-Support-Email

The action group provides a reusable notification mechanism that can be attached to Azure Monitor alert rules.

---

### Step 4 – Configure Alert Rule

The following alert rule was created:

**Alert rule name:**

`ALERT-Administrative-Activity`

**Description:**

`Monitors administrative operations within RG-IT-Support-Lab and notifies the IT support action group when administrative activity occurs.`

The alert rule was enabled upon creation.

---

## Testing

Administrative activity was generated within the Azure environment after the alert rule was enabled.

Azure Monitor subsequently detected multiple administrative events.

The alert appeared in:

**Azure Monitor → Alerts**

with:

- **Alert:** ALERT-Administrative-Activity
- **Severity:** Sev4 – Verbose
- **Alert condition:** Fired
- **User response:** New

This confirmed that the Activity Log condition was functioning.

---

## Email Notification Verification

The configured Azure Monitor action group successfully generated email notifications.

Microsoft Azure delivered an alert email containing:

- Alert name
- Severity
- Monitor condition
- Affected resource
- Resource type
- Resource group
- Alert description
- Link to investigate the alert in Azure Monitor

The received message confirmed that the notification pipeline was working from:

**Administrative event → Azure Activity Log → Alert rule → Action group → Email notification**

---

## Alert Investigation

A fired alert was opened in Azure Monitor for further investigation.

The alert details displayed information including:

- Severity
- Fired time
- Affected resource
- Monitor service
- Alert condition
- User response
- Event level
- Category
- Initiating account
- Operation information
- Event data ID
- Operation ID
- Submission timestamp
- Target resource type
- Alert ID

This information can assist support administrators with determining what administrative operation triggered an alert and identifying the associated Azure resource or identity.

---

## Resolution

Azure Monitor administrative activity monitoring was successfully implemented.

The environment can now:

- Detect administrative operations
- Generate Activity Log alerts
- Record fired alerts in Azure Monitor
- Notify IT support through email
- Provide event details for investigation

The monitoring requirement was considered successfully completed after both the Azure Monitor alert and email notification were verified.

---

## Root Cause

This ticket represents a monitoring configuration request rather than a service failure.

The Azure lab environment initially did not have a dedicated notification workflow for administrative Activity Log events.

Without the alert rule and action group, support personnel would need to manually review the Azure Activity Log to identify administrative changes.

---

## Corrective Action

Created an Azure Monitor Activity Log alert and connected it to a dedicated IT support action group.

The following components were implemented:

1. Administrative Activity Log condition
2. Azure Monitor alert rule
3. IT support action group
4. Email notification
5. Fired-alert verification
6. Alert investigation workflow

---

## Resolution Summary

**Request:** Implement monitoring for Azure administrative activity.

**Solution:** Created an Azure Monitor Activity Log alert.

**Alert Rule:** ALERT-Administrative-Activity

**Action Group:** AG-IT-Support-Alerts

**Notification:** Email

**Testing:** Administrative events successfully triggered the alert.

**Verification:** Fired alerts appeared in Azure Monitor and notification emails were received.

**Ticket Status:** Resolved

---

## Skills Demonstrated

- Microsoft Azure administration
- Azure Monitor
- Azure Activity Log
- Azure alert rules
- Azure action groups
- Email alert configuration
- Cloud monitoring
- Event investigation
- Administrative activity monitoring
- Incident detection
- Support documentation
- Monitoring verification

---

## Evidence

Supporting screenshots should include:

1. Azure Monitor administrative alert condition
2. Action group configuration
3. Alert rule enabled
4. Fired alerts displayed in Azure Monitor
5. Fired alert investigation details
6. Azure Monitor email notification

These screenshots demonstrate the complete monitoring lifecycle from configuration through detection and notification.

---

## Support Technician Notes

Azure Activity Log alerts provide proactive visibility into control-plane operations occurring within an Azure environment.

For support environments, combining Activity Log alerts with action groups allows administrators to move from manually reviewing logs to receiving notifications when relevant administrative activity occurs.

Alert conditions should be scoped carefully in production environments to reduce unnecessary notifications and alert fatigue.
