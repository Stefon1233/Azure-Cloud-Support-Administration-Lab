# Ticket 008 - Resource Group Reader Write Denied

## Ticket Summary

**Category:** Identity and Access Management  
**Service:** Azure RBAC / Azure Resource Manager  
**Priority:** Medium  
**Status:** Resolved  

A user assigned the Azure `Reader` role at the resource-group scope could successfully view resources but was unable to modify resource-group settings. The behavior was investigated and confirmed to be expected least-privilege enforcement rather than a service failure.

---

## User Report

The user reported that resources inside the Azure resource group were visible, but administrative changes could not be performed.

The user specifically encountered permission restrictions when attempting to:

- Modify resource-group locks
- Add or modify resource-group tags

The objective was to determine whether the access failure represented an incorrect role assignment or expected Azure RBAC behavior.

---

## Environment

- Microsoft Azure
- Microsoft Entra ID
- Azure Role-Based Access Control
- Azure Resource Manager
- Resource Group: `RG-IT-Support-Lab`
- Assigned Role: `Reader`
- Scope: Resource group

---

## Initial Investigation

I reviewed the user's role assignment at the resource-group scope.

The user had been intentionally assigned:

`Reader`

The Reader role provides access to view Azure resources and their configuration but does not provide permission to modify those resources.

This suggested that the reported behavior could be expected based on the assigned role.

---

## Access Verification

I signed in using the test Microsoft Entra account and verified that the user could access the Azure resource group.

The user was able to:

- Locate `RG-IT-Support-Lab`
- View resources in the resource group
- Review resource configuration
- Navigate through permitted Azure Portal pages

This confirmed that the Reader role assignment was active.

---

## Write-Permission Test

To verify the limitations of the assigned role, I attempted controlled administrative changes while authenticated as the Reader user.

Two write scenarios were tested.

### Management Lock Access

The resource-group Locks page displayed a permissions message indicating that the user did not have permission to edit locks.

This demonstrated that the Reader role did not grant governance modification permissions.

### Tag Modification

I then attempted to add or modify tags on the resource group.

Azure rejected the operation with an authorization failure.

The write operation could not be completed using the Reader account.

---

## Root Cause

The inability to modify the resource group was caused by the permissions intentionally associated with the Azure `Reader` role.

The Reader role is designed to provide visibility without modification rights.

The access-denied behavior was therefore expected and did not indicate:

- An Azure outage
- A broken role assignment
- A Microsoft Entra authentication failure
- A resource-group configuration problem

Azure RBAC was functioning correctly.

---

## Resolution

No additional permissions were assigned to the Reader account.

Because the user's access level was intentionally designed to be read-only, increasing the role would have violated the least-privilege objective of the test.

Administrative changes were instead performed using the authorized administrator account.

---

## Governance Tag Configuration

After switching back to the authorized administrator account, governance tags were successfully configured on the resource group.

The following tags were applied:

- `Environment = Lab`
- `Department = IT`
- `Purpose = Cloud-Support-Training`
- `Owner = IT-Support`

This verified that the resource itself supported the requested change and that the earlier failure was specifically related to RBAC authorization.

---

## Verification

The troubleshooting results confirmed:

1. The Reader user could view the resource group.
2. The Reader user could inspect Azure resources.
3. The Reader user could not edit management locks.
4. The Reader user could not modify resource-group tags.
5. Azure returned an authorization failure for the attempted write.
6. The administrator account successfully modified the tags.
7. No unnecessary permissions were added to the Reader account.

---

## Least-Privilege Significance

This scenario demonstrates the principle of least privilege.

A support technician should not automatically increase a user's Azure role simply because a write operation fails.

The first question should be whether the requested operation is appropriate for that user's responsibilities.

If read-only access is the intended requirement, a denied write operation confirms that the security control is working correctly.

---

## Troubleshooting Approach

The investigation followed this sequence:

1. Confirm the user's identity.
2. Review the assigned Azure RBAC role.
3. Verify the assignment scope.
4. Confirm that read access works.
5. Test a controlled write operation.
6. Review the Azure authorization response.
7. Compare the attempted operation with the Reader role's intended permissions.
8. Verify the operation using an authorized administrator account.
9. Preserve the user's least-privilege role.

---

## Production Considerations

In a production environment, additional permissions should only be granted when required by the user's job responsibilities.

Before changing an Azure role assignment, support personnel should determine:

- What operation the user needs to perform
- Whether the operation is part of the user's responsibilities
- The minimum role required
- The appropriate assignment scope
- Whether approval is required
- Whether privileged access should be temporary

Broad roles such as Contributor or Owner should not be assigned merely to bypass an authorization error.

---

## Screenshots

Relevant evidence:

- `../Screenshots/Identity/03-Resource-Group-RBAC-Before-Assignment.png`
- `../Screenshots/Identity/04-Resource-Group-Reader-Role-Assigned.png`
- `../Screenshots/Identity/05-Resource-Group-Reader-Access-Verified.png`
- `../Screenshots/Troubleshooting/Identity-Access/11-Resource-Group-Reader-Write-Denied.png`
- `../Screenshots/Troubleshooting/Identity-Access/12-Reader-Tag-Modification-Denied.png`
- `../Screenshots/Resource-Groups/03-Resource-Group-Governance-Tags.png`

---

## Support Notes

Authorization errors should be evaluated in the context of the user's intended access level.

In this case, the error itself provided useful evidence that Azure RBAC was correctly enforcing the Reader role.

The appropriate support resolution was not to bypass the restriction but to confirm that:

- Read access worked.
- Write access was intentionally blocked.
- Administrative changes could still be performed by an authorized account.

---

## Resolution Summary

**Issue:** User could view the Azure resource group but could not modify locks or tags.

**Cause:** The user had the read-only Azure `Reader` role.

**Investigation:** Verified successful read access and reproduced denied write operations.

**Fix:** No privilege escalation was required; administrative changes were performed using the authorized administrator account.

**Result:** Least-privilege access was preserved and Azure RBAC behavior was verified.

**Status:** Resolved
