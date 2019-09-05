
## Scenario
This document describes how to view, enable/disable, modify, and rotate keys.


## Directions

### Viewing a Key
Log in to the KMS Console. Note that CMKs are region-specific. You can view the CMK list of another region by switching regions at the top of the page.

### Enabling/Disabling Keys
You can enable/disable keys [one by one](#step1) or [in batches](#step2).

<span id="step1"></span>
#### Single Key Operation
You can enable and disable a key in the operation column on the right.
![](https://main.qcloudimg.com/raw/6223cb510e8ad0d1b7eee09f88e0dd9c.png)

 <span id="step2"></span>
#### Batch Operation

> If a key is disabled, all encryption and decryption operations that rely on it are also disabled. Therefore, you need to verify that the key is not in use before disabling it.

Find the keys you want to modify and select them. Click **Enable** or **Disable** at the top of the list. A confirmation box will pop up. Click **OK** to perform the corresponding operation on all the selected keys.
![](https://main.qcloudimg.com/raw/f35339e7f5f7315acb3a7f8cd73789f8.png)

If you select keys in different statuses, you will be prompted as such in the pop-up confirmation box after you click **Enable** or **Disable**. Click **OK** and the system will only operate on eligible keys and the remaining keys will remain in their original status.



### Rotating a Key
You can rotate a key in the "Key Rotation" column on the right of the key list page. Key rotation is disabled by default. Once it is enabled, the CMK will be rotated annually.
![](https://main.qcloudimg.com/raw/8871713edc33fbe41a8c4693ea09e947.png)

### Viewing Key Details
On the key list page, click **Key ID/Name** of a key to enter its details page, where you can view and modify the information of the key or use the online tools there for encryption or decryption.
![](https://main.qcloudimg.com/raw/f75e3e948f41231b11d63dc873c52be0.png)

### Renaming or Modifying Purpose
On the key details page, you can change the name and purpose of the key.
Click **Key Name** or **Key Purpose** to update the information in the pop-up dialog box. Note that the key name can only contain letters, numbers, `_`, and `-` and cannot begin with "KMS-".
![](https://main.qcloudimg.com/raw/a83496a991bbe724af8833be44e475a8.png)

