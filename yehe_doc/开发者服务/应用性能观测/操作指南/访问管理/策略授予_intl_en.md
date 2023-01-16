A sub-account has no APM permissions by default and can access APM resources only after being granted relevant permissions by the root account.

## Prerequisites

Log in to the Tencent Cloud console with the root account or a sub-account with the `QcloudCamFullAccess` permission and create a sub-account as instructed in [Creating Sub-User](https://intl.cloud.tencent.com/document/product/598/13674).

## Custom policy

1. Use the root account or a sub-account with the `QcloudCamFullAccess` permission to log in to the **CAM** console and go to the [**Policies**](https://console.cloud.tencent.com/cam/policy) page.
2. Click **Create Custom Policy** > **Create by Policy Syntax** and select **Blank Template**. Edit the policy as instructed in [Policy Syntax Description](https://www.tencentcloud.com/document/product/1166/51688).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/wxAY078_1.png)

## Policy authorization
>?APM creates default permission policies `QcloudAPMFullAccess` (full access to APM) and `QcloudAPMReadOnlyFullAccess` (read-only access to APM) for you. You can search for a default policy for quick authorization. You can also use a custom policy for authorization. Then, the sub-account can access the relevant resources.

1. Use the root account or a sub-account with the `QcloudCamFullAccess` permission to log in to the **CAM** console and go to the [**Policies**](https://console.cloud.tencent.com/cam/policy) page.
2. Go to the policy management page and enter a policy name in the policy search box.
3. Select `QcloudAPMFullAccess` or `QcloudAPMReadOnlyFullAccess` and click **Associate Users/Groups** in the **Operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/mtxe440_2.png)
4. In the pop-up window, select the target user and click **OK**.

