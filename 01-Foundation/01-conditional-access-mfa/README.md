# Conditional Access and MFA for Identity Protection

## Overview

This project focused on strengthening identity security in Microsoft Entra ID through the design, testing, and validation of Conditional Access controls. The lab was built around a practical security objective: protecting privileged access, reducing exposure to legacy authentication, and evaluating how access policies respond to sign-ins from untrusted locations.

Rather than treating Conditional Access as a routine administrative feature, this project approached it as a core security control that directly influences how organizations protect sensitive identities, reduce avoidable access risk, and deploy access restrictions responsibly.

## Business Problem

Privileged accounts are among the most attractive targets in identity based attacks. When these accounts rely only on passwords, or when legacy authentication remains enabled, organizations are left more exposed to credential theft, password spraying, and signin attempts that bypass stronger modern protections.

At the same time, access controls cannot simply be enabled without validation. A policy that is technically correct but operationally disruptive can create lockouts, user friction, or service interruptions if introduced carelessly.

This project addressed both problems by implementing Conditional Access controls in a way that reflected real security priorities while also respecting safe rollout practice.

## Project Objectives

This lab was designed to:

- require multifactor authentication for privileged access
- block legacy authentication protocols
- evaluate sign-ins from untrusted locations
- validate policy behavior through signin logs and report only testing
- demonstrate how Conditional Access supports a stronger identity protection strategy

## Technologies Used

- Microsoft Entra ID
- Conditional Access
- Microsoft Entra administrative roles
- Named Locations
- Signin Logs
- Audit Logs

## What Was Implemented

### 1. MFA for Privileged Roles

A Conditional Access policy was created to require multifactor authentication for privileged roles. This control was designed to reduce the likelihood of unauthorized administrative access by ensuring that sensitive identities were not protected by passwords alone.

To make the control operationally safe, the break glass account was excluded from the policy. This reflects a common enterprise practice in which emergency administrative access is preserved in case of policy misconfiguration or unexpected lockout.

### 2. Blocking Legacy Authentication

A separate Conditional Access policy was created to block legacy authentication. This is an important defensive control because older authentication protocols do not support modern safeguards such as MFA and are frequently associated with password based attack activity.

The policy was configured in a way that targeted legacy client authentication methods while maintaining a safer rollout posture through testing and validation.

### 3. Access Evaluation from Untrusted Locations

A location based Conditional Access policy was also created using a trusted named location. This allowed the lab to evaluate how signin attempts from outside the trusted network would be treated.

The policy was structured so that trusted access from the approved location could be excluded, while sign-ins originating from outside that location could be evaluated separately. This reflects how organizations often apply location aware controls to reduce unnecessary exposure without disrupting expected internal access paths.

## Validation and Testing

The policies were tested through controlled signin activity and structured log review. Rather than enabling every control immediately, the lab used report only evaluation where appropriate so policy impact could be observed safely before full enforcement.

Validation included:

- reviewing Conditional Access results in signin logs
- checking whether privileged access policies applied as expected
- examining legacy authentication related signin behavior
- testing sign-ins originating outside the trusted location
- confirming report only outcomes through Microsoft Entra activity details
- reviewing audit log evidence for policy creation and administrative changes

This reflects a realistic operational workflow: design, test, validate, and then enforce with confidence.

## Real-World Use Case

In a real organization, this set of controls would be used to protect administrative accounts from common identity attack paths while reducing the likelihood of accidental disruption during rollout.

Privileged users would be required to complete MFA, outdated signin methods would be blocked, and location based access policies could be tested safely before enforcement.

## Why This Matters in Practice

This lab reflects several security realities that matter in real environments.

First, privileged accounts should never be treated like ordinary user accounts. The potential impact of administrative compromise is far greater, so these identities require stronger and more deliberate protection.

Second, legacy authentication remains one of the most avoidable weaknesses in many identity environments. Blocking it is often one of the most practical steps an organization can take to reduce unnecessary exposure.

Third, Conditional Access is most effective when deployed with operational discipline. Report only mode is not merely a convenience feature; it is a practical safeguard that allows security teams to understand the likely effect of a policy before enabling enforcement.

Taken together, these controls contribute to a more resilient and defensible identity security posture.

## Implementation Evidence

### Security defaults disabled before Conditional Access rollout
<img width="1919" height="943" alt="01-security-defaults-disabled-for-conditional-access" src="https://github.com/user-attachments/assets/da95374b-9028-4bda-98fc-f2d5e640e922" />

### Lab users created in Microsoft Entra ID
<img width="1918" height="689" alt="02-users-created-lab-identities" src="https://github.com/user-attachments/assets/354a6002-9522-4654-bb72-bb995d966bd2" />

### Security groups created for targeting and exclusions
<img width="1918" height="623" alt="03-groups-created-for-role-targeting-and-exclusions" src="https://github.com/user-attachments/assets/e023d865-65c4-4fe9-8b28-0398d042ee1c" />

### CA01 created to require MFA for privileged roles
<img width="946" height="775" alt="10-ca01-policy-overview-with-break-glass-exclusion" src="https://github.com/user-attachments/assets/19bf7004-e0f9-496b-a324-3bdb91b8fa57" />

### Grant control configured to require multifactor authentication
<img width="1918" height="847" alt="11-ca01-grant-require-mfa" src="https://github.com/user-attachments/assets/662d85c6-974e-4630-968e-9a9669affe24" />

### CA02 configured to block legacy authentication
<img width="841" height="945" alt="18-ca02-policy-overview-report-only" src="https://github.com/user-attachments/assets/9bcf84f3-a388-45d8-9e00-4bc9fbf4ee25" />

### Legacy authentication client apps selected for blocking
<img width="1917" height="947" alt="21-ca02-client-apps-legacy-auth-selected" src="https://github.com/user-attachments/assets/26def9fe-7f44-4e64-8a18-1056db7446df" />

### Trusted named location created for access evaluation
<img width="3200" height="1726" alt="25-ca03-create-trusted-home-lab-ip-named-location" src="https://github.com/user-attachments/assets/cefd1a6c-0f32-446e-9a69-40b665eedbfa" />

### Trusted location excluded from location-based policy scope
<img width="2014" height="1732" alt="29-ca03-network-exclude-trusted-home-lab-ip" src="https://github.com/user-attachments/assets/cda438d8-016b-45bb-a215-a567487ad50b" />

### Sign-in details confirmed report-only failure from untrusted access
<img width="3200" height="1726" alt="33-ca03-sign-in-details-report-only-failure" src="https://github.com/user-attachments/assets/f4242c88-708f-422a-bcbb-3c0e97be17fa" />

## Skills Demonstrated

- Conditional Access policy design
- MFA enforcement for sensitive identities
- privileged access protection
- legacy authentication risk reduction
- location based access control
- signin log interpretation
- audit log review
- identity security validation and testing

## Security Outcome

This implementation reduced privileged signin risk, limited exposure to legacy authentication, and introduced safer validation for locationbased access controls before enforcement.

The result was a more controlled and testable identity protection model aligned with real administrative security practice.
