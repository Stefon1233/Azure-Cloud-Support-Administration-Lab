# Azure Storage

## Overview

This section documents the Azure Storage administration, security, data protection, and troubleshooting work completed in the Azure Cloud Support & Administration Lab.

The storage portion of the lab included hands-on configuration of an Azure Storage Account, Blob Storage containers, file uploads, private access, Microsoft Entra authentication, Azure RBAC, network-access restrictions, lifecycle management, soft delete, blob versioning, 
resource locks, and recovery operations.

Multiple controlled failures were introduced and investigated to demonstrate realistic cloud-support troubleshooting.

---

## Objectives Completed

The Azure Storage portion of the lab demonstrated:

- Azure Storage Account deployment
- Blob Storage administration
- Blob container creation
- Test-file upload
- Private container access
- Storage authentication
- Microsoft Entra authentication
- Azure RBAC
- Management-plane and data-plane permissions
- Storage network-access troubleshooting
- Lifecycle management
- Blob soft delete
- Container soft delete
- Blob versioning
- Resource locks
- Blob recovery
- Container recovery
- Least-privilege access
- Cloud troubleshooting
- Technical documentation

---

## Storage Environment

The primary storage account used throughout the lab was:

- **Storage Account:** `stitsupportlab002`
- **Resource Group:** `RG-IT-Support-Lab`
- **Region:** North Central US
- **Performance:** Standard
- **Redundancy:** Locally Redundant Storage (LRS)
- **Purpose:** Azure cloud-support administration and troubleshooting

Azure Storage account names must be globally unique and follow Azure naming requirements.

This requirement became part of the first storage troubleshooting scenario.

---

## Storage Account Deployment Troubleshooting

An initial storage-account deployment attempt failed because the requested storage account name was invalid or unavailable.

The Azure Portal validation messages were reviewed to identify the naming problem.

The storage account name was corrected to:

`stitsupportlab002`

The corrected deployment was then submitted successfully.

The completed deployment was verified through the Azure Portal.

This scenario demonstrated the importance of reviewing Azure validation messages before attempting unrelated configuration changes.

---

## Storage Deployment Evidence

The storage deployment troubleshooting process is documented with:

- `../Screenshots/Troubleshooting/Azure-Storage/01-Storage-Account-Invalid-Name-Error.png`
- `../Screenshots/Troubleshooting/Azure-Storage/02-Storage-Account-Validation-Failed.png`
- `../Screenshots/Troubleshooting/Azure-Storage/03-Storage-Account-Name-Corrected.png`
- `../Screenshots/Troubleshooting/Azure-Storage/04-Storage-Account-Deployment-Succeeded.png`
- `../Screenshots/Troubleshooting/Azure-Storage/05-Storage-Account-Deployment-Verified.png`

---

## Blob Storage

Azure Blob Storage was used for hands-on storage administration.

A private blob container was configured and test files were uploaded.

The environment was intentionally limited to non-sensitive test data.

The lab did not use production files, credentials, passwords, or confidential business information.

---

## Private Blob Container

A private Blob Storage container was created to demonstrate controlled cloud-storage access.

Private access was used so that anonymous users could not retrieve the stored objects.

This provided a foundation for testing authenticated access and Azure RBAC.

Evidence:

- `../Screenshots/Storage/01-Private-Blob-Container.png`

---

## Blob Upload

A non-sensitive test file was uploaded to Blob Storage.

This demonstrated basic Azure Storage administration and provided an object that could later be used for access-control testing.

Evidence:

- `../Screenshots/Storage/02-Blob-File-Upload.png`

---

## Private Access Verification

Anonymous/private-access behavior was tested.

The blob was not treated as a publicly accessible object.

This demonstrated the difference between:

- Public anonymous access
- Authenticated Azure access
- Authorized data access

Evidence:

- `../Screenshots/Storage/03-Private-Blob-Access-Denied.png`

---

## Authenticated Blob Access

Blob properties and authenticated access were reviewed through Azure.

The lab used authenticated Azure access rather than making the container public.

Evidence:

- `../Screenshots/Storage/04-Blob-Properties-Authenticated-Access.png`

---

## Authentication and Authorization

The storage lab distinguished between authentication and authorization.

**Authentication** determines who the user is.

**Authorization** determines what the authenticated identity is allowed to do.

A successful Microsoft Entra sign-in does not automatically provide access to Azure Storage data.

Access depends on:

- Identity
- Role assignment
- Role scope
- Data-plane permissions
- Management-plane permissions
- Network restrictions
- Authentication method

This distinction became especially important during the RBAC troubleshooting scenarios.

---

## Management Plane vs Data Plane

Azure Storage provided a practical demonstration of the difference between management-plane and data-plane permissions.

Management-plane permissions control operations such as:

- Viewing the storage account
- Reviewing configuration
- Accessing Azure resource information
- Managing Azure resource properties

Data-plane permissions control operations involving the stored data itself, such as:

- Reading blobs
- Uploading blobs
- Modifying blobs
- Deleting blobs

These permissions are not automatically equivalent.

---

## Storage Blob Data Reader

A test Microsoft Entra identity was assigned:

`Storage Blob Data Reader`

This role provided read-oriented Blob Storage data permissions.

However, the user initially could not properly navigate to the storage account through the Azure Portal because the data-plane role alone did not provide the necessary management-plane resource visibility.

This created a realistic RBAC troubleshooting scenario.

---

## Reader Role

To provide management-plane visibility without granting unnecessary modification rights, the standard Azure:

`Reader`

role was added.

The resulting access model provided:

- Reader for Azure resource visibility
- Storage Blob Data Reader for blob-data read access

This demonstrated how multiple narrowly scoped roles can be combined to meet a support requirement without granting broad administrative permissions.

---

## Least-Privilege Validation

After the Reader and Storage Blob Data Reader roles were configured, access was tested.

The test identity could read the blob.

An attempted upload/write operation was denied.

Azure returned an authorization error indicating that the request was not authorized to perform the operation using the available permission.

This was the expected result.

The goal was not to make every operation succeed.

The goal was to verify that the identity could perform the required read operation while unauthorized write operations remained blocked.

This demonstrated least privilege.

---

## RBAC Access Evidence

Relevant screenshots include:

- `../Screenshots/Troubleshooting/Identity-Access/06-RBAC-Reader-Assignment.png`
- `../Screenshots/Troubleshooting/Identity-Access/07-RBAC-Storage-Account-Not-Visible.png`
- `../Screenshots/Troubleshooting/Identity-Access/08-RBAC-Reader-And-Blob-Reader-Roles.png`
- `../Screenshots/Troubleshooting/Identity-Access/09-RBAC-Read-Allowed-Write-Denied.png`
- `../Screenshots/Troubleshooting/Identity-Access/10-RBAC-Blob-Read-Success.png`

---

## Storage Network Access Troubleshooting

A controlled storage-networking failure was also introduced.

Storage networking settings were modified to create a restrictive access condition.

The storage resource was then tested under the restricted configuration.

The resulting access problem was investigated as a network-access issue rather than immediately changing RBAC permissions.

This distinction is important because similar user-facing access errors can originate from different control layers.

---

## Network Access Investigation

The investigation reviewed:

- Storage account availability
- Network-access configuration
- Public network access
- Authentication
- Authorization
- Existing RBAC roles
- Error behavior

The restrictive network configuration was identified as the cause.

The configuration was corrected and storage access was restored.

---

## Storage Network Evidence

The scenario is documented with:

- `../Screenshots/Troubleshooting/Azure-Storage/06-Storage-Network-Access-Before.png`
- `../Screenshots/Troubleshooting/Azure-Storage/07-Storage-Network-Access-Failure.png`
- `../Screenshots/Troubleshooting/Azure-Storage/08-Storage-Network-Access-Restored.png`

---

## Lifecycle Management

Azure Storage lifecycle management was configured to demonstrate automated data-tier management.

A lifecycle rule named:

`Archive-Old-Support-Files`

was created.

The rule targeted:

- Block blobs
- Base blobs

The lifecycle actions included:

- Move blobs to the Cool tier after 30 days since last modification
- Move blobs to the Cold tier after 90 days since last modification

Automatic archive and deletion were not enabled.

This demonstrated how organizations can automate storage-tier transitions based on data age.

---

## Lifecycle Management Evidence

Relevant screenshots include:

- `../Screenshots/Storage/05-Lifecycle-Management-Rule-Configuration.png`
- `../Screenshots/Storage/06-Lifecycle-Management-Rule-Enabled.png`

---

## Data Protection

Azure Storage data-protection settings were configured to reduce the risk of accidental data loss.

The configuration included:

- Blob soft delete: 7 days
- Container soft delete: 7 days
- Blob versioning: Enabled
- Version cleanup period: 30 days

Point-in-time restore and change feed were not enabled for this lab.

Evidence:

- `../Screenshots/Storage/07-Storage-Data-Protection-Configuration.png`

---

## Resource Lock Protection

A resource lock was used to demonstrate protection against accidental Azure resource deletion.

The lock was named:

`Protect-Storage-Account`

The lock type was:

`Delete`

The lock notes documented its purpose as:

`Prevent accidental deletion of IT support lab storage resources`

The lock provided an additional governance control beyond ordinary RBAC permissions.

---

## Resource Lock Testing

The storage resource was tested while the Delete lock was active.

A deletion-related operation was intentionally attempted.

Azure blocked the operation because of the resource lock.

This demonstrated that successful authentication and sufficient RBAC permissions do not automatically override a resource lock.

Evidence:

- `../Screenshots/Troubleshooting/Azure-Storage/09-Storage-Resource-Lock.png`
- `../Screenshots/Troubleshooting/Azure-Storage/10-Resource-Lock-Deletion-Blocked.png`

---

## Blob Soft-Delete Recovery

A controlled blob-deletion and recovery scenario was performed.

The test blob was:

`Recovery-Test.txt`

The file was stored in the:

`rbac-test`

container.

The blob existed before the deletion test.

It was then intentionally deleted.

Because Blob soft delete was enabled, the deleted object remained recoverable during the configured retention period.

---

## Deleted Blob Detection

After deletion, the storage interface was used to display deleted blobs.

`Recovery-Test.txt` was detected as a soft-deleted object.

This demonstrated that deletion did not immediately result in permanent data loss.

---

## Blob Restoration

The deleted blob was restored using Azure's recovery capability.

After restoration, the blob was verified as available again.

This completed the controlled blob-recovery scenario.

---

## Blob Recovery Evidence

The recovery process is documented with:

- `../Screenshots/Troubleshooting/Azure-Storage/11-Blob-Before-Soft-Delete.png`
- `../Screenshots/Troubleshooting/Azure-Storage/12-Blob-Deleted-Soft-Delete-Test.png`
- `../Screenshots/Troubleshooting/Azure-Storage/13-Soft-Deleted-Blob-Detected.png`
- `../Screenshots/Troubleshooting/Azure-Storage/14-Soft-Deleted-Blob-Restored.png`

---

## Container Recovery Scenario

A separate controlled scenario was performed to test container soft delete.

A disposable test container was created:

`recovery-container-test`

The container included a non-sensitive test file:

`Container-Recovery-Test.txt`

The container was documented before deletion.

---

## Container Deletion Blocked

The first attempt to delete the container was blocked because the storage account still had the Delete resource lock.

This created a useful interaction between two Azure protection mechanisms:

1. Resource locks
2. Container soft delete

Before soft-delete recovery could be tested, the resource lock first had to be addressed.

Evidence:

- `../Screenshots/Troubleshooting/Azure-Storage/15-Container-Before-Deletion.png`
- `../Screenshots/Troubleshooting/Azure-Storage/16-Container-Deletion-Blocked-By-Resource-Lock.png`

---

## Controlled Lock Removal

The Delete lock was temporarily removed so the container-recovery scenario could proceed.

This was a controlled administrative action.

The lock was not removed because it was considered unnecessary.

It was temporarily removed because the lab specifically needed to test deletion and recovery behavior.

---

## Container Deletion

After the lock was removed, the test container was successfully deleted.

Evidence:

- `../Screenshots/Troubleshooting/Azure-Storage/17-Container-Deletion-Succeeded-After-Lock-Removal.png`

---

## Deleted Container Detection

Because container soft delete was enabled, the deleted container remained recoverable.

The deleted container was detected through the Azure Storage interface.

Evidence:

- `../Screenshots/Troubleshooting/Azure-Storage/18-Soft-Deleted-Container-Detected.png`

---

## Container Restoration

`recovery-container-test` was restored.

The successful restoration demonstrated the value of container soft delete as a data-protection control.

Evidence:

- `../Screenshots/Troubleshooting/Azure-Storage/19-Soft-Deleted-Container-Restored.png`

---

## Resource Lock Restoration

After completing the controlled deletion and recovery exercise, the Delete lock was restored.

This returned the storage environment to its protected state.

Evidence:

- `../Screenshots/Troubleshooting/Azure-Storage/20-Storage-Delete-Lock-Restored.png`

---

## Layered Protection

The storage portion of the lab demonstrated several different protection layers.

### Identity

Microsoft Entra ID determines the authenticated Azure identity.

### RBAC

Azure RBAC determines which management-plane and data-plane operations an identity is authorized to perform.

### Network Access

Storage networking controls whether the network path is permitted.

### Resource Locks

Resource locks protect Azure resources from accidental administrative deletion.

### Soft Delete

Soft delete provides recovery after supported deletion events.

### Versioning

Blob versioning helps preserve previous versions of stored objects.

### Lifecycle Management

Lifecycle rules automate storage-tier transitions.

These controls solve different problems and should not be treated as interchangeable.

---

## Storage Troubleshooting Methodology

When investigating Azure Storage access problems, the lab used a structured approach.

### 1. Confirm the Resource

Verify:

- Correct subscription
- Correct resource group
- Correct storage account
- Correct container
- Correct blob

### 2. Confirm Identity

Determine which identity is attempting access.

### 3. Review Authentication

Determine how the user is authenticating.

Examples include:

- Microsoft Entra ID
- Storage account key
- Other supported Azure Storage authentication methods

### 4. Review RBAC

Check:

- Assigned roles
- Role scope
- Management-plane permissions
- Data-plane permissions

### 5. Review Network Access

Check whether storage networking restrictions affect access.

### 6. Review Resource Locks

If a management operation fails, determine whether a resource lock is involved.

### 7. Review Data Protection

If data was deleted, determine whether:

- Blob soft delete
- Container soft delete
- Versioning

can be used for recovery.

### 8. Read the Azure Error

Azure error messages should be used to narrow the troubleshooting scope before unrelated settings are changed.

### 9. Apply the Smallest Corrective Action

Use least privilege and avoid granting broad permissions simply to make an error disappear.

### 10. Retest

Verify both:

- Required operations succeed
- Unauthorized operations remain blocked

---

## Security Considerations

The storage lab followed several security principles:

- Private Blob Storage
- Authenticated access
- Least-privilege RBAC
- Separate management-plane and data-plane roles
- Network-access controls
- Resource locks
- Soft-delete protection
- Blob versioning
- Non-sensitive test data
- No public credentials
- No production data

Screenshots intended for GitHub should be reviewed for sensitive Azure identifiers before publication.

---

## Screenshot Privacy

Before publishing Azure Portal screenshots, sensitive information should be obscured where necessary.

Examples include:

- User email addresses
- Subscription IDs
- Tenant IDs
- Object IDs
- Account identifiers
- Access keys
- SAS tokens
- Correlation IDs
- Request IDs

No storage access keys or credentials should be published in the repository.

---

## Completed Storage Screenshots

### Core Storage

- `../Screenshots/Storage/01-Private-Blob-Container.png`
- `../Screenshots/Storage/02-Blob-File-Upload.png`
- `../Screenshots/Storage/03-Private-Blob-Access-Denied.png`
- `../Screenshots/Storage/04-Blob-Properties-Authenticated-Access.png`
- `../Screenshots/Storage/05-Lifecycle-Management-Rule-Configuration.png`
- `../Screenshots/Storage/06-Lifecycle-Management-Rule-Enabled.png`
- `../Screenshots/Storage/07-Storage-Data-Protection-Configuration.png`

### Storage Troubleshooting

- `../Screenshots/Troubleshooting/Azure-Storage/01-Storage-Account-Invalid-Name-Error.png`
- `../Screenshots/Troubleshooting/Azure-Storage/02-Storage-Account-Validation-Failed.png`
- `../Screenshots/Troubleshooting/Azure-Storage/03-Storage-Account-Name-Corrected.png`
- `../Screenshots/Troubleshooting/Azure-Storage/04-Storage-Account-Deployment-Succeeded.png`
- `../Screenshots/Troubleshooting/Azure-Storage/05-Storage-Account-Deployment-Verified.png`
- `../Screenshots/Troubleshooting/Azure-Storage/06-Storage-Network-Access-Before.png`
- `../Screenshots/Troubleshooting/Azure-Storage/07-Storage-Network-Access-Failure.png`
- `../Screenshots/Troubleshooting/Azure-Storage/08-Storage-Network-Access-Restored.png`
- `../Screenshots/Troubleshooting/Azure-Storage/09-Storage-Resource-Lock.png`
- `../Screenshots/Troubleshooting/Azure-Storage/10-Resource-Lock-Deletion-Blocked.png`
- `../Screenshots/Troubleshooting/Azure-Storage/11-Blob-Before-Soft-Delete.png`
- `../Screenshots/Troubleshooting/Azure-Storage/12-Blob-Deleted-Soft-Delete-Test.png`
- `../Screenshots/Troubleshooting/Azure-Storage/13-Soft-Deleted-Blob-Detected.png`
- `../Screenshots/Troubleshooting/Azure-Storage/14-Soft-Deleted-Blob-Restored.png`
- `../Screenshots/Troubleshooting/Azure-Storage/15-Container-Before-Deletion.png`
- `../Screenshots/Troubleshooting/Azure-Storage/16-Container-Deletion-Blocked-By-Resource-Lock.png`
- `../Screenshots/Troubleshooting/Azure-Storage/17-Container-Deletion-Succeeded-After-Lock-Removal.png`
- `../Screenshots/Troubleshooting/Azure-Storage/18-Soft-Deleted-Container-Detected.png`
- `../Screenshots/Troubleshooting/Azure-Storage/19-Soft-Deleted-Container-Restored.png`
- `../Screenshots/Troubleshooting/Azure-Storage/20-Storage-Delete-Lock-Restored.png`

---

## Related Help-Desk Tickets

Storage-related incidents are documented in:

- `../Help-Desk-Tickets/Ticket-001-Blob-Storage-Access-Denied.md`
- `../Help-Desk-Tickets/Ticket-004-RBAC-Resource-Visibility-Issue.md`
- `../Help-Desk-Tickets/Ticket-005-Storage-Network-Access-Failure.md`
- `../Help-Desk-Tickets/Ticket-006-Resource-Lock-Preventing-Deletion.md`
- `../Help-Desk-Tickets/Ticket-007-Azure-Blob-Soft-Delete-Recovery.md`

These tickets document separate troubleshooting layers rather than treating every storage-access problem as an RBAC issue.

---

## Skills Demonstrated

- Microsoft Azure
- Azure Storage
- Azure Blob Storage
- Storage accounts
- Blob containers
- Microsoft Entra authentication
- Azure RBAC
- Management-plane permissions
- Data-plane permissions
- Least privilege
- Storage networking
- Resource locks
- Lifecycle management
- Blob soft delete
- Container soft delete
- Blob versioning
- Data recovery
- Root-cause analysis
- Cloud troubleshooting
- Technical documentation

---

## Outcome

The Azure Storage portion of the lab progressed from basic storage deployment into a multi-layer cloud-support environment.

The completed work demonstrated storage deployment, private blob access, authenticated access, least-privilege RBAC, network-access troubleshooting, lifecycle management, data-protection controls, resource-lock behavior, blob recovery, and container recovery.

Controlled failures were intentionally introduced and resolved to demonstrate troubleshooting rather than only successful configuration.

The resulting environment provides practical evidence of Azure Storage administration, security, recovery, and cloud-support skills.
