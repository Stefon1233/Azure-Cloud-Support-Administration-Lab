# Ticket 003 – NSG RDP Connectivity Issue

## Ticket Information

- **Ticket ID:** AZ-003
- **Category:** Azure Networking / Network Security
- **Priority:** Medium
- **Status:** Resolved
- **Environment:** Microsoft Azure
- **Affected Component:** Network Security Group
- **Network Security Group:** NSG-IT-Support
- **Affected Protocol:** RDP / TCP
- **Affected Port:** 3389
- **Scenario Type:** Simulated network security configuration incident

---

## Issue Summary

A simulated Azure networking incident was created to demonstrate troubleshooting of a Network Security Group rule that could prevent Remote Desktop Protocol (RDP) traffic.

An inbound security rule named `Deny-RDP-Test` was configured on `NSG-IT-Support`.

The rule explicitly denied TCP traffic destined for port 3389.

The configuration was reviewed, identified as the source of the simulated RDP restriction, and removed to restore the Network Security Group to its previous known-good configuration.

---

## Support Scenario

The support scenario represented a user reporting that RDP connectivity was unavailable after a network security configuration change.

The investigation focused on Azure Network Security Group inbound security rules because NSGs can allow or deny network traffic based on:

- Source
- Destination
- Port
- Protocol
- Priority
- Action

The objective was to identify whether an inbound NSG rule could be responsible for blocking RDP traffic.

---

## Baseline Configuration

Before introducing the simulated issue, the inbound security rules for `NSG-IT-Support` were reviewed.

The NSG contained Azure's default inbound security rules, including:

- AllowVnetInBound
- AllowAzureLoadBalancerInBound
- DenyAllInBound

A baseline screenshot was captured before modifying the NSG.

---

## Incident Simulation

A custom inbound security rule was created with the following configuration:

- **Name:** Deny-RDP-Test
- **Priority:** 300
- **Source:** Any
- **Source Port:** Any
- **Destination:** Any
- **Destination Port:** 3389
- **Protocol:** TCP
- **Action:** Deny
- **Service:** RDP

### Description

`Simulated RDP connectivity failure for IT support troubleshooting lab`

Because lower numerical NSG priorities are evaluated before higher numerical priorities, the priority 300 custom rule would be evaluated before Azure's default inbound rules.

---

## Troubleshooting

### Step 1 – Review Inbound Security Rules

The inbound security rules for `NSG-IT-Support` were inspected.

A custom rule named:

`Deny-RDP-Test`

was identified.

The rule was configured to deny TCP port 3389.

Because TCP 3389 is commonly used by Remote Desktop Protocol, the rule was identified as a configuration capable of blocking inbound RDP traffic within its applicable scope.

---

### Step 2 – Inspect Rule Configuration

The `Deny-RDP-Test` rule was opened for detailed inspection.

The configuration confirmed:

- Service: RDP
- Destination port: 3389
- Protocol: TCP
- Action: Deny
- Priority: 300

Azure also displayed warnings associated with the deny rule and its potential effect on network traffic.

This confirmed that the custom NSG configuration represented the intended root cause of the simulated incident.

---

## Root Cause

The simulated incident was caused by an inbound Network Security Group rule explicitly configured to deny TCP traffic on port 3389.

The rule:

`Deny-RDP-Test`

used priority `300`, causing it to be evaluated before Azure's default inbound security rules.

The configuration therefore represented an NSG-level restriction affecting RDP traffic.

---

## Remediation

The erroneous custom rule was removed from `NSG-IT-Support`.

Azure confirmed:

`Successfully deleted security rule 'Deny-RDP-Test'.`

After deletion, the inbound security rule list returned to the previous configuration containing the Azure default rules.

---

## Verification

The following verification steps were completed:

- Confirmed `Deny-RDP-Test` was no longer present.
- Confirmed the custom TCP 3389 deny rule had been removed.
- Confirmed the default NSG inbound rules remained intact.
- Confirmed Azure successfully processed the security-rule deletion.
- Compared the resulting configuration against the original baseline.

The Network Security Group was successfully returned to its previous known-good configuration.

---

## Important Lab Scope Note

This was a simulated NSG configuration troubleshooting scenario.

The lab demonstrated identification and remediation of an NSG rule capable of blocking RDP traffic.

An actual RDP session failure and subsequent successful RDP reconnection were not used as verification evidence for this scenario.

Therefore, the documented resolution is limited to verification that the problematic NSG configuration was identified and removed.

---

## Resolution Summary

**Problem:** Simulated RDP restriction caused by an Azure NSG rule.

**Affected NSG:** NSG-IT-Support

**Problematic Rule:** Deny-RDP-Test

**Protocol:** TCP

**Port:** 3389

**Action:** Deny

**Priority:** 300

**Root Cause:** Custom inbound security rule configured to deny RDP traffic.

**Remediation:** Removed the erroneous custom deny rule.

**Verification:** Confirmed deletion and restoration of the previous NSG rule configuration.

**Ticket Status:** Resolved

---

## Skills Demonstrated

- Microsoft Azure networking
- Network Security Groups
- Azure inbound security rules
- TCP/IP troubleshooting
- RDP port identification
- NSG priority evaluation
- Network access troubleshooting
- Configuration analysis
- Root cause analysis
- Change remediation
- Post-change verification
- Help desk incident documentation

---

## Evidence

Supporting screenshots are stored in:

`Screenshots/Troubleshooting/`

### Screenshot Sequence

1. `06-NSG-Inbound-Rules-Before-Change.png`
   - Baseline NSG configuration before the simulated incident.

2. `07-NSG-Deny-RDP-Rule.png`
   - Custom `Deny-RDP-Test` rule visible in the inbound rule list.

3. `08-NSG-RDP-Blocking-Rule-Diagnosed.png`
   - Detailed inspection showing TCP 3389, Deny action, and priority 300.

4. `09-NSG-Blocking-Rule-Removed.png`
   - Azure confirmation that the problematic rule was successfully deleted and the NSG returned to its previous configuration.

---

## Support Technician Notes

When troubleshooting connectivity problems involving Azure virtual networks, Network Security Groups should be reviewed for custom rules that may deny required traffic.

Important fields include:

- Rule priority
- Source
- Destination
- Protocol
- Destination port
- Allow or Deny action

Administrators should avoid immediately creating broad Allow rules when troubleshooting.

The existing rule set should first be inspected to determine whether an incorrect or obsolete rule is causing the issue.

After remediation, the resulting NSG configuration should be verified against the expected network security baseline.
