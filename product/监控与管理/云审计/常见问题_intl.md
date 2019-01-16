## General FAQs
### What is CloudAudit?
CloudAudit is a web service that records activities made on your account and sends log files to your COS buckets.

### What are the benefits of CloudAudit?
CloudAudit provides visibility into user activities by recording operations performed on your account. It records important information about each operation, including operation event time, user name, event name, resource type and resource name. The information helps you to track changes to Tencent Cloud resources and to address operational issues.

### Who should use CloudAudit?
Customers who need to track changes to resources, answer simple questions related to user activities, demonstrate compliance, troubleshoot, or perform security analysis should use CloudAudit.

## Getting Started
### If I am a new customer or an existing customer of Tencent Cloud who does not configure CloudAudit, do I need to enable or set options to view my account activities?
No. You can directly view your account activities in the past seven days by clicking **Products** -> **Management Tools** -> **CloudAudit** on the **Tencent Cloud** website or using the API.

### What search filters can I use to view account activities?
You can view related account activities according to user name, resource type, resource name, event source, event ID, keyword or corresponding operation event time.



### Will it incur charges for enabling CloudAudit event history when I create an account?
There is no cost for viewing or searching for account activities with CloudAudit event history.

### Can I disable CloudAudit event history for my account?
For any created CloudAudit audit, you can disable logging or delete the audit. In this way, it will also stop sending account activities to COS buckets (you specified as part of your audit configuration).

## Service
### What services are supported by CloudAudit?
CloudAudit supports Cloud Virtual Machine (CVM), Cloud Access Management (CAM) and Account.


### What information does an operation record contain?
A single operation record includes access key, region, error code, event ID, event name, event source, event time, request ID, source IP address and user name.
### How long does it take for CloudAudit to send an API call event?
Typically, the operation record event will be sent to the specified COS bucket 5-10 minutes after the API is called.



## Others
### Will enabling CloudAudit affect the performance of Tencent Cloud resources or increase API call latency?
No. Enabling CloudAudit will neither affect the performance of Tencent Cloud resources nor increase API call latency.


