# Conditional Access and MFA for Identity Protection

## Overview

This project focused on strengthening identity security in Microsoft Entra ID through the design, testing, and validation of Conditional Access controls. The lab was built around a practical security objective: protecting privileged access, reducing exposure to legacy authentication, and evaluating how access policies respond to sign-ins from untrusted locations.

Rather than treating Conditional Access as a routine administrative feature, this project approached it as a core security control that directly influences how organizations protect sensitive identities, reduce avoidable access risk, and deploy access restrictions responsibly.

---

## Business Context

Administrative and high-privilege accounts remain among the most attractive targets in identity-based attacks. When these accounts rely only on passwords, or when legacy authentication remains available in the environment, organizations are left more exposed to credential theft, password spraying, and sign-in attempts that bypass stronger modern protections.

At the same time, security teams cannot afford to deploy access policies carelessly. A policy that is technically correct but operationally disruptive can create lockouts, user friction, or service interruptions if introduced without proper validation.

This lab addressed both concerns by implementing Conditional Access controls in a way that reflected real security priorities while also respecting safe rollout practice.

---

## Project Objectives

This lab was designed to:

- require multi-factor authentication for privileged access
- block legacy authentication protocols
- evaluate sign-ins from untrusted locations
- validate policy behavior through sign-in logs and report-only testing
- demonstrate how Conditional Access supports a stronger identity protection strategy

---

## Technologies Used

- Microsoft Entra ID
- Conditional Access
- Microsoft Entra administrative roles
- Named Locations
- Sign-in Logs
- Audit Logs

---

## Lab Setup and Identity Preparation

Before creating access policies, the environment was prepared with test identities, administrative role assignments, security groups, and baseline identity settings. This allowed each Conditional Access control to be tested in a structured and realistic way.

The lab included privileged administrative identities, standard user accounts, a break glass account for emergency access, and supporting groups used for policy targeting and exclusions.

### Supporting Evidence

**Security defaults disabled before Conditional Access rollout**

<img width="1919" height="943" alt="01-security-defaults-disabled-for-conditional-access" src="https://github.com/user-attachments/assets/297bc8ed-071c-4d89-bc30-94c01dfb0fef" />


**Lab identities created in Microsoft Entra ID**

<img width="1918" height="689" alt="02-users-created-lab-identities" src="https://github.com/user-attachments/assets/5ab59818-5971-4dac-85f8-d7197935d235" />


**Security groups created for targeting and exclusions**

<img width="1918" height="623" alt="03-groups-created-for-role-targeting-and-exclusions" src="https://github.com/user-attachments/assets/7cc702b3-ba4d-4c40-9070-edc692df282b" />


**Authentication methods baseline reviewed**

<img width="1919" height="705" alt="09-authentication-methods-policy-overview" src="https://github.com/user-attachments/assets/aa4d8bda-b2e5-4a57-9b81-34ca6d49674a" />

---

## What Was Implemented

### 1. MFA for Privileged Roles

A Conditional Access policy was created to require multi-factor authentication for privileged roles. This control was designed to reduce the likelihood of unauthorized administrative access by ensuring that sensitive identities were not protected by passwords alone.

To make the control operationally safe, the break glass account was excluded from the policy. This reflects a common enterprise practice in which emergency administrative access is preserved in case of policy misconfiguration or unexpected lockout.

### Validation

Testing focused on privileged sign-in activity and the Conditional Access results recorded in Microsoft Entra sign-in logs. The objective was to confirm that targeted administrative accounts were evaluated correctly and that stronger authentication requirements were enforced as intended.

### Supporting Evidence

**CA01 created to require MFA for privileged roles**

<img width="946" height="775" alt="10-ca01-policy-overview-with-break-glass-exclusion" src="https://github.com/user-attachments/assets/305803c6-f733-42ab-b4c6-b7f9b8009099" />

**Grant control configured to require multifactor authentication**

<img width="1918" height="847" alt="11-ca01-grant-require-mfa" src="https://github.com/user-attachments/assets/47b7785b-6bed-4d44-9bae-d8c4915d65e7" />

**Policy visible in Conditional Access policies list**

<img width="1724" height="581" alt="12-ca01-policy-enabled" src="https://github.com/user-attachments/assets/8390f94c-52c1-4eaa-ba3d-19e61f8aa078" />

**Sign-in evidence showing privileged access evaluation**

<img width="3200" height="1740" alt="15-ca01-sign-in-details-success-security-admin" src="https://github.com/user-attachments/assets/672a82e2-c8c8-4ec3-86a1-a4903fd8749a" />

---

### 2. Blocking Legacy Authentication

A separate Conditional Access policy was created to block legacy authentication. This is an important defensive control because older authentication protocols do not support modern safeguards such as MFA and are frequently associated with password-based attack activity.

The policy was configured in a way that targeted legacy client authentication methods while maintaining a safer rollout posture through testing and validation.

### Validation

Policy behavior was reviewed in sign-in logs to confirm whether legacy authentication attempts were being identified correctly and whether the Conditional Access logic would respond as expected. This step was essential because legacy authentication controls are highly valuable, but they must be verified carefully before enforcement in production.

### Supporting Evidence

**CA02 policy created in report-only mode**

<img width="841" height="945" alt="18-ca02-policy-overview-report-only" src="https://github.com/user-attachments/assets/8de3a9a1-53b6-42a5-9774-4cfb28340798" />

**Break glass account excluded from CA02**

<img width="869" height="943" alt="19-ca02-break-glass-exclusion" src="https://github.com/user-attachments/assets/3bae9416-da1c-43bc-a566-82108168a306" />

**All cloud apps selected as target resources**

<img width="882" height="946" alt="20-ca02-target-all-cloud-apps" src="https://github.com/user-attachments/assets/d955e306-5ca9-4c74-bd4f-fcf81f4e83df" />

**Legacy client apps selected for blocking**

<img width="1917" height="947" alt="21-ca02-client-apps-legacy-auth-selected" src="https://github.com/user-attachments/assets/bdb0de57-bcaf-4de0-8cd8-9fa54b389cc3" />

**Block access configured as the grant control**

<img width="1919" height="945" alt="22-ca02-grant-block-access" src="https://github.com/user-attachments/assets/6dfb1cb0-e9a7-4afc-9fae-27722704c1c0" />

**Policy confirmed in Conditional Access policy list**

<img width="1627" height="940" alt="23-ca02-policy-listed-report-only" src="https://github.com/user-attachments/assets/bee46d1e-e7cd-4dcb-b9c2-aa07dd55c577" />

**Sign-in evidence with client app visibility for validation**

<img width="1916" height="941" alt="24-ca02-sign-in-log-client-app-column" src="https://github.com/user-attachments/assets/194bd38a-efcb-4e4e-b515-be7d71070efd" />

---

### 3. Access Evaluation from Untrusted Locations

A location-based Conditional Access policy was also created using a trusted named location. This allowed the lab to evaluate how sign-in attempts from outside the trusted network would be treated.

The policy was structured so that trusted access from the approved location could be excluded, while sign-ins originating from outside that location could be evaluated separately. This reflects how organizations often apply location-aware controls to reduce unnecessary exposure without disrupting expected internal access paths.

### Validation

Rather than enforcing the policy immediately, report-only testing was used to observe how the policy would behave during sign-in activity from less trusted locations. This allowed the impact to be studied safely before full enforcement.

### Supporting Evidence

**Trusted named location created using home lab IP**

<img width="3200" height="1726" alt="25-ca03-create-trusted-home-lab-ip-named-location" src="https://github.com/user-attachments/assets/3121f64d-c4be-4199-9257-37d3348ba156" />

**CA03 created to block untrusted locations**

<img width="2192" height="1728" alt="26-ca03-policy-overview-report-only" src="https://github.com/user-attachments/assets/09a714ff-05ce-4d6a-aead-5b22861e3fcb" />

**Break glass account excluded from CA03**

<img width="1998" height="1728" alt="27-ca03-break-glass-exclusion" src="https://github.com/user-attachments/assets/f46c1645-e38e-4b8e-b935-0a3bb11573e8" />

**Network condition configured for location-based evaluation**

<img width="1958" height="1724" alt="28-ca03-network-include-any-location" src="https://github.com/user-attachments/assets/8a17b34f-916b-441a-9041-d559bc821c16" />

**Trusted named location excluded from the policy scope**

<img width="2014" height="1732" alt="29-ca03-network-exclude-trusted-home-lab-ip" src="https://github.com/user-attachments/assets/b1694d19-f085-4a2b-9b2a-00f26a7eea14" />

**Block access configured as the control**

<img width="3194" height="1728" alt="30-ca03-grant-block-access" src="https://github.com/user-attachments/assets/cec7bb8b-7d15-4ba7-9a33-8143046e5bba" />

**Sign-in log reviewed for location-based behavior**

<img width="3200" height="1724" alt="31-ca03-report-only-failure-global-admin-untrusted-location" src="https://github.com/user-attachments/assets/53df473f-d902-4eec-9bf7-f89704233a9c" />

**Activity details confirmed report-only failure from untrusted access**

<img width="3200" height="1726" alt="33-ca03-sign-in-details-report-only-failure" src="https://github.com/user-attachments/assets/bcc5ee1a-1a7f-4f9d-af80-cc8a7377ce4e" />

---

## Validation and Testing Approach

The policies were tested through controlled sign-in activity and structured log review. Rather than enabling every control immediately, the lab used report-only evaluation where appropriate so policy impact could be observed safely before full enforcement.

Validation included:

- reviewing Conditional Access results in sign-in logs
- checking whether privileged access policies applied as expected
- examining legacy authentication-related sign-in behavior
- testing sign-ins originating outside the trusted location
- confirming report-only outcomes through Microsoft Entra activity details
- reviewing audit log evidence for policy creation and administrative changes

This reflects a more realistic security workflow: design, test, validate, and then enforce with confidence.

---

## Audit and Administrative Evidence

In addition to sign-in validation, administrative activity was reviewed through audit logs. This provided supporting evidence that user creation, group membership updates, and Conditional Access policy creation had been carried out successfully during the lab.

### Supporting Evidence

**User creation activity recorded in audit logs**

<img width="3198" height="1720" alt="35-audit-log-add-user" src="https://github.com/user-attachments/assets/4d5ebe7d-66af-46e6-a8c4-bdd34817b5e6" />

**Group membership changes recorded in audit logs**

<img width="3200" height="1724" alt="36-audit-log-add-member-to-group" src="https://github.com/user-attachments/assets/a07d007f-7b1e-4590-b43e-bf2dd2e11f5d" />

**Conditional Access policy creation recorded in audit logs**

<img width="2526" height="1188" alt="34-audit-log-conditional-access-policies-created" src="https://github.com/user-attachments/assets/c5fe839e-1300-4204-8c2e-705445f3cc3f" />

---

## Why This Matters in Practice

This lab reflects several security realities that matter in real environments.

First, privileged accounts should never be treated like ordinary user accounts. The potential impact of administrative compromise is far greater, so these identities require stronger and more deliberate protection.

Second, legacy authentication remains one of the most avoidable weaknesses in many identity environments. Blocking it is often one of the most practical steps an organization can take to reduce unnecessary exposure.

Third, Conditional Access is most effective when deployed with operational discipline. Report-only mode is not merely a convenience feature; it is a practical safeguard that allows security teams to understand the likely effect of a policy before enabling enforcement.

Taken together, these controls contribute to a more resilient and defensible identity security posture.

---

## Skills Demonstrated

- Conditional Access policy design
- MFA enforcement for sensitive identities
- privileged access protection
- legacy authentication risk reduction
- location-based access control
- sign-in log interpretation
- audit log review
- identity security validation and testing

---

## Outcome

This project demonstrated how Microsoft Entra Conditional Access can be used to strengthen identity protection through a combination of role-based MFA enforcement, legacy authentication blocking, and location-aware access evaluation.

It also showed the importance of validating access controls through sign-in monitoring before moving to full enforcement, which is a critical part of deploying identity security controls responsibly in a live environment.

---

## Evidence and Validation Screenshots

Selected screenshots are embedded throughout this README to show the main implementation and validation stages of the lab. Additional supporting screenshots, including intermediate configuration screens and duplicate validation views, can be stored in the `screenshots/` folder for reference without overloading the main project page.
