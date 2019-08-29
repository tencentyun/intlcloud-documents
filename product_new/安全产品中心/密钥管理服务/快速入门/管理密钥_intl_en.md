
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
![](https://main.qcloudimg.com/raw/90347ebd779cc051b4e0e6de0f671e73.png)

 <span id="step2"></span>
#### Batch Operation

> If a key is disabled, all encryption and decryption operations that rely on it are also disabled. Therefore, you need to verify that the key is not in use before disabling it.

Find the keys you want to modify and select them. Click **Enable Keys** or **Disable Keys** at the top of the list. A confirmation box will pop up. Click **OK** to perform the corresponding operation on all the selected keys.
![](https://main.qcloudimg.com/raw/8fe7e9294fbba21d2cd7941292855749.png)

If you select keys in different statuses, you will be prompted as such in the pop-up confirmation box after you click **Enable Keys** or **Disable Keys**. Click **OK** and the system will only operate on eligible keys and the remaining keys will remain in their original status.



### Rotating a Key
You can rotate a key in the "Key Rotation" column on the right of the key list page. Key rotation is disabled by default. Once it is enabled, the CMK will be rotated annually.
![](https://main.qcloudimg.com/raw/8de491efe514cd28356daccf10125763.png)

### Viewing Key Details
On the key list page, click **Key ID/Name** of a key to enter its details page, where you can view and modify the information of the key or use the online tools there for encryption or decryption.
![](https://main.qcloudimg.com/raw/28506cebdbaa8b0beba4e50178c83f8e.png)

### Renaming or Modifying Purpose
On the key details page, you can change the name and purpose of the key.
Click **Key Name** or **Key Purpose** to update the information in the pop-up dialog box. Note that the key name can only contain letters, numbers, `_`, and `-` and cannot begin with "KMS-".
![](https://main.qcloudimg.com/raw/4aa2f00e07de53a75e6e51391d920f59.png)

