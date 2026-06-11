# Sentinel Security Operations Baseline

## Overview

This project built a Microsoft Sentinel security operations baseline by connecting Azure and Microsoft Entra ID activity logs into a Log Analytics workspace and validating the data with KQL.

The purpose of this lab was not just to enable Sentinel, but to prove that the workspace could collect the core log sources needed for security monitoring, investigation, and future detection engineering.

This lab forms the foundation for the advanced security operations projects that follow, including identity threat detection, privileged access investigation, analytics rule creation, and incident response workflows.

## Business Problem

Security teams cannot investigate threats properly if important cloud activity is not being collected.

In many cloud environments, security visibility is weak because logs are either not enabled, not centralized, or not validated after configuration. Without reliable log ingestion, incidents such as privileged role assignment, suspicious signins, policy changes, or administrative activity may go unnoticed.

A cloud security team needs a central place where Azure and identity logs can be collected, queried, and used for detection.

This lab addresses that problem by setting up Microsoft Sentinel as a central monitoring layer for Azure and Entra ID activity.

## Project Objectives

The main objectives of this lab were to:

* Create a dedicated resource group for the Sentinel baseline environment.
* Deploy a Log Analytics workspace for centralized log storage.
* Enable Microsoft Sentinel on the workspace.
* Install and configure the Azure Activity connector.
* Install and configure the Microsoft Entra ID connector.
* Validate Azure management activity logs using KQL.
* Validate Microsoft Entra signin logs using KQL.
* Validate Microsoft Entra audit logs using KQL.
* Prepare the environment for later detection and investigation labs.

## Technologies Used

* Microsoft Azure
* Microsoft Sentinel
* Log Analytics Workspace
* Azure Activity Logs
* Microsoft Entra ID
* Microsoft Entra Signin Logs
* Microsoft Entra Audit Logs
* Kusto Query Language (KQL)

## What Was Implemented

### 1. Resource Group for the Security Operations Baseline

A dedicated resource group was created to keep the Sentinel baseline resources organized and separated from other lab environments.

This helps simulate a clean security operations workspace where monitoring resources can be managed in a structured way.

### 2. Log Analytics Workspace

A Log Analytics workspace was created as the central location for collecting and querying security relevant logs.

The workspace acts as the data foundation for Microsoft Sentinel. Without a working workspace, Sentinel cannot ingest, store, or query the logs needed for security operations.

### 3. Microsoft Sentinel Enablement

Microsoft Sentinel was enabled on the Log Analytics workspace.

This turned the workspace into a cloud native SIEM environment that can support data connectors, analytics rules, incidents, workbooks, and hunting queries.

### 4. Azure Activity Connector

The Azure Activity connector was configured to collect Azure management plane activity.

This log source is important because it captures administrative actions such as resource creation, role assignments, policy changes, and other subscription level or resource level operations.

### 5. Microsoft Entra ID Connector

The Microsoft Entra ID connector was configured to collect identity related logs, including sign in logs and audit logs.

This is important because identity is one of the most common attack paths in cloud environments. Signin and audit logs are required for detecting suspicious authentication behavior, account changes, and administrative identity activity.

## Validation and Testing

After enabling the connectors, KQL queries were used to confirm that data was actually being ingested into the workspace.

This validation step is important because enabling a connector alone is not enough. A security engineer must confirm that logs are arriving and can be queried successfully.

The following log tables were validated:

* `AzureActivity`
* `SigninLogs`
* `AuditLogs`

The successful query results confirmed that the workspace was receiving Azure and Entra ID data and was ready to support later detection and investigation work.

## Detection and Investigation Logic

This lab focused on log onboarding and validation rather than alert creation.

The main logic was to confirm that the correct tables were available and populated:

* `AzureActivity` was used to validate Azure management plane activity.
* `SigninLogs` was used to validate identity signin activity.
* `AuditLogs` was used to validate Entra ID administrative activity.

These tables are used in later labs to build detections for suspicious signins, privileged account activity, role assignment changes, and post assignment user behavior.

## Real World Use Case

In a real cloud environment, this type of baseline is one of the first steps in building a security monitoring capability.

A security team needs to know:

* Who is signing in?
* Which accounts are failing authentication?
* Which administrators are making changes?
* Which Azure resources are being modified?
* When privileged access changes are happening?
* Whether logs are available for investigation after an incident?

This lab creates the visibility foundation needed to answer those questions.

## Production Considerations

This lab was built in a controlled training environment, but the same concept applies to production environments.

In production, a Sentinel baseline should also consider:

* Log retention requirements.
* Cost control and ingestion volume.
* Connector health monitoring.
* Role based access control for Sentinel users.
* Separation between production and test workspaces.
* Diagnostic settings for important Azure resources.
* Alert rules for high risk administrative and identity activity.
* Data collection aligned with compliance and incident response requirements.

For a production deployment, enabling connectors should always be followed by validation queries and ongoing connector health monitoring.

## Why This Matters in Practice

Microsoft Sentinel is only useful if the right data is being collected.

A detection rule cannot work without logs. An incident investigation cannot be trusted if logs are missing. A security operations team cannot respond confidently if there is no central visibility across cloud and identity activity.

This lab shows the practical starting point of cloud security monitoring: collect the right logs, validate them, and prepare the environment for detection engineering.

## Implementation Evidence

### Resource Group Created

The lab began with a dedicated resource group for the Sentinel security operations baseline.

<img width="1917" height="542" alt="01-resource-group-created" src="https://github.com/user-attachments/assets/002f8957-6fc1-492a-9cce-4d18153bb47a" />

### Log Analytics Workspace Created

A Log Analytics workspace was created to store and query security logs.

<img width="1919" height="806" alt="02-log-analytics-workspace-created" src="https://github.com/user-attachments/assets/171dea30-8ba5-4e11-aa72-28b1dabff96d" />

### Microsoft Sentinel Enabled

Microsoft Sentinel was enabled on the Log Analytics workspace.

<img width="1907" height="919" alt="03-microsoft-sentinel-enabled" src="https://github.com/user-attachments/assets/3af53f7f-047b-47e7-8a0f-9addcd30cd49" />

### Azure Activity Solution Installed

The Azure Activity solution was installed to support Azure management activity monitoring.

<img width="1919" height="942" alt="04-azure-activity-solution-installed" src="https://github.com/user-attachments/assets/4c90b05a-8545-4fb2-b096-aa500fa73d67" />

### Azure Activity Connector Enabled

The Azure Activity connector was configured to send Azure management activity into the workspace.

<img width="3198" height="1724" alt="05-azure-activity-connector-enabled" src="https://github.com/user-attachments/assets/1418ac3f-7d45-4810-bda3-82487bd7e196" />

### Microsoft Entra ID Solution Installed

The Microsoft Entra ID solution was installed to support identity log monitoring.

<img width="3200" height="1712" alt="06-Entra-Id-solution-installed" src="https://github.com/user-attachments/assets/65f37e44-b9d2-489a-a008-ad117409de26" />

### Microsoft Entra ID Connector Enabled

The Microsoft Entra ID connector was configured to collect sign-in and audit logs.

<img width="3200" height="1718" alt="07-entra-id-connector-enabled" src="https://github.com/user-attachments/assets/86014716-0ba2-4ba1-acc6-ff914260dfbb" />

### AzureActivity Query Validation

KQL was used to confirm that Azure Activity logs were being ingested successfully.

<img width="3182" height="1698" alt="08-azureactivity-query-results" src="https://github.com/user-attachments/assets/6f95acf7-533f-4c8b-aecc-b8f757da0c1c" />

### SigninLogs Query Validation

KQL was used to confirm that Microsoft Entra sign-in logs were available in the workspace.

<img width="3200" height="1638" alt="09-signinlogs-query-results" src="https://github.com/user-attachments/assets/fdb342a1-578e-40a0-bfb9-fc10201bcfc8" />

### AuditLogs Query Validation

KQL was used to confirm that Microsoft Entra audit logs were available in the workspace.

<img width="3200" height="1694" alt="10-auditlogs-query-results" src="https://github.com/user-attachments/assets/b7d0cf3f-b42b-45f5-bec6-6265ee7b350b" />

## KQL Queries

The validation queries used in this lab are stored in the `kql` folder:

* `kql/01-azure-activity-validation.kql`
* `kql/02-entra-signin-validation.kql`
* `kql/03-entra-audit-validation.kql`

## Skills Demonstrated

This project demonstrates the ability to:

* Configure a Microsoft Sentinel workspace.
* Connect Azure Activity logs to Sentinel.
* Connect Microsoft Entra ID logs to Sentinel.
* Validate log ingestion using KQL.
* Understand the purpose of core cloud security log sources.
* Build a foundation for detection engineering and incident investigation.
* Organize cloud security evidence for portfolio documentation.
* Explain security monitoring work in a business-focused way.

## Security Outcome

This lab established a working Microsoft Sentinel monitoring baseline for Azure and Microsoft Entra ID activity.

The environment was successfully prepared for advanced security operations work, including identity threat detection, privileged access investigation, analytics rule creation, and incident response validation.

The key security outcome was improved visibility: Azure management activity, Entra sign-in activity, and Entra audit activity were all connected and validated in a central security monitoring workspace.

