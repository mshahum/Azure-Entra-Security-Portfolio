# Implementing Azure RBAC and Least Privilege Access

## Overview

This project focused on implementing role based access control in Azure by assigning different permissions to test users at a controlled resource group scope.

Rather than treating Azure RBAC as a basic access assignment feature, this lab approached it as a core cloud security control. The objective was to demonstrate how different Azure roles affect what users can and cannot do inside a resource group.

The lab was built around a practical least privilege scenario: one user was assigned read only access, while another user was assigned contributor access. Their permissions were then tested against a storage account inside the resource group to validate the difference between visibility, modification, and administrative control.

## Business Problem

Cloud environments often contain many users, teams, applications, and administrators. If permissions are granted too broadly, users may be able to modify or delete resources they do not actually need to manage.

This creates serious operational and security risks. Excessive permissions can lead to accidental misconfiguration, unauthorized changes, data exposure, service disruption, or privilege misuse.

This project addressed that problem by using Azure RBAC to assign permissions at the resource group scope and validate the principle of least privilege. The Reader user was able to view resources but could not modify or delete them. The Contributor user was able to perform management actions on resources inside the assigned scope.

## Project Objectives

This lab was designed to:

- create a dedicated Azure resource group for RBAC testing
- deploy a storage account inside the resource group
- create separate test users for Reader and Contributor access
- assign the Reader role at the resource group scope
- assign the Contributor role at the resource group scope
- validate that the Reader user could not modify resource tags
- validate that the Reader user could not delete the resource group
- validate that the Contributor user could perform allowed management actions
- review Activity Log evidence for successful Contributor activity

## Technologies Used

- Microsoft Azure
- Microsoft Entra ID
- Azure RBAC
- Azure Resource Groups
- Azure Storage Account
- Reader role
- Contributor role
- Azure Activity Log

## What Was Implemented

### 1. Resource Group for RBAC Testing

A dedicated resource group named `RG-RBAC-LAB` was created to provide a controlled scope for access testing.

Using a resource group scope allowed the lab to test RBAC permissions without affecting unrelated Azure resources. This reflects a common enterprise pattern where access is assigned at the lowest practical scope rather than across the full subscription.

### 2. Storage Account as the Test Resource

A storage account named `stgrbaclab` was created inside the resource group.

The storage account acted as the test resource for validating permission boundaries. It allowed the lab to test whether users could view, modify, tag, or attempt administrative actions based on their assigned Azure role.

### 3. RBAC Test Users

Two test users were used for the lab:

- `RBAC Reader User`
- `RBAC Contributor User`

These users represented different access levels that may exist in a real cloud environment. The Reader user represented a view only role, while the Contributor user represented an operational role that can manage resources within a defined scope.

### 4. Reader Role Assignment

The `RBAC Reader User` was assigned the Reader role at the `RG-RBAC-LAB` resource group scope.

This gave the user visibility into resources within the resource group but did not allow the user to modify, delete, or update resource configuration.

This role assignment demonstrated least privilege for users who only need visibility for review, audit, monitoring, or support purposes.

### 5. Contributor Role Assignment

The `RBAC Contributor User` was assigned the Contributor role at the same resource group scope.

This allowed the user to manage resources within the resource group, including updating resource properties such as tags. However, the role was still limited to the assigned scope and did not provide full subscription ownership.

This demonstrated how operational access can be granted without assigning unnecessary Owner permissions.

## Validation and Testing

The implementation was tested by signing in with the RBAC test users and attempting different actions against the storage account and resource group.

The Reader user attempted to add tags to the storage account. The action failed with an authorization error, proving that Reader access allowed visibility but did not allow write operations.

The Reader user also attempted to delete the resource group. This action failed because the user did not have permission to perform delete operations at the resource group scope.

The Contributor user then performed an allowed management action by writing tags to the storage account. The successful activity was visible in the storage account Activity Log, confirming that the Contributor role had the required permission for that type of operation.

The validation confirmed:

- the Reader role allowed resource visibility but not modification
- the Reader user could not write tags to the storage account
- the Reader user could not delete the resource group
- the Contributor role allowed permitted management actions within the assigned scope
- Azure Activity Log captured the successful Contributor activity
- RBAC permissions were enforced according to assigned roles and scope

## Real World Use Case

In a real organization, not every user should have the same level of access to Azure resources.

A security analyst may need to review resources but should not be able to modify or delete them. In that case, the Reader role may be appropriate.

An operations engineer may need to manage resources inside a specific resource group, but should not have full subscription ownership. In that case, the Contributor role at resource group scope may be more appropriate than assigning Owner at the subscription level.

This lab demonstrates how Azure RBAC can be used to align access with job responsibility, reducing unnecessary privilege while still allowing users to perform required work.

## Why This Matters in Practice

This lab reflects an important cloud security principle: access should be granted based on need, not convenience.

Over permissioned identities are a common risk in cloud environments. If every user receives broad Contributor or Owner access, the environment becomes harder to control, audit, and secure.

Azure RBAC helps reduce this risk by allowing permissions to be assigned at specific scopes such as management group, subscription, resource group, or individual resource level.

By assigning Reader and Contributor roles at the resource group scope, this lab demonstrated how permissions can be controlled, tested, and validated in a practical Azure environment.

This approach supports least privilege, reduces the risk of accidental changes, and improves accountability for administrative actions.

## Implementation Evidence

### Storage account created inside the RBAC lab resource group

A storage account was created inside `RG-RBAC-LAB` to act as the target resource for RBAC permission testing.

<img width="3200" height="798" alt="02-storage-account-created-in-rbac-lab" src="https://github.com/user-attachments/assets/e55ed3bc-beb5-4244-be8c-3660b932d8ae" />

### Reader and Contributor roles assigned at resource group scope

The RBAC test users were assigned different roles at the resource group scope. The Reader user received read only access, while the Contributor user received resource management permissions within the same scope.

<img width="3200" height="1734" alt="05-reader-and-contributor-roles-assigned" src="https://github.com/user-attachments/assets/d52e0219-a441-4c01-a14b-1b6b39413d74" />

### Reader user denied tag write operation

The Reader user attempted to add tags to the storage account, but the operation failed with an authorization error. This confirmed that Reader access does not allow write operations.

<img width="3194" height="1728" alt="06-reader-user-denied-tag-write" src="https://github.com/user-attachments/assets/b5ca2d4c-1116-4ac0-a79a-e37471ecf9c8" />

### Reader user denied resource group deletion

The Reader user attempted to delete the resource group, but the operation failed because the user did not have delete permissions at the assigned scope.

<img width="3180" height="1730" alt="07-reader-user-denied-resource-group-deletion" src="https://github.com/user-attachments/assets/38ae2407-0422-4e68-885f-bd34a16ea8a9" />

### Contributor user activity validated through Activity Log

The Contributor user successfully performed a tag write operation on the storage account. The successful action was visible in the Activity Log, confirming that Contributor permissions allowed the operation.

<img width="3198" height="1302" alt="08-contributor-user-tag-write-activity-log" src="https://github.com/user-attachments/assets/98f6b826-38a8-41fa-9fc1-9ab3fecfb611" />

## Skills Demonstrated

- Azure RBAC role assignment
- least privilege access design
- resource group scoped permissions
- Reader role validation
- Contributor role validation
- Azure Storage resource management
- permission boundary testing
- failed authorization testing
- Activity Log review
- role based access troubleshooting
- identity and access control validation in Azure

## Security Outcome

This implementation demonstrated how Azure RBAC can be used to enforce least privilege access at the resource group scope.

The Reader user was able to view resources but was prevented from modifying tags or deleting the resource group. The Contributor user was able to perform permitted management actions within the assigned scope, and the successful activity was captured in Azure Activity Log.

The result was a controlled access model that aligned permissions with user responsibility, reduced unnecessary privilege, and provided evidence that Azure RBAC was enforcing access boundaries correctly.
