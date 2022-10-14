A sub-account has no RUM permissions by default and can access RUM resources only after being granted relevant permissions by the root account.

## Prerequisites
Log in to the Tencent Cloud console with the root account or a sub-account with the `QcloudCamFullAccess` permission and create a sub-account as instructed in [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).

## Custom Policy
1. Use the root account or a sub-account with the `QcloudCamFullAccess` permission to log in to the **CAM** console and go to the [**Policies**](https://console.cloud.tencent.com/cam/policy) page.
2. Click **Create Custom Policy** > **Create by Policy Syntax** and select **Blank Template**. Edit the policy as instructed in [Policy Syntax Description](https://intl.cloud.tencent.com/document/product/1131/44511).
<img src = "https://qcloudimg.tencent-cloud.cn/raw/75840c4c667d7e6b853a273c6e5a2017.png" style = "width:90%">

## Policy Authorization
>?RUM creates default permission policies `QcloudRUMFullAccess` (full access to RUM) and `QcloudRUMReadOnlyAccess` (read-only access to RUM) for you. You can search for a default policy for quick authorization. You can also use a custom policy for authorization. Then, the sub-account can access the relevant resources.

1. Use the root account or a sub-account with the `QcloudCamFullAccess` permission to log in to the **CAM** console and go to the [**Policies**](https://console.cloud.tencent.com/cam/policy) page.
2. Go to the policy management page and enter a policy name in the policy search box.
3. Select `QcloudRUMReadOnlyAccess` or `QcloudRUMFullAccess` and click **Associate Users/Groups** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/30e7a4e5f075b4507af23d347b2cc34e.png)
4. In the pop-up window, select the target user and click **OK**.
