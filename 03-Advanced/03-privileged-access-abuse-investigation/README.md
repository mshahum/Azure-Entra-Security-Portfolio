
# Privileged Access Abuse Investigation

## Overview

This project simulated a privileged access investigation in Azure by creating a controlled role assignment, detecting the role assignment event in Microsoft Sentinel, reviewing the operation timeline, checking post assignment activity, and removing the access to restore least privilege.

The purpose of this lab was to demonstrate how Azure RBAC activity can be investigated using AzureActivity logs and KQL, especially when a user is granted elevated access to a resource group.

This lab follows a realistic security operations flow: detect the access change, identify the caller, investigate the operation, review whether the assigned user used the access, and validate remediation after the role assignment was removed.

## Business Problem

Privileged access changes are high risk events in cloud environments.

If a user is granted a powerful role such as Contributor, Owner, or User Access Administrator, that user may be able to modify resources, deploy services, change configurations, or support further privilege escalation. If the access was granted unexpectedly, it may indicate misuse, poor access governance, or a possible compromise of an administrator account.

Security teams need a reliable way to detect and investigate Azure RBAC role assignments.

This lab addresses that problem by showing how role assignment activity can be identified in Microsoft Sentinel, investigated using correlation IDs, reviewed for post assignment activity, and remediated by removing unnecessary access.

## Project Objectives

The main objectives of this lab were to:

* Create a controlled Azure resource group for the investigation scenario.
* Assign Contributor access to a test user at resource group scope.
* Detect the Azure RBAC role assignment event using KQL.
* Identify the caller who created the role assignment.
* Use the correlation ID to review the operation timeline.
* Check whether the assigned user performed activity after receiving access.
* Remove the Contributor role assignment to restore least privilege.
* Validate the remediation event using AzureActivity logs.
* Document the investigation in a clear, evidence-based format.

## Technologies Used

* Microsoft Azure
* Microsoft Sentinel
* Log Analytics Workspace
* Azure Activity Logs
* Azure Role-Based Access Control (RBAC)
* Microsoft Entra ID test users
* Kusto Query Language (KQL)
* Resource group IAM
* Cloud security investigation workflow

## What Was Implemented

### 1. Controlled Investigation Resource Group

A dedicated resource group was created for the privileged access investigation scenario.

This provided a safe and isolated scope for testing role assignment activity without affecting production resources.

### 2. Contributor Role Assignment

A test user was assigned the Contributor role at the resource group scope.

This simulated a realistic privileged access event where a user receives elevated permissions over a defined Azure scope.

The role assignment evidence was captured from the Azure IAM view to confirm the assigned user, assigned role, and scope.

### 3. Role Assignment Detection with AzureActivity

A KQL query was used to detect Azure RBAC role assignment creation events in the `AzureActivity` table.

The query focused on the operation:

`MICROSOFT.AUTHORIZATION/ROLEASSIGNMENTS/WRITE`

This operation indicates that a role assignment was created.

The detection identified the caller, operation name, status, affected resource group, resource provider, and correlation ID.

### 4. Operation Timeline Investigation

The role assignment event was investigated further using the correlation ID.

The correlation ID helped group related AzureActivity records belonging to the same operation. This made it possible to review the start and success stages of the role assignment event.

This step demonstrated how a security analyst can move from a single detection result into a more complete operation timeline.

### 5. Post Assignment Activity Review

After the user received Contributor access, AzureActivity logs were reviewed to check whether the assigned user performed activity in the same resource group.

This is an important investigation step because the risk is not only that access was granted. The risk increases if the user actually used that access afterward.

The post assignment review showed activity performed by the assigned user after the role assignment time.

### 6. Access Removal and Remediation Validation

After the investigation, the Contributor role assignment was removed.

A KQL query was then used to validate the remediation event by detecting:

`MICROSOFT.AUTHORIZATION/ROLEASSIGNMENTS/DELETE`

This confirmed that the unnecessary access was removed and that the cleanup action was also recorded in AzureActivity logs.

## Validation and Testing

The lab was validated through a full investigation and remediation workflow.

Validation included:

* Confirming the test resource group was created.
* Confirming Contributor access was assigned to the test user.
* Detecting the role assignment creation event in AzureActivity.
* Reviewing the operation timeline using the correlation ID.
* Confirming activity by the assigned user after the access was granted.
* Removing the role assignment from the resource group.
* Confirming the role assignment deletion event in AzureActivity.

This validation proved that the investigation did not stop at detection. It followed the full lifecycle from access creation through post assignment review and remediation.

## Detection and Investigation Logic

This lab used KQL to investigate Azure RBAC changes and related activity.

The main detection focused on Azure role assignment creation:

`MICROSOFT.AUTHORIZATION/ROLEASSIGNMENTS/WRITE`

This operation was used to identify when privileged access was granted.

The investigation then used:

* `Caller` to identify the account that performed the role assignment.
* `ActivityStatusValue` to confirm whether the operation succeeded.
* `ResourceGroup` to identify the affected scope.
* `CorrelationId` to connect related activity records.
* `TimeGenerated` to build the event timeline.
* A post assignment time filter to review activity after access was granted.

The remediation validation focused on:

`MICROSOFT.AUTHORIZATION/ROLEASSIGNMENTS/DELETE`

This operation was used to confirm that the role assignment was removed successfully.

## Real World Use Case

In a real cloud environment, this type of investigation would be useful when a security team needs to review unexpected or high risk Azure access changes.

Examples include:

* A user receiving Contributor access unexpectedly.
* An administrator assigning access outside an approved change window.
* A helpdesk user receiving more permissions than required.
* A privileged role assignment created without a ticket or approval.
* A suspicious account making RBAC changes after compromise.
* A user performing actions shortly after receiving elevated access.

This lab demonstrates how a cloud security analyst can investigate the event, understand who initiated it, review whether access was used, and confirm that remediation was completed.

## Production Considerations

This lab was performed in a controlled environment, but the same investigation logic applies to production environments.

In production, role assignment monitoring should include additional controls and enrichment, such as:

* Approved RBAC administrator lists.
* Privileged Identity Management (PIM) activation logs.
* Change ticket or approval validation.
* Alerting for high risk roles such as Owner, Contributor, and User Access Administrator.
* Alerting for broad scopes such as subscription or management group level.
* Watchlists for sensitive users, break glass accounts, and external users.
* Entity mapping in Sentinel analytics rules.
* Automation playbooks for enrichment and notification.
* Regular access reviews for standing privileged access.
* Documentation of remediation actions.

An important investigation lesson from this lab is that AzureActivity reliably shows the role assignment operation, caller, status, affected resource group, and correlation ID. However, the friendly name of the user receiving the role is not always clearly available in the basic AzureActivity columns. For that reason, the assigned user, role, and scope were confirmed through IAM role assignment evidence.

This reflects a realistic production scenario: activity logs often need to be enriched with IAM, Azure Resource Manager, Microsoft Graph, Azure CLI, or change management data before final conclusions are made.

## Why This Matters in Practice

Privileged access is one of the most important areas of cloud security.

A single unnecessary role assignment can increase the attack surface of an Azure environment. If the wrong user receives Contributor or Owner access, they may be able to modify resources, deploy new services, change configurations, or support further compromise.

This lab matters because it demonstrates more than basic alerting. It shows an investigation mindset:

* What happened?
* Who performed the action?
* Was it successful?
* What scope was affected?
* Did the assigned user use the access?
* Was the access removed?
* Can the remediation be verified in logs?

That type of thinking is important for cloud security engineering, IAM security, and security operations roles.

## Implementation Evidence

### Test Resource Group Created

A dedicated resource group was created to safely simulate the privileged access investigation scenario.

<img width="3200" height="988" alt="01-test-resource-group-created" src="https://github.com/user-attachments/assets/ea900dfb-7fe2-4887-9708-8a7d199d47e1" />

### Contributor Role Assigned to Test User

Contributor access was assigned to the test user at resource group scope to simulate a privileged access event.

<img width="3200" height="1312" alt="02-test-role-assignment-created" src="https://github.com/user-attachments/assets/a0ddbbde-fbf6-463f-a68e-45248bc11395" />

### RBAC Role Assignment Detected in AzureActivity

A KQL query detected the successful Azure RBAC role assignment creation event.

<img width="3194" height="1690" alt="03-rbac-role-assignment-query-results" src="https://github.com/user-attachments/assets/62051280-1820-46e7-9805-b9458858c539" />

### Role Assignment Timeline Investigated

The correlation ID was used to review the related activity records for the role assignment operation.

<img width="3200" height="1718" alt="04-role-assignment-investigation-timeline" src="https://github.com/user-attachments/assets/752c1066-a037-4092-ae54-30d2dba820bb" />

### Post Assignment Activity Reviewed

AzureActivity logs were reviewed to check whether the assigned user performed activity after receiving access.

<img width="3192" height="1410" alt="06-post-assignment-activity-review" src="https://github.com/user-attachments/assets/4a1914e4-699c-44db-90bf-ce76941f621c" />

### Role Assignment Removed

The Contributor role assignment was removed from the resource group to restore least privilege.

<img width="3198" height="1224" alt="07-role-assignment-removed-portal" src="https://github.com/user-attachments/assets/f9471d9d-4730-4b48-a3f2-10bdaa897ebe" />

### Remediation Validated in AzureActivity

A KQL query confirmed that the role assignment deletion event completed successfully.

<img width="3190" height="1702" alt="08-role-assignment-remediation-query-results" src="https://github.com/user-attachments/assets/bbfd3ba0-6f8e-4849-a726-83f123362ce4" />


## KQL Queries

The KQL queries used in this lab are stored in the `kql` folder:

* `kql/01-rbac-role-assignment-detection.kql`
* `kql/02-role-assignment-investigation-timeline.kql`
* `kql/03-post-assignment-activity-review.kql`
* `kql/04-role-assignment-remediation-validation.kql`

## Skills Demonstrated

This project demonstrates the ability to:

* Investigate Azure RBAC role assignment activity.
* Use AzureActivity logs for cloud security investigation.
* Identify the caller behind a privileged access change.
* Use correlation IDs to investigate related operation records.
* Review post-assignment activity after elevated access is granted.
* Validate remediation through role assignment deletion logs.
* Apply least privilege principles after investigation.
* Understand the limits of raw log data and the need for enrichment.
* Document an investigation in a clear and evidence-based way.
* Explain privileged access risk in business and security terms.

## Security Outcome

This lab demonstrated a full privileged access investigation and remediation workflow in Azure.

The key security outcome was that a high risk role assignment was detected, investigated, reviewed for post assignment activity, and removed after validation. The lab also showed that remediation actions can be confirmed through AzureActivity logs.

This project strengthened cloud security visibility around Azure RBAC changes and demonstrated practical investigation skills relevant to cloud security, IAM security, and security operations roles.

