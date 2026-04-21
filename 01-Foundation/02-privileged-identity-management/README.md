# Privileged Identity Management (PIM) for Entra Roles and Azure Resources

## Overview

This project focused on reducing standing privilege and improving administrative control through Microsoft Entra Privileged Identity Management (PIM). The lab was designed around a practical security objective: replacing persistent privileged access with time bound, just-in-time elevation for both Microsoft Entra roles and Azure resource roles.

Rather than treating PIM as a feature that only manages role assignments, this project approached it as an operational security control. The implementation demonstrated how organizations can limit unnecessary privilege exposure, require stronger activation conditions, and build a more defensible model for administrative access.

## Business Problem

Permanent administrative access creates avoidable risk. When privileged roles remain active all the time, compromise of a single account can lead directly to broad control over identity systems, cloud resources, or both. This increases the blast radius of credential theft, insider misuse, and session hijacking.

Modern security programs try to reduce that risk by ensuring that privileged access is granted only when needed, for a limited time, and under defined conditions. That is the core value of Privileged Identity Management.

This project addressed that problem in two practical areas:

- Microsoft Entra role governance
- Azure resource role governance

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
- Microsoft Entra role settings and assignment controls

## What Was Implemented

### PIM for Microsoft Entra Roles

Privileged Identity Management was used to manage access to Microsoft Entra roles. A test identity was assigned the **Global Reader** role as an **eligible** assignment rather than permanent access. This reflected the principle that even lower-risk administrative roles should not remain active unnecessarily when just-in-time access is available.

The role configuration was then reviewed to confirm that activation settings supported stronger operational control, including limited activation duration and additional requirements at activation time.

### Entra Role Activation Validation

The eligible Microsoft Entra role was then activated to confirm that the access model worked as intended. This validated the transition from **eligible** to **active**, which is central to how PIM reduces standing privilege.

### PIM for Azure Resources

The project also extended beyond Entra roles into Azure resource governance. Within Azure resource scope, an eligible **Contributor** assignment was configured for a dedicated test user against the **RG-PIM-Lab** resource group.

This is an important distinction because identity privilege and resource privilege are often managed separately in real environments.

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

## Real World Use Case

In a real Azure environment, this setup would allow administrators to hold no standing privileged access until a maintenance, support, or governance task actually required elevation.

That reduces exposure if an account is compromised outside of the activation window and improves accountability around when privileged access is used.

## Why This Matters in Practice

This lab reflects several important security realities.

First, privileged access should not remain active by default. Permanent role assignments create unnecessary exposure and make it easier for attackers to convert a single compromised identity into wider administrative control.

Second, privileged access governance must extend beyond directory roles. In real cloud environments, risk also exists at the subscription, resource group, and workload levels. Securing only Entra roles while leaving Azure resource roles permanently active would be incomplete.

Third, PIM is valuable because it introduces friction where friction is appropriate. Time limits, activation requirements, and explicit elevation workflows reduce casual misuse and improve control over high impact access.

Together, these controls support a more mature least privilege model and a stronger operational security posture.

## Implementation Evidence

### PIM overview for Entra roles
<img width="3200" height="1530" alt="01-pim-control-plane-overview" src="https://github.com/user-attachments/assets/f5395337-9f3b-4558-b2d0-1a2933d98c11" />

### Eligible Global Reader assignment
<img width="3200" height="1414" alt="02-pim-eligible-global-reader-assignment" src="https://github.com/user-attachments/assets/5f601ef8-20dd-4d6a-b08c-2eb1ce9e7fd1" />

### Global Reader role settings
<img width="3200" height="1728" alt="03-global-reader-role-settings" src="https://github.com/user-attachments/assets/42f2039b-66a4-462b-92ee-192c3f543a0b" />

### Global Reader role activated
<img width="1919" height="466" alt="04-global-reader-role-activated" src="https://github.com/user-attachments/assets/e06f03d4-a329-4a76-922f-2b165cb221c8" />

### Azure resource role assigned through PIM
<img width="3196" height="1730" alt="06-resource-group-role-assigned-to-pim-user" src="https://github.com/user-attachments/assets/5124b2f3-73eb-4ef9-ac2b-6cf49f9f49c8" />

### Contributor role settings for Azure resource
<img width="3200" height="1730" alt="07-contributor-role-settings-for-azure-resource" src="https://github.com/user-attachments/assets/dad278db-fe23-422f-907e-507a2025ff19" />

### Contributor activation pane
<img width="1919" height="938" alt="09-contributor-role-activation-pane" src="https://github.com/user-attachments/assets/a41b2f7b-cac1-4477-a1f7-84a25dfe68c2" />

### Contributor role activated on resource group
<img width="1919" height="947" alt="10-contributor-role-activated-on-resource-group" src="https://github.com/user-attachments/assets/b561e4cc-e95a-4c11-ba96-cfd45d1392b6" />

## Skills Demonstrated

- Privileged Identity Management configuration
- just-in-time privileged access design
- eligible versus active role assignment handling
- Microsoft Entra role governance
- Azure resource privilege governance
- privileged access validation and testing
- role setting analysis for activation control
- least privilege security implementation

## Security Outcome

This implementation reduced standing privilege and strengthened administrative control across both identity and cloud resource layers.

The result was a more controlled just-in-time access model in which privileged roles could be assigned as **eligible**, activated only when needed, and governed through stronger operational settings.
