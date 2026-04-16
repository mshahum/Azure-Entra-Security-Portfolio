# Conditional Access and MFA for Identity Protection

## Overview

This project focused on strengthening identity security in Microsoft Entra ID through the design and testing of Conditional Access controls. The lab was built around a practical security goal: protecting privileged access, reducing exposure to legacy authentication, and evaluating how access policies respond to sign-ins from untrusted locations.

Rather than treating Conditional Access as a purely administrative feature, this project approached it as a real security control that shapes how organizations protect sensitive identities and reduce common sign-in risks.

---

## Business Context

Administrative and high-privilege accounts are among the most attractive targets in modern identity attacks. If these accounts are protected only by passwords, or if legacy authentication remains enabled, an organization is left exposed to credential theft, password spraying, and access attempts that bypass stronger modern controls.

At the same time, many organizations need a safe way to test how new access policies will behave before enforcing them in production. A policy that is technically correct but operationally disruptive can create serious business problems if deployed carelessly.

This project addresses those challenges by implementing Conditional Access controls in a way that reflects both security priorities and practical rollout considerations.

---

## Project Objectives

The objectives of this lab were to:

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

## What Was Implemented

### MFA for Privileged Roles

A Conditional Access policy was created to require multi-factor authentication for privileged roles. This control helps reduce the likelihood of unauthorized administrative access by ensuring that sensitive actions are not protected by passwords alone.

### Blocking Legacy Authentication

A separate policy was configured to block legacy authentication. This is an important control because older authentication protocols do not support modern protections such as MFA and are often used in password-based attack activity.

### Access Evaluation from Untrusted Locations

A location-based policy was also created using a trusted named location. Sign-in activity from outside the trusted network was then reviewed to understand how the policy would behave under less trusted conditions.

This helped demonstrate how organizations can apply location-aware access controls without immediately enforcing them in a way that risks lockout or disruption.

---

## Validation and Testing

The policies were tested through controlled sign-in activity and log review. Rather than enabling every control immediately, the lab used report-only evaluation where appropriate so policy impact could be observed safely.

Validation included:

- reviewing Conditional Access results in sign-in logs
- checking whether legacy authentication policy applied as expected
- testing sign-ins from an IP outside the trusted location
- confirming that the location-based policy showed the expected report-only outcome
- reviewing policy behavior through activity details in Microsoft Entra sign-in events

This approach reflects a more realistic security workflow: design, test, validate, and then enforce with confidence.

---

## Why This Matters in Practice

This lab reflects several security realities that matter in real organizations.

First, privileged accounts should never be treated like ordinary user accounts. They require stronger protection because the damage caused by compromise is far greater.

Second, legacy authentication remains one of the most avoidable identity weaknesses in many environments. Blocking it is often a straightforward way to reduce unnecessary exposure.

Third, Conditional Access is most effective when it is tested properly. Report-only mode is not just a convenience feature; it is an operational safeguard that helps security teams understand the effect of a policy before turning it on fully.

Together, these controls contribute to a more practical and defensible identity security posture.

---

## Key Screenshots

This project includes screenshots that document:

1. Conditional Access policy requiring MFA for privileged roles  
2. Conditional Access policy blocking legacy authentication  
3. trusted location and untrusted location access logic  
4. sign-in log evidence showing policy behavior in report-only mode  

---

## Skills Demonstrated

- Conditional Access policy design
- MFA enforcement for sensitive identities
- legacy authentication risk reduction
- location-based access control
- sign-in log interpretation
- identity security validation and testing

---

## Outcome

This project demonstrated how Microsoft Entra Conditional Access can be used to strengthen identity protection through a combination of role-based MFA enforcement, legacy authentication blocking, and location-aware policy evaluation.

It also showed the value of validating access controls through sign-in monitoring before moving to full enforcement, which is a critical part of deploying security controls responsibly in a live environment.
