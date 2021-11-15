You can enable/disable unauthorized access in the TencentDB for MongoDB console.
>?Unauthorized access is currently supported only for MongoDB v3.6 and v4.0.


## Directions
<span id = "sjnhbb"></span>
### (Optical) Upgrading the kernel version
>?To enable unauthorized access, the existing instances created before the unauthorized access feature became available need upgrade their kernel versions first.

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb). In the instance list, select a region, click an instance ID, and enter the instance details page.
2. Click **Upgrade** to the right of **Unauthorized Access** in the **Basic Info** section.
![](https://main.qcloudimg.com/raw/86de5591810d175b3f894802850d334a.png)
3. In the pop-up dialog box, click **OK**.
>!There is a short disconnection lasting for seconds during the upgrade.
>
![](https://main.qcloudimg.com/raw/9abf4438b26a9f573034ae6e772bad2d.png)
4. On the instance details page, the instance status changes to "Processing". When the instance status changes to "Running", you can enable unauthorized access for it.
![](https://main.qcloudimg.com/raw/2561653b1b5c4564632df3fc4c171b29.png)

### Enabling unauthorized access
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb). In the instance list, select a region, click an instance ID, and enter the instance details page.
2. Click **Enable** to the right of **Unauthorized Access** in the **Basic Info** section.
![](https://main.qcloudimg.com/raw/4ffd1f99bf0240bf2f9553168dff8cc6.png)
3. In the pop-up dialog box, click **OK**.
![](https://main.qcloudimg.com/raw/bf12dc0f3b27ae0b7bdb532a7d8c77ed.png)
4. On the instance details page, when the instance status changes to "Running", you can use the instance with unauthorized access enabled.

### Disabling unauthorized access
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb). In the instance list, select a region, click an instance ID, and enter the instance details page.
2. Click **Disable** to the right of **Unauthorized Access** in the **Basic Info** section.

## References
TencentDB for MongoDB can be accessed through MongoDB shell or drivers which support various programming languages. For more information, please see [Access Connection](https://intl.cloud.tencent.com/document/product/240/7092).

