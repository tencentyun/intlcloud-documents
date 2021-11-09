## General

### What is CloudAudit?

CloudAudit is a web service that records the activities of your account and delivers log files to your COS bucket.

### What are the benefits of CloudAudit?

CloudAudit provides visibility into user activities by recording operations performed on your account. It records important information about each operation, including operation event time, username, event name, resource type and resource name. Such information helps you track changes to Tencent Cloud resources and address operational issues.

### Who should use CloudAudit?

CloudAudit is designed for customers who need to track resource changes, answer simple questions about user activity, prove compliance, troubleshoot, or perform security analysis.

## Getting Started
### Do I need to enable or set options to view my account activity if I'm a new or current Tencent Cloud customer who hasn't set up CloudAudit?

No. You can directly view account activities in the last 30 days in the console (**Tencent Cloud** > **Management and Audit** > **CloudAudit**) or through APIs.

### What search filters can I use to view account activities?

You can view related account activities by username, resource type, resource name, event source, event ID, keyword, or corresponding operation event time.

### Will there be any charges if I enable CloudAudit event history when I create an account?

There are no charges for viewing or searching for account activities with CloudAudit event history.

### Can I disable CloudAudit event history for my account?

For any created CloudAudit tracking set, you can disable the logging feature or delete the tracking set. This operation will also stop delivering account activities to your COS bucket (the one specified as part of your tracking set configuration).

## Service

### What services are supported by CloudAudit?

CloudAudit currently supports most Tencent Cloud services. You can view them in the **Resource Event Name** drop-down list on the [Operation Record](https://console.cloud.tencent.com/cloudaudit) page.


### What information does an operation record contain?

A single operation record includes access key, region, error code, event ID, event name, event source, event time, request ID, source IP address and user name.

### How long does it take for CloudAudit to send an API call event?

Typically, the operation record event will be delivered to the specified COS bucket 5-10 minutes after the API is called.


## Others

### Will enabling CloudAudit affect the performance of Tencent Cloud resources or increase API call latency?

No. Enabling CloudAudit will not affect the performance of Tencent Cloud resources or increase the API call latency.


