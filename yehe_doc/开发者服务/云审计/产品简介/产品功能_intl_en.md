CloudAudit provides operation record, tracking set, and record export among other features.

## Operation Record
CloudAudit records operations performed under a Tencent Cloud account in the last 30 days.
- **Operation record list**
  You can view the operation records and their event time, username, event name, resource type, and resource name.
- **Operation record details**
  You can also view details of an operation, including the key ID, region, error code, event ID, event name, event source, event generation time, request ID, source IP address, and username.

## Tracking Set
Tracking set is an enhanced feature of the operation record. It tracks operations performed by customers' staff on their assets and thus ensures asset security. It contains types, paths, and other information of operation logs. When a tracking set is enabled, it stores operation logs under your account to the specified bucket. If it is disabled, it will not store operation logs to the bucket.

### Tracking set settings
CloudAudit ships operation logs to the specified COS bucket every five minutes. Currently, you can only use a tracking set to specify buckets in Beijing, Shanghai, and Hong Kong (China) regions for log storage.
Moreover, you can create and delete tracking sets, edit their configurations, and disable operation log recording.
>!During the beta test of CloudAudit, you can create up to 5 tracking sets.

### Tracking set advanced settings

#### Setting log file prefix
You can set a log file prefix to specify the log storage path in a COS bucket.
Both the specified bucket name and file prefix are included in the log file path. One log file is generated every hour.
For example, if the specified bucket is "audit" bucket and the file prefix is "myaudit", your CloudAudit log storage path will be:
```
audit/myaudit/${YYYYMMDDH}/xxxxxxxxxxxxx ("xxxxxxxxxxxxx" is the file name)
```


## Record Export
>?We recommend you use the tracking set preferably, as it offers more comprehensive log information without time limits. For more information, please see [Shipping Log with Tracking Set](https://intl.cloud.tencent.com/document/product/1021/42145).
>
You can only view logs of the last 30 days online. If you want to view older logs, please request for export, which contains three steps:
- **Select a time period**
  Select a time period of logs for export. The backend will start exporting logs in offline mode after receiving your request.
- **Export data in offline mode**
  The export operation can be canceled before 24:00 of the day you send the request. After that, you cannot cancel the operation. Once the data is successfully exported, we will send you a notification.
- **Ship data to COS**
  After the export, CloudAudit will store the data for up to five business days. To achieve persistent storage, please ship the data to a COS bucket.



