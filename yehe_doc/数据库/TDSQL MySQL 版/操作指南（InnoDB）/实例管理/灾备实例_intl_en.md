This document describes how to create and manage disaster recovery read-only instances in the console.

## Overview
TDSQL for MySQL provides cross-AZ/region disaster recovery read-only instances to enhance your capacity to deliver continuous services at low costs while improving data reliability for applications with greater service continuity, data reliability, and compliance requirements.
>?Disaster recovery read-only instance costs the same as the source instance. For detailed pricing, see [Pricing](https://intl.cloud.tencent.com/document/product/1042/35777).

## Use Cases
- Remote disaster recovery: To ensure data security, you can use disaster recovery instances to back up your business and data in multiple regions. In the event that an instance becomes unavailable due to an AZ/region failure, you can quickly switch to a cross-AZ/region disaster recovery instance to minimize the impact on your business.
- Nearby access: You can use an instance in a specific AZ as the source instance and those in other AZs/regions as read-only instances, which provides users with nearby access, remote read capabilities, and improved access speed.
- Multi-region deployment: TDSQL for MySQL instance can be deployed across multiple regions. When an instance experiences network fluctuations or unavailability in an AZ/region, it can be switched to another AZ/region based on business needs.

## Features
- Disaster recovery read-only instances provide separate database connection addresses for read-only access. They can be used for nearby access and data analysis at a lower cost of device redundancy.
- A source instance can create one disaster recovery read-only instance that can be deployed in another region and AZ.
- Disaster recovery read-only instances support high-availability (1-source-1-replica and 1-source-2-replica) architecture, which helps avoid single point of failure for databases.
- If the source instance fails, the disaster recovery read-only instance can be activated in seconds to provide full read/write capability.
- Data in a disaster recovery read-only instance is synced over a private network, which has lower latency and greater stability than a public network.
- The traffic of data sync over the private network is currently free of charge during the promotion period. If fees will be charged for it, we will inform you in advance.

## Feature Limits
- Disaster recovery read-only instance do not support parameter setting and account management features.
Database version of disaster recovery read-only instance is the same as that of the source instance by default. Instance specification and disk size should be greater than or equal to that of the source instance.

## Directions
### Creating disaster recovery read-only instance
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/dcdb) and click an instance ID in the instance list to enter the instance management page.
2. In instance architecture diagram on the instance details page, click **Add Disaster Recovery Read-Only Instance**, and enter instance purchase page.
![](https://qcloudimg.tencent-cloud.cn/raw/cc2132fa43b38fab37e5ed2761d3a0be.png)
3. On the purchase page, select the billing mode, region, and other basic information of the disaster recovery read-only instance, and click **Buy Now**.
>?
>- The time required to complete the creation depends on the amount of data, and no operations can be performed on the source instance in the console during the creation. We recommend you do so at an appropriate time.
>- Only the entire instance data can be synced. Make sure that the disk space is sufficient.
>- Make sure that the source instance is in the running status and no tasks are executing; otherwise, the sync task may fail.  
3. Return to instance list after payment, initialize the instance, and you can proceed to the subsequent operations.

### Manage disaster recovery read-only instances
- **View disaster recovery read-only instances**
 You can view disaster recovery read-only instances from the region where they reside, and filter them out in the instance list.
![](https://qcloudimg.tencent-cloud.cn/raw/12a0753a3f9e67b4ebbffe99efe4818f.png)
- **View the relationship between the source instance and the disaster recovery read-only instance**
In instance architecture diagram on the instance details page, you can view the relationship between the source instance and the disaster recovery read-only instance.
![](https://qcloudimg.tencent-cloud.cn/raw/de145e7a78a76fb7902a7388e6e56de0.png)
- **Disaster recovery read-only instance feature**
 Disaster recovery read-only instance provides instance details, shard management, monitoring and alarms, parameter settings, data security, backup and restoration, and performance optimization features.


### Promoting disaster recovery read-only instance to source instance
You can promote a disaster recovery read-only instance to source instance in the console as needed.
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/dcdb), select the target disaster recovery read-only instance in the instance list, and click the instance ID to enter the instance management page.
2. Click **Promote to Source Instance** in the top-right corner to promote the disaster recovery read-only instance to source instance. After the promotion, the sync link with the source instance will be disconnected, so that the promoted instance can get data write capability and full TDSQL for MySQL functionality.
>!The disconnected sync link cannot be reconnected. You must exercise caution with this operation.
> 

