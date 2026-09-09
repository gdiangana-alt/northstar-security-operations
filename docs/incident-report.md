# NorthStar Sentinel Incident Report

## Incident Summary

**Incident:** NorthStar - Failed Azure Control Plane Operation  
**Severity:** Medium  
**Detection Platform:** Microsoft Sentinel  
**Detection Method:** Scheduled KQL analytics rule  
**Final Status:** Resolved  
**Classification:** Benign Positive — Security Testing  

## Detection

Microsoft Sentinel detected a failed Azure control-plane operation within the NorthStar environment.

The custom analytics rule monitored Azure Activity logs for failed management operations affecting `NORTHSTAR-AZURE-RG`.

```kusto
AzureActivity
| where ResourceGroup =~ "NORTHSTAR-AZURE-RG"
| where ActivityStatusValue =~ "Failure"
| project TimeGenerated, OperationNameValue, ActivityStatusValue, ResourceGroup
