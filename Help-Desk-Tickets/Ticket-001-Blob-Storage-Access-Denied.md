# Ticket 001 – Azure Blob Storage Access Denied

## Ticket Information

- **Ticket ID:** AZ-001
- **Category:** Azure Storage / Identity & Access Management
- **Priority:** Medium
- **Status:** Resolved
- **Environment:** Microsoft Azure
- **Affected Service:** Azure Blob Storage
- **Storage Account:** stitupportlab001
- **Container:** support-files
- **Authentication Method:** Microsoft Entra ID
- **Resolution:** Azure RBAC role assignment

---

## Issue Summary

A user was unable to access files stored in the `support-files` Azure Blob Storage container while authenticating with a Microsoft Entra user account.

The Azure portal displayed an authorization error indicating that the account did not have permission to list the data within the container.

The same storage container contained the test file:

`Azure-Support-Test.txt`

The issue was investigated as an Azure role-based access control (RBAC) permissions problem.

---

## User-Reported Issue

The user reported being unable to view files stored within the Azure Blob Storage container.

When the container was opened using Microsoft Entra authentication, Azure displayed an authorization error and returned no blob objects.

### Error Observed

Azure reported that the account did not have permission to list the data using Microsoft Entra ID.

The container displayed:

`No items found`

even though a blob had previously been uploaded successfully.

---

## Initial Investigation

The Azure Storage container configuration was reviewed to determine whether the problem involved:

- Blob availability
- Container configuration
- Authentication method
- Azure RBAC permissions
- Storage account access
- User role assignments

The blob had previously been confirmed to exist in the container, which indicated that the problem was related to authorization rather than missing data.

---

## Troubleshooting

### Step 1 – Reproduce the Problem

The `support-files` container was opened using:

**Authentication method:** Microsoft Entra user account

Azure returned an authorization error indicating that the signed-in account did not have sufficient permission to list blob data.

This successfully reproduced the user's reported problem.

---

### Step 2 – Review Azure RBAC

The container's:

**Access Control (IAM) → Role assignments**

configuration was reviewed.

The investigation showed that access to blob data depended on an appropriate Azure data-plane RBAC role.

The required role was identified as:

**Storage Blob Data Reader**

This role provides read access to Azure Blob Storage data without granting unnecessary write or administrative permissions.

---

### Step 3 – Assign the Required Role

The following RBAC assignment was configured:

- **Role:** Storage Blob Data Reader
- **Assignment type:** User
- **Scope:** `support-files` container
- **Authentication:** Microsoft Entra ID

The role was assigned to the affected user account.

Azure confirmed that the role assignment was successfully added.

---

## Resolution

After the **Storage Blob Data Reader** role was assigned, the container was reopened using the Microsoft Entra user account authentication method.

The container successfully displayed:

`Azure-Support-Test.txt`

The previous authorization error was no longer present.

This confirmed that the issue was caused by insufficient Azure RBAC permissions.

---

## Verification

The following checks were completed after remediation:

- Microsoft Entra authentication was selected.
- The authorization error no longer appeared.
- The `support-files` container loaded successfully.
- `Azure-Support-Test.txt` became visible.
- Blob metadata was accessible.
- The RBAC assignment was confirmed in Access Control (IAM).

The incident was considered resolved after successful access verification.

---

## Root Cause

The affected account did not initially have an Azure data-plane role that permitted it to read and list Blob Storage data.

Having access to Azure resources does not automatically provide access to the underlying blob data.

The missing **Storage Blob Data Reader** role prevented the account from listing objects within the container.

---

## Corrective Action

Assigned:

**Storage Blob Data Reader**

at the container scope to provide the minimum required permissions for the user.

This followed the principle of least privilege by granting read access rather than broader contributor or owner permissions.

---

## Resolution Summary

**Problem:** User could not access Azure Blob Storage data using Microsoft Entra ID.

**Cause:** Missing Blob Storage data-plane RBAC permissions.

**Fix:** Assigned the Storage Blob Data Reader role at the container level.

**Result:** Blob access was successfully restored and verified.

**Ticket Status:** Resolved

---

## Skills Demonstrated

- Microsoft Azure administration
- Azure Blob Storage
- Microsoft Entra ID
- Azure Role-Based Access Control (RBAC)
- Identity and access troubleshooting
- Data-plane permissions
- Principle of least privilege
- Help desk incident documentation
- Root cause analysis
- Troubleshooting and verification

---

## Evidence

Supporting screenshots are stored in the repository's `Screenshots/Troubleshooting` and `Screenshots/Storage` directories.

The troubleshooting sequence demonstrates:

1. Successful blob creation and storage
2. Access failure using Microsoft Entra authentication
3. RBAC investigation
4. Storage Blob Data Reader assignment
5. Successful restoration of blob access

---

## Support Technician Notes

This incident demonstrates the distinction between Azure resource management permissions and Azure Storage data permissions.

When troubleshooting Azure Storage authorization issues, administrators should verify both the authentication method and the user's data-plane RBAC assignments before modifying storage configuration or granting broader administrative access.
