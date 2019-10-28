
## Scenario
This document describes how to view, enable/disable, modify, rotate, and delete keys.


## Directions

### Viewing a Key
Log in to the KMS Console. Note that CMKs are region-specific. You can view the CMK list of another region by switching regions at the top of the page.

### Enabling/Disabling Keys
You can enable/disable keys [one by one](#step1) or [in batches](#step2).

<span id="step1"></span>
#### Single Key Operation
You can enable and disable a key in the operation column on the right.
![](https://main.qcloudimg.com/raw/06fcbd0cfedffb6ce36f82ed0697a40e.png)

 <span id="step2"></span>
#### Batch Operation

> If a key is disabled, all encryption and decryption operations that rely on it are also disabled. Therefore, you need to verify that the key is not in use before disabling it.

Find the keys you want to modify and select them. Click **Enable** or **Disable** at the top of the list. A confirmation box will pop up. Click **OK** to perform the corresponding operation on all the selected keys.
![](https://main.qcloudimg.com/raw/139b3ff4ddb80c14ecf2e47b90d8c350.png)

If you select keys in different statuses, you will be prompted as such in the pop-up confirmation box after you click **Enable** or **Disable**. Click **OK** and the system will only operate on eligible keys and the remaining keys will remain in their original status.



### Rotating a Key
You can rotate a key in the "Key Rotation" column on the right of the key list page. Key rotation is disabled by default. Once it is enabled, the CMK will be rotated annually.
![](https://main.qcloudimg.com/raw/eea7f293820006ffa11ad87451a016e5.png)

### Viewing Key Details
On the key list page, click **Key ID/Name** of a key to enter its details page, where you can view and modify the information of the key or use the online tools there for encryption or decryption.
![](https://main.qcloudimg.com/raw/460688ab752af3d1b2c04efb0124939c.png)

### Renaming or Modifying Purpose
On the key details page, you can change the name and purpose of the key.
Click **Key Name** or **Key Purpose** to update the information in the pop-up dialog box. Note that the key name can only contain letters, numbers, `_`, and `-` and cannot begin with "KMS-".
![](https://main.qcloudimg.com/raw/6b010990b2c603315b40386790c919c2.png)

### Deleting a Key

> Once a key is deleted, it cannot be restored, and all the data encrypted by the key can no longer be decrypted. To avoid accidental deletion, KMS adopts a scheduled deletion mechanism. Once you schedule a deletion, it will be carried out after a waiting period ranging from 7 to 30 days. You can cancel the scheduled deletion any time before it is carried out.

1. Log in to the KMS Console.
2. Click **Schedule Deletion** to the right of the key you want to delete. If the key is enabled then, you will need to disable it first.
![](https://请在此处插入控制台密钥列表页【计划删除】截图.png)
3. Enter the length of the waiting period and click **OK**. The key will be deleted after the waiting period.
![](https://请在此处插入控制台【计划删除密钥弹框】截图.png)
>!The waiting period before the deletion can be set to 7-30 days. Once a key is deleted, it cannot be restored, and all the data encrypted by the key can no longer be decrypted.
To prevent accidental deletion, the KMS automatic alarm will be triggered:
>- Before a key is deleted, any attempt to call the key will trigger the alarm.
>- The alarm will be triggered every day in the last 3 days before a key is deleted.
4. To cancel the scheduled key deletion, click **Cancel Key Deletion**. Once you cancel the deletion of a key, the key will be reset to the disabled state, and you will be able to perform operations on it, such as enabling, disabling, modifying, and deleting it.

