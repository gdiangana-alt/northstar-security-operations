# NorthStar Detection Strategy

## Detection Objective

Identify failed Azure control-plane operations affecting the NorthStar environment.

Failed administrative operations can result from configuration mistakes, unauthorized attempts, reconnaissance, or attempts to modify protected cloud resources.

## Data Source

**Source:** Azure Activity Log  
**SIEM:** Microsoft Sentinel  
**Workspace:** `northstar-soc-workspace`  
**Table:** `AzureActivity`

Azure Activity Log telemetry is streamed to the Log Analytics workspace and analyzed by Microsoft Sentinel.

## Detection Logic

```kusto
AzureActivity
| where ResourceGroup =~ "NORTHSTAR-AZURE-RG"
| where ActivityStatusValue =~ "Failure"
| project TimeGenerated, OperationNameValue, ActivityStatusValue, ResourceGroup
