## Overview
To download a backup with a sub-account, you need to first authorize the sub-account with the root account. This document describes how to grant a sub-account permissions on the CAM console.

## Directions
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/policy), go to **Policies** from the left sidebar and click **Create Custom Policy**.
2. Click **Create by Policy Syntax** in the pop-up dialog box.
3. Select **Blank Template** and click **Next**.
4. Set the **policy content** by referring to the following custom policy syntax, and click **Done**.
 - uid: the value is fixed to 1257588757.
 - COS bucket path: it can be obtained from **Backup and Rollback** tab on the instance details page in the [MongoDB Console](https://console.cloud.tencent.com/mongodb).
![](https://main.qcloudimg.com/raw/21779499370def25c7d82fab11972dfa.png)
Policy syntax (we are using `cmongo-gz-backup-1257588757` for the COS bucket path in the following example):
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cos:*",
            "effect": "allow",
            "resource": "qcs::cos::uid/1257588757:cmongo-gz-backup-1257588757/*"
        }
    ]
}
```
![](https://main.qcloudimg.com/raw/8d12cb51b4c7229361c519cc35a61b41.png)
5. Return to **Policies**, locate the new policy, and click **Associate** in the "Operation" column to associate with the sub-account.
6. After association, see [Download Backup File](https://intl.cloud.tencent.com/document/product/240/32463) for instructions on how to configure COSCMD for downloading backup files.
