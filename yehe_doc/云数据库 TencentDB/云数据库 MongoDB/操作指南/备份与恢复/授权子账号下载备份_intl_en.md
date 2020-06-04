## Operation Scenario
To download a backup with a sub-account, you need to authorize the sub-account through the root account. This document describes how to grant a sub-account permissions on the CAM console.

## Directions
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/policy) and click **Create Custom Policy** on the policy management page.
2. Click **Create by Policy Syntax** in the pop-up dialog box.
3. Select **Blank Template** on the policy template selection page, and click **Next**.
4. In the "Policy Content" section on the policy edit page, set the policy content by referring to the following custom policy syntax, and then click **Done**.
In the following example, the `uid` is `125xxx8757`, which can be obtained from the "APPID" on the [Account Information](https://console.cloud.tencent.com/developer) page; the COS bucket path is `cmongo-gz-backup-125xxx8757`, which can be obtained from the backup download page on the [MongoDB Console](https://console.cloud.tencent.com/mongodb).
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
5. Return to the policy management page, find the new policy, and click **Associate** in the "Operation" column to associate with the sub-account.
6. After the association, configure COSCMD to download backups by referring to [Download Backup File](https://intl.cloud.tencent.com/document/product/240/32463).
