# Ticket 007 - Azure Blob Soft-Delete Recovery

## Ticket Summary

**Category:** Azure Storage / Data Recovery  
**Service:** Azure Blob Storage  
**Priority:** Medium  
**Status:** Resolved  

A blob was intentionally deleted from an Azure Storage container to simulate an accidental file deletion incident. Azure Blob soft delete had already been configured with a seven-day retention period, allowing the deleted object to be identified and restored without 
recreating the file from an external backup.

---

## User Report

A user reported that a file stored in an Azure Blob Storage container had been deleted and needed to be recovered.

The objective was to determine whether Azure's configured data-protection features could restore the deleted object.

---

## Environment

- Microsoft Azure
- Azure Storage
- Azure Blob Storage
- Azure Storage Data Protection
- Resource Group: `RG-IT-Support-Lab`
- Storage Account: `stitsupportlab002`
- Container: `rbac-test`
- Recovery Test File: `Recovery-Test.txt`

---

## Data Protection Configuration

Before performing the recovery test, I reviewed the Azure Storage account's Data protection settings.

The environment had the following protection enabled:

- Soft delete for blobs
- Blob soft-delete retention: 7 days
- Soft delete for containers
- Container soft-delete retention: 7 days
- Blob versioning
- Automatic deletion of previous blob versions after 30 days

These controls provided multiple layers of protection against accidental deletion and unwanted data changes.

---

## Initial State

The `rbac-test` container contained the recovery test file:

`Recovery-Test.txt`

The blob was confirmed to exist before beginning the deletion test.

This established a known-good state before reproducing the incident.

---

## Incident Simulation

I intentionally deleted `Recovery-Test.txt` from the blob container.

The deletion simulated a common cloud-support scenario in which a user accidentally removes a required file from Azure Storage.

Because blob soft delete was enabled, Azure retained the deleted blob rather than immediately removing the underlying data permanently.

---

## Investigation

After the deletion, I reviewed the container and enabled the option to display deleted blobs.

The deleted `Recovery-Test.txt` object became visible as a soft-deleted blob.

This confirmed that:

1. The file had been deleted.
2. Azure Storage soft delete had captured the deletion.
3. The file was still within its configured retention period.
4. Recovery was possible without an external backup.

---

## Root Cause

The missing file was caused by a deletion operation rather than:

- An Azure RBAC access problem
- A storage networking failure
- A service outage
- A synchronization issue
- Permanent data loss

Azure Storage was operating normally.

The configured soft-delete protection was functioning as intended.

---

## Resolution

I selected the deleted `Recovery-Test.txt` blob and used Azure's **Undelete** functionality.

Azure restored the soft-deleted object to the container.

No file re-upload or external backup restoration was required.

---

## Verification

After performing the recovery:

1. `Recovery-Test.txt` was restored.
2. The blob was again available from the container.
3. Azure displayed confirmation that the undelete operation succeeded.
4. The storage account remained operational.
5. Existing data-protection settings remained enabled.

The incident was considered resolved after the restored blob was verified.

---

## Troubleshooting Process

The recovery workflow followed these steps:

1. Confirm the reported file was missing.
2. Verify the Azure Storage account and container were available.
3. Review Data protection configuration.
4. Confirm blob soft delete was enabled.
5. Display deleted blobs in the affected container.
6. Locate `Recovery-Test.txt`.
7. Confirm the object was still within the retention period.
8. Perform the Undelete operation.
9. Verify that the blob was restored.

---

## Data Protection Significance

Soft delete provides a recovery window after a blob is deleted.

Without soft delete or another backup/recovery mechanism, accidental deletion could result in permanent data loss.

For support personnel, checking Azure Storage data-protection settings should therefore be an early troubleshooting step when investigating missing blob data.

---

## Additional Recovery Testing

The lab also included a separate container-level recovery scenario.

A disposable container named `recovery-container-test` was created and populated with a test file.

The container was then deleted after temporarily removing the storage account's Delete management lock.

Azure container soft delete retained the deleted container, allowing it to be detected and restored.

After recovery was completed, the Delete management lock was restored.

This demonstrated protection at both the individual blob level and container level.

---

## Security and Operational Considerations

In a production environment, recovery procedures should include:

- Confirming the deletion was accidental.
- Identifying the affected storage account and container.
- Reviewing the configured retention period.
- Avoiding unnecessary permission changes.
- Recovering only the required data.
- Verifying restored content.
- Documenting the recovery operation.

Retention periods should be selected according to organizational recovery requirements and data-governance policies.

---

## Screenshots

Blob recovery evidence:

- `../Screenshots/Troubleshooting/Azure-Storage/11-Blob-Before-Soft-Delete.png`
- `../Screenshots/Troubleshooting/Azure-Storage/12-Blob-Deleted-Soft-Delete-Test.png`
- `../Screenshots/Troubleshooting/Azure-Storage/13-Soft-Deleted-Blob-Detected.png`
- `../Screenshots/Troubleshooting/Azure-Storage/14-Soft-Deleted-Blob-Restored.png`

Additional container recovery evidence:

- `../Screenshots/Troubleshooting/Azure-Storage/15-Container-Before-Deletion.png`
- `../Screenshots/Troubleshooting/Azure-Storage/18-Soft-Deleted-Container-Detected.png`
- `../Screenshots/Troubleshooting/Azure-Storage/19-Soft-Deleted-Container-Restored.png`
- `../Screenshots/Troubleshooting/Azure-Storage/20-Storage-Delete-Lock-Restored.png`

---

## Support Notes

This scenario demonstrates that a deleted cloud object should not automatically be treated as permanently lost.

Azure support personnel should determine which recovery controls were configured before the deletion occurred.

For Azure Blob Storage, relevant protections can include:

- Blob soft delete
- Container soft delete
- Blob versioning
- Backup and recovery solutions

The recovery method should be selected based on the affected object and the available protection configuration.

---

## Resolution Summary

**Issue:** A blob was deleted from Azure Storage.

**Cause:** A deletion operation removed `Recovery-Test.txt` from the active container view.

**Protection:** Azure Blob soft delete retained the deleted object for seven days.

**Fix:** Located the soft-deleted blob and performed an Undelete operation.

**Result:** `Recovery-Test.txt` was successfully restored without requiring an external backup.

**Status:** Resolved
