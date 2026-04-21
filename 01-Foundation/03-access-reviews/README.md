# Access Reviews for Privileged Group Governance

## Overview
This project focused on strengthening identity governance in Microsoft Entra ID by designing and validating an access review process for a privileged administrative group.

The lab was built around a practical security objective: ensuring that privileged group membership is reviewed on a recurring basis so that access remains limited to users who still have a valid business need.

Rather than treating access reviews as a compliance checkbox, this project approached them as an operational security control that helps reduce privilege creep, improve accountability, and support stronger governance over sensitive identities.

## Business Context
Privileged access is one of the highest-risk areas in any identity environment. Even when strong controls such as Conditional Access, multifactor authentication, and Privileged Identity Management are in place, access can still become excessive over time if it is not reviewed regularly.

Users may change responsibilities, move to different teams, or retain access that is no longer justified. If privileged memberships are left unchecked, organizations create unnecessary exposure and weaken the principle of least privilege.

Access reviews help address this problem by introducing a structured process for validating whether elevated access should still be retained. In practice, this allows security teams to move from one-time access assignment toward ongoing access governance.

This project demonstrates that process by reviewing a privileged admin group, assigning a reviewer, configuring recurring review settings, and validating the review lifecycle from creation through final decision.

## Project Objectives
The objectives of this lab were to:

- create an access review for a privileged administrative group
- assign a reviewer responsible for validating group membership
- configure recurring review settings and governance options
- validate the reviewer experience through the My Access portal
- confirm that review decisions were recorded successfully in Microsoft Entra ID

## Technologies Used
- Microsoft Entra ID
- Identity Governance
- Access Reviews
- Microsoft Entra Groups
- My Access portal

## What Was Implemented

### Access Review for a Privileged Group
An access review was created for a privileged administrative group to ensure that membership could be reviewed on a recurring basis rather than remaining unchecked over time.

This is important because privileged groups often provide indirect access to highly sensitive roles, permissions, or administrative capabilities. Reviewing those memberships helps reduce standing risk and strengthens governance over elevated access.

### Reviewer Assignment and Review Scheduling
The review was configured with a designated reviewer and a recurring schedule. This ensured that the review process was not a one-time event, but part of an ongoing governance cycle.

This kind of configuration reflects real operational practice, where access decisions should be revisited periodically rather than assumed to remain valid indefinitely.

### Governance and Decision Settings
Additional review settings were configured to support more structured governance, including decision guidance and review behavior options.

These settings matter because they shape how consistently access reviews are performed and how much administrative confidence exists in the review outcomes.

### Reviewer-Side Validation
The review was then validated from the reviewer perspective through the My Access portal. This step confirmed that the assigned reviewer could see the review, evaluate the listed group members, and perform approval actions as expected.

Testing from the reviewer side is important because it verifies that the review is not only configured correctly in the admin center, but is also operationally usable by the person responsible for the decision.

### Outcome Validation
After the review was completed, the results were checked in Microsoft Entra ID to confirm that review decisions were recorded successfully.

This completed the full lifecycle of the lab: creation, configuration, activation, reviewer action, and final result validation.

## Validation and Testing
The lab was validated through a structured sequence of checks:

- confirming that the access review appeared in Microsoft Entra ID after creation
- reviewing the configured reviewer and recurrence settings
- verifying that the access review became active
- validating the reviewer experience in the My Access portal
- confirming that final review decisions were captured successfully in the results view

This approach reflects a realistic governance workflow: define the review scope, assign accountability, execute the review, and verify the recorded outcome.

## Why This Matters in Practice
This lab reflects several identity governance realities that matter in real organizations.

First, privileged access should not remain trusted indefinitely. Even when access was originally justified, that does not mean it should continue forever without review.

Second, governance controls are most effective when they are repeatable. A recurring access review process creates a structured mechanism for checking whether sensitive access is still appropriate over time.

Third, access governance is not only about technical configuration. It also depends on decision ownership, reviewer accountability, and evidence that reviews were actually completed.

Together, these practices support stronger least-privilege enforcement, improved audit readiness, and a more disciplined identity security posture.

## Key Screenshots

### 1. Access Review Listed After Creation
This screenshot shows the newly created access review for the privileged admin group.

<img width="1918" height="943" alt="02-access-review-list-created-review" src="https://github.com/user-attachments/assets/cbe0de6e-8110-4599-9f70-6d81615b1e56" />

### 2. Reviewer and Recurrence Settings
This screenshot shows the reviewer assignment, review duration, and recurring schedule for the privileged group review.

<img width="1919" height="943" alt="03-access-review-reviewer-and-recurrence-settings" src="https://github.com/user-attachments/assets/be911665-ca28-47ea-a9fa-9d1de4bbe264" />

### 3. Active Review Overview
This screenshot shows the access review after activation, including the review scope and governance details.

<img width="1917" height="942" alt="06-access-review-overview-active-review" src="https://github.com/user-attachments/assets/3e9c15e2-a764-470b-947b-17e8a2594f11" />


### 4. Review Performed by Security Admin
This screenshot shows the reviewer-side experience in the My Access portal, where the assigned reviewer evaluates privileged group membership.

<img width="1913" height="989" alt="08-access-review-performed-by-security-admin" src="https://github.com/user-attachments/assets/f8de7e24-715a-407f-b963-8ea461fa4674" />


### 5. Results After Reviewer Decision
This screenshot shows the final approved outcomes after the reviewer completed the access review.

<img width="1918" height="945" alt="09-access-review-results-after-decision" src="https://github.com/user-attachments/assets/ed1c625c-6c83-4da9-b3ee-72f2379bea14" />


## Skills Demonstrated
- identity governance configuration
- access review design for privileged groups
- reviewer assignment and recurring review scheduling
- governance-oriented access validation
- reviewer workflow testing through My Access
- interpretation of review results in Microsoft Entra ID

## Outcome
This project demonstrated how Microsoft Entra ID Access Reviews can be used to strengthen governance over privileged group membership through structured, recurring validation.

It showed how a privileged group review can be created, assigned, tested, and completed in a way that supports least-privilege principles and improves long-term control over sensitive access.

More broadly, the lab highlights that strong identity security is not only about granting and protecting access, but also about reviewing access continuously to ensure it remains justified.
