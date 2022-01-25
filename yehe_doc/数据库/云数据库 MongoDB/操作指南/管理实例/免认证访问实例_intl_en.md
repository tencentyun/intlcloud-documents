TencentDB for MongoDB supports unauthorized access to instances. You can enable it for quick connection and access to databases.

## Background
Unauthorized access enables you to efficiently and quickly access database instances but brings security risks. Therefore, enable this feature with caution.

## Version Description
Currently, only TencentDB for MongoDB 3.6 and 4.0 support unauthorized access.

## Notes
- Upgrade to support unauthorized access involves kernel upgrade and momentary disconnections.
- After unauthorized access is enabled, the instance will restart. Therefore, enable this feature during off-peak hours.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB instance is in **Running** status.
- The TencentDB for MongoDB instance is a replica set or sharded instance on 3.6 or 4.0.

## Directions
### [(Optional) Upgrading kernel version](id:sjnhbb)
>?If you want to use the unauthorized access feature on an instance created before this feature is launched, you need to upgrade the instance's kernel version first.

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page.
6. In the **Basic Info** section on the **Instance Details** page, click **Upgrade** after **Unauthorized Access**.
![](https://main.qcloudimg.com/raw/86de5591810d175b3f894802850d334a.png)
7. In the **Upgrade to Support Unauthorized Access** pop-up window, read the prompt message carefully and click **OK**.
> !Upgrade to support unauthorized access involves kernel upgrade and momentary disconnections.
> 
![](https://main.qcloudimg.com/raw/9abf4438b26a9f573034ae6e772bad2d.png)
8. On the **Instance Details** page, the instance status becomes **Upgrading database version**. After the status becomes **Running**, you can proceed to the subsequent operations.
![](https://main.qcloudimg.com/raw/2561653b1b5c4564632df3fc4c171b29.png)

### Enabling unauthorized access
1. In the **Basic Info** section on the **Instance Details** page, click **Enable** after **Unauthorized Access**.
![](https://main.qcloudimg.com/raw/4ffd1f99bf0240bf2f9553168dff8cc6.png)
2. In the **Enable Unauthorized Access** pop-up window, read the prompt message carefully and click **OK**.
![](https://main.qcloudimg.com/raw/bf12dc0f3b27ae0b7bdb532a7d8c77ed.png)
3. On the **Instance Details** page, wait for the instance status to become **Running**, and then you can use the instance normally.

### Disabling unauthorized access
In the **Basic Info** section on the **Instance Details** page, click **Disable** after **Unauthorized Access** to disable this feature.

## Relevant Operations
You can access TencentDB for MongoDB databases by using MongoDB shell or drivers in various programming languages as instructed in [Connecting to TencentDB for MongoDB Instance](https://intl.cloud.tencent.com/document/product/240/7092).

