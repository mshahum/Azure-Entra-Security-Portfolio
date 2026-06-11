# Identity Threat Detection with KQL

## Overview

This project focused on building identity based detection logic in Microsoft Sentinel using Microsoft Entra ID signin logs and Kusto Query Language (KQL).

The lab simulated common identity security monitoring scenarios, including failed signin bursts, successful signins after repeated failures, privileged account signin monitoring, and break glass account activity detection.

The purpose of this lab was to move beyond basic log ingestion and demonstrate how raw identity logs can be turned into useful detection logic for security operations.

## Business Problem

Identity is one of the most common attack paths in modern cloud environments.

Attackers often try to gain access by guessing passwords, using stolen credentials, targeting privileged accounts, or attempting to sign in with emergency access accounts. If these activities are not monitored, a security team may miss early signs of account compromise or privilege misuse.

Organizations need detection logic that can identify suspicious identity behavior quickly and help analysts decide whether an event requires investigation.

This lab addresses that problem by using Microsoft Sentinel and KQL to detect identity activity that may indicate account abuse, credential attacks, or unauthorized use of sensitive accounts.

## Project Objectives

The main objectives of this lab were to:

* Validate Microsoft Entra signin log ingestion in Microsoft Sentinel.
* Build KQL queries to identify failed signin bursts.
* Detect successful signins after repeated password failures.
* Monitor privileged administrator account signin activity.
* Monitor break glass account signin activity.
* Convert tested KQL logic into a Microsoft Sentinel analytics rule.
* Document detection logic in a clear and repeatable way.
* Separate lab testing settings from production tuning recommendations.

## Technologies Used

* Microsoft Azure
* Microsoft Sentinel
* Log Analytics Workspace
* Microsoft Entra ID
* Microsoft Entra Signin Logs
* Kusto Query Language (KQL)
* Sentinel Scheduled Analytics Rules
* Identity security monitoring concepts

## What Was Implemented

### 1. Signin Log Baseline Validation

The lab began by validating that Microsoft Entra signin logs were available in the Sentinel connected Log Analytics workspace.

This step confirmed that identity events were being collected successfully before building any detection logic.

The baseline query reviewed recent signin activity and confirmed that the `SigninLogs` table contained usable authentication data.

### 2. Failed Signin Burst Detection

A failed signin burst query was created to identify users with repeated failed signin attempts within a short time window.

This type of detection can help identify password guessing, brute force attempts, account lockout patterns, or users experiencing repeated authentication failures.

The query grouped failed signins by user and time window, then highlighted accounts with multiple failures in a 15 minute period.

### 3. Successful Signin After Password Failures

A second detection query was created to identify a successful signin shortly after repeated password failures.

This scenario is important because repeated failures followed by a success may indicate that an attacker eventually guessed the correct password, used a valid stolen credential, or completed authentication after multiple failed attempts.

The query compared failed password attempts with later successful signins for the same user and looked for success within a short time period after the failures.

### 4. Privileged Account Sign-in Monitoring

A privileged administrator account monitoring query was created to review sign-in activity for sensitive administrative accounts.

Privileged accounts require closer monitoring because compromise of an admin account can lead to major impact, including access changes, policy modification, resource control, or tenant-wide security risk.

The query summarized successful sign-ins, failed or interrupted sign-ins, applications accessed, conditional access results, and recent activity timeframes for monitored admin users.

### 5. Break glass Account Monitoring

A break glass account monitoring query was created to detect signin activity from emergency access accounts.

Break glass accounts should be used rarely and only during exceptional situations. Any activity from such an account should be reviewed because it may indicate emergency use, policy bypass, or possible account misuse.

The query identified signin activity from the break glass account and marked the event as high priority for review.

### 6. Sentinel Analytics Rule Creation

The break glass account detection was converted into a Microsoft Sentinel scheduled analytics rule.

This moved the lab from manual hunting into automated detection. The rule was configured to run on a schedule and generate security findings when monitored break glass account activity was detected.

## Validation and Testing

The lab was validated using real sign in activity from test accounts in the lab environment.

Validation included:

* Confirming that `SigninLogs` returned recent authentication events.
* Generating controlled failed signin attempts.
* Confirming that the failed signin burst query returned expected results.
* Testing a successful signin after failed attempts.
* Monitoring privileged account activity.
* Monitoring break glass account activity.
* Creating a Sentinel analytics rule from tested KQL logic.

The validation showed that identity log data could be queried, filtered, summarized, and converted into operational detection logic.

## Detection and Investigation Logic

This lab used several KQL techniques that are commonly used in security monitoring:

* `where` was used to filter signin events by time, user, and result type.
* `summarize` was used to group events and count signin activity.
* `count()` was used to calculate the number of events.
* `countif()` was used to separately count successful and failed/interrupted signins.
* `min()` and `max()` were used to identify first and last event times.
* `make_set()` was used to collect related applications, failure reasons, and conditional access results.
* `bin()` was used to group events into time windows.
* `join` was used to compare failed signins with later successful signins.
* `project` was used to display only the most useful investigation columns.

The detection logic was designed to make the output useful for a security analyst, not just technically correct. The queries focused on showing who was involved, what happened, when it happened, which applications were used, and whether the activity required review.

## Real World Use Case

In a real security operations environment, this type of detection helps analysts monitor identity risk and respond to suspicious authentication behavior.

Examples include:

* A user account showing repeated failed signins.
* A successful signin shortly after multiple password failures.
* Unexpected activity from a privileged administrator account.
* Any signin activity from a break glass account.
* Signins that may require conditional access or account review.

These detections support early investigation before suspicious identity activity turns into a larger security incident.

## Production Considerations

This lab was performed in a controlled environment, so some settings were adjusted for learning and validation.

In production, the detection logic should be tuned further before being used as a live alerting rule.

Important production considerations include:

* Using watchlists for privileged and break glass accounts instead of hardcoding names directly in queries.
* Adding entity mapping for users, accounts, and IP addresses in Sentinel analytics rules.
* Tuning thresholds to reduce false positives.
* Using suppression or grouping to avoid duplicate alerts.
* Separating failed password errors from other interrupted signin events.
* Reviewing conditional access results as part of the investigation.
* Adding approved maintenance or emergency access windows where appropriate.
* Documenting an incident response process for break glass account activity.
* Reviewing sign-in risk, user risk, device details, and location data where licensing allows.

For lab validation, short query windows and simplified account lists were acceptable. In production, the same detections should be aligned with the organization’s identity baseline, risk tolerance, and incident response process.

## Why This Matters in Practice

Identity detections are important because many cloud incidents begin with authentication activity.

A suspicious signin pattern may be the first sign of password spraying, credential compromise, account misuse, or unauthorized access. Without structured signin monitoring, a security team may only notice the problem after damage has already occurred.

This lab demonstrates the practical skill of turning signin logs into useful detections. It also shows the difference between simply collecting logs and actually using those logs for security monitoring.

## Implementation Evidence

### Signin Log Baseline Validation

The `SigninLogs` table was queried to confirm that Microsoft Entra sign-in data was available in the Sentinel workspace.

<img width="3198" height="1718" alt="01-signinlogs-baseline-validation" src="https://github.com/user-attachments/assets/82f3a3ff-ea68-4529-a4a6-6779db90bd46" />


### Failed Sign-in Burst Detection

A KQL query was used to detect multiple failed signins within a 15-minute window.

<img width="3200" height="1702" alt="02-failed-signin-burst-query-results" src="https://github.com/user-attachments/assets/8832d8a8-cc6c-4387-9c40-a707864b713e" />

### Successful Signin After Failed Attempts

A correlation query was used to identify a successful signin after repeated failed password attempts.

<img width="1919" height="896" alt="03-success-after-failed-signins-query-results" src="https://github.com/user-attachments/assets/1ad1d59c-97f1-441e-bc9b-27351c43a468" />

### Privileged Account Signin Monitoring

A privileged account monitoring query summarized signin activity for an administrative account.

<img width="3196" height="1704" alt="04-admin-account-signin-query-results" src="https://github.com/user-attachments/assets/33adaa68-20e4-4739-be55-eac569c0d736" />

### Break-glass Account Signin Monitoring

A break glass account query identified activity from an emergency access account and marked it as high priority for review.

<img width="3200" height="1698" alt="05-breakglass-account-signin-query-results" src="https://github.com/user-attachments/assets/3ffba9dd-b434-433c-af97-2a332c224c83" />

### Sentinel Analytics Rule Created

The break glass account detection query was converted into a Microsoft Sentinel scheduled analytics rule.

<img width="3200" height="1728" alt="06-breakglass-analytics-rule-created" src="https://github.com/user-attachments/assets/0e4b933c-ee5e-4b20-a5a9-35295b194b8b" />

## KQL Queries

The KQL queries used in this lab are stored in the `kql` folder:

* `kql/01-signinlogs-baseline-validation.kql`
* `kql/02-failed-signin-burst-detection.kql`
* `kql/03-success-after-failed-signins.kql`
* `kql/04-admin-account-signin-monitoring.kql`
* `kql/05-breakglass-account-signin-monitoring.kql`
* `kql/06-breakglass-account-analytics-rule-query.kql`

## Skills Demonstrated

This project demonstrates the ability to:

* Query Microsoft Entra signin logs using KQL.
* Build identityfocused detection logic in Microsoft Sentinel.
* Detect failed signin bursts using time window analysis.
* Correlate failed signins with later successful authentication.
* Monitor privileged administrator account activity.
* Monitor break glass account signin activity.
* Convert tested KQL logic into a Sentinel analytics rule.
* Understand lab validation versus production tuning.
* Present security detection work in a clear, evidence based format.

## Security Outcome

This lab turned Microsoft Entra signin logs into practical identity threat detection logic.

The environment was able to identify failed signin patterns, review successful authentication after password failures, monitor privileged account activity, and generate a Sentinel analytics rule for break glass account signins.

The key security outcome was improved identity visibility and detection readiness: authentication events were not only collected, but actively queried, analyzed, and converted into security monitoring logic.

