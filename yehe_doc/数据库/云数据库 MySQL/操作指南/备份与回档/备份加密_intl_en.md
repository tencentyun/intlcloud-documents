TencentDB for MySQL supports backup encryption. To use an encrypted backup, you need to download it and its encryption key for decryption. This document describes how to enable or disable the backup encryption feature and download a key.

## Prerequisites
The MySQL instance architecture is two-node/three-node.

## Note
- After backup encryption is enabled, the previous backup will not be encrypted, but the new physical backup files will be automatically encrypted for storage.
- You cannot modify the backup encryption key.
- After backup encryption is enabled, you don't need to manually decrypt a backup in the console, as the backend will decrypt it automatically before relevant operations such as cloning. However, if you download an encrypted backup, you need to download its key for decryption. For more information, see [Restoring Database from Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910).

## Enabling backup encryption
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Backup and Restoration** and click **Backup Encryption**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/TUzv572_2.png)
3. In the pop-up window, click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/m4ER607_3.png)
4. After backup encryption is enabled, click **Manual Backup** on the **Backup and Restoration** tab.
5. On the manual backup settings page, select the configuration and click **OK**. Then, new physical backups will be encrypted.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Backup Mode</td>
<td>Select **Physical cold backup**.</td></tr>
<tr>
<td>Object</td>
<td>It is the instance by default.</td></tr>
<tr>
<td>Backup Encryption</td>
<td>It is enabled by default.</td></tr>
<tr>
<td>Backup Name</td>
<td>It can contain up to 60 letters, digits, or symbols (-_./()[]+=:@).</td></tr>
</tbody></table>

## Disabling backup encryption
>? After backup encryption is disabled, the previous backup will not be decrypted, and the new physical backup files will not be encrypted for storage.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click the ID of the target instance or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Backup and Restoration** and click **Backup Encryption**.
3. In the pop-up window, click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Utbk681_4.png)

## Downloading a backup key
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click the ID of the target instance or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Backup and Restoration** > **Data Backup List** tab, find the target backup, and click **Download Key** in the **Operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/GMMj645_5.png)
3. In the pop-up window, select the file path where to save the key and click **Download**.

