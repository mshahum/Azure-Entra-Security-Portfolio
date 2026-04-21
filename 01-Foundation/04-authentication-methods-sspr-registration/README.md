# Self-Service Password Reset (SSPR) with Authentication Methods and Registration Campaign

## Overview

This project focused on improving identity resilience in Microsoft Entra ID by implementing **Self-Service Password Reset (SSPR)** for a controlled pilot group, enabling secure recovery methods, and validating the end user password reset experience through audit evidence.

Rather than treating password reset as a routine helpdesk function, this lab approached it as an important identity security control. A well designed SSPR rollout reduces dependency on manual support, shortens account recovery time, and gives users a secure way to regain access without weakening authentication standards.

The lab was built around a practical security objective: enabling password reset for a defined group of users, requiring stronger recovery methods, encouraging modern authentication registration, and confirming that the reset workflow completed successfully.

## Business Problem

Password related lockouts are one of the most common operational issues in real environments. When users cannot regain access quickly, productivity is interrupted and support teams absorb avoidable workload. At the same time, poorly designed reset processes can introduce security risk if recovery methods are weak, overly broad, or difficult to audit.

Organizations therefore need more than a basic password reset feature. They need a controlled rollout model, secure recovery methods, and clear visibility into what happened during the reset process.

This project addressed those needs by implementing SSPR in a way that reflected both **security discipline** and **operational practicality**.

## Project Objectives

The objectives of this lab were to:

- enable Self Service Password Reset for a defined pilot group
- configure secure authentication methods to support password recovery
- enable Microsoft Authenticator as a modern recovery option
- enable SMS as a backup recovery method
- use a registration campaign to encourage method enrollment
- test the end-user reset experience
- confirm reset activity through audit logs

## Technologies Used

- Microsoft Entra ID
- Self-Service Password Reset (SSPR)
- Authentication Methods Policy
- Microsoft Authenticator
- SMS Authentication
- Registration Campaign
- Microsoft Entra Groups
- Audit Logs

## What Was Implemented

### Pilot Group for Controlled Rollout

A dedicated group was created and populated with pilot users for the SSPR rollout. This allowed the feature to be introduced in a scoped and manageable way rather than enabling it broadly across the tenant from the start.

### Self Service Password Reset Policy

SSPR was enabled for the selected pilot group. This ensured that only the intended users could perform self service recovery while the environment remained controlled and easier to validate.

### Authentication Methods for Recovery

Microsoft Authenticator was enabled for the pilot group as a stronger and more modern recovery method. SMS was also enabled as a backup recovery option to provide additional resilience where needed.

Together, these settings reflected a practical balance between stronger authentication and operational flexibility.

### Registration Campaign

A registration campaign was configured to target the pilot group and prompt users to register Microsoft Authenticator. This added an important operational layer to the lab, because secure recovery depends not only on policy configuration but also on successful user enrollment.

### End User Reset Validation

The reset workflow was tested from the user perspective. This included the method registration prompt, verification through the configured recovery option, and successful password reset completion.

### Audit and Evidence Review

Finally, audit logs were reviewed to confirm that the password reset activity completed successfully. This provided administrative proof of the workflow and demonstrated the importance of visibility, traceability, and validation in identity operations.

## Validation and Testing

The implementation was validated through controlled testing and evidence review.

Validation included:

- confirming that the pilot users were added to the SSPR target group
- verifying that SSPR was enabled only for the selected group
- reviewing Microsoft Authenticator targeting for the pilot group
- reviewing SMS targeting as a backup recovery method
- confirming that the registration campaign targeted the correct group
- testing the end user password reset experience
- validating successful reset activity through audit logs

This approach reflects a stronger operational workflow: **configure, target, test, validate, and then expand with confidence**.

## Real World Use Case

In a real organization, this type of implementation would reduce helpdesk dependency for common account recovery issues while still ensuring that users can only reset passwords through approved and properly registered methods.

It provides a more resilient recovery process without weakening identity assurance.

## Why This Matters in Practice

This lab reflects several practical identity security realities.

First, password reset is not only a convenience feature. It is part of business continuity. When users can recover access securely and quickly, operational disruption is reduced.

Second, recovery methods matter. A reset capability is only as strong as the authentication methods behind it. Enabling Microsoft Authenticator improves the recovery experience while supporting stronger identity assurance.

Third, rollout strategy matters. Using a pilot group and a registration campaign shows how identity features can be introduced in a controlled and measurable way instead of being pushed blindly to all users.

Finally, audit visibility matters. Security teams need evidence that the process worked, which users were affected, and whether the activity completed successfully.

Together, these controls support a more mature identity protection and user recovery model.

## Implementation Evidence

### Pilot group membership for SSPR rollout
<img width="3200" height="1736" alt="01-sspr-pilot-group-members" src="https://github.com/user-attachments/assets/9b41a464-ffd3-4046-bdef-ea010f89f6d8" />

### SSPR enabled for the pilot group
<img width="3200" height="1730" alt="02-sspr-enabled-for-pilot-group" src="https://github.com/user-attachments/assets/17650ab2-28cf-42be-993f-810b8b089d6f" />

### Microsoft Authenticator enabled for the pilot group
<img width="3200" height="1730" alt="03-microsoft-authenticator-enabled-for-pilot-group" src="https://github.com/user-attachments/assets/1e90ffa7-5d9e-4ba0-8827-8e573e00b869" />

### SMS enabled as backup recovery method
<img width="3200" height="1730" alt="04-sms-enabled-as-backup-recovery-method" src="https://github.com/user-attachments/assets/5bba7ca3-8f1f-436d-8706-f2bab4cd5fc4" />

### Registration campaign targeted to the pilot group
<img width="3200" height="1728" alt="06-registration-campaign-targeted-to-pilot-group" src="https://github.com/user-attachments/assets/535cf184-22ec-4638-99e5-c8a1036c5a4d" />

### Audit log showing successful password reset activity
<img width="3200" height="1726" alt="10-sspr-audit-log-password-reset-success" src="https://github.com/user-attachments/assets/71bb5375-6b97-4eae-b9ba-be016f7ee980" />

## Skills Demonstrated

- Self Service Password Reset deployment
- scoped identity rollout using pilot groups
- authentication methods policy configuration
- Microsoft Authenticator targeting
- SMS recovery method configuration
- registration campaign planning
- audit log interpretation and evidence review
- operational identity security design

## Security Outcome

This implementation improved identity resilience by enabling a controlled self service recovery process backed by stronger verification methods and clear audit evidence.

The result was a more secure and operationally effective password reset model that reduced support dependency while preserving recovery assurance.
