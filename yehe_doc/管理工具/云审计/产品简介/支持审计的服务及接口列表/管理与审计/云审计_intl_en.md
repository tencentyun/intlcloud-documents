With CloudAudit (CA), you can get the history of API calls under your Tencent Cloud account, including those made through the Tencent Cloud Console, Tencent Cloud SDK, CLI, and other Tencent Cloud services, to monitor any deployment behaviors in Tencent Cloud. You can determine which sub-users and collaborators use TencentCloud API, from which source IP addresses calls are made, and when calls are made. You can configure multiple tracking sets to track different logs and control when to enable or disable CloudAudit logging at any time.

CloudAudit operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|------|------|--------------|
| Searching log | ca   | LookUpEvents |
| Creating CloudAudit instance               | cloudaudit | CreateAudit             |
| Deleting CloudAudit instance               | cloudaudit | DeleteAudit             |
| Getting the search scope of event           | cloudaudit | GetEventNameSearchValue |
| GetSearchValueRange | cloudaudit | GetSearchValueRange     |
| Pulling CloudAudit instance list             | cloudaudit | ListAudits              |
| Searching for log                | cloudaudit | LookupEvents            |
| Searching for log                | cloudaudit | LookUpEvents            |
| Searching for sensitive operation log            | cloudaudit | LookupSensitiveEvents   |
| Enabling log collection              | cloudaudit | StartLogging            |
| Disabling log collection              | cloudaudit | StopLogging             |
| Updating CloudAudit               | cloudaudit | UpdateAudit             |
