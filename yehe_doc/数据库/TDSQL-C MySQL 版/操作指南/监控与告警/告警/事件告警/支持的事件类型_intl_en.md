This document describes the event types in TDSQL-C for MySQL for which alarms can be reported.

| Event | Event Name | Description |
|---------|---------|---------|
| Memory OOM | GuestOom | The system memory was overloaded. |
| Instance read-only (excessive storage) | DiskOverQuota | The used storage space exceeded the limit, so data could only be read but not written. |
| Database agent mount node removal | ProxyNodeFaultEliminated | A database proxy mount node was removed due to a failure. |
| Database agent exception | ProxyUnHealthy | An exception occurred in the database proxy. |
| HA (instance high availability) | HA | An HA switch occurred in the instance. |
| Version upgrade | UpgradeVersion | The minor version was upgraded in the cluster. |
| Cross-AZ latency | CrossAzReplicationLag | The cross-AZ source-replica latency was too high. |
| TencentCloud API operation (CloudAudit) | ApiCall | A TencentCloud API was called. |
| Console operation (CloudAudit) | ConsoleCall | An operation was performed in the console. |
