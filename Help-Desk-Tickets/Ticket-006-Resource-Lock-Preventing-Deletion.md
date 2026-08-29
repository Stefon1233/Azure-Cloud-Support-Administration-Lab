# Ticket 006 - Azure Resource Lock Preventing Deletion

## Ticket Summary

**Category:** Azure Resource Management / Governance  
**Service:** Azure Storage  
**Priority:** Medium  
**Status:** Resolved  

An attempted deletion operation against an Azure Storage resource was blocked even though the administrative account otherwise had sufficient permissions. Investigation determined that a Delete management lock named `Protect-Storage-Account` was protecting the storage 
resource.

The lock was verified as the cause of the failed deletion. It was later temporarily removed during a controlled recovery test and restored after the test was completed.

---

## User Report

An administrator attempted to perform a deletion operation involving the Azure Storage environment but Azure prevented the action.

The resource remained available even though the deletion operation had been initiated.

The objective was to determine whether the failure was caused by:

- Azure RBAC permissions
- Storage configuration
- Resource dependencies
- Azure Policy
- A management lock

---

## Environment

- Microsoft Azure
- Azure Resource Manager
- Azure Storage
- Azure Management Locks
- Azure Activity Log
- Resource Group: `RG-IT-Support-Lab`
- Storage Account: `stitsupportlab002`
- Lock Name: `Protect-Storage-Account`
- Lock Type: `Delete`

---

## Initial Investigation

I reviewed the storage resource and confirmed that it was still deployed.

Because the deletion operation was blocked, I investigated the governance controls applied to the resource.

The storage account had an Azure management lock configured with the following settings:

**Lock Name:** `Protect-Storage-Account`

**Lock Type:** `Delete`

**Notes:** Prevent accidental deletion of IT support lab storage resources.

---

## Root Cause

The deletion failure was caused by the Azure `Delete` management lock.

A Delete lock allows authorized users to read and modify a protected resource while preventing deletion until the lock is removed by an appropriately authorized administrator.

This behavior is separate from standard Azure RBAC authorization.

Having sufficient permissions to administer a resource does not automatically bypass an Azure management lock.

---

## Troubleshooting

I verified the lock configuration and reproduced the blocked deletion behavior.

The troubleshooting sequence included:

1. Confirming that the storage resource still existed.
2. Reviewing the storage account's management locks.
3. Identifying `Protect-Storage-Account`.
4. Confirming that the lock type was `Delete`.
5. Attempting the controlled deletion operation.
6. Observing Azure block the operation.
7. Determining that the lock was functioning as designed.

No additional Azure RBAC role was required.

---

## Resolution

For the later controlled container recovery test, the Delete lock was temporarily removed by the administrator.

After the lock was removed, the intended deletion operation was allowed to proceed.

The resource recovery test was then completed using Azure Storage soft-delete functionality.

After recovery was verified, the protection control was restored.

The following management lock was recreated:

**Name:** `Protect-Storage-Account`

**Type:** `Delete`

This returned the storage environment to its protected state.

---

## Verification

I verified the resolution by confirming:

1. The original deletion attempt was blocked while the lock existed.
2. The lock was identified as the reason for the failure.
3. The controlled deletion succeeded after the lock was removed.
4. The recovery procedure was completed.
5. `Protect-Storage-Account` was restored afterward.
6. The storage environment was again protected against accidental deletion.

---

## Governance Significance

Azure management locks provide an additional layer of protection beyond Azure RBAC.

This scenario demonstrates the difference between:

- **Authorization** — whether an identity has permission to perform an operation.
- **Governance protection** — whether Azure allows the operation because of controls such as management locks.

This distinction is important when troubleshooting deletion failures.

An administrator should investigate governance controls before assuming the failure is caused by insufficient RBAC permissions.

---

## Production Considerations

In a production environment, management locks should not be removed casually.

Before removing a Delete lock, an administrator should:

- Confirm the requested change is authorized.
- Determine why the lock was originally implemented.
- Review the scope of the lock.
- Understand which resources inherit the protection.
- Document the change.
- Perform the required maintenance.
- Restore the lock when appropriate.

This reduces the risk of accidental resource deletion.

---

## Screenshots

Relevant evidence:

- `../Screenshots/Troubleshooting/Azure-Storage/09-Storage-Resource-Lock.png`
- `../Screenshots/Troubleshooting/Azure-Storage/10-Resource-Lock-Deletion-Blocked.png`
- `../Screenshots/Troubleshooting/Azure-Storage/16-Container-Deletion-Blocked-By-Resource-Lock.png`
- `../Screenshots/Troubleshooting/Azure-Storage/17-Container-Deletion-Succeeded-After-Lock-Removal.png`
- `../Screenshots/Troubleshooting/Azure-Storage/20-Storage-Delete-Lock-Restored.png`

---

## Support Notes

When an Azure deletion operation unexpectedly fails, troubleshooting should include checking:

- Azure RBAC
- Management locks
- Azure Policy
- Resource dependencies
- Activity Log events

In this incident, the management lock was not a malfunction. It was correctly enforcing the governance configuration applied to the storage resource.

The appropriate resolution was therefore to identify the protection mechanism, temporarily remove it only when required for the controlled test, and restore it afterward.

---

## Resolution Summary

**Issue:** Azure prevented a deletion operation against the storage environment.

**Cause:** A Delete management lock named `Protect-Storage-Account` was protecting the resource.

**Fix:** Verified the lock as the cause and temporarily removed it for an authorized recovery test.

**Result:** The controlled deletion and recovery procedure succeeded, and the Delete lock was restored afterward.

**Status:** Resolved
