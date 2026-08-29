# Ticket 004 - RBAC Resource Visibility Issue

## Ticket Summary

**Category:** Identity and Access Management  
**Service:** Azure Storage / Azure RBAC  
**Priority:** Medium  
**Status:** Resolved  

A user had been assigned the **Storage Blob Data Reader** role on an Azure Storage account but could not see or browse the storage account from the Azure Portal. The issue was caused by the user having data-plane permissions for blob access without the required 
management-plane permissions to view the storage resource itself.

---

## User Report

The user reported that access had been granted to blob data, but the storage account was not visible when signing in with the assigned Microsoft Entra account.

The user expected to be able to locate the storage account and access the permitted blob container.

---

## Environment

- Microsoft Azure
- Microsoft Entra ID
- Azure Role-Based Access Control
- Azure Storage
- Resource Group: `RG-IT-Support-Lab`
- Storage Account: `stitsupportlab002`

---

## Initial Investigation

I reviewed the role assignments applied to the affected user.

The user had been assigned:

- `Storage Blob Data Reader`

This role allowed the user to read blob data but did not provide sufficient management-plane permissions to browse the storage account through the Azure Portal.

This explained why the user could have blob-level permissions while still being unable to locate the storage resource.

---

## Root Cause

The issue was caused by a difference between:

- **Data-plane permissions**
- **Management-plane permissions**

`Storage Blob Data Reader` grants read access to blob data.

It does not independently provide the broader Azure Resource Manager permissions required to view and navigate the storage account resource in the Azure Portal.

The user therefore required an additional read-only management role.

---

## Resolution

I assigned the user the standard Azure RBAC role:

`Reader`

The final role configuration included:

- `Reader`
- `Storage Blob Data Reader`

The `Reader` role provided visibility into the Azure resource while `Storage Blob Data Reader` maintained the required blob-level read access.

---

## Verification

After the `Reader` role was assigned:

1. The user signed in using the Microsoft Entra account.
2. The storage account became visible in the Azure Portal.
3. The user was able to navigate to the permitted blob container.
4. Blob read access succeeded.
5. Write access remained denied, confirming least-privilege access was preserved.

---

## Least-Privilege Validation

The user was intentionally not assigned:

- Contributor
- Storage Blob Data Contributor
- Owner

This ensured the user could view the resource and read blob data without gaining unnecessary modification permissions.

A later upload attempt was denied, confirming that the user retained read-only access.

---

## Screenshots

Relevant evidence:

- `../Screenshots/Troubleshooting/Identity-Access/06-RBAC-Reader-Assignment.png`
- `../Screenshots/Troubleshooting/Identity-Access/07-RBAC-Storage-Account-Not-Visible.png`
- `../Screenshots/Troubleshooting/Identity-Access/08-RBAC-Reader-And-Blob-Reader-Roles.png`
- `../Screenshots/Troubleshooting/Identity-Access/09-RBAC-Read-Allowed-Write-Denied.png`
- `../Screenshots/Troubleshooting/Identity-Access/10-RBAC-Blob-Read-Success.png`

---

## Support Notes

This scenario demonstrates an important Azure support distinction between management-plane and data-plane RBAC permissions.

A user can have permission to access Azure Storage data while still lacking permission to browse or view the storage resource through Azure Resource Manager.

When troubleshooting similar incidents, review both:

- Resource-level RBAC permissions
- Data-level Azure Storage roles

---

## Resolution Summary

**Issue:** User could not see an Azure Storage account despite having blob read permissions.

**Cause:** `Storage Blob Data Reader` provided data-plane access but not sufficient management-plane visibility.

**Fix:** Added the Azure `Reader` role while retaining `Storage Blob Data Reader`.

**Result:** Storage account visibility and blob read access were restored while write access remained blocked.

**Status:** Resolved
