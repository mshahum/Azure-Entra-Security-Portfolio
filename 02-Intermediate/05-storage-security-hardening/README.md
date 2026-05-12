# Azure Storage Security Hardening

## Overview

This project focused on strengthening the security posture of an Azure Storage account by applying multiple storage hardening controls and validating that insecure or unauthorized access was blocked.

Rather than treating storage security as a single configuration setting, this lab approached it as a layered protection model. The objective was to secure blob storage by disabling anonymous access, enforcing HTTPS, maintaining a minimum TLS version, using a private container, and restricting public network access to a trusted IP address.

The lab was built around a practical cloud security scenario: a storage account contained internal files that should not be publicly accessible, should not be reachable over insecure HTTP, and should only be accessible from trusted network locations.

## Business Problem

Storage accounts often contain sensitive business data such as internal documents, logs, backups, exports, application files, and operational records. If storage is misconfigured, data can be exposed through anonymous access, insecure transport, overly broad public network access, or weak security settings.

A weak storage configuration can allow files to be accessed without authentication, transmitted over insecure HTTP, or reached from untrusted networks. These risks can lead to data leakage, compliance issues, unauthorized access, and loss of control over business information.

This project addressed that problem by applying storage security controls and validating the result through real access testing.

## Project Objectives

This lab was designed to:

- create an Azure Storage account for security hardening
- review baseline storage security settings
- confirm that blob anonymous access was disabled
- enforce secure transfer for storage access
- maintain minimum TLS version 1.2
- create a private blob container
- upload a test internal file to the private container
- test anonymous blob access from a browser
- test insecure HTTP access through PowerShell
- restrict storage public network access to a trusted IP address
- validate that access from an untrusted network was blocked

## Technologies Used

- Azure Storage Account
- Azure Blob Storage
- Azure Storage Containers
- Storage account networking
- Secure transfer required
- Minimum TLS version
- Public network access controls
- Trusted IP allow-listing
- Windows PowerShell
- curl.exe
- Browser based access testing

## What Was Implemented

### 1. Secure Storage Account Configuration

An Azure Storage account named `stsecurelab01` was created inside the resource group `RG-Storage-Security-Lab`.

The storage account was reviewed to confirm important baseline security settings, including secure transfer enforcement, disabled blob anonymous access, and minimum TLS version 1.2.

These settings helped establish a stronger security baseline before testing external access behavior.

### 2. Private Blob Container

A private container named `internal-documents` was created inside the storage account.

The container was configured with private access, meaning blobs inside the container could not be accessed anonymously from the public internet.

A test file named `Internal-file.txt` was uploaded to the container to simulate an internal business file that should remain protected.

### 3. Anonymous Access Protection

The blob URL was tested in an Incognito browser session to simulate unauthenticated public access.

The request was blocked with a `PublicAccessNotPermitted` error, confirming that anonymous blob access was not allowed for the storage account.

This demonstrated that public users could not directly access the blob without proper authorization.

### 4. Secure Transfer Enforcement

Secure transfer was enabled on the storage account to require HTTPS for storage access.

The HTTP version of the blob URL was tested using PowerShell and `curl.exe`. The request returned an `AccountRequiresHttps` error and confirmed that the storage account did not support insecure HTTP access.

This validated that insecure transport was blocked at the storage account level.

### 5. Network Access Restriction

Public network access was changed from broad access to selected network access.

The trusted public IP address was added to the storage account network rules:

```text
31.10.35.202
```

This restricted storage account access so that only approved network locations could reach the storage account through the public endpoint.

### 6. Untrusted Network Access Testing

Access was tested again from an untrusted network after network restrictions were applied.

The request failed with an `AuthorizationFailure` error, confirming that access from an unapproved network location was blocked.

This validated that the storage account network controls were enforcing the intended access boundary.

## Validation and Testing

The implementation was validated through browser-based and command-line testing.

First, the uploaded blob was tested through an Incognito browser session. The request returned a `PublicAccessNotPermitted` error, confirming that anonymous public access was blocked.

Second, insecure HTTP access was tested using PowerShell:

```powershell
curl.exe -v "http://stsecurelab01.blob.core.windows.net/internal-documents/Internal-file.txt"
```

The response returned an `AccountRequiresHttps` error and confirmed that the storage account did not support HTTP access.

This test was important because modern browsers may automatically upgrade HTTP requests to HTTPS, which can hide whether secure transfer enforcement is working. PowerShell testing provided clearer validation of the HTTP block.

Finally, network access was restricted to a trusted IP address, and access from an untrusted network was tested. The request returned an `AuthorizationFailure` error, confirming that untrusted network access was blocked.

The validation confirmed:

- blob anonymous access was disabled
- the container was private
- unauthenticated browser access was blocked
- secure transfer was enforced
- insecure HTTP access was denied
- minimum TLS version was configured as TLS 1.2
- public network access was restricted to a trusted IP
- access from an untrusted network was blocked

## Real World Use Case

In a real organization, Azure Storage may be used to store internal documents, application files, exports, backups, logs, or sensitive operational data.

If a storage account is left open to anonymous access or broad public network access, sensitive files may be exposed. If insecure HTTP is allowed, data may be transmitted without proper transport protection.

A stronger design uses private containers, disables anonymous blob access, enforces HTTPS, maintains a secure TLS baseline, and limits network access to trusted locations.

For example, an organization storing internal finance exports in Azure Blob Storage could use these controls to ensure that files are not publicly available, cannot be accessed over HTTP, and are reachable only from trusted office or administrative networks.

## Why This Matters in Practice

This lab reflects an important cloud security principle: storage accounts should be hardened before sensitive data is placed inside them.

Storage misconfiguration is one of the most common causes of cloud data exposure. A storage account may appear simple, but it contains several settings that directly affect data confidentiality, transport security, and network exposure.

Disabling anonymous access protects against unauthenticated data exposure. Secure transfer enforcement protects data in transit. Minimum TLS settings help maintain a stronger cryptographic baseline. Network restrictions reduce exposure by limiting where storage access can originate.

By combining these controls, this lab demonstrated a defense in depth approach to Azure Storage security.

## Implementation Evidence

### Storage account created with security baseline visible

The storage account was created and reviewed with key security settings visible, including secure transfer, disabled anonymous blob access, and minimum TLS version 1.2.

<img width="3200" height="1566" alt="01-storage-account-created-overview" src="https://github.com/user-attachments/assets/67bf95be-1f09-49e0-b249-badcb0c38e20" />

### Private container with internal file uploaded

A private container named `internal-documents` was created, and a test file named `Internal-file.txt` was uploaded for access validation.

<img width="3200" height="1164" alt="04-private-container-blob-uploaded" src="https://github.com/user-attachments/assets/e0c8fa36-0dd4-4a63-872d-c9083f00ce6b" />

### Anonymous blob access blocked

Unauthenticated browser access to the blob was blocked with a `PublicAccessNotPermitted` error.

<img width="3200" height="1028" alt="06-anonymous-blob-access-blocked" src="https://github.com/user-attachments/assets/ffcb80fe-7ac4-4038-960a-8a759208a553" />

### Insecure HTTP access blocked by secure transfer enforcement

PowerShell testing confirmed that HTTP access was blocked with an `AccountRequiresHttps` response.

<img width="3198" height="1148" alt="07-secure-transfer-http-blocked-powershell" src="https://github.com/user-attachments/assets/12ad94de-37f7-4c41-8ff5-bd6e45f4e71f" />

### Storage network access restricted to trusted IP

Public network access was restricted to selected networks, with only the trusted public IP address allowed.

<img width="3200" height="1718" alt="08-storage-network-access-restricted-to-trusted-ip" src="https://github.com/user-attachments/assets/79e77645-704d-4c07-a643-33092c9c8d96" />

### Access blocked from untrusted network

Access from an untrusted network was blocked with an `AuthorizationFailure` error, confirming that the storage network restriction was enforced.

<img width="3196" height="782" alt="09-storage-access-blocked-from-untrusted-network" src="https://github.com/user-attachments/assets/b9f2c073-da28-4558-90ad-803c496dbbd0" />

## Skills Demonstrated

- Azure Storage account configuration
- Azure Blob Storage security hardening
- private container configuration
- anonymous access restriction
- secure transfer enforcement
- TLS baseline review
- public network access restriction
- trusted IP allow-listing
- browser-based access testing
- PowerShell and curl-based validation
- storage access troubleshooting
- interpretation of Azure Storage authorization errors
- defense-in-depth storage security design

## Security Outcome

This implementation demonstrated a layered Azure Storage security model.

The storage account blocked anonymous blob access, enforced HTTPS, maintained a minimum TLS baseline, and restricted public network access to a trusted IP address. Validation testing confirmed that unauthenticated access, insecure HTTP access, and untrusted network access were blocked.

The result was a hardened storage configuration that reduced data exposure risk, strengthened transport security, and improved control over where storage access could originate.
