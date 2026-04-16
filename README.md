# Azure & Microsoft Entra Security Portfolio

This repository is my hands-on portfolio for building practical skills in **Microsoft Entra ID**, **Azure security**, **identity governance**, and **cloud security operations**.

The portfolio is structured as a progressive learning path across three phases:

- **Foundation**
- **Intermediate**
- **Advanced**

The goal is to move beyond theory and document security controls in a way that reflects how they solve real operational problems inside organizations.

---

## Portfolio Purpose

I built this portfolio to create practical evidence of my work in:

- **Azure security**
- **Microsoft Entra ID**
- **Identity and Access Management (IAM)**
- **Identity governance**
- **Cloud security administration**

This work supports my progression toward **AZ-500** and **SC-300**, while helping me build a stronger project portfolio for Microsoft-focused security roles.

---

## Portfolio Roadmap

### 01 - Foundation
The Foundation phase focuses on core identity and access security controls that are widely used in real organizations.

This phase covers:

- Conditional Access and MFA
- Privileged Identity Management (PIM)
- Access Reviews
- Authentication Methods
- Self-Service Password Reset (SSPR)
- Registration Campaigns

These labs are designed to build a strong base in identity protection, privileged access control, and secure user recovery.

### 02 - Intermediate
The Intermediate phase is intended to expand from identity-focused controls into broader Azure and Microsoft security engineering scenarios.

Planned areas in this phase include:

- Key Vault and Managed Identity
- Defender for Cloud workload protection
- Logging, monitoring, and detection workflows
- Secure storage and private access design
- Application identity and permissions security

This phase will focus more on operational cloud security and service-to-service trust.

### 03 - Advanced
The Advanced phase will move toward more mature security design and investigation scenarios.

Planned areas in this phase include:

- Zero Trust-oriented identity architecture
- Privileged access governance design
- Identity incident investigation
- End-to-end cloud security case studies
- Policy-driven security design across Microsoft security controls

This phase is intended to reflect more strategic and architecture-level security thinking.

---

## Current Progress

At present, the **Foundation phase** is the most developed part of this portfolio and contains the first completed set of hands-on projects.

Current completed Foundation labs:

| Project | Focus Area | Security Problem Addressed |
|---|---|---|
| 01 | Conditional Access + MFA | Protects privileged accounts and reduces risky sign-ins |
| 02 | Privileged Identity Management | Reduces standing privilege through just-in-time access |
| 03 | Access Reviews | Helps detect and remove unnecessary privileged access |
| 04 | Authentication Methods + SSPR | Enables secure registration and self-service account recovery |

Intermediate and Advanced sections are included intentionally so the portfolio can continue to grow in a structured way.

---

## How the Projects Are Documented

Each lab is documented as a practical case study and typically includes:

- the business problem being addressed
- the security objective of the lab
- the Microsoft technologies used
- implementation steps
- validation and test evidence
- selected screenshots
- the practical value of the control in a real-world environment

The aim is not only to complete labs, but to explain why each control matters and how it would be used in practice.

---

## Repository Structure

```text
Azure-Entra-Security-Portfolio/
├── README.md
├── 01-Foundation/
│   ├── 01-conditional-access-mfa/
│   ├── 02-privileged-identity-management/
│   ├── 03-access-reviews/
│   └── 04-authentication-methods-sspr-registration/
├── 02-Intermediate/
└── 03-Advanced/
