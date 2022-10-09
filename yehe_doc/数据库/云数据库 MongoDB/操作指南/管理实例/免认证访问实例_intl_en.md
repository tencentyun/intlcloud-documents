## Background
Auth-free access allows you to access your TencentDB instance quickly and efficiently. However, it also involves security risks. We recommend you enable this feature in test or maintenance scenarios and disable it during business operations.

## Version requirements
Instances on v3.6, v4.0, v4.2 and v4.4 support auth-free access.

## Notes
- Upgrade to support auth-free access involves kernel upgrade and momentary disconnections.
- After auth-free access is enabled, the instance will **restart**. Therefore, enable this feature during off-peak hours.

## Prerequisites
- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB instance is in **Running** status.
- On the **Instance Details** page, the status of **Auth-Free Access** is **Not enabled yet**.

## Enabling auth-free access
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the instance ID to enter the **Instance Details** page.
6. On the **Instance Details** page, click **Enable** after **Auth-Free Access**.
7. In the **Enable Auth-Free Access** pop-up window, confirm the impact of enabling this feature and click **OK**.
![](https://main.qcloudimg.com/raw/9abf4438b26a9f573034ae6e772bad2d.png)
8. On the **Instance Details** page, wait for the instance status to become **Running**. Then, you can connect to the database at the configured private IPv4 address and port without entering the username and password.

## Disabling auth-free access
On the **Instance Details** page, click **Disable** after **Auth-Free Access** to disable this feature.

## Relevant operations
You can access TencentDB for MongoDB databases by using MongoDB shell or drivers in various programming languages as instructed in [Connecting to TencentDB for MongoDB Instance](https://intl.cloud.tencent.com/document/product/240/7092).

