CloudAudit provides various features such as operation log, tracking set, and operation log export.

## Operation Log
This feature logs the operations performed under a Tencent Cloud account in the past 30 days.
- **Operation log list**
  In the CloudAudit console, you can view the operation log list as well as other information such as the event time, username, event name, resource type, and resource name.
- **Operation log details**
  You can also view the details of a single log, including access key, region, error code, event ID, event name, event source, event time, quest ID, source IP address, and username. 

## Tracking Set
Tracking set is an enhanced feature of the operation log. It ensures the traceability and security of your staff's operations on assets. It includes such information as operation log type and storage path. When your tracking set is functioning normally, it stores the operation logs under your account in the configured bucket. If it is disabled, operation logs will not be stored in the bucket.

### Operations of tracking set
CloudAudit delivers your operation logs to the specified COS bucket every 5 minutes. Currently, the tracking set feature only supports configuring buckets in Beijing, Shanghai, and Hong Kong (China) region for log storage.
It allows you to create and delete tracking sets, edit the configuration of tracking sets, and disable the operation logging feature.
> You can only create one tracking set during the beta period of CloudAudit.

### Advanced features of tracking set
#### Setting log file prefix
The log file prefix, i.e., the prefix of log files stored in COS, is mainly used to specify the file storage path.
One file is generated per hour. The specified bucket and file prefix are two elements of the log file path.
For example, if you specify "audit" as your storage bucket, and the file prefix is "myaudit", then the path of your CloudAudit logs will be:
```
audit/myaudit/${YYYYMMDDH}/xxxxxxxxxxxxx ("xxxxxxxxxxxxx" indicates the file name).
```


## Operation Log Export
You can export logs of the past 30 days in the CloudAudit console. To export older logs, please submit a ticket for application. Logs can be exported in the following three steps:
- **Selecting time period**:
  You can export the logs in a specified time period, and the backend will start exporting logs offline after receiving your request.
- **Exporting data offline**:
  The export request can be canceled before 00:00 on the next day. After then, the export process cannot be canceled. Once the data export is completed, the export result will be sent to you.
- **Delivering data to COS**:
  After the data is exported, the system will store it for up to 5 business days. If you want to persist the storage, the data should be delivered to a COS bucket.



