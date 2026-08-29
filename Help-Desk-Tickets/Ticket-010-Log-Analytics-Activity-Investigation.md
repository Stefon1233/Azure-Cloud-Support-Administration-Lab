# Ticket 010 - Log Analytics Activity Investigation

## Ticket Summary

**Category:** Azure Monitoring / Log Analysis  
**Service:** Azure Monitor / Log Analytics  
**Priority:** Medium  
**Status:** Resolved

Azure administrative activity needed to be centralized and queried for troubleshooting and operational monitoring. A Log Analytics workspace was deployed, the Azure subscription Activity Log was exported through a diagnostic setting, and Kusto Query Language (KQL) was 
used to investigate activity records.

An Azure Monitor Workbook was then created to provide a reusable view of recent Azure activity.

---

## User Report

IT support required a centralized method to review Azure administrative events rather than relying only on individual resource Activity Log pages.

The monitoring solution needed to support:

- Centralized log collection
- Administrative activity investigation
- Operation-status review
- KQL-based filtering
- Activity summarization
- Reusable dashboard visualization

---

## Environment

- Microsoft Azure
- Azure Monitor
- Log Analytics
- Azure Activity Log
- Kusto Query Language
- Azure Monitor Workbooks
- Resource Group: `RG-IT-Support-Lab`
- Log Analytics Workspace: `LAW-IT-Support-Lab`
- Region: North Central US
- Diagnostic Setting: `Activity-Log-to-LAW`
- Workbook: `IT-Support-Monitoring-Workbook`

---

## Initial Assessment

Azure Activity Log information was already available through the Azure Portal, but the lab did not yet have a centralized Log Analytics workspace for querying the data.

Centralizing the Activity Log would make it possible to investigate events using KQL and create reusable monitoring views.

---

## Log Analytics Workspace Deployment

I created a dedicated Log Analytics workspace:

`LAW-IT-Support-Lab`

The workspace was deployed in the lab resource group and configured in North Central US.

Governance tags were applied where appropriate to maintain consistency with the rest of the environment.

---

## Governance Tags

The lab uses the following resource tags:

- `Environment = Lab`
- `Department = IT`
- `Purpose = Cloud-Support-Training`
- `Owner = IT-Support`

These tags provide basic resource classification and ownership information.

---

## Activity Log Diagnostic Setting

After creating the workspace, I opened the Azure subscription Activity Log and configured a diagnostic setting.

The diagnostic setting was named:

`Activity-Log-to-LAW`

The destination was:

`LAW-IT-Support-Lab`

The following Activity Log categories were selected:

- Administrative
- Security
- ServiceHealth
- Alert
- Recommendation
- Policy
- Autoscale
- ResourceHealth

This provided centralized collection of subscription-level Azure activity.

---

## Initial Query

After configuring the diagnostic setting, I opened Azure Logs and queried the `AzureActivity` table.

The initial query was:

    AzureActivity
    | take 20

The workspace initially returned limited or no results because the diagnostic setting had only recently been enabled.

This required allowing time for Azure to ingest new Activity Log records.

---

## Log Ingestion Verification

After additional Azure activity occurred and ingestion completed, the `AzureActivity` table returned records.

To produce a cleaner troubleshooting view, I projected only operationally useful fields.

    AzureActivity
    | where TimeGenerated > ago(1h)
    | project TimeGenerated, OperationNameValue, ActivityStatusValue, CategoryValue, ResourceGroup
    | sort by TimeGenerated desc
    | take 20

The query successfully returned Azure activity associated with the lab environment.

This verified that:

1. The diagnostic setting was functioning.
2. Activity Log records were reaching Log Analytics.
3. The `AzureActivity` table was available.
4. KQL queries could be used for investigation.

---

## Failed Operation Investigation

I also created a KQL query designed to identify failed Azure operations.

    AzureActivity
    | where TimeGenerated > ago(24h)
    | where ActivityStatusValue =~ "Failed"
    | project TimeGenerated, OperationNameValue, ActivityStatusValue, CategoryValue, ResourceGroup
    | sort by TimeGenerated desc

No failed events were available in the workspace during the query period.

This was not treated as a monitoring failure because other Azure Activity records were being successfully ingested.

---

## Administrative Activity Investigation

A separate query was created to isolate administrative events.

    AzureActivity
    | where TimeGenerated > ago(24h)
    | where CategoryValue == "Administrative"
    | project TimeGenerated, OperationNameValue, ActivityStatusValue, ResourceGroup
    | sort by TimeGenerated desc

Administrative events required additional ingestion time before appearing in the workspace.

After ingestion completed, Azure activity associated with resource-tag modification became visible.

The operation included:

`MICROSOFT.RESOURCES/TAGS/WRITE`

The activity showed successful administrative processing.

---

## Activity Summary Query

To summarize the collected Azure Activity data, I used the KQL `summarize` operator.

    AzureActivity
    | where TimeGenerated > ago(24h)
    | summarize EventCount=count() by CategoryValue, ActivityStatusValue
    | sort by EventCount desc

This grouped activity by category and status and produced a simple operational summary.

The query demonstrated the ability to move beyond raw log records and create aggregated monitoring information.

---

## Root Cause / Investigation Finding

There was no Azure service outage associated with this investigation.

The primary issue encountered was the expected delay between:

1. Generating Azure activity
2. Exporting the activity through the diagnostic setting
3. Ingesting the data into Log Analytics
4. Making the records available for KQL queries

Once ingestion completed, the expected records became available.

The diagnostic configuration was therefore functioning correctly.

---

## Azure Monitor Workbook

After validating the Log Analytics data, I created an Azure Monitor Workbook named:

`IT-Support-Monitoring-Workbook`

The workbook provides a reusable monitoring view based on data from `LAW-IT-Support-Lab`.

Three monitoring components were created.

---

## Workbook Component 1 - Azure Activity Summary

The first component summarizes Azure Activity by category and status.

    AzureActivity
    | summarize EventCount=count() by CategoryValue, ActivityStatusValue
    | sort by EventCount desc

The component was titled:

`Azure Activity Summary`

This provides a quick view of the types and statuses of activity being recorded.

---

## Workbook Component 2 - Administrative Activity Details

The second component focuses specifically on administrative operations.

    AzureActivity
    | where CategoryValue == "Administrative"
    | project TimeGenerated, OperationNameValue, ActivityStatusValue, ResourceGroup
    | sort by TimeGenerated desc

The component was titled:

`Administrative Activity Details`

This view can help support personnel identify recent configuration changes.

---

## Workbook Component 3 - Recent Azure Activity

The third component displays recent activity across categories.

    AzureActivity
    | project TimeGenerated, CategoryValue, OperationNameValue, ActivityStatusValue, ResourceGroup
    | sort by TimeGenerated desc
    | take 20

The component was titled:

`Recent Azure Activity`

This provides a broader operational view of the most recent subscription activity.

---

## Verification

The completed monitoring solution was verified by confirming:

1. `LAW-IT-Support-Lab` was active.
2. `Activity-Log-to-LAW` was configured.
3. All required Activity Log categories were selected.
4. Azure Activity records appeared in Log Analytics.
5. KQL queries executed successfully.
6. Administrative activity became visible after ingestion.
7. Activity could be summarized by category and status.
8. The Azure Monitor Workbook displayed Log Analytics data.
9. The workbook was successfully saved.
10. The monitoring views could be reused for future investigations.

---

## Troubleshooting Process

The investigation followed this workflow:

1. Deploy a Log Analytics workspace.
2. Configure Azure Activity Log export.
3. Select the required diagnostic categories.
4. Send the logs to the workspace.
5. Open Azure Logs.
6. Scope queries to the Log Analytics workspace.
7. Test the `AzureActivity` table.
8. Allow time for log ingestion.
9. Query recent activity.
10. Filter administrative operations.
11. Search for failed operations.
12. Summarize activity using KQL.
13. Create a reusable Azure Monitor Workbook.
14. Verify workbook results.

---

## Support Significance

Centralized logging is valuable during cloud-support investigations because a technician may need to answer questions such as:

- What administrative changes occurred?
- When did a configuration change happen?
- Did an Azure operation succeed or fail?
- Which resource group was affected?
- Are there recent alert events?
- Are multiple events related to the same incident?

Log Analytics and KQL provide a more flexible investigation method than manually browsing individual resource pages.

---

## Production Considerations

In a production Azure environment, Log Analytics design should consider:

- Data retention requirements
- Workspace architecture
- Diagnostic-setting coverage
- Log ingestion costs
- Access controls
- Sensitive information
- Alerting requirements
- Saved queries
- Workbooks
- Automation and incident-response integrations

Queries and dashboards should be designed around operational requirements rather than collecting data without a defined purpose.

---

## Security and Privacy

Azure log records can expose identifiers and account information.

Before publishing screenshots publicly, sensitive fields should be reviewed and redacted where appropriate.

Examples include:

- Subscription IDs
- Tenant IDs
- User email addresses
- Correlation IDs
- Activity IDs
- Workspace IDs
- Event identifiers

The portfolio screenshots use limited projected fields where possible to reduce unnecessary exposure.

---

## Screenshots

### Log Analytics Configuration

- `../Screenshots/Monitoring/22-Log-Analytics-Workspace-Created.png`
- `../Screenshots/Monitoring/23-Activity-Log-Diagnostic-Setting.png`

### KQL Investigation

- `../Screenshots/Monitoring/24-Log-Analytics-Azure-Activity-Query.png`
- `../Screenshots/Monitoring/25-KQL-Activity-Summary.png`

### Azure Monitor Workbook

- `../Screenshots/Monitoring/26-Azure-Monitor-Workbook-Activity-Summary.png`
- `../Screenshots/Monitoring/27-Azure-Monitor-Workbook-Activity-Details.png`

---

## Skills Demonstrated

This ticket demonstrates experience with:

- Azure Monitor
- Log Analytics
- Azure Activity Log
- Diagnostic settings
- Kusto Query Language
- Log ingestion troubleshooting
- Administrative activity investigation
- Operational monitoring
- Azure Monitor Workbooks
- Cloud troubleshooting
- Technical documentation

---

## Resolution Summary

**Issue:** Azure administrative activity needed to be centralized for investigation and monitoring.

**Configuration:** Created `LAW-IT-Support-Lab` and exported subscription Activity Logs using `Activity-Log-to-LAW`.

**Investigation:** Used KQL to review activity, filter administrative operations, search for failures, and summarize event status.

**Additional Finding:** Newly generated records required time to appear because of Azure log-ingestion latency.

**Monitoring Improvement:** Created `IT-Support-Monitoring-Workbook` with reusable activity views.

**Result:** Centralized Azure Activity monitoring and KQL-based investigation were successfully implemented and verified.

**Status:** Resolved
