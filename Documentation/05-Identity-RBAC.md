# Azure Identity and Role-Based Access Control

## Overview

This section documents the planned identity and access management 
configuration for the Azure Cloud Support & Administration Lab.

Microsoft Entra ID and Azure Role-Based Access Control (RBAC) will be used to 
demonstrate authentication, authorization, role assignments, permission 
scope, least privilege, and troubleshooting of Azure resource access 
problems.

The actual users, role assignments, scopes, and troubleshooting results will 
be documented after the Azure environment is configured.

---

## Objectives

The objectives of this portion of the lab are to:

- Review Microsoft Entra ID identities
- Understand Azure Role-Based Access Control
- Review Azure built-in roles
- Assign permissions to Azure resources
- Understand RBAC assignment scope
- Apply the principle of least privilege
- Troubleshoot missing resource access
- Troubleshoot incorrect role assignments
- Differentiate authentication from authorization
- Verify access after permission changes
- Document realistic Azure access support scenarios

---

## Microsoft Entra ID

Microsoft Entra ID provides identity and access management services used 
throughout Microsoft Azure.

The lab will review how identities interact with Azure resources.

Identity concepts covered include:

- Users
- Groups
- Authentication
- Authorization
- Role assignments
- Administrative access
- Resource access

Microsoft Entra ID establishes the identity of the user, while Azure RBAC 
determines what that identity is authorized to do with Azure resources.

---

## Authentication vs Authorization

Authentication and authorization represent two different parts of Azure 
access management.

### Authentication

Authentication answers:

**Who is the user?**

A user successfully signing into Microsoft Azure demonstrates that their 
identity has been authenticated.

### Authorization

Authorization answers:

**What is the user allowed to do?**

A successfully authenticated user may still be unable to access or modify an 
Azure resource if the appropriate permissions have not been assigned.

This distinction is important when troubleshooting Azure access problems.

A successful Azure sign-in does not automatically provide access to every 
Azure resource.

---

## Azure Role-Based Access Control

Azure Role-Based Access Control determines what actions an identity can 
perform against Azure resources.

An Azure RBAC assignment consists of three primary components:

1. Security principal
2. Role definition
3. Scope

Together, these determine who receives access, what actions they can perform, 
and where those permissions apply.

---

## Security Principal

A security principal represents the identity receiving the Azure role 
assignment.

Examples include:

- User
- Group
- Service principal
- Managed identity

For the support scenarios in this lab, user or group identities may be used 
to demonstrate resource access.

Actual identities used will be documented after the Azure environment is 
configured.

---

## Role Definition

A role definition contains a collection of permissions describing which Azure 
operations can be performed.

The lab may evaluate built-in Azure roles including:

- Reader
- Contributor
- Virtual Machine Contributor
- Storage-related roles

Actual roles used will depend on the support scenarios performed.

---

## Reader Role

The Reader role provides visibility into Azure resources without broad 
modification permissions.

This role may be useful when a user needs to:

- View resources
- Review configuration
- Review resource status
- Inspect resource information

A user assigned Reader access should not automatically receive permission to 
modify the resource.

---

## Contributor Role

The Contributor role provides broader resource management capabilities.

This role may allow a user to create or modify supported Azure resources 
while not automatically granting unrestricted permission to manage access for 
other users.

Contributor access will only be used when required by the scenario.

---

## Virtual Machine Contributor

The Virtual Machine Contributor role may be evaluated for VM-specific 
administrative tasks.

This provides an opportunity to compare a specialized Azure role with broader 
roles such as Contributor.

The goal is to determine whether a narrower role can satisfy the user's job 
requirement.

---

## Storage Roles

Storage-specific Azure roles may be evaluated during the Azure Storage 
portion of the lab.

The storage scenario will demonstrate that access to a storage account 
resource does not necessarily mean a user has permission to access the 
underlying stored data.

Actual storage roles used will be documented after configuration.

---

## RBAC Scope

Azure role assignments can apply at different levels.

The planned hierarchy is:

Subscription
    |
    v
Resource Group
    |
    v
Individual Resource

Possible scopes include:

- Subscription
- Resource Group
- Individual Resource

A role assigned at a broader scope may be inherited by resources beneath that 
scope.

For example, a role assigned to RG-IT-Support-Lab may apply to supported 
resources contained within that resource group.

---

## Planned Resource Group Scope

The primary resource group for this lab is:

**RG-IT-Support-Lab**

Some permission scenarios may use the resource group as the assignment scope.

Other scenarios may intentionally use an individual resource scope to 
demonstrate more restrictive access.

---

## Principle of Least Privilege

Role assignments will follow the principle of least privilege.

Users should receive only the permissions required to perform their assigned 
responsibilities.

The lab will follow these guidelines:

- Do not assign Owner simply to resolve a basic access problem
- Select the narrowest appropriate Azure role
- Select the narrowest appropriate scope
- Avoid unnecessary administrative permissions
- Review inherited permissions
- Verify access after changes
- Remove unnecessary permissions when appropriate

This approach reduces security risk while still allowing users to perform 
required tasks.

---

## Planned Access Scenario

### User Report

A user successfully signs into Azure but cannot access a required Azure 
resource.

### Initial Assessment

Because authentication succeeds, the investigation will focus primarily on 
authorization and Azure resource permissions.

### Planned Investigation

1. Confirm the user's identity
2. Confirm the correct Azure tenant and subscription
3. Identify the affected resource
4. Open Access Control (IAM)
5. Review existing role assignments
6. Review inherited role assignments
7. Determine the user's current role
8. Review the role assignment scope
9. Determine the permissions required for the user's task
10. Select an appropriate least-privilege role
11. Apply the role assignment if required
12. Allow time for permission propagation if necessary
13. Retest access
14. Verify that unnecessary permissions were not granted

---

## Planned Incorrect RBAC Assignment Scenario

A second support scenario will involve a user who can view an Azure resource 
but cannot perform the administrative action required by their job.

This scenario will demonstrate that having some access to a resource does not 
necessarily provide permission to perform every operation.

### Planned Investigation

The investigation will compare:

- User identity
- Existing role
- Required operation
- Permissions included in the existing role
- Assignment scope
- Inherited permissions
- Appropriate replacement or additional role
- Least-privilege requirements

For example, a user with Reader access may be able to view a resource while 
being unable to modify it.

The actual role configuration and resolution will be documented after 
reproducing the scenario in Azure.

---

## Missing Resource Access Troubleshooting

When a user reports that an Azure resource is missing or inaccessible, the 
investigation will review:

- Correct user identity
- Correct Microsoft Entra tenant
- Correct Azure subscription
- Resource existence
- Resource group
- Access Control (IAM)
- Existing role assignments
- Inherited assignments
- Role definition
- Assignment scope
- Permission propagation
- Authentication status

The investigation should identify the cause before permissions are changed.

---

## Incorrect Role Troubleshooting

When a user can access a resource but cannot perform a required operation, 
the investigation will review:

1. What action the user is attempting
2. What role the user currently has
3. What permissions that role provides
4. Where the role is assigned
5. Whether the role is inherited
6. What minimum permissions are required
7. Whether a more appropriate built-in role exists

The goal is to correct the permission problem without unnecessarily 
increasing the user's privileges.

---

## Permission Scope Troubleshooting

A technically correct role may still fail to provide access if it is assigned 
at the wrong scope.

The lab will examine situations where:

- A role exists but applies to the wrong resource
- A role applies only to an individual resource
- A role is inherited from a resource group
- A broader assignment provides unintended access
- A narrower assignment better satisfies least privilege

Scope will therefore be reviewed as part of every RBAC troubleshooting 
scenario.

---

## Permission Propagation

Azure permission changes may not always appear immediately.

When testing a new role assignment, the troubleshooting process may include:

- Refreshing the Azure portal
- Signing out and back in when appropriate
- Waiting for permission changes to propagate
- Confirming the correct identity is being tested
- Reviewing the role assignment again

A temporary delay should not automatically be treated as a failed role 
assignment.

---

## Planned Validation

After performing the identity and RBAC portion of the lab, verify that:

- Microsoft Entra identities can be reviewed
- Azure Access Control (IAM) can be accessed
- Existing role assignments can be identified
- Built-in roles can be reviewed
- Role scope can be identified
- Resource-level and resource-group-level permissions can be distinguished
- Missing access can be reproduced
- Incorrect permissions can be diagnosed
- Least-privilege access can be assigned
- Access can be retested after remediation
- Excessive permissions are not granted

---

## Planned Screenshot Evidence

Potential screenshots include:

- Azure Access Control (IAM)
- Role assignments
- Built-in Azure roles
- Reader role assignment
- Resource group scope
- Individual resource scope
- Missing resource access scenario
- Incorrect RBAC assignment
- Corrected role assignment
- Successful access after remediation

Screenshots will only be added after the scenarios are actually performed.

Sensitive account information will be excluded or obscured when necessary.

---

## Related Help Desk Tickets

This documentation will support:

### Ticket 004 — Missing Resource Access

A user authenticates successfully but cannot access the required Azure 
resource.

Primary concepts:

- Authentication
- Authorization
- IAM
- RBAC
- Role assignment
- Scope

### Ticket 005 — Incorrect RBAC Assignment

A user can access an Azure resource but cannot perform the required 
administrative operation.

Primary concepts:

- Existing role
- Required permissions
- Role definition
- Scope
- Least privilege

### Ticket 006 — Storage Access Denied

Azure identity and RBAC concepts may also contribute to troubleshooting 
storage-access permissions.

---

## Security Considerations

Identity and permission configuration will follow these principles:

- Least privilege
- Avoid unnecessary Owner assignments
- Avoid unnecessarily broad scope
- Verify the correct identity before changing permissions
- Review inherited access
- Protect account information in screenshots
- Do not document passwords or credentials
- Validate access after changes

---

## Expected Outcome

After the Azure environment is built, this portion of the lab should 
demonstrate the ability to investigate and resolve realistic Azure 
authorization problems using Microsoft Entra ID, Azure IAM, RBAC roles, and 
assignment scope.

Actual results, role assignments, troubleshooting findings, and verification 
evidence will be added after the scenarios are completed.

---

## Skills Demonstrated

- Microsoft Azure
- Microsoft Entra ID
- Azure Role-Based Access Control
- Identity and Access Management
- Authentication
- Authorization
- Azure Access Control (IAM)
- Built-in Azure roles
- Role assignments
- Permission scope
- Least privilege
- Permissions troubleshooting
- Technical support
- Root cause analysis
- Technical documentation

