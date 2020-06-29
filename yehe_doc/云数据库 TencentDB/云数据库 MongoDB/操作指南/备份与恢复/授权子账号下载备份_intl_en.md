## Overview
To download a backup with a sub-account, you need to first authorize the sub-account with the root account. This document describes how to grant a sub-account permissions on the CAM console.

## Directions
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/policy), go to **Policies** from the left sidebar and click **Create Custom Policy**.
2. Click **Create by Policy Syntax** in the pop-up dialog box.
3. Select **Blank Template** and click **Next**.
4. Set the **policy content** by referring to the following custom policy syntax, and click **Done**.
In the following example, we are using `125xxx8757` for the `uid`. This is the **APPID** in [Account Information](https://console.cloud.tencent.com/developer). We are using `cmongo-gz-backup-125xxx8757` for the COS bucket path. This can be obtained from **Backup and Rollback** tab in the instance details page on the [MongoDB Console](https://console.cloud.tencent.com/mongodb).
Policy syntax:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cos:*",
            "effect": "allow",
            "resource": "qcs::cos::uid/125xxx8757:cmongo-gz-backup-125xxx8757/*"
        }
    ]
}
```
![](https://main.qcloudimg.com/raw/b06d62f32fad931f2a7c031c22847035.png)
5. Return to **Policies**, locate the new policy, and click **Associate** in the "Operation" column to associate with the sub-account.
6. After association, see [Download Backup File](https://intl.cloud.tencent.com/document/product/240/32463) for instructions on how to configure COSCMD for downloading backup files.
