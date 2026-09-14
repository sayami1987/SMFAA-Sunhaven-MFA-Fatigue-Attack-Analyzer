# SMFAA Scope Boundary and Team Non-Overlap

## 1. Purpose

This document defines the exact technical boundary of the **Sunhaven MFA Fatigue Attack Analyzer (SMFAA)**.

Its purpose is to prevent duplication of team members' work and ensure the component remains a clearly identifiable individual technical contribution.

---

## 2. SMFAA Core Question

SMFAA answers:

> **Does this time-based sequence of MFA authentication events resemble MFA-fatigue or push-bombing behaviour?**

---

## 3. What SMFAA Owns

SMFAA owns:

- synthetic MFA event analysis;
- timestamp validation;
- chronological event ordering;
- identity grouping;
- rolling time-window correlation;
- prompt-burst detection;
- repeated-denial detection;
- denial-to-success detection;
- threshold logic;
- finding severity;
- explainable findings;
- detector testing.

---

## 4. What SMFAA Does Not Own

SMFAA does not implement:

- Microsoft Entra MFA configuration;
- Conditional Access configuration;
- user provisioning;
- account disablement;
- role changes;
- group changes;
- JML;
- RBAC enforcement;
- access-review remediation;
- device-trust policy;
- network-location policy;
- shared-device session assurance;
- session timeout;
- Flask/Jinja2 pages;
- audit dashboard/search functionality;
- attack-path simulation;
- automatic remediation.

---

## 5. Boundary Against Rifat's Core IAM Work

Rifat's core area includes operational IAM/security functions such as:

- Entra identity configuration;
- MFA;
- RBAC;
- JML;
- access review;
- security policy/evidence.

SMFAA does not configure, enforce or remediate those controls.

```text
Rifat / Core IAM:
MFA configuration and operational IAM control.

SMFAA:
MFA authentication-event sequence analysis.
```

---

## 6. Boundary Against Prothom's Work

Prothom's technical contribution focuses on the Flask/Jinja2 presentation layer, including:

- dashboard/navigation;
- audit presentation;
- residents views;
- protected pages;
- 403 handling;
- logout;
- audit search/filter presentation.

SMFAA does not provide presentation-layer functionality.

```text
Prothom:
Present IAM/audit information.

SMFAA:
Analyse time-correlated MFA events.
```

---

## 7. Boundary Against Adnan's CAPE

CAPE evaluates contextual access using factors such as:

- resource sensitivity;
- device status;
- network location.

SMFAA does not decide whether an access request should be allowed.

```text
CAPE:
Should this request proceed?

SMFAA:
Does this MFA event sequence look suspicious?
```

---

## 8. Boundary Against Adnan's SSSA

SSSA focuses on shared-workstation session safety after authentication.

SMFAA focuses on the MFA authentication interaction itself.

```text
SSSA:
Is this current session safe?

SMFAA:
Was the MFA event sequence suspicious?
```

---

## 9. Boundary Against SITAS

SITAS performs identity threat and attack-path simulation.

SMFAA does not model attack paths.

```text
SITAS:
Simulated attack paths.

SMFAA:
Concrete synthetic MFA event-sequence analysis.
```

---

## 10. Data Boundary

SMFAA may process:

```text
fictional user ID
event ID
event type
timestamp
fictional privilege classification
synthetic correlation metadata
```

SMFAA shall not require:

```text
real passwords
real MFA codes
live access tokens
real resident information
real employee information
production tenant credentials
```

---

## 11. Output Boundary

SMFAA produces:

- analysis results;
- finding IDs;
- affected fictional user;
- relevant time window;
- event sequence;
- triggered rule;
- severity;
- reason;
- review recommendation.

SMFAA does not execute the recommendation.

---

## 12. Feature-Gate Rule

Before adding any feature, ask:

1. Does it analyse MFA event-sequence behaviour?
2. Is it read-only?
3. Can it be tested with synthetic data?
4. Is it different from MFA configuration, JML, CAPE, SSSA and the Flask interface?
5. Does it improve detection quality, testing or explainability?

If not, the feature should not be added without a scope review.

---

## 13. Locked Project Description

> **SMFAA is a standalone, read-only cybersecurity-analysis prototype that correlates synthetic MFA authentication events to identify suspicious MFA-fatigue patterns, including prompt bursts, repeated denials and denial-to-success sequences. It performs no MFA configuration, access enforcement, session management or automatic remediation.**
