# NorthStar Incident Response Workflow

## Overview

The NorthStar Security Operations environment demonstrates an end-to-end Microsoft Sentinel detection and incident-response workflow.

## 1. Detect

Azure control-plane telemetry is collected through Azure Activity Log and streamed to the NorthStar Log Analytics workspace.

Microsoft Sentinel analyzes the telemetry using custom KQL detection logic.

## 2. Alert

A scheduled analytics rule evaluates the detection every five minutes.

When one or more matching events are identified, Microsoft Sentinel generates a Medium-severity security alert.

## 3. Create Incident

Incident creation is enabled on the analytics rule.

Matching alerts are automatically converted into Microsoft Sentinel incidents for investigation.

## 4. Triage

The analyst reviews:

- Alert severity and category
- Detection source
- Activity timestamps
- Azure operation
- Operation status
- Targeted resource group
- Related alerts and evidence

## 5. Investigate

The detected operation is correlated with known administrative activity.

The analyst determines whether the activity represents:

- Expected administration
- Security testing
- Misconfiguration
- Suspicious activity
- Confirmed malicious activity

## 6. Respond

Response actions depend on the investigation outcome.

Potential actions include:

- Containing compromised identities
- Removing unauthorized access
- Reverting malicious configuration changes
- Preserving evidence
- Escalating the incident
- Tuning detection logic
- Documenting benign activity

For the NorthStar validation incident, no containment was necessary because Azure rejected the attempted change and investigation confirmed authorized security testing.

## 7. Classify

The validation incident was classified as:

**Benign Positive — Security Testing**

This indicates that the detection correctly identified the activity, but investigation established that it was authorized.

## 8. Resolve

After investigation and classification, the incident was marked:

**Resolved**

## Validated SOC Pipeline

```text
Azure Control Plane
        ↓
Azure Activity Log
        ↓
Log Analytics
        ↓
Microsoft Sentinel
        ↓
KQL Detection
        ↓
Scheduled Analytics Rule
        ↓
Security Alert
        ↓
Sentinel Incident
        ↓
Triage & Investigation
        ↓
Classification
        ↓
Response / Resolution
