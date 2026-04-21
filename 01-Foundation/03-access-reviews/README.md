# Access Reviews for Privileged Group Governance

## Overview

This project focused on strengthening identity governance in Microsoft Entra ID through the design, execution, and validation of an Access Review workflow for privileged group membership. The lab was built around a practical governance objective: ensuring that privileged group membership is reviewed on a recurring basis so that access remains limited to users who still have a valid business need.

Rather than treating Access Reviews as a compliance formality, this project approached them as an operational security control. In real environments, privileged access often accumulates over time. Without regular review, group membership can become outdated, excessive, or risky. This lab demonstrated how Microsoft Entra ID Access Reviews can be used to enforce accountability, support least privilege, and improve long term control over privileged access.

## Business Problem

Excess access is one of the most common weaknesses in identity governance. Users may retain privileged access long after their responsibilities have changed, especially when permissions are assigned through groups and not revisited on a regular basis. Over time, this creates unnecessary risk, weakens internal control, and increases the impact of account compromise or misuse.

Privileged groups require special attention because they often grant indirect access to high value roles, sensitive administrative actions, or broader control across the environment. If group membership is not reviewed periodically, organizations lose confidence that access remains justified.

This project addressed that challenge by creating a recurring access review for a privileged administrative group, assigning a reviewer, configuring review logic and notifications, validating the reviewer experience in the My Access portal, and confirming final approved outcomes inside Microsoft Entra ID.

## Project Objectives

The objectives of this lab were to:

- create an access review for a privileged administrative group
- assign a reviewer responsible for validating group membership
- configure recurrence, duration, notifications, and decision settings
- test the reviewer-side experience in the My Access portal
- validate review outcomes before and after reviewer action
- demonstrate how Access Reviews support stronger identity governance

## Technologies Used

- Microsoft Entra ID
- Identity Governance
- Access Reviews
- Microsoft Entra Groups
- My Access portal

## What Was Implemented

### Access Review for a Privileged Group

An access review was created for the **GRP-Privileged-Admins** group. This established a structured governance process to verify whether existing members should continue to retain access.

### Reviewer and Recurrence Configuration

A designated reviewer was selected, and the review was configured with a defined review duration and monthly recurrence. This reflects how real organizations operationalize governance as a repeated control rather than a one time manual check.

### Decision and Notification Settings

The review was configured with decision helpers, justification requirements, notifications, and reminders. These settings matter because an access review is only effective when it is usable, consistent, and auditable.

### Reviewer Validation Through My Access

The review was tested from the reviewer perspective through the My Access portal. This demonstrated how a reviewer sees recommendations, evaluates members, and records decisions.

### Result Validation

The review was validated both before and after reviewer action. This helped confirm the full lifecycle of the review, from creation to completion and final approved outcomes.

## Validation and Testing

The review was validated through a complete governance workflow rather than configuration alone.

Validation included:

- confirming the access review appeared in Microsoft Entra ID after creation
- reviewing the configured reviewer and recurrence settings
- validating that the access review became active
- testing the reviewer experience in the My Access portal
- confirming approved outcomes after reviewer action
- validating the final completed review summary

This reflects a realistic governance process: create, configure, activate, review, validate, and document.

## Real World Use Case

In a real organization, this type of review would be used to prevent privileged group membership from quietly remaining in place after a role change, project handoff, or shift in operational responsibility.

It provides a repeatable way to challenge whether elevated access is still appropriate rather than assuming it should continue indefinitely.

## Why This Matters in Practice

This lab reflects several governance realities that matter in production environments.

First, privileged access should never remain in place indefinitely without review. Even if access was originally justified, that does not mean it should continue forever without revalidation.

Second, group based administration is efficient, but it can also hide stale privilege when governance controls are weak. Access Reviews restore visibility and accountability.

Third, strong identity protection is not only about authentication and signin controls. It is also about continuously verifying who should have access in the first place. Access Reviews complement other security controls by reducing unnecessary standing privilege over time.

Together, these practices support a more disciplined, auditable, and defensible identity governance model.

## Implementation Evidence

### Access review listed after creation
<img width="1918" height="943" alt="02-access-review-list-created-review" src="https://github.com/user-attachments/assets/f6280b85-6920-4d0e-bfce-281c30dd967a" />

### Reviewer and recurrence settings
<img width="1919" height="943" alt="03-access-review-reviewer-and-recurrence-settings" src="https://github.com/user-attachments/assets/7b786f1a-4e92-4c66-bcb2-47f84a85ff41" />

### Active review overview
<img width="1917" height="942" alt="06-access-review-overview-active-review" src="https://github.com/user-attachments/assets/d82b64ea-b0ec-4350-8640-588dc10198f3" />

### Review performed by Security Admin
<img width="1913" height="989" alt="08-access-review-performed-by-security-admin" src="https://github.com/user-attachments/assets/00e52bdd-e99f-4b03-ab21-607dea4ebb1a" />

### Results after reviewer decision
<img width="1918" height="945" alt="09-access-review-results-after-decision" src="https://github.com/user-attachments/assets/33093196-44e9-4cc7-b631-efa64ca6c0cb" />

## Skills Demonstrated

- identity governance configuration
- access review design for privileged groups
- reviewer assignment and recurring review scheduling
- governance oriented access validation
- reviewer workflow testing through My Access
- interpretation of review results in Microsoft Entra ID

## Security Outcome

This implementation introduced a structured, recurring governance process for privileged group membership and reduced the risk of stale elevated access remaining in place without validation.

The result was stronger accountability, clearer reviewer ownership, and more defensible control over sensitive group based privilege.
