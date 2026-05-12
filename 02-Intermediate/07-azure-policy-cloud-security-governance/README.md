# Enforcing Cloud Security Governance with Azure Policy

## Overview

This project focused on using Azure Policy to enforce a basic cloud governance control across Azure resources.

The lab implemented a policy assignment that required resources inside a specific lab scope to include an `Owner` tag. The purpose was to demonstrate how Azure Policy can be used to enforce organizational standards before or during resource deployment.

Instead of relying on users to manually remember tagging requirements, Azure Policy was used as a governance guardrail. If a resource was created without the required tag, Azure blocked or flagged the deployment. When the required tag was added, the resource became compliant.

## Business Problem

Cloud environments can quickly become difficult to manage when resources are created without consistent ownership, naming, tagging, or security standards.

A missing owner tag may look small, but in real organizations it creates serious operational problems. Security, finance, and platform teams may not know who owns a resource, which team is responsible for it, whether it is still needed, or who should approve changes.

This can affect incident response, cost management, audit readiness, and accountability.

This project addressed that problem by using Azure Policy to enforce an `Owner` tag requirement at the resource group scope.

## Project Objectives

This lab was designed to:

- create a dedicated governance lab resource group
- review Azure Policy compliance from the Azure portal
- assign a built-in Azure Policy definition
- require an `Owner` tag on resources within the lab scope
- test resource creation without the required tag
- confirm policy enforcement blocked or flagged the missing tag
- create a compliant storage account with the required tag
- validate policy compliance after successful deployment
- demonstrate governance enforcement using Azure Policy

## Technologies Used

- Azure Policy
- Azure Policy Assignments
- Azure Policy Compliance
- Azure Resource Groups
- Azure Storage Account
- Azure Tags
- Azure Governance
- Azure Portal
- Policy enforcement mode

## What Was Implemented

### 1. Governance Lab Resource Group

A dedicated resource group named `RG-Policy-Governance-Lab` was used as the scope for the policy assignment.

Scoping the policy to a specific resource group kept the lab controlled and avoided applying governance rules across the entire subscription.

This is an important enterprise practice because Azure Policy should be assigned carefully based on the intended governance boundary.

### 2. Azure Policy Review

Azure Policy was reviewed from the Azure portal to understand the policy compliance dashboard and assignment area.

The Azure Policy dashboard provided a central view of compliance state, policy assignments, and governance recommendations.

This step helped establish where cloud governance controls are configured and monitored.

### 3. Required Tag Policy Assignment

A policy assignment named `POLICY-Require-Owner-Tag` was created.

The assignment used a policy definition that required resources in the lab scope to include an `Owner` tag. The parameter value was configured as:

```text
Owner
```

This meant that resources inside the policy scope were expected to include an `Owner` tag before they could be considered compliant.

### 4. Policy Scope Configuration

The policy assignment was scoped to:

```text
Azure for Students / RG-Policy-Governance-Lab
```

This ensured the policy applied only to resources created inside the governance lab resource group.

Using a scoped assignment avoided unnecessary impact on unrelated resources in the subscription.

### 5. Non-Compliant Deployment Test

A storage account was created without providing the required `Owner` tag.

Azure Policy detected that the required tag was missing and showed a validation error during the storage account creation process.

This confirmed that the policy was actively enforcing the governance rule.

### 6. Compliant Storage Account Deployment

A second storage account was created with the required `Owner` tag.

The tag was configured as:

```text
Owner : SecurityAdmin
```

After the required tag was added, the storage account deployment succeeded and appeared as compliant under the policy compliance results.

### 7. Policy Compliance Validation

The policy compliance page showed the storage account as compliant.

The compliance result confirmed that the assigned policy was working as expected and that the resource met the required governance condition.

## Validation and Testing

The policy was validated by testing both a failed and successful deployment scenario.

First, a storage account was created without the required `Owner` tag. Azure Policy detected the missing tag and produced a validation error. This showed that the policy was enforcing governance requirements instead of relying on manual review.

Second, a compliant storage account was created with the required `Owner` tag. The storage account was successfully deployed with:

```text
Owner : SecurityAdmin
```

Finally, Azure Policy compliance was reviewed. The policy compliance result showed the resource as compliant, proving that the policy assignment correctly evaluated the storage account against the required tag rule.

The validation confirmed:

- the policy assignment was created successfully
- the policy was scoped to the governance lab resource group
- the `Owner` tag was required by policy
- resource creation without the required tag was blocked or flagged
- resource creation with the required tag succeeded
- the compliant storage account appeared in Azure Policy compliance results

## Real World Use Case

In a real cloud environment, Azure Policy is commonly used to enforce governance standards across subscriptions, management groups, and resource groups.

Examples include requiring owner tags, enforcing allowed regions, blocking public IP addresses, requiring diagnostic settings, restricting insecure storage configurations, and ensuring resources follow organizational security baselines.

For example, a company may require every resource to include:

```text
Owner
CostCenter
Environment
Application
DataClassification
```

Without policy enforcement, users may forget to apply these tags. With Azure Policy, the organization can automatically enforce standards and improve accountability.

This lab demonstrates a simple but realistic governance use case: ensuring every resource has an accountable owner.

## Why This Matters in Practice

Azure Policy is important because cloud security is not only about configuring one resource securely. It is also about enforcing standards consistently across the environment.

Manual governance does not scale. In a real company, many users, teams, and automation pipelines may create resources. Without policy, misconfigurations and missing metadata can spread quickly.

Azure Policy helps prevent that by applying rules at scale.

This lab matters because it shows how governance can be built into the deployment process. Instead of finding missing tags later, Azure Policy enforces the requirement when the resource is created or evaluated.

This improves:

- accountability
- audit readiness
- cost tracking
- operational ownership
- security governance
- cloud compliance posture

## Implementation Evidence

### Policy assignment created

The policy assignment was created inside Azure Policy and scoped to the governance lab resource group.

<img width="3200" height="1108" alt="03-policy-assignment-created" src="https://github.com/user-attachments/assets/46bc023a-1f64-4613-923b-0cada0ecf14f" />

### Owner tag configured as a policy parameter

The policy assignment required the tag name `Owner`, ensuring that resources in scope must include ownership metadata.

<img width="3198" height="1116" alt="04-policy-assignment-owner-tag-parameter" src="https://github.com/user-attachments/assets/741eead1-48ca-4c0b-bdff-98b914099eff" />

### Storage account creation failed without the required tag

A storage account deployment was tested without the required `Owner` tag. Azure Policy detected the missing tag and showed a validation error.

<img width="3200" height="826" alt="06- policy-validation-missing-owner-tag" src="https://github.com/user-attachments/assets/521f0200-19bb-4352-ae47-664c1ad51542" />

### Compliant storage account created with Owner tag

A storage account was successfully created after adding the required `Owner : SecurityAdmin` tag.

<img width="3198" height="1732" alt="07-compliant-storage-account-created-with-owner-tag" src="https://github.com/user-attachments/assets/928f19df-9426-47d8-815b-f2615dc9d214" />

### Policy compliance result validated

Azure Policy compliance showed the storage account as compliant after it was created with the required tag.

<img width="3200" height="1464" alt="08-policy-compliance-result-owner-tag" src="https://github.com/user-attachments/assets/abd81cfc-0277-4195-8d1e-7309923601cb" />

## Skills Demonstrated

- Azure Policy assignment
- cloud governance implementation
- policy scope management
- tag-based governance
- resource compliance validation
- policy enforcement testing
- storage account deployment testing
- Azure Policy compliance review
- governance control validation
- cloud accountability controls
- audit and compliance evidence collection
- Azure portal governance workflow

## Security Outcome

This implementation demonstrated how Azure Policy can enforce cloud governance requirements across Azure resources.

A policy assignment was created to require an `Owner` tag within the lab resource group. Resource deployment without the required tag was blocked or flagged, while a storage account created with the required `Owner : SecurityAdmin` tag passed validation and appeared as compliant.

The result was a practical governance control that improved accountability, resource ownership, audit readiness, and cloud compliance posture.
