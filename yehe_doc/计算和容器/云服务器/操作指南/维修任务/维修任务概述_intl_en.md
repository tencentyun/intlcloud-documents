The maintenance task feature aims to provide a standard authorized failure maintenance service. When the platform detects an exception that affects the instance running status (such as occasional sudden host failure or perceptible platform upgrade and maintenance), it will send you a notification, record the maintenance task, and perform specified maintenance operations at the specified maintenance time.

A maintenance task helps you stay on top of and handle sudden problems with instances, improve your system stability and maintenance efficiency, and reduce the maintenance costs. You can back up the data promptly before executing system events to get prepared at the application layer. In addition, you can query the processed maintenance tasks in the last month to get data such as failure processing and recovery time.


<dx-alert infotype="explain" title="">
To use the maintenance task feature, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.
</dx-alert>




## Strengths

#### Free enablement
You can enable this feature as needed without purchasing it additionally. After creating and using an instance, you can view the maintenance task list and handle the current risks.

#### Comprehensive coverage
This feature covers various instance exceptions such as instance running exception, running (risk) alarm, disk exception, and network connection exception.

#### Elastic configuration
This feature allows you to configure multiple preset processing policies, each of which can be associated with different computing product instances. After a preset processing policy is configured, it can be automatically associated with an instance through a tag during instance creation.

#### Flexible service
The authorization center provides a custom authorization service, which can be connected to through standard TencentCloud API 3.0 or the console.


## Use Cases

#### Real-Time risk monitoring
You can view the major risk events that occurred in instances during the operations of underlying platform infrastructure services in real time in the list in the authorization center.

#### Custom authorization
You can customize authorization policies. To configure custom authorization for an instance, you can set instance tags and preset authorization policies.

#### Prompt exception handling
The risk and exception event information of instances are sent to the authorization center immediately, where you can prevent business risks and process authorization promptly.


## Usage Limits
Currently, this feature is applicable to CVM, CVM Dedicated Host, and CPM 2.0 instances.
