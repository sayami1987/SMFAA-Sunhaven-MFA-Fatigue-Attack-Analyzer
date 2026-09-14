# SMFAA Initial Requirements

## 1. Purpose

This document defines the initial functional, security and non-functional requirements for the **Sunhaven MFA Fatigue Attack Analyzer (SMFAA)**.

The requirements will be refined as the event schema and detection rules are designed.

---

# 2. Functional Requirements

## SMFAA-FR-01 — Load Synthetic MFA Events

The system shall load a controlled synthetic MFA-event dataset.

## SMFAA-FR-02 — Validate Required Fields

The system shall verify that each event contains the required fields.

Initial expected fields:

```text
event_id
user_id
timestamp
event_type
```

Additional fields may be introduced during the event-schema stage.

## SMFAA-FR-03 — Validate Timestamps

The system shall reject or clearly report invalid timestamps.

## SMFAA-FR-04 — Order Events

The system shall analyse events in chronological order.

## SMFAA-FR-05 — Group by Identity

The system shall group MFA events by fictional identity before correlation.

## SMFAA-FR-06 — Apply Detection Windows

The system shall analyse relevant events inside configurable time windows.

## SMFAA-FR-07 — Detect Prompt Bursts

The system shall identify repeated MFA challenge/prompt events that reach the configured prompt-burst threshold within the configured time window.

## SMFAA-FR-08 — Detect Repeated Denials

The system shall identify repeated MFA denial/rejection events that reach the configured denial threshold within the configured time window.

## SMFAA-FR-09 — Detect Denial-to-Success Behaviour

The system shall identify repeated MFA denials followed by an MFA success within the configured correlation period.

## SMFAA-FR-10 — Support Normal Baselines

The system shall support normal and low-volume MFA behaviour without generating a fatigue finding unless a configured detection condition is met.

## SMFAA-FR-11 — Apply Severity

The system shall assign a transparent severity to each finding according to configured detection rules.

## SMFAA-FR-12 — Produce Explainable Findings

Each finding shall identify the relevant detection evidence.

Planned finding fields include:

```text
finding_id
user_id
finding_type
rule_id
window_start
window_end
event_count
event_sequence
severity
reason
```

## SMFAA-FR-13 — Support Repeatable Scenarios

The system shall support repeatable synthetic scenarios representing normal, suspicious, boundary and invalid-data behaviour.

## SMFAA-FR-14 — Generate Structured Output

The later prototype shall support:

```text
Console
CSV
JSON
```

---

# 3. Security Requirements

## SMFAA-SR-01 — Read-Only Operation

SMFAA shall not modify Microsoft Entra ID or any other operational IAM environment.

## SMFAA-SR-02 — Synthetic Data

All development and demonstration data shall be fictional.

## SMFAA-SR-03 — No Authentication Secrets

The repository shall not require or store:

- passwords;
- MFA codes;
- access tokens;
- refresh tokens;
- client secrets.

## SMFAA-SR-04 — Safe Failure

Invalid data shall not be silently treated as valid authentication activity.

## SMFAA-SR-05 — Explainable Detection

A finding shall identify the rule and sequence responsible for the decision.

## SMFAA-SR-06 — No Automatic Remediation

The system shall not automatically disable accounts, revoke sessions or alter MFA settings.

---

# 4. Non-Functional Requirements

## SMFAA-NFR-01 — Deterministic Behaviour

The same valid data and detection configuration shall produce the same result.

## SMFAA-NFR-02 — Configurable Thresholds

Detection thresholds and time windows shall be stored outside core detection logic where practical.

## SMFAA-NFR-03 — Modular Design

Loading, validation, correlation, detection and reporting shall be separated into logical modules.

## SMFAA-NFR-04 — Testability

Core analysis logic shall support automated testing.

## SMFAA-NFR-05 — Maintainability

Detection rules and thresholds shall be documented clearly enough to be changed without redesigning the entire system.

## SMFAA-NFR-06 — Privacy-Safe Evidence

Screenshots and generated evidence shall contain only fictional identities and non-sensitive event data.

## SMFAA-NFR-07 — Honest Claims

A detection shall be described as a **suspicious or possible MFA-fatigue pattern**, not definitive proof that a real attacker was present.

## SMFAA-NFR-08 — Scope Independence

SMFAA shall remain independent from:

- operational MFA configuration;
- JML;
- RBAC;
- access-review remediation;
- CAPE;
- SSSA;
- Flask/Jinja2 presentation;
- SITAS attack-path simulation.

---

# 5. Initial Acceptance Criteria

The later prototype should satisfy the following:

1. valid MFA events can be loaded;
2. invalid timestamps are rejected;
3. missing required fields are rejected;
4. events are sorted correctly;
5. events are grouped by user;
6. normal scenarios do not trigger unnecessary alerts;
7. repeated-denial scenarios trigger when the configured threshold is reached;
8. prompt-burst scenarios trigger when the configured threshold is reached;
9. denial-to-success sequences are detected;
10. just-below-threshold cases remain below detection;
11. findings explain the triggering sequence;
12. analysis remains read-only.

---

# 6. Initial Exclusions

The first version will not include:

```text
machine learning
IP reputation
geolocation
device compliance
real-time SIEM integration
Graph remediation
automatic account disablement
automatic session revocation
live alert delivery
password-spray detection
```

These exclusions keep the project focused, testable and separate from other Sunhaven components.
