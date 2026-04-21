# Self-Service Password Reset (SSPR) with Authentication Methods and Registration Campaign

## Overview

This project focused on improving identity resilience in Microsoft Entra ID by implementing **Self-Service Password Reset (SSPR)** for a controlled pilot group, enabling secure recovery methods, and validating the end-user password reset experience through audit evidence.

Rather than treating password reset as a routine helpdesk function, this lab approached it as an important identity security control. A well-designed SSPR rollout reduces dependency on manual support, shortens account recovery time, and gives users a secure way to regain access without weakening authentication standards.

The lab was built around a practical security objective: enabling password reset for a defined group of users, requiring stronger recovery methods, encouraging modern authentication registration, and confirming that the reset workflow completed successfully.

---

## Business Context

Password-related lockouts are one of the most common operational issues in real environments. When users cannot regain access quickly, productivity is interrupted and support teams absorb avoidable workload. At the same time, poorly designed reset processes can introduce security risk if recovery methods are weak, overly broad, or difficult to audit.

Organizations therefore need more than a basic password reset feature. They need a controlled rollout model, secure recovery methods, and clear visibility into what happened during the reset process.

This project addresses those needs by implementing SSPR in a way that reflects both **security discipline** and **operational practicality**.

---

## Project Objectives

The objectives of this lab were to:

- enable Self-Service Password Reset for a defined pilot group
- configure secure authentication methods to support password recovery
- enable Microsoft Authenticator as a modern recovery option
- enable SMS as a backup recovery method
- use a registration campaign to encourage method enrollment
- validate the end-user reset experience from registration through successful password recovery
- confirm reset activity through audit logs

---

## Technologies Used

- Microsoft Entra ID
- Self-Service Password Reset (SSPR)
- Authentication Methods Policy
- Microsoft Authenticator
- SMS Authentication
- Registration Campaign
- Microsoft Entra Groups
- Audit Logs

---

## What Was Implemented

### Pilot Group for Controlled Rollout

A dedicated group was created and populated with pilot users for the SSPR rollout. This allowed the feature to be introduced in a scoped and manageable way rather than enabling it broadly across the tenant from the start.

This is important in real environments because identity controls should be tested with a limited audience before wider deployment.

### Self-Service Password Reset Policy

SSPR was enabled for the selected pilot group through the password reset policy. This ensured that only the intended users could perform self-service recovery, while the environment remained controlled and easier to validate.

The configuration demonstrated how password reset can be introduced gradually without affecting every user at once.

### Authentication Methods for Recovery

To support secure recovery, authentication methods were configured for the pilot group.

**Microsoft Authenticator** was enabled as a modern recovery method to strengthen the reset process and align with stronger identity verification practices.

**SMS** was also enabled as a backup method to provide an additional recovery path where appropriate.

Together, these settings reflected a more realistic design: primary reliance on a stronger modern method, with a secondary method available for resilience.

### Registration Campaign

A registration campaign was configured to target the pilot group and prompt users to register Microsoft Authenticator. This added an important operational layer to the lab, because secure recovery depends not only on policy configuration but also on successful user enrollment.

The campaign demonstrated how organizations can drive adoption of stronger authentication methods without relying entirely on manual user communication.

### End-User Password Reset Validation

The reset workflow was tested from the user perspective. This included the method registration prompt, verification through the configured recovery option, and successful password reset completion.

This stage was essential because it showed that the design worked not only in the administrator view, but also in the actual user experience.

### Audit and Evidence Review

Finally, audit logs were reviewed to confirm that the password reset activity completed successfully. This provided administrative proof of the reset workflow and demonstrated the importance of visibility, traceability, and validation in identity operations.

---

## Validation and Testing

The implementation was validated through controlled testing and evidence review.

Validation included:

- confirming that the pilot users were added to the SSPR target group
- verifying that SSPR was enabled only for the selected group
- reviewing Microsoft Authenticator targeting for the pilot group
- reviewing SMS targeting as a backup recovery method
- confirming that the registration campaign targeted the correct group
- testing the end-user password reset experience
- validating successful reset activity through audit logs

This approach reflects a stronger operational workflow: **configure, target, test, validate, and then expand with confidence**.

---

## Why This Matters in Practice

This lab reflects several practical identity security realities.

First, password reset is not only a convenience feature. It is part of business continuity. When users can recover access securely and quickly, operational disruption is reduced.

Second, recovery methods matter. A reset capability is only as strong as the authentication methods behind it. Enabling Microsoft Authenticator improves the recovery experience while supporting stronger identity assurance.

Third, rollout strategy matters. Using a pilot group and a registration campaign shows how identity features can be introduced in a controlled and measurable way instead of being pushed blindly to all users.

Finally, audit visibility matters. Security teams need evidence that the process worked, which users were affected, and whether the activity completed successfully.

Together, these controls support a more mature identity protection and user recovery model.

---

## Key Screenshots

### 1. Pilot Group Membership for SSPR Rollout
Shows the dedicated pilot group used to scope the SSPR deployment.

<img width="3200" height="1736" alt="01-sspr-pilot-group-members" src="https://github.com/user-attachments/assets/97e331ac-789a-4a36-ada3-cdcb9997dc73" />

### 2. SSPR Enabled for the Pilot Group
Shows that self-service password reset was enabled only for the selected pilot group.

<img width="3200" height="1730" alt="02-sspr-enabled-for-pilot-group" src="https://github.com/user-attachments/assets/ba08af3a-f316-4a4e-abd8-669bbbdd9a86" />

### 3. Microsoft Authenticator Enabled for the Pilot Group
Shows Microsoft Authenticator configured as a recovery method for the pilot users.

<img width="3200" height="1730" alt="03-microsoft-authenticator-enabled-for-pilot-group" src="https://github.com/user-attachments/assets/f58ca4b2-18d8-4c53-90b8-9f69ce0d66ba" />

### 4. SMS Enabled as Backup Recovery Method
Shows SMS configured as a secondary recovery option for the same pilot group.

<img width="3200" height="1730" alt="04-sms-enabled-as-backup-recovery-method" src="https://github.com/user-attachments/assets/f9ef2017-c1e3-410c-bc51-5d6c44015996" />

### 5. Registration Campaign Targeted to the Pilot Group
Shows the registration campaign configuration used to encourage enrollment in modern authentication methods.

<img width="3200" height="1728" alt="06-registration-campaign-targeted-to-pilot-group" src="https://github.com/user-attachments/assets/d1d7675e-70e1-4781-b84f-1026fcace992" />

### 6. Audit Log Showing Successful Password Reset Activity
Shows the audit evidence confirming that the password reset workflow completed successfully.

<img width="3200" height="1726" alt="10-sspr-audit-log-password-reset-success" src="https://github.com/user-attachments/assets/c3bea664-b25c-422f-8b98-0878a401ad95" />

---

## Skills Demonstrated

- Self-Service Password Reset deployment
- scoped identity rollout using pilot groups
- authentication methods policy configuration
- Microsoft Authenticator targeting
- SMS recovery method configuration
- registration campaign planning
- end-user identity recovery validation
- audit log interpretation and evidence review
- operational identity security design

---

## Outcome

This project demonstrated how Microsoft Entra ID can be used to deliver a more secure and operationally effective password recovery process through **Self-Service Password Reset**, **modern authentication method targeting**, and **controlled user onboarding**.

It also showed the value of combining policy configuration with user registration strategy and audit validation, which is critical when deploying identity features in a real environment.
