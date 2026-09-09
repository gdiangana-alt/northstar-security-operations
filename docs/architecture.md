# NorthStar Security Operations Architecture

## Architecture Overview

NorthStar Security Operations uses Azure-native telemetry and Microsoft Sentinel to provide centralized cloud monitoring, detection, and incident response.

## Architecture

```text
NorthStar Azure Environment
        │
        │ Azure control-plane operations
        ▼
Azure Activity Log
        │
        │ Subscription diagnostic settings
        ▼
NorthStar-SOC-Workspace
Azure Log Analytics
        │
        │ AzureActivity table
        ▼
Microsoft Sentinel
        │
        ├── KQL Analysis
        │
        └── Scheduled Analytics Rules
                    │
                    ▼
              Security Alert
                    │
                    ▼
             Sentinel Incident
                    │
                    ▼
          Analyst Investigation
                    │
             ┌──────┴──────┐
             ▼             ▼
        Containment    Classification
                             │
                             ▼
                         Resolution
