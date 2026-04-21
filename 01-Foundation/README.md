# Foundation Labs

This phase contains the foundational Microsoft Entra ID and Azure security labs in this portfolio.

The purpose of this phase is to demonstrate practical control over the areas that matter most in day to day identity security work: protecting sign-ins, limiting privileged access, governing sensitive memberships, and enabling secure account recovery.

Rather than treating these labs as isolated technical exercises, this phase is structured as a connected identity security track. Together, the projects show how Microsoft Entra ID can be used to protect access at multiple stages of the identity lifecycle:

- before access is granted
- while privileged access is in use
- after access has been assigned
- when users need to recover access safely

## What This Phase Demonstrates

This phase demonstrates practical experience in:

- identity protection through Conditional Access
- privileged access control through Privileged Identity Management
- access governance through Access Reviews
- secure user recovery through SSPR and authentication method configuration

These are the core administrative and security controls used in real organizations to reduce risk, enforce least privilege, and improve operational resilience.

## Foundation Projects

### 1. Conditional Access + MFA
This project focused on protecting privileged identities through Conditional Access policy design, including MFA enforcement, legacy authentication blocking, and location based access evaluation.

### 2. Privileged Identity Management (PIM)
This project focused on reducing standing privilege by configuring just-in-time (JIT) access for both Microsoft Entra roles and Azure resource roles.

### 3. Access Reviews
This project focused on strengthening identity governance by creating and validating a recurring access review for a privileged administrative group.

### 4. Authentication Methods + SSPR + Registration Campaign
This project focused on improving identity resilience through secure password recovery, stronger authentication methods, and targeted registration prompting.

## Why These Labs Matter Together

Viewed individually, each project demonstrates a specific identity control. Viewed together, they show a more complete security story.

- **Conditional Access** reduces sign-in risk.
- **PIM** reduces standing privileged access.
- **Access Reviews** reduce stale or unnecessary access over time.
- **SSPR and Authentication Methods** improve secure recovery when users lose access.

This progression reflects understanding of identity security: strong environments do not rely on one control alone. They combine prevention, governance, privilege control, and recovery design.

## Skills Built in This Phase

Across these projects, the Foundation phase demonstrates:

- Microsoft Entra ID administration
- identity security control implementation
- privileged access governance
- reviewer-based access validation
- authentication method targeting
- secure password recovery design
- configuration validation through logs and user side testing
- professional documentation of technical security work

## Outcome

The Foundation phase establishes a practical base in Microsoft identity security by showing how key controls can be configured, tested, and documented in a real administrative workflow.

It is designed to support progression into more advanced Azure and Microsoft security engineering work in later phases of the portfolio.

## Repository Structure

```text
Azure-Entra-Security-Portfolio/
├── README.md
├── 01-Foundation/
│   ├── 01-conditional-access-mfa/
│   ├── 02-privileged-identity-management/
│   ├── 03-access-reviews/
│   └── 04-authentication-methods-sspr-registration/
