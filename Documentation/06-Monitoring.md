# Azure Monitoring

## Overview

This section documents the planned monitoring, logging, and 
performance-troubleshooting activities for the Azure Cloud Support & 
Administration Lab.

Azure monitoring tools will be used to investigate resource health, 
administrative activity, virtual machine performance, availability, and 
potential causes of support incidents.

The actual metrics, Activity Log events, troubleshooting findings, and 
screenshots will be added after the Azure environment is built and the 
monitoring scenarios are performed.

---

## Objectives

The objectives of this portion of the lab are to:

- Review Azure Monitor
- Review Azure virtual machine metrics
- Review Azure Activity Log
- Review resource health information
- Monitor CPU utilization
- Review disk and network activity
- Identify recent administrative changes
- Investigate a virtual machine performance complaint
- Use monitoring data during troubleshooting
- Compare symptoms with technical evidence
- Validate system behavior after corrective action
- Document monitoring findings professionally

---

## Azure Monitor

Azure Monitor provides monitoring and observability capabilities for Azure 
resources.

The lab will use available Azure monitoring information to support 
troubleshooting and incident investigation.

Monitoring data may help determine:

- Whether a resource is available
- Whether performance is abnormal
- Whether resource behavior changed
- Whether an administrative action occurred
- When a configuration change happened
- Whether the reported issue corresponds with measurable activity

Azure Monitor should support the troubleshooting process rather than replace 
it.

---

## Virtual Machine Monitoring

The primary Azure virtual machine used in the lab is planned as:

**VM-ITSupport-01**

After deployment, monitoring information will be reviewed for this resource.

The VM will provide a realistic system for investigating performance, 
availability, and administrative events.

---

## Planned VM Metrics

Metrics reviewed may include:

- CPU percentage
- Network activity
- Disk read activity
- Disk write activity
- Network inbound traffic
- Network outbound traffic
- Availability-related information
- Other metrics exposed by the Azure portal

The exact metric names and values will be recorded after the VM is deployed.

---

## CPU Monitoring

CPU utilization can provide useful evidence when investigating a report of 
poor system performance.

The technician will review:

- Current CPU utilization
- Recent CPU trends
- Sustained high CPU usage
- Temporary CPU spikes
- Time periods associated with the reported issue

High CPU utilization alone will not automatically be treated as the root 
cause.

The investigation should determine whether CPU activity actually corresponds 
with the user's symptoms.

---

## Disk Monitoring

Disk performance may contribute to slow applications or delayed system 
response.

Where available, the lab will review:

- Disk read activity
- Disk write activity
- Disk throughput
- Disk-related trends
- Changes occurring during the reported issue

Disk evidence will be compared with other VM metrics before drawing 
conclusions.

---

## Network Monitoring

Network activity may help identify whether performance or connectivity 
problems involve network behavior.

The lab may review:

- Network inbound traffic
- Network outbound traffic
- Traffic trends
- Unusual increases or decreases in network activity

Network metrics will be used together with Azure networking configuration and 
client-side testing when investigating connectivity-related incidents.

---

## Azure Activity Log

Azure Activity Log records management-plane events related to Azure 
resources.

The Activity Log may help identify administrative changes that occurred 
before or during a reported support issue.

Examples of events that may appear include:

- VM started
- VM stopped
- VM restarted
- Resource created
- Resource modified
- Resource deleted
- Deployment activity
- Network configuration changes
- Role-assignment changes
- Administrative operations

The actual events captured during the lab will be documented after testing.

---

## Activity Log Troubleshooting

The Activity Log may help answer questions such as:

- Was the VM recently stopped?
- Did an administrator restart the VM?
- Was a resource modified?
- Did a deployment occur?
- Was a network configuration changed?
- Was an access-related change performed?
- When did the change occur?
- Which resource was affected?

This information can be useful when a user reports that a system suddenly 
stopped working or changed behavior.

---

## Resource Health

Where available, Azure resource-health information will be reviewed.

Resource health may help distinguish among different categories of problems.

Examples include:

- Azure platform issue
- Resource configuration issue
- Virtual machine operating-system issue
- Connectivity issue
- User-access issue

Resource health information should be combined with other troubleshooting 
evidence before determining the root cause.

---

## Planned Performance Support Scenario

### User Report

A user reports that the Azure-hosted Windows system is running slowly and 
applications are taking longer than expected to respond.

### Initial Assessment

The technician will first confirm:

- Affected VM
- Scope of impact
- When the issue began
- Whether the issue is constant or intermittent
- Whether recent changes occurred
- Whether other services are affected

### Planned Investigation

The technician will review:

1. VM power state
2. Resource availability
3. Azure Monitor
4. CPU metrics
5. Disk activity
6. Network activity
7. Activity Log
8. VM configuration
9. VM size
10. Recent administrative changes
11. Available operating-system information
12. Workload behavior

The investigation will use measurable evidence before deciding on a 
corrective action.

---

## Avoiding Assumptions

The lab will not assume that a performance problem has a specific cause 
before evidence is reviewed.

Potential causes may include:

- High CPU usage
- Heavy disk activity
- Network congestion
- Resource sizing
- Application workload
- Temporary workload spike
- Operating-system process
- Recent configuration change
- Resource availability issue
- Other system conditions

The root cause will only be documented after the scenario is performed and 
investigated.

---

## Planned Availability Investigation

Monitoring tools may also be used when a user reports that an Azure-hosted 
resource is unavailable.

The technician may review:

- VM power state
- Resource health
- Activity Log
- Recent administrative actions
- Network configuration
- Azure metrics
- Resource status

This will help determine whether the issue involves:

- A stopped VM
- A configuration change
- A platform event
- A networking issue
- Another resource condition

---

## Monitoring-Based Troubleshooting Workflow

The planned workflow is:

User Reports Issue

↓

Confirm Affected Resource

↓

Check Resource State

↓

Review Azure Monitor Metrics

↓

Review Activity Log

↓

Review Resource Health

↓

Compare Symptoms With Evidence

↓

Identify Likely Cause

↓

Apply Corrective Action

↓

Retest

↓

Verify Resolution

This process encourages evidence-based troubleshooting.

---

## Planned Corrective Actions

The exact corrective action will depend on the findings.

Possible examples may include:

- Starting a stopped VM
- Restarting a resource when appropriate
- Correcting a configuration issue
- Adjusting a support-related setting
- Investigating a resource-sizing problem
- Correcting a network issue
- Correcting an access issue

No corrective action will be documented as completed until it has actually 
been performed.

---

## Validation Plan

After performing the monitoring portion of the lab, verify that:

- Azure Monitor can be accessed
- VM metrics are visible
- CPU activity can be reviewed
- Disk activity can be reviewed
- Network activity can be reviewed
- Activity Log events can be identified
- Resource health information can be reviewed where available
- Monitoring data can support troubleshooting
- Administrative changes can be correlated with support incidents
- Performance symptoms can be compared with measurable evidence
- Corrective actions can be validated using post-change monitoring

---

## Planned Screenshot Evidence

Potential screenshots include:

- Azure Monitor overview
- VM monitoring page
- CPU metric
- Disk metric
- Network metric
- Activity Log
- Resource health
- Performance issue evidence
- Administrative event related to a support scenario
- Monitoring after corrective action

Screenshots will only be added after the scenarios are performed.

Sensitive account, subscription, and connection information will be excluded 
or obscured when necessary.

---

## Related Help Desk Tickets

This documentation will support several Azure help-desk scenarios.

### Ticket 003 — VM Unavailable

Monitoring and Activity Log information may help determine why a VM became 
unavailable.

Possible areas reviewed include:

- VM state
- Administrative events
- Resource health
- Recent changes

### Ticket 007 — VM Performance Issue

This is the primary monitoring-focused scenario.

The investigation will review:

- CPU
- Disk
- Network
- Azure Monitor
- Activity Log
- VM configuration
- Recent changes

### Ticket 010 — Azure Resource Recovery

Activity Log and resource-state information may help identify what happened 
before a resource required recovery.

---

## Documentation Standards

Monitoring findings should document:

- User-reported symptoms
- Affected resource
- Time of issue
- Metrics reviewed
- Activity Log events reviewed
- Resource-health findings
- Technical interpretation
- Root cause
- Corrective action
- Verification

The final documentation should clearly distinguish observations from 
conclusions.

---

## Security Considerations

Monitoring screenshots and documentation should avoid exposing unnecessary 
sensitive information.

Do not publish:

- Passwords
- Access keys
- Secrets
- Full authentication tokens
- Sensitive account details
- Unnecessary subscription identifiers

Only information necessary to demonstrate the technical work should be 
included.

---

## Expected Outcome

After the Azure environment is built, this portion of the lab should 
demonstrate the ability to use Azure monitoring information to investigate 
realistic availability and performance incidents.

The completed documentation should show how Azure metrics, Activity Log 
events, resource status, and troubleshooting evidence can be combined to 
identify and verify technical issues.

Actual results will be added after the lab scenarios are performed.

---

## Skills Demonstrated

- Microsoft Azure
- Azure Monitor
- Azure Virtual Machines
- Azure metrics
- Azure Activity Log
- Resource health
- Performance monitoring
- Performance troubleshooting
- Availability troubleshooting
- Incident investigation
- Root cause analysis
- Evidence-based troubleshooting
- Technical support
- Technical documentation
