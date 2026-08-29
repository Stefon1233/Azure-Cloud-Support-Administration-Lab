# Microsoft Entra ID and Azure RBAC

## Overview

This section documents the identity, authorization, Azure Role-Based Access Control (RBAC), and least-privilege testing completed in the Azure Cloud Support & Administration Lab.

The identity portion of the lab focused on practical Azure support scenarios involving Microsoft Entra ID identities, Azure RBAC role assignments, role scope, management-plane permissions, data-plane permissions, resource visibility, storage access, and denied 
administrative operations.

Controlled access failures were intentionally reproduced so that permissions could be investigated and corrected without granting unnecessary administrative access.

The completed scenarios demonstrate an important Azure support principle:

Successful authentication does not automatically mean that a user is authorized to perform every operation on an Azure resource.

---

## Objectives Completed

The identity and RBAC portion of the lab demonstrated:

- Microsoft Entra ID identity testing
- Azure RBAC administration
- Existing role-assignment review
- Storage Blob Data Reader assignment
- Reader role assignment
- Resource-group scoped RBAC
- Storage-account scoped access
- Role-scope analysis
- Management-plane permissions
- Data-plane permissions
- Least-privilege access
- Resource visibility troubleshooting
- Blob access troubleshooting
- Read-versus-write permission testing
- Resource-group write-denial testing
- Tag modification denial
- Access verification
- RBAC troubleshooting methodology
- Technical documentation

---

## Identity and Authorization Model

Azure access involves multiple layers.

A technician troubleshooting an access problem should determine which layer is responsible before changing permissions.

The major layers demonstrated in this lab included:

1. Authentication
2. Authorization
3. Role assignment
4. Role definition
5. Role scope
6. Management-plane access
7. Data-plane access
8. Network access
9. Resource locks

These controls perform different functions and should not be treated as interchangeable.

---

## Microsoft Entra ID

Microsoft Entra ID provided the identity layer for Azure access testing.

A test identity was used to reproduce user-access scenarios without modifying the permissions of the primary administrative account.

The test identity was used to evaluate:

- Azure resource visibility
- Blob Storage access
- Reader permissions
- Storage Blob Data Reader permissions
- Resource-group access
- Write restrictions
- Tag modification restrictions
- Least-privilege behavior

Sensitive identity information should be obscured before screenshots are published to GitHub.

---

## Authentication

Authentication verifies the identity attempting to access Azure.

In this lab, Microsoft Entra authentication was used when testing the permissions of the test identity.

Successful authentication confirmed who the user was.

It did not determine whether the user could:

- View a resource
- Read blob data
- Upload blob data
- Modify tags
- Change Azure configuration
- Delete resources
- Modify resource locks

Those actions depend on authorization.

---

## Authorization

Authorization determines what an authenticated identity is allowed to do.

Azure RBAC was used to control authorization.

Authorization decisions depend on factors including:

- Assigned role
- Role definition
- Assignment scope
- Resource type
- Requested operation
- Management-plane permissions
- Data-plane permissions

This distinction became central to several troubleshooting scenarios.

---

## Azure Role-Based Access Control

Azure RBAC provides access management for Azure resources.

An Azure role assignment connects three primary components:

- Security principal
- Role definition
- Scope

The security principal identifies who receives access.

The role definition determines what operations are allowed.

The scope determines where those permissions apply.

---

## Security Principal

The security principal can represent an Azure identity such as:

- User
- Group
- Service principal
- Managed identity

A test Microsoft Entra user was used for the hands-on RBAC scenarios in this lab.

---

## Role Definition

The role definition specifies the permissions granted by the assignment.

Built-in Azure roles were used instead of creating unnecessarily broad custom permissions.

Important roles demonstrated during the lab included:

- Reader
- Storage Blob Data Reader

These roles were selected because they provided different types of access.

---

## Scope

Azure RBAC permissions can be assigned at different scopes.

Common Azure scopes include:

- Management group
- Subscription
- Resource group
- Individual resource

Permissions assigned at a higher scope may be inherited by resources beneath that scope.

The lab demonstrated assignments at both resource and resource-group levels.

---

## Existing Role Assignment Review

Existing Azure role assignments were reviewed before adding new access.

This is an important troubleshooting step because adding another role without understanding existing permissions can:

- Create excessive access
- Make troubleshooting more difficult
- Hide the original cause
- Violate least-privilege principles

Evidence:

`../Screenshots/Identity/01-RBAC-Existing-Role-Assignment.png`

---

## Storage Blob Data Reader Assignment

The test identity was assigned:

`Storage Blob Data Reader`

This role was selected to provide read access to Azure Blob Storage data without granting unnecessary write permissions.

Evidence:

`../Screenshots/Identity/02-RBAC-Blob-Data-Reader-Assignment.png`

The role allowed the lab to test data-plane access separately from management-plane access.

---

## Management Plane and Data Plane

One of the most important RBAC concepts demonstrated in the lab was the difference between Azure management-plane and data-plane permissions.

### Management Plane

Management-plane operations relate to the Azure resource itself.

Examples include:

- Viewing a storage account
- Viewing resource properties
- Viewing resource configuration
- Reviewing Azure resource information

### Data Plane

Data-plane operations interact with the data stored inside the service.

For Blob Storage, examples include:

- Reading blobs
- Uploading blobs
- Modifying blobs
- Deleting blobs

A user can have data-plane permissions without having sufficient management-plane permissions to navigate or view the Azure resource through the Portal.

---

## Resource Visibility Troubleshooting Scenario

A practical RBAC issue was reproduced using the test identity.

The user had:

`Storage Blob Data Reader`

but the storage account was not properly visible through the expected Azure Portal workflow.

This initially appeared to be a storage-access problem.

Further investigation showed that the user had data-plane permissions but lacked sufficient management-plane visibility.

---

## Investigation

The troubleshooting process reviewed:

1. The affected identity
2. The storage account
3. Existing role assignments
4. Role scope
5. Storage Blob Data Reader permissions
6. Azure resource visibility
7. Management-plane requirements

The investigation showed that Storage Blob Data Reader alone did not provide the management-plane visibility needed for the intended Portal workflow.

Evidence:

`../Screenshots/Troubleshooting/Identity-Access/07-RBAC-Storage-Account-Not-Visible.png`

---

## Reader Role Assignment

The built-in Azure:

`Reader`

role was added to provide management-plane read visibility.

Reader allows a user to view Azure resources without granting permission to modify them.

This made it appropriate for the support scenario.

Evidence:

`../Screenshots/Troubleshooting/Identity-Access/06-RBAC-Reader-Assignment.png`

---

## Combined Least-Privilege Model

The final access configuration used:

- `Reader`
- `Storage Blob Data Reader`

The two roles provided separate capabilities.

Reader provided management-plane resource visibility.

Storage Blob Data Reader provided Blob Storage data read access.

Evidence:

`../Screenshots/Troubleshooting/Identity-Access/08-RBAC-Reader-And-Blob-Reader-Roles.png`

This demonstrated that Azure support issues sometimes require understanding multiple permission layers rather than simply assigning a more powerful role.

---

## Access Verification

After the role configuration was corrected, the test identity was used to verify the resulting permissions.

The verification focused on two questions:

1. Can the user perform the required operation?
2. Are operations outside the user's responsibility still blocked?

Both are necessary when validating least privilege.

---

## Successful Blob Read

The test identity successfully accessed the required blob data.

This confirmed that the Storage Blob Data Reader role provided the intended data-plane read access.

Evidence:

`../Screenshots/Troubleshooting/Identity-Access/10-RBAC-Blob-Read-Success.png`

---

## Write Operation Denied

A write/upload operation was then attempted.

Azure denied the operation.

The authorization error indicated that the request was not authorized to perform the requested operation using the available permissions.

Evidence:

`../Screenshots/Troubleshooting/Identity-Access/09-RBAC-Read-Allowed-Write-Denied.png`

This was an expected security result.

The denied operation was not treated as an unresolved problem.

It confirmed that the identity had read access without unnecessary write access.

---

## Least Privilege

Least privilege means granting only the permissions required to perform an assigned task.

The goal of troubleshooting is not to make every Azure operation succeed.

The goal is to provide the required access while preserving appropriate restrictions.

The final storage RBAC configuration demonstrated this principle:

- Required resource visibility: Allowed
- Required blob read access: Allowed
- Unnecessary blob write access: Denied

A broader role was not assigned merely to eliminate the authorization error.

---

## Resource Group RBAC Scenario

RBAC testing was also performed at the resource-group level.

The test identity was assigned the built-in:

`Reader`

role at:

`RG-IT-Support-Lab`

This provided an additional opportunity to validate read-only Azure administration.

---

## Resource Group Before Assignment

The resource-group IAM configuration was reviewed before the Reader assignment.

This established the starting state for the scenario.

Evidence:

`../Screenshots/Identity/03-Resource-Group-RBAC-Before-Assignment.png`

---

## Reader Role Assigned

The Reader role was assigned to the test identity at the resource-group scope.

Evidence:

`../Screenshots/Identity/04-Resource-Group-Reader-Role-Assigned.png`

Because the role was assigned at the resource-group level, the test identity received applicable read permissions for resources within that scope.

---

## Reader Access Verified

The role assignment was verified after configuration.

Evidence:

`../Screenshots/Identity/05-Resource-Group-Reader-Access-Verified.png`

This confirmed that the intended read-oriented access was available.

---

## Read-Only Access Testing

Simply confirming that a role appears in IAM is not enough to fully validate access.

The lab therefore tested operations that Reader should not be allowed to perform.

This provided evidence that the permission boundary was working as intended.

---

## Resource Lock Modification Restriction

The test identity attempted to interact with resource-lock administration.

Azure indicated that the identity did not have permission to edit the locks.

Evidence:

`../Screenshots/Troubleshooting/Identity-Access/11-Resource-Group-Reader-Write-Denied.png`

This was expected behavior for a Reader assignment.

The result demonstrated that read visibility did not provide administrative modification rights.

---

## Tag Modification Denied

Another write-oriented operation was tested by attempting to modify resource-group tags.

Azure returned an authorization failure.

Evidence:

`../Screenshots/Troubleshooting/Identity-Access/12-Reader-Tag-Modification-Denied.png`

This further validated the Reader permission boundary.

The identity could view the resource group but could not make unauthorized configuration changes.

---

## Resource Group Governance Tags

The administrative account configured governance tags on the resource group.

The tags included:

- `Environment = Lab`
- `Department = IT`
- `Purpose = Cloud-Support-Training`
- `Owner = IT-Support`

Evidence:

`../Screenshots/Resource-Groups/03-Resource-Group-Governance-Tags.png`

These tags demonstrated basic Azure resource organization and governance.

The Reader identity could view applicable resource information but was not granted permission to modify the tags.

---

## Controlled Permission Testing

The identity portion of the lab intentionally tested both successful and unsuccessful operations.

Successful tests demonstrated required access.

Denied tests demonstrated security boundaries.

This distinction is important when documenting Azure support work.

A denied operation can be successful verification when the assigned role is intentionally read-only.

---

## Storage Access Issue

A separate storage-access scenario was used to investigate an authorization problem involving Azure Blob Storage.

The investigation reviewed:

- Identity
- Role assignment
- Role scope
- Storage permissions
- Authentication method
- Required operation

Evidence:

`../Screenshots/Troubleshooting/Identity-Access/01-Storage-Access-Issue.png`

---

## RBAC Permission Investigation

Azure IAM and role assignments were reviewed to determine whether the affected identity had the required permissions.

Evidence:

`../Screenshots/Troubleshooting/Identity-Access/02-RBAC-Permissions-Investigation.png`

This demonstrated the importance of inspecting the actual role assignment rather than assuming a successful Azure sign-in means storage access should work.

---

## Microsoft Entra Blob Permission Denial

The access problem was reproduced while using Microsoft Entra authentication.

The identity encountered a permission-related failure.

Evidence:

`../Screenshots/Troubleshooting/Identity-Access/03-Entra-Blob-Access-Permission-Denied.png`

This helped isolate the problem to authorization rather than basic authentication.

---

## Storage Blob Data Reader Remediation

The appropriate least-privilege data role was assigned:

`Storage Blob Data Reader`

Evidence:

`../Screenshots/Troubleshooting/Identity-Access/04-Storage-Blob-Data-Reader-Role-Assigned.png`

The goal was to provide the required read access rather than broad storage administration.

---

## Storage Access Restored

After the correct role assignment was applied and access was retested, the required Blob Storage access was restored.

Evidence:

`../Screenshots/Troubleshooting/Identity-Access/05-Storage-Blob-Access-Restored.png`

This completed the original Blob Storage access-denied troubleshooting scenario.

---

## RBAC Troubleshooting Methodology

A structured RBAC troubleshooting workflow was used throughout the lab.

### 1. Identify the User

Confirm the exact identity experiencing the problem.

Do not troubleshoot permissions using assumptions about which account is signed in.

### 2. Identify the Resource

Confirm:

- Subscription
- Resource group
- Resource
- Container or data object where applicable

### 3. Identify the Required Operation

Determine exactly what the user needs to do.

Examples include:

- View resource
- Read blob
- Upload blob
- Modify configuration
- Edit tags
- Delete resource

The required operation determines the permissions that should be investigated.

### 4. Review Existing Role Assignments

Check Azure IAM before adding permissions.

Review:

- Role name
- Assigned identity
- Scope
- Inheritance

### 5. Determine the Permission Plane

Determine whether the required operation is:

- Management plane
- Data plane

This is especially important for Azure Storage.

### 6. Review Scope

Verify whether the role applies at the correct scope.

Possible scopes include:

- Subscription
- Resource group
- Resource

### 7. Reproduce the Error

Where safe, reproduce the access problem.

Record the Azure error behavior.

### 8. Apply Least Privilege

Select the smallest appropriate role that satisfies the support requirement.

Avoid granting Contributor, Owner, or other broad roles when a narrower role is sufficient.

### 9. Retest Required Access

Confirm the required operation now works.

### 10. Test the Security Boundary

Where appropriate, verify that unauthorized operations remain blocked.

This provides stronger evidence of correct RBAC configuration.

---

## Common RBAC Troubleshooting Questions

When investigating an Azure permissions issue, useful questions include:

- Which identity is affected?
- Is the identity authenticated successfully?
- Which Azure resource is affected?
- What exact operation is failing?
- Which roles are already assigned?
- At what scope are they assigned?
- Is the required permission management plane or data plane?
- Is the assignment inherited?
- Is there an explicit network restriction?
- Is a resource lock affecting the operation?
- Is the user attempting a write operation with a read-only role?
- Has the role assignment had time to propagate?

These questions help narrow the problem before permissions are changed.

---

## RBAC vs Network Access

RBAC and networking solve different security problems.

RBAC determines whether an identity is authorized to perform an operation.

Network controls determine whether the request can reach the service through the permitted network path.

A user can therefore have correct RBAC permissions and still encounter a network-access failure.

Likewise, an open network path does not grant authorization.

The lab demonstrated both RBAC and storage-networking failures so that these causes could be investigated independently.

---

## RBAC vs Resource Locks

RBAC and resource locks also perform different functions.

RBAC determines what an identity is authorized to do.

Resource locks protect Azure resources from specific administrative changes such as deletion.

A user with significant Azure permissions may still encounter an operation blocked by a resource lock.

The storage portion of the lab demonstrated this behavior through a Delete lock.

---

## RBAC vs Azure Policy

Azure Policy and RBAC serve different purposes.

RBAC controls who can perform actions.

Azure Policy evaluates or enforces resource configuration requirements.

The lab separately configured Azure Policy to demonstrate governance.

Permissions problems should not automatically be treated as policy problems, and policy compliance problems should not automatically be treated as RBAC problems.

---

## Role Assignment Security Principles

The following principles were applied during the lab:

- Review existing access before adding roles
- Use built-in roles when appropriate
- Prefer narrow roles over broad administrative access
- Assign permissions at the smallest reasonable scope
- Separate management-plane and data-plane requirements
- Verify required operations
- Verify unauthorized operations remain blocked
- Remove temporary access when no longer required
- Document role changes
- Protect identity information in screenshots

---

## Roles Not Used as Shortcuts

Broad Azure roles should not be assigned simply to resolve an access error quickly.

Examples of powerful roles include:

- Owner
- Contributor
- User Access Administrator

These roles can provide substantially more access than a read-only support requirement needs.

The completed lab demonstrated that combining:

`Reader`

with:

`Storage Blob Data Reader`

could satisfy the tested visibility and blob-read requirements without granting unnecessary write access.

---

## Role Propagation

Azure role assignments may require time to propagate.

When validating a new role assignment, a technician should account for possible propagation delay before concluding that the assignment failed.

Repeatedly adding broader roles during a propagation delay can create excessive access.

The safer approach is to:

1. Verify the assignment
2. Verify the scope
3. Allow reasonable propagation time
4. Refresh or reauthenticate where appropriate
5. Retest

---

## Evidence Collection

RBAC troubleshooting evidence should capture enough information to demonstrate:

- The affected resource
- Relevant role assignment
- Assignment scope
- Access failure
- Corrective action
- Successful required access
- Expected denied access where applicable

Sensitive identifiers should be obscured before public publication.

---

## Screenshot Privacy

Azure identity screenshots can expose sensitive information.

Before publishing screenshots to GitHub, review them for:

- Email addresses
- User principal names
- Subscription IDs
- Tenant IDs
- Object IDs
- Principal IDs
- Account identifiers
- IP addresses
- Correlation IDs
- Request IDs

Credentials, access tokens, passwords, access keys, and other secrets must never be published.

---

## Identity Screenshot Evidence

Core RBAC screenshots include:

- `../Screenshots/Identity/01-RBAC-Existing-Role-Assignment.png`
- `../Screenshots/Identity/02-RBAC-Blob-Data-Reader-Assignment.png`
- `../Screenshots/Identity/03-Resource-Group-RBAC-Before-Assignment.png`
- `../Screenshots/Identity/04-Resource-Group-Reader-Role-Assigned.png`
- `../Screenshots/Identity/05-Resource-Group-Reader-Access-Verified.png`

---

## Identity and Access Troubleshooting Evidence

Additional troubleshooting screenshots include:

- `../Screenshots/Troubleshooting/Identity-Access/01-Storage-Access-Issue.png`
- `../Screenshots/Troubleshooting/Identity-Access/02-RBAC-Permissions-Investigation.png`
- `../Screenshots/Troubleshooting/Identity-Access/03-Entra-Blob-Access-Permission-Denied.png`
- `../Screenshots/Troubleshooting/Identity-Access/04-Storage-Blob-Data-Reader-Role-Assigned.png`
- `../Screenshots/Troubleshooting/Identity-Access/05-Storage-Blob-Access-Restored.png`
- `../Screenshots/Troubleshooting/Identity-Access/06-RBAC-Reader-Assignment.png`
- `../Screenshots/Troubleshooting/Identity-Access/07-RBAC-Storage-Account-Not-Visible.png`
- `../Screenshots/Troubleshooting/Identity-Access/08-RBAC-Reader-And-Blob-Reader-Roles.png`
- `../Screenshots/Troubleshooting/Identity-Access/09-RBAC-Read-Allowed-Write-Denied.png`
- `../Screenshots/Troubleshooting/Identity-Access/10-RBAC-Blob-Read-Success.png`
- `../Screenshots/Troubleshooting/Identity-Access/11-Resource-Group-Reader-Write-Denied.png`
- `../Screenshots/Troubleshooting/Identity-Access/12-Reader-Tag-Modification-Denied.png`

---

## Related Help-Desk Tickets

The identity and RBAC work is supported by several completed help-desk tickets.

### Ticket 001

`../Help-Desk-Tickets/Ticket-001-Blob-Storage-Access-Denied.md`

Documents a Blob Storage access-denied scenario and RBAC remediation.

### Ticket 004

`../Help-Desk-Tickets/Ticket-004-RBAC-Resource-Visibility-Issue.md`

Documents the difference between Blob Storage data access and Azure resource visibility.

### Ticket 008

`../Help-Desk-Tickets/Ticket-008-Resource-Group-Reader-Write-Denied.md`

Documents expected write denial while using the Reader role at resource-group scope.

---

## Support Scenario Summary

The completed RBAC scenarios demonstrated several distinct access problems.

### Scenario 1 — Blob Access Denied

**Problem:** Authenticated user lacked required Blob Storage data permissions.

**Investigation:** Azure IAM and data access were reviewed.

**Resolution:** Storage Blob Data Reader was assigned.

**Verification:** Required blob access was restored.

---

### Scenario 2 — Storage Account Not Visible

**Problem:** User had Blob data permissions but insufficient management-plane visibility.

**Investigation:** Existing roles and permission planes were reviewed.

**Resolution:** Reader was added.

**Verification:** Resource visibility and blob read access were available.

---

### Scenario 3 — Blob Write Denied

**Problem:** Test identity could read but could not upload/write.

**Investigation:** Assigned roles were reviewed.

**Finding:** The identity intentionally had read-only permissions.

**Resolution:** No additional permissions were required.

**Verification:** Read succeeded and write remained denied.

This was correct least-privilege behavior.

---

### Scenario 4 — Resource Group Write Denied

**Problem:** Reader identity could view the resource group but could not perform administrative changes.

**Investigation:** Reader permissions were reviewed.

**Finding:** Reader is intentionally read-only.

**Resolution:** No additional role was assigned.

**Verification:** Read access remained available while write operations remained denied.

This was also correct least-privilege behavior.

---

## Skills Demonstrated

- Microsoft Azure
- Microsoft Entra ID
- Azure RBAC
- Identity and access management
- Role assignments
- Role scope
- Reader role
- Storage Blob Data Reader
- Management-plane permissions
- Data-plane permissions
- Azure Storage authorization
- Least privilege
- Resource-group access control
- Access-denied troubleshooting
- Resource visibility troubleshooting
- Permission verification
- Root-cause analysis
- Cloud security
- Technical documentation
- Help-desk troubleshooting

---

## Outcome

The identity and RBAC portion of the Azure Cloud Support & Administration Lab demonstrated practical Azure access-management troubleshooting rather than simply assigning broad administrative permissions.

The lab reproduced multiple access conditions, investigated Azure role assignments and scopes, distinguished management-plane access from data-plane access, corrected missing permissions using built-in roles, and verified least-privilege boundaries through both 
successful and denied operations.

The completed scenarios demonstrated that:

- Authentication and authorization are separate
- Management-plane and data-plane permissions are separate
- Role scope matters
- Resource visibility does not automatically provide data access
- Data access does not automatically provide resource-management visibility
- Reader access does not provide write access
- Denied operations can be evidence of correctly configured least privilege
- Troubleshooting should identify the required operation before permissions are changed

The resulting configuration provides portfolio evidence of Microsoft Entra ID, Azure RBAC, least-privilege access control, and cloud-support troubleshooting.
