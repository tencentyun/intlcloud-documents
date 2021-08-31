 ## Overview  

CloudAudit (CA) is used to perform supervision, compliance check, operation review, and risk review for your Tencent Cloud account. It records logs, and monitors and records account activities associated with operations performed through Tencent Cloud console, APIs, command line tools, and other services in the Tencent Cloud infrastructure. The records will help you conduct security analysis, resource change tracking, and troubleshooting.


## How It Works  

CloudAudit will be enabled when you create a Tencent Cloud account. An activity under your Tencent Cloud account will be recorded as an event by CloudAudit. You can view event records on the **Operation Record** page of the CloudAudit console.

On this page, you can view and search for your Tencent Cloud account activities in the last 30 days. You can also create a CloudAudit tracking set to archive, analyze, and respond to changes in your Tencent Cloud resources. A tracking set is used to specify a COS bucket to store event records. You can create a tracking set via CloudAudit console or APIs.

>!You can specify a COS bucket of any supported region for both operation records and tracking sets.

CloudAudit can directly access other Tencent Cloud services, record user operations on service resources, and display the latest TencentCloud API operation records. Thus, CloudAudit can well replace any existing operation log features.
Two types of operations can be performed on event records:  
- Creating and storing event records
  When you perform operations such as addition, deletion, or modification on a service which CloudAudit can access, such as elastic CVM, CBS, or TCR, the service will automatically record the operations and results and then send the event record file in the specified format to CloudAudit for archiving. The CloudAudit console retains operation records for the last 30 days. 
- Querying event records
  You can select a time period and other filters on the **Operation Record** page to query operation records for the last 30 days.  
  A tracking set is a log application associated with CloudAudit when the service is activated. It contains types, paths, and other information of operation logs. It allows you to create a directory of operation records for the last 30 days.
