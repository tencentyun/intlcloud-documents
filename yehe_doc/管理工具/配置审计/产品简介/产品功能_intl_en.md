Features

Config Audit allows you to log and view Tencent Cloud resource configuration changes, manage configuration monitoring, detect configuration compliance, and perform other relevant operations.

**1.** **Configuration monitoring management**

After activating Config Audit, you need to set the monitoring scope. After a Tencent Cloud service is added to the monitoring scope, the system will generate a copy of initial configuration data based on the current configuration of the added service, which will act as a reference basis for future configuration changes. Then, the service configuration will be pulled and compared once every 10 minutes, and once a configuration change is detected, a new change log will be generated and retained.

**2.** **Configuration change log**

The change logs can be traced back to the moment the corresponding Tencent Cloud service is added to the monitoring scope. You can query the service logs by various information such as resource type and resource name and then view the change transactions on the details page. In addition, Config Audit allows you to query the configuration change details in different time periods by specifying the time period, associates configuration change logs with CloudAudit operation logs, and provides other relevant features to help you quickly locate change details.

**3.** **Quick activation/deactivation**

You can activate/deactivate this service in the console with no additional configuration required. If you activate the service again after it is deactivated, the configuration changes during the deactivation period will not be logged by the system.

 

 

 

 