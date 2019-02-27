 
## Product Introduction  
CloudAudit (CA) is a service that records Tencent Cloud resource operations to allow you to view events on console when any problem occurs. The existing operation log records the operation information pushed by cloud products via the provided APIs, it has limited fields and the content is incomplete. In addition, it needs to gain the access to cloud products and operations individually, which causes the waste of manpower and other resources. Tencent Cloud CloudAudit solves the above problems. When you create a Tencent Cloud account, CloudAudit will be enabled by the account to automatically access different cloud products. Any activity that occurs in your Tencent Cloud account will be recorded in the CloudAudit events.
 

## How Does It Work  
When you create a Tencent Cloud account, CloudAudit will be enabled. When an activity occurs under your Tencent Cloud account, it is recorded in the CloudAudit events. You can easily view the events on the CloudAudit console by going to event history.

Through event history, you can view and search for activities that occur under your Tencent Cloud account in the last 7 days. In addition, you can create a CloudAudit audit to further archive, analyze, and respond to changes in your Tencent Cloud resources. An audit is a configuration that sends events to the specified COS bucket. You can create an audit using the CloudAudit console or CloudAudit APIs.




> **Note:**  
> You can specify COS buckets from any region for both operation record and tracking set.

CloudAudit has the direct access to other services on Tencent Cloud, it records the operation information of the user's cloud service resources, and displays the latest cloud API operation records. This make it a good replacement for any existing operation log.
You can perform the following operations on the event files:  

-  Create and store event files
When you perform such operations as addition, deletion or modification in a service to which CloudAudit has access to, such as elastic CVM, CBS and image service, the service automatically records the actions and results and sends the event file in the specified format to CloudAudit for archiving. The CloudAudit console retains operation records for the last 7 days. 

-  Query event files
You can query the operation records for the last 7 days by using the time and condition filters in the event list page of CloudAudit. 
The tracking set associated when CloudAudit is enabled is a logging application, which contains the information of operation log such as type and path. It allows you to create a directory to store your operation records. This directory displays the operation records for the last 7 days.


