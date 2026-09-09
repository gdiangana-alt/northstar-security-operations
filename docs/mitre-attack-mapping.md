# NorthStar MITRE ATT&CK Mapping

## Purpose

The NorthStar Sentinel detection monitors failed Azure control-plane operations.

A failed administrative operation is not inherently malicious. The detection provides a signal that can be investigated alongside identity, resource, and other security telemetry.

## Relevant ATT&CK Context

### T1098 — Account Manipulation

Unauthorized administrative activity may involve attempts to modify cloud access, permissions, or account-related configuration.

The NorthStar detection can provide supporting telemetry when failed Azure management operations occur during this type of activity.

### T1548 — Abuse Elevation Control Mechanism

Attempts to obtain or modify elevated privileges may generate Azure control-plane activity, including unsuccessful administrative operations.

Failed operations affecting privileged Azure resources should therefore be investigated in context with RBAC and identity activity.

### T1562 — Impair Defenses

An adversary attempting to modify security controls, monitoring configuration, diagnostic settings, or other defensive resources may generate failed Azure management operations.

The detection can contribute to identifying unsuccessful attempts to alter defensive cloud configuration.

## Detection Limitation

The current KQL rule detects failed management operations broadly:

```kusto
AzureActivity
| where ResourceGroup =~ "NORTHSTAR-AZURE-RG"
| where ActivityStatusValue =~ "Failure"
| project TimeGenerated, OperationNameValue, ActivityStatusValue, ResourceGroup
