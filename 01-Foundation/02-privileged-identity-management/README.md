# Privileged Identity Management (PIM) for Entra Roles and Azure Resources

## Overview

This project focused on reducing standing privilege and improving administrative control through Microsoft Entra Privileged Identity Management (PIM). The lab was designed around a practical security objective: replacing persistent privileged access with time-bound, just-in-time elevation for both Microsoft Entra roles and Azure resource roles.

Rather than treating PIM as a feature that only manages role assignments, this project approached it as an operational security control. The implementation demonstrated how organizations can limit unnecessary privilege exposure, require stronger activation conditions, and create a more defensible model for administrative access.

## Business Context

Permanent administrative access creates avoidable risk. When privileged roles remain active all the time, compromise of a single account can lead directly to broad control over identity systems, cloud resources, or both. This expands the blast radius of credential theft, insider misuse, and session hijacking.

Modern security programs try to reduce that risk by ensuring that privileged access is granted only when needed, for a limited time, and under defined conditions. That is the core value of Privileged Identity Management.

This project addressed that problem in two practical areas:

- Microsoft Entra role governance
- Azure resource role governance

By applying PIM across both control planes, the lab showed how privileged access can be restricted, activated only when necessary, and validated through visible role state changes.

## Project Objectives

The objectives of this lab were to:

- configure Privileged Identity Management for Microsoft Entra roles
- assign an Entra role as **eligible** instead of permanently active
- validate activation behavior for an Entra administrative role
- configure PIM for Azure resource roles
- assign an Azure resource role as **eligible** at resource group scope
- test just-in-time activation for Azure resource access
- review role settings that govern duration, MFA, and justification requirements
- demonstrate the difference between eligible and active privileged access

## Technologies Used

- Microsoft Entra ID
- Privileged Identity Management (PIM)
- Microsoft Entra roles
- Azure role-based access control (Azure RBAC)
- Azure Resource Groups
- Role activation workflows
- Microsoft Entra audit and assignment views

## What Was Implemented

### PIM for Microsoft Entra Roles

Privileged Identity Management was used to manage access to Microsoft Entra roles. A test identity was assigned the **Global Reader** role as an **eligible** assignment rather than permanent access. This reflected the principle that even lower-risk administrative roles should not remain active unnecessarily when just-in-time access is available.

The role configuration was then reviewed to confirm that activation settings supported stronger operational control, including limited activation duration and additional requirements at activation time.

### Entra Role Activation Validation

The eligible Microsoft Entra role was then activated to confirm that the access model worked as intended. This validated the transition from **eligible** to **active**, which is central to how PIM reduces standing privilege.

This part of the lab demonstrated that access can remain dormant until required, which is more secure than leaving administrative permissions continuously available.

### PIM for Azure Resources

The project also extended beyond Entra roles into Azure resource governance. Within Azure resource scope, an eligible **Contributor** assignment was configured for a dedicated test user against the **RG-PIM-Lab** resource group.

This is an important distinction because identity privilege and resource privilege are often managed separately in real environments. Demonstrating both in one project shows a broader understanding of privileged access governance.

### Azure Resource Role Settings and Activation

The Contributor role settings were reviewed to confirm how activation was governed at the Azure resource layer. The lab then validated activation through the PIM user experience, including the role activation pane and the final active assignment state.

This showed how organizations can allow operational access to cloud resources without assigning those permissions permanently.

## Validation and Testing

The lab was validated by reviewing assignment state, role settings, and activation outcomes across both Entra and Azure resource scopes.

Validation included:

- confirming that the **Global Reader** role was assigned as **eligible**
- reviewing role settings for the Entra role
- activating the Entra role and confirming it became active
- confirming that the **Contributor** role was assigned as **eligible** at resource group scope
- reviewing role settings for the Azure resource role
- activating the Azure resource role through the PIM workflow
- confirming that the Azure resource role became active after activation

This approach demonstrated not only configuration, but also the operational effect of the controls.

## Why This Matters in Practice

This lab reflects several important security realities.

First, privileged access should not remain active by default. Permanent role assignments create unnecessary exposure and make it easier for attackers to convert a single compromised identity into wider administrative control.

Second, privileged access governance must extend beyond directory roles. In real cloud environments, risk also exists at the subscription, resource group, and workload levels. Securing only Entra roles while leaving Azure resource roles permanently active would be incomplete.

Third, PIM is valuable because it introduces friction where friction is appropriate. Time limits, activation requirements, and explicit elevation workflows reduce casual misuse and improve control over high-impact access.

Together, these controls support a more mature least-privilege model and a stronger operational security posture.

## Key Screenshots

The following screenshots in the main README demonstrate the clearest story without overwhelming the page:

### 1. PIM overview for Entra roles

<img width="3200" height="1530" alt="01-pim-control-plane-overview" src="https://github.com/user-attachments/assets/e7d1bf9c-9929-487d-94df-42528545ea1b" />

### 2. Eligible Global Reader assignment

<img width="3200" height="1414" alt="02-pim-eligible-global-reader-assignment" src="https://github.com/user-attachments/assets/1d015ba1-4047-46a8-b0f2-862bc6de3ee9" />

### 3. Global Reader role settings

<img width="3200" height="1728" alt="03-global-reader-role-settings" src="https://github.com/user-attachments/assets/2369e98e-bc78-45a1-858f-e6a4ca91c399" />

### 4. Global Reader role activated

<img width="1919" height="466" alt="04-global-reader-role-activated" src="https://github.com/user-attachments/assets/374a4326-77f1-4059-b91e-e106454a51ae" />

### 5. Azure resource role assigned through PIM

<img width="3196" height="1730" alt="06-resource-group-role-assigned-to-pim-user" src="https://github.com/user-attachments/assets/6503155f-f131-4a7c-9ddc-b513ab11d597" />

### 6. Contributor role settings for Azure resource

<img width="3200" height="1730" alt="07-contributor-role-settings-for-azure-resource" src="https://github.com/user-attachments/assets/bf2c4257-0297-424a-88d4-4c13ce07576a" />

### 7. Contributor activation pane

<img width="1919" height="938" alt="09-contributor-role-activation-pane" src="https://github.com/user-attachments/assets/fad6faf0-ac57-4967-a383-ed6f41bbdb25" />

### 8. Contributor role activated on resource group

<img width="1919" height="947" alt="10-contributor-role-activated-on-resource-group" src="https://github.com/user-attachments/assets/61cfc610-446b-4536-b0cb-951160c5093f" />

## Skills Demonstrated

- Privileged Identity Management configuration
- just-in-time privileged access design
- eligible versus active role assignment handling
- Microsoft Entra role governance
- Azure resource privilege governance
- privileged access validation and testing
- role setting analysis for activation control
- least-privilege security implementation

## Outcome

This project demonstrated how Microsoft Entra Privileged Identity Management can be used to reduce standing privilege and strengthen administrative control across both identity and cloud resource layers.

It showed how privileged access can be assigned as **eligible**, activated only when needed, and governed through role settings that support tighter operational control. It also demonstrated that effective privileged access management should cover both Microsoft Entra roles and Azure resource roles rather than treating them as separate security concerns.

Overall, the lab reflects a practical and security-focused approach to privileged access governance in Microsoft cloud environments.
