# Azure & Microsoft Entra Security Portfolio

This repository is a hands-on cloud security portfolio focused on **Microsoft Entra ID, Azure security, identity governance, cloud security operations, and secure Azure architecture**.

The portfolio is structured as a progressive learning path. It begins with foundational identity security controls, then moves into intermediate Azure security engineering scenarios involving access control, secret management, monitoring, logging, governance, storage protection, and private connectivity.

The purpose of this portfolio is not only to complete labs, but to document security controls in a way that reflects real operational problems inside organizations.

---

## Portfolio Purpose

This portfolio was built to demonstrate practical capability in:

- Microsoft Entra ID security
- Azure Identity and Access Management
- Conditional Access and MFA
- Privileged access governance
- Azure RBAC and least privilege
- Key Vault and Managed Identity
- Azure monitoring and alerting
- Log Analytics and KQL validation
- Storage account hardening
- Azure Policy governance
- Private Endpoint and Private DNS architecture
- Cloud security operations readiness

Each project is documented as a practical case study with a business problem, implementation evidence, validation steps, screenshots, skills demonstrated, and a security outcome.

---

## Portfolio Roadmap

```text
Azure-Entra-Security-Portfolio/
├── 01-Foundation/
├── 02-Intermediate/
└── 03-Advanced/
```

### 01 - Foundation

The Foundation phase focuses on core identity and access security controls in Microsoft Entra ID.

This phase demonstrates how organizations can protect users, privileged accounts, authentication methods, and access review processes using Microsoft identity security features.

### 02 - Intermediate

The Intermediate phase expands from identity-focused security into broader Azure security engineering.

This phase demonstrates how Azure resources can be protected through least privilege access, secure secret retrieval, network restrictions, monitoring, logging, storage hardening, policy enforcement, and private connectivity.

### 03 - Advanced

The Advanced phase is planned to focus on Microsoft Sentinel, Defender for Cloud, detection engineering, incident investigation, automation, KQL-based threat hunting, and end-to-end cloud security operations.

This phase will move from configuration-based security labs into security operations workflows that are closer to real SOC, cloud security analyst, and security engineer responsibilities.

---

## Current Portfolio Status

| Phase | Status | Focus |
|---|---|---|
| Foundation | Completed | Microsoft Entra ID identity security and governance |
| Intermediate | Completed | Azure security engineering and cloud resource protection |
| Advanced | Planned | SIEM, detection engineering, incident response, automation, and cloud security operations |

---

## Completed Foundation Labs

| No. | Project | Focus Area |
|---|---|---|
| 01 | [Conditional Access and MFA](01-Foundation/01-conditional-access-mfa/) | Protecting privileged access and reducing risky sign-ins |
| 02 | [Privileged Identity Management](01-Foundation/02-privileged-identity-management/) | Reducing standing privilege through just-in-time access |
| 03 | [Access Reviews](01-Foundation/03-access-reviews/) | Reviewing and removing unnecessary access |
| 04 | [Authentication Methods, SSPR, and Registration](01-Foundation/04-authentication-methods-sspr-registration/) | Strengthening authentication registration and self-service recovery |

---

## Completed Intermediate Labs

| No. | Project | Focus Area |
|---|---|---|
| 01 | [Key Vault + Managed Identity](02-Intermediate/01-key-vault-managed-identity/) | Secure secret retrieval without hardcoded credentials |
| 02 | [Azure RBAC + Least Privilege](02-Intermediate/02-rbac-least-privilege/) | Role-based access control and permission boundary validation |
| 03 | [NSG Restricted SSH Access](02-Intermediate/03-nsg-restricted-ssh-access/) | Restricting administrative access to trusted IP sources |
| 04 | [Azure Monitor Activity Log Alerts](02-Intermediate/04-azure-monitor-activity-log-alerts/) | Detecting RBAC role assignment changes through alerts |
| 05 | [Azure Storage Security Hardening](02-Intermediate/05-storage-security-hardening/) | Hardening blob storage against anonymous, insecure, and untrusted access |
| 06 | [Diagnostic Settings + Log Analytics](02-Intermediate/06-diagnostic-settings-log-analytics/) | Centralizing Activity Logs and validating ingestion with KQL |
| 07 | [Azure Policy Cloud Security Governance](02-Intermediate/07-azure-policy-cloud-security-governance/) | Enforcing ownership tagging through Azure Policy |
| 08 | [Private Endpoint Secure Storage Access](02-Intermediate/08-private-endpoint-secure-storage-access/) | Securing storage access through Private Endpoint and Private DNS |

---

## Planned Advanced Labs

The Advanced phase is planned to focus on cloud security operations, detection engineering, SIEM workflows, incident investigation, automated response, and advanced Microsoft security tooling.

These labs will build on the Foundation and Intermediate phases by moving from configuration and validation into real security monitoring, investigation, and response scenarios.

| No. | Planned Project | Focus Area |
|---|---|---|
| 01 | Microsoft Sentinel SIEM Deployment and Data Connector Configuration | Connecting Azure logs to Sentinel for centralized security monitoring |
| 02 | Sentinel Analytics Rule for Suspicious Sign-in Detection | Creating KQL-based detection logic for identity-related threats |
| 03 | Sentinel Incident Investigation Workflow | Investigating generated incidents using entities, logs, and timeline evidence |
| 04 | Sentinel Automation Rule and Logic App Response | Automating notification or response actions for security incidents |
| 05 | Defender for Cloud Security Posture Review and Remediation | Reviewing recommendations, prioritizing risks, and documenting remediation |
| 06 | Identity Threat Detection with Entra Sign-in Logs | Detecting failed login bursts, suspicious access patterns, and risky sign-in behavior |
| 07 | Privileged Access Monitoring with KQL | Monitoring role assignments, privilege changes, and administrative activity |
| 08 | Infrastructure as Code Security with Bicep or Terraform | Deploying repeatable Azure security controls through code |
| 09 | Azure Firewall and Network Traffic Control | Controlling outbound and inbound traffic using centralized firewall rules |
| 10 | End-to-End Cloud Security Incident Response Lab | Combining logs, alerts, investigation, and response into a complete workflow |

---

## What This Portfolio Demonstrates

This portfolio demonstrates practical security implementation across several important Microsoft cloud security areas.

### Identity Security

The Foundation phase demonstrates how Microsoft Entra ID can be used to protect users and privileged identities through Conditional Access, MFA, PIM, Access Reviews, authentication methods, and self-service password reset.

### Least Privilege Access

The RBAC and PIM labs demonstrate how access should be scoped, tested, and validated rather than granted broadly. These labs show the difference between visibility, modification permissions, privileged access, and controlled administrative capability.

### Secret Protection

The Key Vault and Managed Identity lab demonstrates how workloads can retrieve secrets without storing credentials directly inside scripts, applications, or virtual machines.

### Network Security

The NSG and Private Endpoint labs demonstrate how network controls can reduce exposure by restricting SSH access and moving sensitive storage connectivity into a private network path.

### Monitoring and Detection

The Azure Monitor and Log Analytics labs demonstrate how security-relevant activity can be detected, alerted, centralized, and queried for investigation.

### Storage Protection

The storage security hardening lab demonstrates how blob storage can be protected through private containers, secure transfer enforcement, anonymous access blocking, trusted IP restrictions, and real validation testing.

### Governance and Compliance

The Azure Policy lab demonstrates how governance controls can enforce required standards, such as ownership tagging, before resources are accepted as compliant.

### Private Access Architecture

The Private Endpoint lab demonstrates how sensitive Azure Storage access can be moved away from public exposure and validated through private DNS resolution and private endpoint connectivity.

---

## How the Labs Are Documented

Each lab is documented as a practical security case study and follows a consistent structure:

- Overview
- Business Problem
- Project Objectives
- Technologies Used
- What Was Implemented
- Validation and Testing
- Real-World Use Case
- Why This Matters in Practice
- Implementation Evidence
- Skills Demonstrated
- Security Outcome

The goal is to make each project readable for both technical reviewers and hiring managers.

Each lab includes selected screenshots in the README, while additional supporting screenshots are kept inside the relevant `screenshots/` folder.

---

## Repository Structure

```text
Azure-Entra-Security-Portfolio/
│
├── README.md
│
├── 01-Foundation/
│   ├── 01-conditional-access-mfa/
│   ├── 02-privileged-identity-management/
│   ├── 03-access-reviews/
│   └── 04-authentication-methods-sspr-registration/
│
├── 02-Intermediate/
│   ├── 01-key-vault-managed-identity/
│   ├── 02-rbac-least-privilege/
│   ├── 03-nsg-restricted-ssh-access/
│   ├── 04-azure-monitor-activity-log-alerts/
│   ├── 05-storage-security-hardening/
│   ├── 06-diagnostic-settings-log-analytics/
│   ├── 07-azure-policy-cloud-security-governance/
│   └── 08-private-endpoint-secure-storage-access/
│
└── 03-Advanced/
    ├── 01-sentinel-siem-data-connectors/
    ├── 02-sentinel-suspicious-signin-analytics-rule/
    ├── 03-sentinel-incident-investigation/
    ├── 04-sentinel-automation-logic-app-response/
    ├── 05-defender-for-cloud-posture-remediation/
    ├── 06-entra-signin-threat-detection/
    ├── 07-privileged-access-monitoring-kql/
    ├── 08-iac-security-bicep-terraform/
    ├── 09-azure-firewall-network-traffic-control/
    └── 10-cloud-security-incident-response/
```

---

## Security Themes Covered

This portfolio currently covers:

- Identity protection
- Privileged access governance
- Least privilege access control
- Secure authentication and recovery
- Secret management
- Managed Identity
- Network access restriction
- Azure Storage hardening
- Activity Log alerting
- Centralized logging
- KQL-based validation
- Azure Policy governance
- Private Endpoint architecture
- Private DNS validation
- Public exposure reduction
- Cloud security operations readiness

---

## Portfolio Outcome

The completed Foundation and Intermediate phases provide practical evidence of Microsoft cloud security skills across identity, access control, monitoring, logging, governance, storage protection, and private network architecture.

The Foundation phase establishes identity security fundamentals. The Intermediate phase builds on that foundation by applying security controls across Azure resources and validating them through real tests, logs, alerts, and screenshots.

This portfolio will continue into the Advanced phase with deeper security operations scenarios, including Microsoft Sentinel, Defender for Cloud, KQL detection logic, automated response, and incident investigation workflows.
