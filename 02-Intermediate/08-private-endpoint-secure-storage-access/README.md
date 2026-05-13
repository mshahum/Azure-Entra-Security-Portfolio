# Azure Private Endpoint for Secure Storage Access

## Overview

This project focused on securing Azure Storage access by using Azure Private Endpoint, Private DNS, and virtual network-based connectivity.

Rather than allowing the storage account to depend on public network access, this lab created a private access path through an Azure Virtual Network. A private endpoint was configured for the storage account Blob service, a Private DNS zone was linked to the virtual network, and a test virtual machine was used to validate private DNS resolution and private connectivity.

The lab was built around a practical enterprise scenario: sensitive storage should remain accessible to approved internal Azure workloads while reducing direct public network exposure.

## Business Problem

Azure Storage accounts often contain sensitive business data such as internal files, backups, logs, reports, application data, and operational records. If these storage accounts are reachable through public endpoints, they become part of the public attack surface.

Even when authentication is required, organizations may still want sensitive storage accounts to be reachable only through private network paths. This is especially important for regulated workloads, internal applications, backup systems, and environments where public exposure must be minimized.

This project addressed that problem by using Azure Private Endpoint to give the storage account a private IP address inside an Azure Virtual Network, then disabling public network access after private connectivity was validated.

## Project Objectives

This lab was designed to:

- create a dedicated resource group for the private endpoint lab
- create a virtual network with separate workload and private endpoint subnets
- deploy an Azure Storage Account for private access testing
- create a Private Endpoint for the storage account Blob service
- assign a private IP address to the storage account through Private Link
- configure a Private DNS zone for Blob Storage private endpoint resolution
- link the Private DNS zone to the virtual network
- deploy a test virtual machine inside the workload subnet
- validate that the storage account resolves to a private IP from inside the VNet
- test HTTPS connectivity to the storage account through the private endpoint
- disable public network access on the storage account
- confirm private access still works after public access is disabled
- test the public path from outside the VNet to confirm it is not the approved access route

## Technologies Used

- Azure Storage Account
- Azure Blob Storage
- Azure Private Endpoint
- Azure Private Link
- Azure Virtual Network
- Azure Subnets
- Azure Private DNS Zone
- Azure Virtual Machine
- Ubuntu Linux
- SSH
- DNS resolution testing
- `nslookup`
- `curl`
- Azure Portal

## What Was Implemented

### 1. Private Endpoint Lab Resource Group

A dedicated resource group named `RG-PrivateEndpoint-Lab` was created to organize the resources used in this lab.

This kept the virtual network, subnets, storage account, private endpoint, Private DNS zone, and test virtual machine grouped together under a controlled lab scope.

### 2. Virtual Network and Subnet Design

A virtual network named `VNET-PrivateEndpoint-Lab` was created in Canada Central with the address space:

```text
10.30.0.0/16
```

Two subnets were created inside the virtual network:

```text
Subnet-Workload:        10.30.1.0/24
Subnet-PrivateEndpoint: 10.30.2.0/24
```

The workload subnet was used for the test virtual machine. The private endpoint subnet was used for the storage account private endpoint.

This separation reflects a cleaner enterprise network design pattern where application workloads and private service access points are placed in separate network segments.

### 3. Storage Account for Private Access

A storage account named `stpeblob01` was created as the protected Azure service.

The storage account represented a sensitive storage service that should be reachable privately by approved internal workloads rather than accessed directly through the public network path.

### 4. Private Endpoint for Blob Storage

A Private Endpoint named `pe-stpeblob-blob` was created for the Blob sub-resource of the storage account.

The private endpoint was placed inside:

```text
VNET-PrivateEndpoint-Lab / Subnet-PrivateEndpoint
```

The private endpoint connection was approved successfully, and Azure created a private network interface for the storage account Blob service.

### 5. Private IP Address Assignment

The private endpoint received the private IP address:

```text
10.30.2.4
```

This private IP became the private access point for the storage account Blob service inside the virtual network.

In practice, this means approved internal workloads can reach the storage account through a private IP path instead of relying on the public endpoint.

### 6. Private DNS Configuration

A Private DNS zone was created for Blob Storage private endpoint resolution:

```text
privatelink.blob.core.windows.net
```

An A record was created for the storage account:

```text
stpeblob01 -> 10.30.2.4
```

The Private DNS zone was linked to:

```text
VNET-PrivateEndpoint-Lab
```

This DNS configuration allowed resources inside the virtual network to resolve the storage account name to the private endpoint IP address.

### 7. Test Virtual Machine inside the Workload Subnet

A Linux virtual machine named `VM-PrivateEndpoint-Test` was deployed inside:

```text
VNET-PrivateEndpoint-Lab / Subnet-Workload
```

The VM received the private IP address:

```text
10.30.1.4
```

This VM acted as an internal workload used to test DNS resolution and private connectivity to the storage account.

### 8. Private DNS Resolution from the VM

After connecting to the VM through SSH, DNS resolution was tested using:

```bash
nslookup stpeblob01.blob.core.windows.net
```

The result showed that the storage account resolved through the Private Link DNS name:

```text
stpeblob01.privatelink.blob.core.windows.net
```

and returned the private endpoint IP address:

```text
10.30.2.4
```

This confirmed that the Private DNS zone was working correctly for resources inside the virtual network.

### 9. Private Connectivity Testing

HTTPS connectivity to the storage account was tested from inside the VM using:

```bash
curl -v https://stpeblob01.blob.core.windows.net
```

The output showed that the VM connected to:

```text
10.30.2.4:443
```

This confirmed that the VM was reaching the storage account through the private endpoint path.

### 10. Public Network Access Disabled

After private DNS and private connectivity were validated, public network access was disabled on the storage account.

This reduced public exposure and ensured the storage account was no longer intended to be accessed through the normal public network path.

### 11. Private Access Validation after Public Access Was Disabled

After disabling public network access, connectivity was tested again from inside the VM.

The VM continued to connect to the storage account through:

```text
10.30.2.4:443
```

This confirmed that private endpoint access still worked even after public network access was disabled.

### 12. Public Path Access Test

A public path test was performed from outside the virtual network.

The public side test resolved the storage account to a public Azure Storage IP and returned an authorization failure response. This confirmed that the public path was not the approved access route after the private endpoint design was implemented.

## Validation and Testing

The implementation was validated through DNS and connectivity testing from inside the virtual network.

First, the test VM was used to confirm that the storage account name resolved to the private endpoint IP address:

```bash
nslookup stpeblob01.blob.core.windows.net
```

The result showed:

```text
stpeblob01.privatelink.blob.core.windows.net
10.30.2.4
```

This proved that Private DNS resolution was working.

Next, connectivity was tested from the VM using:

```bash
curl -v https://stpeblob01.blob.core.windows.net
```

The output showed that the VM connected to:

```text
10.30.2.4:443
```

This proved that the storage account was being reached through the private endpoint IP.

After public network access was disabled on the storage account, the same private connectivity test was repeated from the VM. The VM still connected through `10.30.2.4:443`, proving that private access continued to work after public access was removed.

The validation confirmed:

- the private endpoint was created and approved
- the private endpoint received IP address `10.30.2.4`
- the Private DNS zone contained the correct storage account record
- the Private DNS zone was linked to the virtual network
- the VM resolved the storage account name to the private endpoint IP
- the VM connected to the storage account through the private endpoint
- public network access was disabled
- private access still worked after public access was disabled
- the external/public path was not the approved access route

## Real World Use Case

In a real organization, sensitive storage accounts may contain internal business documents, audit files, application data, logs, or backups.

A company may not want these services to be directly reachable through the public internet. Instead, internal workloads such as application servers, automation hosts, or backup systems should access storage through a private network path.

For example, a finance application running on an Azure VM may need to store and retrieve files from Azure Blob Storage. With a Private Endpoint, that application can access the storage account through a private IP inside the Azure virtual network. Public network access can then be disabled to reduce exposure.

This design is commonly used in enterprise landing zones, regulated environments, internal application platforms, and security sensitive storage architectures.

## Why This Matters in Practice

This lab reflects an important cloud security principle: sensitive platform services should not be unnecessarily exposed to public networks.

Private Endpoint improves the security posture by giving Azure services a private IP address inside the virtual network. Private DNS allows internal workloads to use the normal service hostname while resolving it to the private endpoint IP. Disabling public network access reduces public exposure and forces access through the approved private path.

This matters in real environments because identity permissions alone are not always enough. A stronger architecture combines identity controls, private networking, DNS control, and public exposure reduction.

By implementing and validating Private Endpoint access, this lab demonstrated an enterprise style approach to securing Azure Storage connectivity.

## Implementation Evidence

### Virtual network and dedicated subnets created

The virtual network was created with separate workload and private endpoint subnets.

<img width="3200" height="1012" alt="02-vnet-subnets-created" src="https://github.com/user-attachments/assets/b10aa037-8ca4-4018-9893-39c9937dce99" />

### Private Endpoint created and approved

The Private Endpoint was created for the storage account Blob service, and the connection was approved successfully.

<img width="3200" height="1104" alt="06-private-endpoint-created-and-approved" src="https://github.com/user-attachments/assets/8e876de9-ae31-47b5-b32b-874666281b3e" />

### Private Endpoint IP and DNS configuration reviewed

The Private Endpoint DNS configuration showed the storage account mapped to the private endpoint IP address `10.30.2.4`.

<img width="3200" height="1502" alt="07-private-endpoint-private-ip-and-dns-configured" src="https://github.com/user-attachments/assets/cc6aca9f-e785-4dea-ad4c-dabc09645553" />

### Private DNS record created for storage account

The Private DNS zone contained an A record mapping `stpeblob01` to `10.30.2.4`.

<img width="3182" height="1162" alt="08-private-dns-record-created-for-storage" src="https://github.com/user-attachments/assets/a0dc6f35-588e-4dce-b20a-3fde9d2f1682" />

### Private DNS zone linked to the virtual network

The Private DNS zone was linked to `VNET-PrivateEndpoint-Lab` so internal resources could resolve the storage account privately.

<img width="3200" height="1058" alt="09 - private-dns-zone-linked-to-vnet" src="https://github.com/user-attachments/assets/d65e7b25-8dde-44f0-a746-790edd97a41a" />

### Storage account resolved to private IP from the VM

From inside the test VM, the storage account hostname resolved to the Private Link DNS name and private IP address `10.30.2.4`.

<img width="2684" height="422" alt="12-private-dns-resolves-storage-to-private-ip" src="https://github.com/user-attachments/assets/2d10b4fd-6351-49b8-981c-b70ca3741558" />

### VM connected to storage through the Private Endpoint

The test VM connected to the storage account through the private endpoint IP address on port 443.

<img width="2406" height="1420" alt="13-vm-connects-to-storage-through-private-endpoint" src="https://github.com/user-attachments/assets/c87c4f68-e130-4e46-b3de-ed022667e337" />

### Public network access disabled on storage account

Public network access was disabled on the storage account after private endpoint connectivity was validated.

<img width="3200" height="1240" alt="14-storage-public-network-access-disabled" src="https://github.com/user-attachments/assets/032bd5c5-646d-4259-b6d6-7d80f346cdfe" />

### Private access continued after public access was disabled

After public network access was disabled, the VM still connected to the storage account through `10.30.2.4:443`.

<img width="1856" height="366" alt="15-private-access-works-after-public-access-disabled" src="https://github.com/user-attachments/assets/0619a1ed-f598-4f74-a8c5-23d62a6b004b" />

### Public path access blocked after Private Endpoint configuration

A public-side test returned an authorization failure response, confirming that the external/public route was not the approved access path.

<img width="2860" height="1074" alt="16-public-path-access-blocked-after-private-endpoint" src="https://github.com/user-attachments/assets/1fd7261f-aaf0-4323-aa8d-4285d2b91a6d" />

## Skills Demonstrated

- Azure Virtual Network design
- subnet planning for workload and private endpoint resources
- Azure Storage Account deployment
- Azure Private Endpoint configuration
- Azure Private Link implementation
- Private DNS zone configuration
- DNS record validation
- virtual network link configuration
- Linux VM deployment for internal testing
- SSH-based validation workflow
- `nslookup` testing for private DNS resolution
- `curl` testing for private endpoint connectivity
- public network access restriction
- private access validation after public access removal
- secure Azure storage networking architecture

## Security Outcome

This implementation demonstrated a secure private access model for Azure Storage.

The storage account was connected to the virtual network through a Private Endpoint and assigned the private IP address `10.30.2.4`. Private DNS was configured so that internal workloads resolved the storage account name to the private endpoint IP. A test VM inside the virtual network validated both DNS resolution and HTTPS connectivity through the private endpoint.

After public network access was disabled, private connectivity continued to work from inside the VNet. This confirmed that the storage account could remain accessible to approved internal workloads while reducing public exposure.

The result was an enterprise style storage access architecture based on private connectivity, controlled DNS resolution, and reduced public network attack surface.
