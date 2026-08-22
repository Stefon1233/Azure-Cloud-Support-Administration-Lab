# Azure Storage

## Overview

This section documents the planned Azure Storage configuration and support 
scenarios for the Azure Cloud Support & Administration Lab.

Azure Storage will be used to demonstrate cloud storage administration, 
access management, permissions, file operations, and troubleshooting of 
storage-access issues.

## Objectives

- Create an Azure Storage Account
- Review Azure storage services
- Create a test storage resource
- Upload non-sensitive test data
- Configure access
- Review storage permissions
- Understand storage authentication
- Troubleshoot access-denied errors
- Validate restored access

## Planned Storage Account

- **Name:** To be determined
- **Resource Group:** RG-IT-Support-Lab
- **Region:** To be determined
- **Performance Tier:** To be determined
- **Redundancy:** To be determined
- **Purpose:** IT support lab storage testing

The final storage account name will be recorded after Azure accepts an 
available globally unique name.

## Storage Services

The lab may explore:

- Blob Storage
- Containers
- Azure Files
- File shares

The exact services used will depend on availability, cost, and lab 
requirements.

## Test Data

Only non-sensitive test files will be used.

Example files may include:

- IT support documentation
- Sample logs
- Test text files
- Troubleshooting notes

No passwords, credentials, personal information, or sensitive production data 
will be stored.

## Access Management

Storage access will be reviewed through the appropriate Azure permissions and 
authentication controls.

The lab will evaluate:

- Identity
- Role assignment
- Scope
- Storage data permissions
- Authentication
- Authorization

## Planned Storage Access Scenario

### User Report

A user reports that they cannot access a required Azure storage resource.

### Investigation

The planned investigation includes:

1. Confirm the affected storage resource
2. Confirm the user's identity
3. Verify the storage account exists
4. Review access configuration
5. Review Azure role assignments
6. Review role scope
7. Review data-access permissions
8. Test access
9. Apply the least-privilege corrective action
10. Retest access

## Authentication vs Authorization

The lab will distinguish between:

**Authentication** — verifying who the user is.

**Authorization** — determining what the authenticated user is permitted to 
access.

A successful Azure sign-in does not automatically provide access to every 
storage resource.

## Least Privilege

Users should receive only the permissions necessary to perform their required 
task.

Broad roles will not be assigned simply to bypass a permissions problem.

## Troubleshooting Methodology

Storage troubleshooting will review:

- Resource availability
- Correct storage account
- Correct target resource
- Identity
- Role assignment
- Scope
- Data permissions
- Authentication method
- Access restrictions
- Error messages

## Validation Plan

Verify:

- Storage account exists
- Test storage resource exists
- Test data can be stored
- Authorized access succeeds
- Unauthorized access remains restricted
- Access failures can be reproduced
- Permissions can be corrected
- Access can be retested successfully

## Screenshot Evidence

Planned screenshots:

- Storage account overview
- Storage service
- Test container or file share
- IAM configuration
- Access failure
- Corrected permissions
- Successful access after remediation

## Skills Demonstrated

- Azure Storage
- Storage accounts
- Blob/File storage concepts
- Azure permissions
- RBAC
- Access troubleshooting
- Least privilege
- Cloud administration
