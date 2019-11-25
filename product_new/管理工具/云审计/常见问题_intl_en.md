## General FAQs

### What is CloudAudit?

CloudAudit is a web service that records the activities of your account and delivers log files to your COS bucket.

### What are the benefits of CloudAudit?

CloudAudit provides visibility into user activities by recording operations performed on your account. It records important information about each operation, including operation event time, username, event name, resource type, and resource name. Such information helps you track changes to Tencent Cloud resources and address operational issues.

### Who should use CloudAudit?

CloudAudit is ideal for those who need to track changes to resources, answer simple questions about user activities, demonstrate compliance, troubleshoot issues, or perform security analysis.

## Getting Started

### If I am a new customer of Tencent Cloud or an existing customer with no CloudAudit set up, do I need to enable or set options to view my account activities?

No. You can directly view your account activities in the past 30 days by clicking **Products** > **Management Tools** > **CloudAudit** on the **Tencent Cloud** website or using APIs.

### What search filters can I use to view account activities?

You can view relevant account activities by username, resource type, resource name, event source, event ID, keyword, or corresponding operation event time.

### Will there be any charges if I enable CloudAudit event history when I create an account?

There is no cost for viewing or searching for account activities with CloudAudit event history.

### Can I disable CloudAudit event history for my account?

For any created CloudAudit tracking set, you can disable the logging feature or delete the tracking set. This operation will also stop delivering account activities to your COS bucket (the one specified as part of your tracking set configuration).

## Services

### What services are supported by CloudAudit?

CloudAudit supports Cloud Virtual Machine (CVM), Cloud Access Management (CAM), and your Tencent Cloud account.

### What information does an operation record contain?

A single operation record contains information of access key, region, error code, event ID, event name, event source, event time, request ID, source IP address, and username.

### How long does it take for CloudAudit to send an API call event?

Typically, the operation record event will be delivered to the specified COS bucket 5-10 minutes after the API is called.



## Other

### Will enabling CloudAudit affect the performance of Tencent Cloud resources or increase the API call latency?

No. Enabling CloudAudit will not affect the performance of Tencent Cloud resources or increase the API call latency.
