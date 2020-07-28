Overview

---------



 **Product overview**

Config Audit, a subproduct of Account Security Service (ACSS), is used to monitor Tencent Cloud resource configuration changes. With Config Audit, you can view the relationships between and configurations of Tencent Cloud resources as well as the resource configuration change details by time in a centralized manner. In addition, Config Audit provides a compliance audit feature, which effectively helps you use Tencent Cloud resources in a more compliant way. Once a non-compliant configuration change occurs, it will immediately send an alarm notification to ensure your account resource security.

**How it works**

After you activate Config Audit and set the monitoring scope, the system will generate a copy of initial configuration items for each monitored Tencent Cloud resource as a reference basis and continue to monitor the CloudAudit data changes of the corresponding services. If configuration changes, a new configuration item log will be generated, and the legacy configuration item will be logged. In addition, Config Audit data is also associated with the operation log data in CloudAudit; therefore, you can monitor the resource configuration change details and the corresponding operation logs over time.

  ![image-20200715203019066](https://main.qcloudimg.com/raw/472be465dd738e5f669ea3331d2e5167.png)

  Config Audit Flowchart

