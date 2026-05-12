# Detecting RBAC Changes with Azure Monitor Alerts

## Overview

This project focused on detecting sensitive Azure access changes by using Azure Monitor Activity Log alerts to identify when a role assignment is created.

Rather than treating Azure Monitor as a basic notification tool, this lab approached it as a security detection control. The objective was to monitor administrative activity in Azure and generate an alert when a new RBAC role assignment was created.

The lab was built around a practical security operations scenario: if a user is granted access to Azure resources, the security team should be notified because role assignments can directly affect privilege, access scope, and cloud environment risk.

## Business Problem

Azure role assignments control who can access, manage, modify, or administer cloud resources. If role assignments are created without visibility, excessive access can be granted without timely review.

This creates a serious security risk. Unauthorized or unnecessary role assignments can lead to privilege escalation, accidental misconfiguration, data exposure, or unauthorized resource changes.

This project addressed that problem by creating an Azure Monitor Activity Log alert that detects successful RBAC role assignment creation events and sends an email notification through an Action Group.

## Project Objectives

This lab was designed to:

- create a dedicated resource group for the monitoring lab
- configure an Action Group for email notification
- create an Activity Log alert rule for RBAC role assignment creation
- monitor the `Microsoft.Authorization/roleAssignments/write` operation
- trigger the alert by creating a test Reader role assignment
- validate that the alert fired in Azure Monitor
- confirm that an email notification was received
- document the detection workflow as a security monitoring use case

## Technologies Used

- Azure Monitor
- Activity Log Alerts
- Action Groups
- Azure RBAC
- Azure Resource Groups
- Microsoft.Authorization
- Microsoft.Insights resource provider
- Email notification
- Azure Activity Log

## What Was Implemented

### 1. Monitoring Resource Group

A dedicated resource group named `RG-Monitor-Alert-Lab` was created to organize the monitoring resources used in this lab.

This provided a controlled scope for creating the Action Group and Activity Log alert rule without mixing the lab resources with unrelated Azure services.

### 2. Action Group for Email Notification

An Action Group named `ag-security-alerts` was created to send alert notifications by email.

The Action Group was configured with an email notification receiver so that security-related alert activity could be sent to the designated recipient.

During the lab, Action Group creation initially failed because the subscription was not registered for the `Microsoft.Insights` resource provider. The issue was resolved by registering the `Microsoft.Insights` provider under the subscription resource providers section, after which the Action Group was created successfully.

### 3. Activity Log Alert Rule

An Activity Log alert rule named `ALERT-RBAC-RoleAssignment-Created` was created.

The alert rule was configured to monitor administrative Activity Log events where the operation name matched role assignment creation.

The monitored operation was:

```text
Microsoft.Authorization/roleAssignments/write
```

This operation is important because it represents the creation of a new Azure RBAC role assignment.

### 4. Alert Condition and Scope

The alert rule was configured at the subscription scope so that RBAC role assignment creation activity could be detected across the selected Azure subscription.

The condition was configured to trigger when the Activity Log recorded a successful `Create role assignment` event.

This allowed the lab to detect access changes that may affect Azure resource permissions.

### 5. RBAC Role Assignment Test Event

To validate the alert rule, a test Reader role assignment was created.

This generated a real Azure Activity Log event for role assignment creation. The alert rule detected the event and moved to a fired state in Azure Monitor.

### 6. Email Notification Validation

After the alert fired, an email notification was received from Azure Monitor.

The notification confirmed that the Activity Log alert was activated for the RBAC role assignment creation event. This validated the end to end detection and notification workflow.

## Validation and Testing

The implementation was validated by generating a real RBAC role assignment event.

A Reader role assignment was created as the test activity. This produced an Azure Activity Log event for the `Microsoft.Authorization/roleAssignments/write` operation.

Azure Monitor detected the event and fired the alert rule named `ALERT-RBAC-RoleAssignment-Created`.

The validation confirmed:

- the Action Group was configured for email notification
- the alert rule monitored RBAC role assignment creation
- the test Reader role assignment generated a real Activity Log event
- Azure Monitor detected the role assignment creation event
- the alert appeared in a fired state
- an email notification was successfully received
- RBAC access changes could be detected through Azure Monitor

## Real World Use Case

In a real organization, Azure role assignments are sensitive administrative actions.

If a user is assigned Contributor, Owner, Reader, or another privileged role, that change may affect the security posture of the environment. Security teams need visibility into these access changes so they can investigate whether the assignment was approved, expected, and properly scoped.

For example, if a new Contributor role is assigned at the subscription level outside a normal change window, an alert can help the security team detect the activity quickly and review whether it was legitimate.

This lab demonstrates how Azure Monitor can support security operations by detecting access control changes and notifying the responsible team.

## Why This Matters in Practice

This lab reflects an important cloud security principle: access changes should be monitored, not only configured.

RBAC controls who can perform actions in Azure, but monitoring is needed to detect when those permissions change. Without alerting, role assignments may be created and remain unnoticed until they cause a security or operational issue.

Azure Monitor Activity Log alerts help close that visibility gap by detecting management-plane events such as role assignment creation.

By combining Activity Log monitoring with Action Group notifications, this lab demonstrated a practical detection workflow for cloud access governance and security operations.

## Implementation Evidence

### Action Group configured for email notification

An Action Group was created to send email notifications when the RBAC role assignment alert was triggered.

<img width="3200" height="1232" alt="05-action-group-email-notification-configured" src="https://github.com/user-attachments/assets/0bf5e3d1-48c0-4026-a676-836a3dede1cd" />

### Activity Log alert rule created for RBAC role assignment changes

The alert rule was configured to detect successful `Create role assignment` events at the subscription scope.

<img width="3200" height="1538" alt="07-activity-log-alert-rule-created" src="https://github.com/user-attachments/assets/d7e1b80d-8848-4bab-b024-e0922325af0c" />

### Reader role assignment created to trigger the alert

A Reader role assignment was created as a controlled test event to generate a real RBAC role assignment activity.

<img width="3200" height="1336" alt="08-reader-role-assignment-created-for-testing" src="https://github.com/user-attachments/assets/a5ce260f-7edb-4135-a1bd-d8a5c1b011fa" />

### RBAC role assignment alert fired in Azure Monitor

Azure Monitor detected the role assignment creation event and showed the alert in a fired state.

<img width="3200" height="1262" alt="09-rbac-role-assignment-alert-fired" src="https://github.com/user-attachments/assets/96b5c83f-836e-4aae-a0af-03a467603a72" />

### Email notification received for the alert

The configured Action Group sent an email notification confirming that the RBAC role assignment alert had been activated.

<img width="2546" height="1346" alt="10-email-notification-received-for-alert" src="https://github.com/user-attachments/assets/a7c8e612-5ecc-4522-8391-c5ddfae82f3f" />

## Skills Demonstrated

- Azure Monitor alert configuration
- Activity Log alert rule creation
- Action Group configuration
- email notification setup
- Azure RBAC monitoring
- management-plane event detection
- Microsoft.Authorization event tracking
- role assignment change detection
- alert validation through controlled testing
- Azure Activity Log interpretation
- troubleshooting Microsoft.Insights resource provider registration
- security monitoring workflow documentation

## Security Outcome

This implementation demonstrated a practical detection workflow for Azure RBAC access changes.

A successful role assignment creation event triggered an Azure Monitor Activity Log alert, and the configured Action Group sent an email notification. This showed that sensitive access changes could be detected and surfaced for review.

The result was a stronger monitoring control that improved visibility into Azure permission changes and supported a more accountable cloud security operations process.
