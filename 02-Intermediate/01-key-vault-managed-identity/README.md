# Securing Secrets with Azure Key Vault and Managed Identity

## Overview

This project focused on strengthening secret management in Azure by using Azure Key Vault and Managed Identity to retrieve sensitive information without storing credentials directly inside a virtual machine, script, or configuration file.

Rather than treating Key Vault as a simple storage location for secrets, this lab approached it as a core cloud security control. The objective was to demonstrate how Azure workloads can securely access secrets through identity based authentication, least privilege role assignment, and centralized secret management.

The lab is built around a practical security scenario: a virtual machine needed to retrieve a database password from Key Vault without using hardcoded credentials or manually stored service principal secrets.

## Business Problem

Applications and workloads often require access to sensitive values such as database passwords, API keys, certificates, connection strings, or service credentials. A weak approach is to store these values directly inside application code, configuration files, scripts, or virtual machines.

This creates a serious security risk. If the code repository, script, or server is exposed, the secret may also be exposed. Hardcoded credentials are difficult to rotate, difficult to audit, and easy to copy across environments without proper control.

This project addressed that problem by storing the secret in Azure Key Vault and allowing the virtual machine to access it through a system assigned Managed Identity. This removed the need to store credentials directly on the VM and allowed access to be controlled through Azure role based access control.

## Project Objectives

This lab was designed to:

- create an Azure Key Vault for secure secret storage
- create a test secret inside Key Vault
- deploy a virtual machine as a workload requiring secret access
- enable a system assigned Managed Identity on the virtual machine
- assign least privilege Key Vault access to the VM managed identity
- authenticate from the VM using Managed Identity
- retrieve the Key Vault secret through Azure CLI without stored credentials
- validate access through command line testing and Azure Activity Log evidence

## Technologies Used

- Azure Key Vault
- Azure Virtual Machine
- Managed Identity
- Microsoft Entra ID
- Azure RBAC
- Key Vault Secrets Officer
- Key Vault Secrets User
- Azure CLI
- SSH
- Azure Activity Log

## What Was Implemented

### 1. Azure Key Vault Deployment

An Azure Key Vault was created inside a dedicated resource group to provide centralized secret storage for the lab.

The Key Vault was used to store a secret named `DbPassword`, representing a sensitive application or database role based access control.

### 2. Administrative Secret Management Access

The administrator account was assigned the `Key Vault Secrets Officer` role at the Key Vault scope. This allowed the administrator to create and manage secrets inside the vault while keeping secret management permissions controlled through Azure RBAC.

This reflected a role based access model where secret management permissions are assigned deliberately rather than granted broadly.

### 3. Virtual Machine with System Assigned Managed Identity

A Linux virtual machine was deployed as the test workload. A system assigned Managed Identity was enabled on the VM, allowing Azure to create an identity for the virtual machine in Microsoft Entra ID.

This identity allowed the VM to authenticate to Azure services without needing a password, client secret, or manually managed service principal credential.

### 4. Key Vault Access for the VM Managed Identity

The VM managed identity was assigned the `Key Vault Secrets User` role at the Key Vault scope. This gave the VM permission to read secrets from Key Vault without granting broader administrative access.

This role assignment followed the principle of least privilege. The VM did not need to manage the Key Vault or modify secrets; it only needed to retrieve the required secret.

### 5. Secret Retrieval from the Virtual Machine

The virtual machine was accessed through SSH. From inside the VM, Azure CLI was used to authenticate using the VM managed identity.

The Key Vault secret was then retrieved from the VM using Azure CLI. The successful retrieval confirmed that the managed identity had the correct permission to access the secret and that no hardcoded credentials were required.

## Validation and Testing

The implementation was tested from inside the virtual machine.

The VM authenticated to Azure using its system assigned Managed Identity:

```bash
az login --identity
```

After authentication, the Key Vault secret was retrieved using Azure CLI:

```bash
az keyvault secret show \
  --vault-name keyvault-mi-testing-01 \
  --name DbPassword \
  --query value \
  -o tsv
```

The command returned the secret value successfully, proving that the VM could access Key Vault through Managed Identity.

The validation confirmed:

- the VM managed identity was enabled
- the VM could authenticate to Azure without stored credentials
- the VM identity had the correct Key Vault role assignment
- the Key Vault secret could be retrieved securely through Azure CLI
- access was controlled through Azure RBAC rather than hardcoded credentials

The secret value was redacted in the screenshot before documentation to avoid exposing sensitive information.

## Real-World Use Case

In a real organization, an application running on a virtual machine may need to connect to a database, API, or internal service. A poor design would store the database password or API key directly inside the application code or configuration file.

A stronger design stores the secret in Azure Key Vault and allows the workload to retrieve it at runtime using Managed Identity.

For example, a finance application running on an Azure VM could retrieve its database password from Key Vault without the password being stored on the server. If the VM needs access, Azure verifies the VM identity and checks whether that identity has permission to read the secret.

This model reduces credential exposure and improves control over secret access.

## Why This Matters in Practice

This lab reflects an important cloud security principle: workloads should use identity based access instead of hardcoded secrets.

Managed Identity reduces the need to manually manage credentials for Azure resources. Azure Key Vault provides a centralized and controlled location for sensitive values. When used together, they allow applications and virtual machines to access secrets securely while keeping permissions auditable and scoped.

This approach matters in real environments because exposed secrets can lead to database compromise, unauthorized service access, lateral movement, or broader cloud account abuse.

By using Managed Identity and Key Vault together, organizations can reduce the risk of credential leakage, improve secret governance, and apply least privilege access to sensitive information.

## Implementation Evidence

### Azure Key Vault deployment completed

The Azure Key Vault was successfully deployed as the secure location for storing sensitive secrets.



### DbPassword secret created in Azure Key Vault

A secret named `DbPassword` was created inside Azure Key Vault to represent a sensitive application or database credential.

![DbPassword secret created in Azure Key Vault](screenshots/04-key-vault-secret-dbpassword-created.png)

### System assigned Managed Identity enabled on the virtual machine

A system assigned Managed Identity was enabled on the VM so the workload could authenticate to Azure without stored credentials.

![System assigned Managed Identity enabled on the virtual machine](screenshots/06-vm-system-assigned-managed-identity-enabled.png)

### Key Vault Secrets User role assigned to the VM managed identity

The VM managed identity was assigned the `Key Vault Secrets User` role, allowing it to read secrets from the Key Vault without broader administrative permissions.

![Key Vault Secrets User role assigned to the VM managed identity](screenshots/07-key-vault-secrets-user-assigned-to-vm-managed-identity.png)

### Key Vault secret retrieved from the VM using Managed Identity

The VM authenticated using Managed Identity and successfully retrieved the Key Vault secret through Azure CLI. The secret value was redacted before documentation.

![Key Vault secret retrieved from the VM using Managed Identity](screenshots/09-vm-managed-identity-retrieves-key-vault-secret.png)

### Key Vault Activity Log reviewed for role assignment and update evidence

The Key Vault Activity Log provided audit evidence of role assignment and update events related to the lab configuration.

![Key Vault Activity Log reviewed for role assignment and update evidence](screenshots/10-key-vault-activity-log-role-assignment-events.png)

## Skills Demonstrated

- Azure Key Vault deployment and configuration
- secure secret creation and management
- system assigned Managed Identity configuration
- Azure RBAC role assignment
- least privilege access design
- Key Vault Secrets Officer and Secrets User role usage
- SSH access to Linux virtual machines
- Azure CLI authentication with Managed Identity
- secure secret retrieval from a cloud workload
- Activity Log review for administrative evidence
- identity based access control for Azure resources
- reduction of hardcoded credential exposure

## Security Outcome

This implementation demonstrated a secure secret access model for Azure workloads.

The virtual machine was able to retrieve a Key Vault secret by using its system assigned Managed Identity rather than a stored username, password, or client secret. Access to the secret was controlled through Azure RBAC and limited to the required Key Vault role.

The result was a more secure and auditable secret management workflow aligned with real cloud security practice.
