# Ticket 005 - Azure Storage Network Access Failure

## Ticket Summary

**Category:** Cloud Storage / Networking  
**Service:** Azure Storage  
**Priority:** Medium  
**Status:** Resolved  

Access to an Azure Storage account failed after its network access configuration was restricted. The incident was investigated by reviewing the storage account networking configuration, identifying the access restriction, restoring the appropriate network setting, and 
verifying that storage access returned successfully.

---

## User Report

The user reported that an Azure Storage resource that had previously been accessible could no longer be reached.

The issue appeared after changes were made to the storage account's network access configuration.

The objective was to determine whether the failure was related to:

- Azure RBAC permissions
- Storage authentication
- Network access restrictions
- Storage service availability

---

## Environment

- Microsoft Azure
- Azure Storage
- Azure Storage Networking
- Azure Portal
- Resource Group: `RG-IT-Support-Lab`
- Storage Account: `stitsupportlab002`

---

## Initial Investigation

I first reviewed the storage account configuration to determine whether the account itself was available.

The storage resource remained deployed and operational.

Because the failure occurred after a networking configuration change, I focused the investigation on the storage account's network access settings.

---

## Network Configuration Review

Azure Storage provides network-level controls that determine which networks and clients are permitted to reach the storage account.

The configuration had been changed from its previously accessible state.

After the network restriction was applied, access to the storage resource failed.

This demonstrated that successful authentication or RBAC authorization alone does not guarantee access when the Azure Storage network layer blocks the connection.

---

## Root Cause

The root cause was a restrictive Azure Storage networking configuration.

The storage account's network access settings prevented the client from reaching the storage service.

This was a network-layer issue rather than an Azure RBAC role-assignment failure.

---

## Resolution

I returned to the Azure Storage networking configuration and restored the network access setting required for the lab environment.

After applying the corrected configuration, I allowed Azure time to process the change and then tested access again.

---

## Verification

After restoring the network configuration:

1. The Azure Storage resource remained healthy.
2. The storage account could be reached again.
3. The blob container became accessible.
4. The previous network-related access failure no longer occurred.
5. No additional RBAC permissions were required to resolve the incident.

The successful test confirmed that the networking configuration had been the cause of the failure.

---

## Troubleshooting Approach

The troubleshooting process followed this sequence:

1. Confirm the Azure resource still existed.
2. Review the recent configuration change.
3. Determine whether the problem involved identity, authorization, or networking.
4. Inspect the storage account network access configuration.
5. Identify the restrictive setting.
6. Restore the required network access.
7. Retest the storage resource.
8. Confirm service restoration.

---

## Security Considerations

Network restrictions are an important Azure Storage security control and should not automatically be disabled during troubleshooting.

In a production environment, the preferred resolution would depend on organizational requirements and could involve:

- Approved public network access
- Selected virtual networks
- Firewall rules
- Private endpoints
- Authorized IP ranges

For this lab, the configuration was restored to the setting required for the controlled test environment.

---

## Screenshots

Relevant evidence:

- `../Screenshots/Troubleshooting/Azure-Storage/06-Storage-Network-Access-Before.png`
- `../Screenshots/Troubleshooting/Azure-Storage/07-Storage-Network-Access-Failure.png`
- `../Screenshots/Troubleshooting/Azure-Storage/08-Storage-Network-Access-Restored.png`

---

## Support Notes

This scenario demonstrates why Azure support investigations should evaluate both authorization and network controls.

An Azure user may have valid credentials and correct RBAC permissions but still be unable to access a storage resource when network-level restrictions block the connection.

This distinction helps prevent unnecessary role changes when the actual problem exists at the networking layer.

---

## Resolution Summary

**Issue:** Azure Storage access failed after a networking configuration change.

**Cause:** The storage account's network access configuration restricted connectivity.

**Fix:** Restored the appropriate storage network access configuration.

**Result:** Storage connectivity was restored without changing the user's RBAC permissions.

**Status:** Resolved
