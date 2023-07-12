## Overview

CLS provides various types of resources. Some of its APIs allow you to configure user permissions based on resources. See [here](https://intl.cloud.tencent.com/document/product/614/45004) for examples.
The following table lists the types of resources that can be authorized in Cloud Access Management (CAM). Note that authorization by tag indicates whether a tag can be used to specify the range of resources on which users have operation permissions.

| Resource Type                                | Resource Description Method in Access Policies                                     | Authorization by Tag |
| :-------------------------------------- | :----------------------------------------------------------- | ---------- |
| Logset                                  | `qcs::cls:$region:$account:logset/*`<br />`qcs::cls:$region:$account:logset/$logsetId` | Supported       |
| Log topic                                | `qcs::cls:$region:$account:topic/*`<br />`qcs::cls:$region:$account:topic/$topicId` | Supported       |
| Machine group                                  | `qcs::cvm:$region:$account:machinegroup/*`<br />`qcs::cvm:$region:$account:machinegroup/$machinegroupId` | Supported       |
| Collection configuration                                | `qcs::cls:$region:$account:config/*`<br />`qcs::cls:$region:$account:config/$configId` | Not supported     |
| Dashboard                                  | `qcs::cls:$region:$account:dashboard/*`<br />`qcs::cls:$region:$account:dashboard/$dashboardId` | Supported       |
| Alarm policy                                | `qcs::cls:$region:$account:alarm/*`<br />`qcs::cls:$region:$account:alarm/$alarmId` | Not supported     |
| Notification channel group                              | `qcs::cls:$region:$account:alarmNotice/*`<br />`qcs::cls:$region:$account:alarmNotice/$alarmNoticeId` | Not supported     |
| Data processing task                            | `qcs::cls:$region:uin/$account:datatransform/*`<br />`qcs::cls:$region:uin/$account:datatransform/$TaskId` | Not supported     |
| Shipping task (COS)                         | `qcs::cls:$region:$account:shipper/*`<br />`qcs::cls:$region:$account:shipper/$shipperId` | Not supported     |
| Other resource types (disused; used by APIs of earlier versions only) | Single chart in the dashboard:<br />`qcs::cls:$region:$account:chart/*`<br />`qcs::cls:$region:$account:chart/$chartId` | Not supported     |

You need to change the variable parameters such as `$region` and `$account` to your actual parameter information.

For all the APIs supported by CLS and their resource description methods, see here. APIs adopting the authorization granularity of resource support user permission configuration by using the methods of the corresponding resource types described above. For APIs adopting the authorization granularity of API, the corresponding resource range in a CAM permission policy must be `*`.


## Practice

Different types of resources in CLS are associated with each other. For example, log sets contain log topics, and log topics must apply collection configuration to machine groups. Directly configuring user permissions in CAM permission policies according to resource IDs results in difficult management and is likely to cause the error where users do not have permissions on some APIs. Therefore, you are advised to configure CAM permission policies as follows:
- For resource types and corresponding APIs that support authorization by tag, bind related resources with tags and use tags to specify the ranges of resources on which users have operation permissions. For example, you can bind log topics, logsets, and related dashboards with tags so that you can [assign management permissions on log topics with specified tags](https://intl.cloud.tencent.com/document/product/614/45004) or [assign management permissions on log topics and dashboards with specified tags](https://intl.cloud.tencent.com/document/product/614/45004). In either way, you can enable users to have the operation permissions on the APIs of the three types of resources.
- For resource types and corresponding APIs that do not support authorization by tag, to simplify management, you can directly set the resource range in the CAM permission policy to `*`, indicating all resources. To avoid misoperations by ordinary users, you can configure read-only permissions for ordinary users and management permissions for admins. For example, you can [assign admins the management permissions on all data processing tasks](https://intl.cloud.tencent.com/document/product/614/45004) and [assign ordinary users the read-only permissions on all data processing tasks](https://intl.cloud.tencent.com/document/product/614/45004).

>?For more use cases, see [Examples of Custom Access Policies](https://intl.cloud.tencent.com/document/product/614/45004).

