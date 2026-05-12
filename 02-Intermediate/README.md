# Intermediate Labs

This phase contains the intermediate Azure security engineering labs in this portfolio.

Its purpose is to demonstrate practical implementation of security controls across Azure resources, identity permissions, network exposure, storage protection, monitoring, centralized logging, governance, and private access architecture.

Rather than treating these labs as isolated technical exercises, this phase is structured as a connected Azure security track. Together, the projects show how cloud environments can be secured through least privilege, secret protection, network restriction, security monitoring, log collection, policy enforcement, and private connectivity.

## What This Phase Demonstrates

This phase demonstrates practical experience in:

- secret protection through Azure Key Vault and Managed Identity
- least privilege access control through Azure RBAC
- network exposure reduction through Network Security Groups
- security event detection through Azure Monitor Activity Log alerts
- storage hardening through public access control, HTTPS enforcement, and network restrictions
- centralized logging through Diagnostic Settings and Log Analytics
- governance enforcement through Azure Policy
- private access architecture through Private Endpoint and Private DNS

These are practical Azure security controls used in real environments to reduce exposure, control access, improve visibility, enforce standards, and protect sensitive cloud resources.

## Intermediate Projects

### 1. Key Vault + Managed Identity

This project focused on securing secret access by using Azure Key Vault with Managed Identity, reducing the need for hardcoded credentials and demonstrating identity-based access to sensitive values.

### 2. Azure RBAC + Least Privilege

This project focused on implementing least privilege access by assigning Azure roles at controlled scopes and validating the difference between read-only and contributor-level permissions.

### 3. Network Security Group Restricted SSH Access

This project focused on reducing administrative exposure by allowing SSH access only from a trusted public IP and denying SSH access from all other internet sources.

### 4. Azure Monitor + Activity Log Alerts

This project focused on detecting Azure RBAC role assignment changes by creating an Activity Log alert and sending email notifications through an Action Group.

### 5. Azure Storage Security Hardening

This project focused on protecting Azure Blob Storage by disabling anonymous access, enforcing HTTPS, validating insecure HTTP blocking, and restricting storage access to a trusted network source.

### 6. Diagnostic Settings + Log Analytics

This project focused on centralizing Azure Activity Logs into a Log Analytics workspace and validating log ingestion through KQL queries for investigation and audit readiness.

### 7. Azure Policy Governance

This project focused on enforcing cloud governance by requiring an ownership tag at a controlled resource group scope and validating policy behavior against compliant and non-compliant deployments.

### 8. Private Endpoint for Secure Storage Access

This project focused on securing Azure Storage access through a Private Endpoint and Private DNS, disabling public network access, and validating private connectivity from inside the virtual network.

## Why These Labs Matter Together

Viewed individually, each project demonstrates a specific Azure security control. Viewed together, they form a broader cloud security workflow:

- Key Vault and Managed Identity reduce secret exposure
- RBAC enforces least privilege access
- NSGs restrict administrative network access
- Azure Monitor alerts detect sensitive access changes
- Storage hardening protects cloud data from public and insecure access
- Log Analytics centralizes investigation evidence
- Azure Policy enforces governance standards
- Private Endpoint removes public exposure for sensitive platform services

This progression reflects practical cloud security thinking. Secure Azure environments do not rely on one control alone. They combine access control, network restriction, monitoring, logging, governance, data protection, and private connectivity to reduce operational and security risk.

## Intermediate Phase Value

Across these projects, this phase demonstrates:

- Azure resource security implementation
- identity-based access control
- least privilege design
- secure secret management
- network security rule configuration
- storage account hardening
- security alerting and notification
- centralized activity log collection
- KQL-based validation
- Azure Policy governance
- private endpoint and private DNS configuration
- evidence-based validation of security controls
- professional documentation of cloud security work

## Outcome

The Intermediate phase establishes practical Azure security engineering capability by showing how key cloud security controls can be configured, tested, validated, and documented through realistic administrative and security workflows.

It builds on the Foundation phase by moving beyond core identity controls into broader Azure resource protection, monitoring, logging, governance, and private network access design.

This phase is intended to support progression into more advanced Microsoft security engineering scenarios, including Microsoft Sentinel, Defender for Cloud, automated response, identity threat detection, and security operations workflows.

## Repository Structure

    Azure-Entra-Security-Portfolio/
    ├── README.md
    ├── 01-Foundation/
    ├── 02-Intermediate/
    │   ├── 01-key-vault-managed-identity/
    │   ├── 02-rbac-least-privilege/
    │   ├── 03-nsg-restricted-ssh-access/
    │   ├── 04-azure-monitor-activity-log-alerts/
    │   ├── 05-storage-security-hardening/
    │   ├── 06-diagnostic-settings-log-analytics/
    │   ├── 07-azure-policy-governance/
    │   └── 08-private-endpoint-secure-storage-access/
