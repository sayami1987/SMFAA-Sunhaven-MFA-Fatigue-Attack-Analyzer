# 01 — SMFAA Policy and Project Alignment

## 1. Purpose

This document explains how the **Sunhaven MFA Fatigue Attack Analyzer (SMFAA)** supports the wider Sunhaven Care IAM project's authentication-security objectives while remaining technically independent from operational IAM components.

SMFAA is an educational prototype. It does not replace the project's authentication policy and does not provide formal compliance certification.

---

## 2. Relevant Sunhaven Security Context

The wider Sunhaven project includes:

- MFA;
- secure authentication;
- RBAC;
- identity lifecycle management;
- audit evidence;
- shared-device security.

MFA is intended to reduce the risk of account compromise when a password alone is insufficient.

However, repeated MFA prompts can create a separate user-interaction risk.

SMFAA addresses this narrow analytical gap.

---

## 3. Project Alignment

| Project objective | SMFAA contribution |
|---|---|
| Strong authentication | Analyses suspicious behaviour affecting MFA |
| Protect workforce accounts | Detects patterns that may indicate MFA prompt abuse |
| Protect resident information | Supports early review of suspicious authentication behaviour |
| Auditable security evidence | Produces explainable event-based findings |
| Secure shared environment | Strengthens authentication monitoring without duplicating session controls |
| Technical testing | Provides repeatable normal, suspicious and boundary scenarios |

---

## 4. Authentication-Control Boundary

```text
Sunhaven policy:
MFA should be used.

Operational IAM:
Configure and enforce MFA.

SMFAA:
Analyse the resulting MFA event sequence.
```

SMFAA therefore supports authentication assurance without replacing the operational control.

---

## 5. Proposed Detection Principles

SMFAA will use transparent rule-based analysis rather than opaque classification.

Potential evidence includes:

```text
Number of MFA prompts
Number of denials
Time concentration
Order of events
Successful MFA after repeated denials
```

A finding will be based on an explicit rule and time window.

---

## 6. False-Positive Awareness

Not every denial means an attack.

Examples of ordinary behaviour may include:

- user accidentally rejects one request;
- user initially fails and later succeeds;
- isolated events separated by a long period.

SMFAA therefore includes benign baseline and threshold-boundary scenarios.

This is an important design goal because a useful security detector should not simply label all failed authentication activity as malicious.

---

## 7. Privacy and Evidence Handling

SMFAA shall use:

- fictional users;
- synthetic timestamps/events;
- non-sensitive authentication metadata.

SMFAA shall not use:

- real passwords;
- MFA codes;
- tokens;
- resident records;
- real employee information;
- production secrets.

---

## 8. Relationship to Compliance

SMFAA can support the wider project's secure-access and evidence objectives.

Correct wording:

> **SMFAA supports the Sunhaven project's authentication-security and access-governance objectives.**

Incorrect wording:

> **SMFAA makes Sunhaven compliant with ISO 27001 or the Australian Privacy Principles.**

Formal organisational compliance is outside the project scope.

---

## 9. Relationship to Team Components

### Core IAM / Rifat

SMFAA does not configure MFA, RBAC or JML.

### Prothom

SMFAA does not build the Flask/audit presentation layer.

### CAPE / Adnan

SMFAA does not make device/network/resource-based access decisions.

### SSSA / Adnan

SMFAA does not monitor authenticated sessions.

### SITAS

SMFAA does not model attack paths.

---

## 10. Alignment Conclusion

SMFAA is aligned with the Sunhaven project because MFA is already a central authentication control and suspicious MFA prompt behaviour is directly relevant to protecting workforce identities.

The component remains unique by focusing on **read-only temporal analysis of MFA event sequences**, especially prompt bursts, repeated denials and denial-to-success behaviour.

The output is an explainable security finding for review, not an automatic access-control action.
