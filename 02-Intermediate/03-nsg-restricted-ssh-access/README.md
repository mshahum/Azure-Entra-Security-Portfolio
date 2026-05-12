# Restricting SSH Access with Network Security Groups

## Overview

This project focused on reducing public administrative exposure to an Azure virtual machine by using a Network Security Group to restrict SSH access to a trusted public IP address.

Rather than allowing SSH access from the entire internet, this lab implemented a more controlled network access model. The objective was to demonstrate how inbound management access can be limited through explicit allow and deny rules.

The lab was built around a practical security scenario: a Linux virtual machine required SSH access for administration, but that access needed to be restricted so only a trusted source IP could connect.

## Business Problem

Virtual machines exposed to the public internet are common targets for brute force attempts, password spraying, vulnerability scanning, and unauthorized login attempts.

A weak configuration allows SSH access from any public IP address. Even if SSH keys are used instead of passwords, leaving port 22 open to the internet increases the attack surface and creates unnecessary exposure.

This project addressed that problem by using a Network Security Group to allow SSH only from a trusted public IP address and deny SSH from all other internet sources.

## Project Objectives

This lab was designed to:

- create a dedicated resource group for the NSG lab
- create a virtual network and workload subnet
- deploy a Linux virtual machine inside the subnet
- create a Network Security Group for access control
- associate the NSG with the workload subnet
- allow SSH access only from a trusted public IP address
- deny SSH access from all other internet sources
- validate successful SSH access from the trusted IP
- validate failed SSH access from an untrusted network

## Technologies Used

- Microsoft Azure
- Azure Virtual Network
- Azure Subnet
- Azure Virtual Machine
- Network Security Group
- Inbound Security Rules
- SSH
- Windows PowerShell
- Ubuntu Linux

## What Was Implemented

### 1. Network Foundation

A dedicated resource group named `RG-NSG-Lab` was created to organize the lab resources.

A virtual network named `VNET-NSG-Lab` was created with the address space `10.0.0.0/16`. A workload subnet named `Subnet-Workload` was created with the address range `10.0.1.0/24`.

This provided a controlled network foundation for hosting the test virtual machine.

### 2. Linux Virtual Machine Deployment

A Linux virtual machine named `vm-nsg-lab` was deployed inside the workload subnet.

The VM was configured with SSH key authentication. During initial deployment, SSH was available so the VM could be accessed for testing. The VM later became the target resource for NSG-based access restriction.

### 3. Network Security Group Creation

A Network Security Group named `NSG-VM-Access-Control` was created to control inbound network access.

The NSG was associated with the workload subnet so its rules would apply to resources inside that subnet, including the test virtual machine.

### 4. Trusted IP SSH Allow Rule

An inbound security rule named `Allow-SSH-From-My-IP` was created.

This rule allowed TCP port `22` only from the trusted public IP address:

```text
31.10.35.202/32
```

Using `/32` restricted the rule to one specific public IP address rather than allowing a wider network range.

### 5. Internet SSH Deny Rule

A second inbound security rule named `Deny-SSH-From-Internet` was created to deny SSH traffic from all other internet sources.

The trusted IP allow rule was given a higher priority than the deny rule. This allowed SSH from the approved IP while blocking SSH from untrusted sources.

This rule structure created a cleaner security model:

```text
Trusted IP → SSH allowed
Other internet sources → SSH denied
```

## Validation and Testing

The implementation was validated through controlled SSH testing.

First, SSH access was tested from the trusted public IP address. The connection succeeded, confirming that the allow rule was working correctly.

Then SSH access was tested from an untrusted network. The connection failed with a timeout, confirming that the deny rule was blocking SSH traffic from unauthorized sources.

The validation confirmed:

- the VM was deployed inside the intended workload subnet
- the NSG was associated with the subnet
- SSH was allowed only from the trusted public IP
- SSH from untrusted sources was denied
- inbound rule priority worked as expected
- administrative access was restricted without removing legitimate access

## Real  World Use Case

In a real organization, administrators may need SSH access to Linux virtual machines for support, maintenance, patching, or troubleshooting.

However, allowing SSH from the entire internet is risky. Attackers continuously scan public IP ranges for open management ports such as SSH and RDP.

A stronger design restricts management access to trusted sources such as:

- corporate office public IPs
- VPN egress IPs
- jump boxes
- bastion hosts
- approved administrator networks

This lab demonstrates that pattern by allowing SSH only from a known trusted IP and denying SSH from everywhere else.

## Why This Matters in Practice

This lab reflects an important cloud security principle: management ports should not be broadly exposed to the internet.

Even when SSH keys are used, open SSH access increases the attack surface. Restricting inbound access at the network layer reduces unnecessary exposure and makes unauthorized access attempts less likely to reach the VM.

Network Security Groups provide an important layer of defense because they control traffic before it reaches the virtual machine. They help enforce basic network segmentation and administrative access control.

By combining a specific allow rule with a broader deny rule, this lab demonstrated how Azure network security controls can be used to protect administrative access in a practical environment.

## Implementation Evidence

### Virtual network and workload subnet created

A virtual network and workload subnet were created to host the test virtual machine in a controlled network environment.

<img width="3196" height="1730" alt="02-vnet-and-subnet-created" src="https://github.com/user-attachments/assets/dc7eedda-d7ad-4174-b833-8e14af2f9fc7" />

### Virtual machine deployed and running

The Linux virtual machine was deployed successfully inside the workload subnet and used as the target for SSH access testing.

<img width="3200" height="1732" alt="09-vm-deployed-and-running" src="https://github.com/user-attachments/assets/4214ec38-073b-4bc5-9069-ecb57a14f3dd" />

### NSG associated with the workload subnet

The Network Security Group was associated with the workload subnet so the inbound security rules applied to the virtual machine.

<img width="3200" height="1048" alt="10-nsg-associated-with-workload-subnet" src="https://github.com/user-attachments/assets/557b7923-5a34-4e9d-aa42-706da3ba6c1c" />

### SSH allowed from trusted IP and denied from the internet

The NSG inbound rules allowed SSH from the trusted public IP and denied SSH from other internet sources.

<img width="3200" height="994" alt="13-nsg-allow-trusted-ip-and-deny-internet-rules" src="https://github.com/user-attachments/assets/e8bfa97a-10d0-4491-b7d4-0de67db5fd45" />

### SSH access succeeded from the trusted IP

SSH access to the VM succeeded from the trusted public IP, confirming that authorized administrative access was still available.

<img width="2564" height="1382" alt="14-ssh-access-success-from-trusted-ip" src="https://github.com/user-attachments/assets/96b78283-be5d-4997-bb0b-ca061bebe8a1" />

### SSH access denied from an untrusted network

SSH access from an untrusted network failed with a connection timeout, confirming that unauthorized SSH traffic was blocked.

<img width="2756" height="1318" alt="15-ssh-access-denied-from-untrusted-network" src="https://github.com/user-attachments/assets/cac082d2-b021-433b-b03a-d1242874c30c" />

## Skills Demonstrated

- Azure Virtual Network configuration
- subnet creation and resource placement
- Azure virtual machine deployment
- Network Security Group creation
- NSG subnet association
- inbound security rule configuration
- SSH access restriction
- trusted IP allow listing
- deny rule implementation
- rule priority understanding
- network access validation
- administrative exposure reduction
- troubleshooting SSH connectivity

## Security Outcome

This implementation demonstrated how Azure Network Security Groups can reduce public administrative exposure to virtual machines.

SSH access was restricted to a trusted public IP address, while SSH from untrusted internet sources was denied. The successful and failed SSH tests confirmed that the NSG rules were enforcing the intended access boundary.

The result was a more secure administrative access model that preserved legitimate SSH access while reducing exposure to unauthorized internet based connection attempts.
