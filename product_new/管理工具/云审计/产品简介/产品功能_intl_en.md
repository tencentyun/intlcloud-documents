CloudAudit mainly provides various features such as operation log record, tracking set, and history export.

## Operation Record
This feature records the operations performed by a user under the Tencent Cloud account in the past 30 days.
-**Operation record list**:
  You can view the operation record list as well as the operation time, username, event name, resource type, resource name, and other information in the console.
-**Operation record details**:
  You can also obtain the details of a single operation record, including the access key, region, error code, event ID, event name, event source, event time, request ID, source IP address, and username.

## Tracking Set
Tracking set is an enhanced feature of operation record. It ensures the traceability and security of your staff's operations on assets. It includes such information as operation log type and path. When your tracking set is functioning normally, it stores the operation log records under your account in the configured bucket. If it is disabled, operation logs will not be stored in the bucket.

### Tracking set operations
You can perform the following operations on a tracking set: creating and deleting a tracking set, editing its configuration, and disabling its logging feature.
>You can only create one tracking set during the beta test of CloudAudit.

### Advanced features of tracking set
#### Setting log file prefix
The log file prefix, i.e., the prefix of log files stored in COS, is mainly used to specify the file storage path.
If you specify a prefix of "test", then the log path will be `/test/Year/Month/Day`; for example:
```shell
/test/2017/11/02
```
Log file naming convention: `year/month/day/time (down to the hash value of minute).gz; for example:
```shell
201711021635_26c6f84d-bd41-4211-a9d4-2c223e31295d_0.gz
```



## History Export
You can export logs of the past 30 days in the CloudAudit Console. To export older logs, please submit a ticket for application. Logs can be exported in the following three steps:
-**Selecting time period**:
  You can export the logs in the specified time period, and the backend will start the offline export after receiving your request.
-**Exporting data offline**:
  The export request can be canceled before 00:00 on the next day. After then, the export process cannot be canceled. Once the data export is completed, the export result will be sent to you.
-**Delivering data to COS**:
  After the data is exported, the system will store it for up to 5 business days. If you want to persist the storage, the data should be delivered to a COS bucket.



