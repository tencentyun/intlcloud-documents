A sub-account has no CAT permissions by default and can access CAT resources only after being granted relevant permissions by the root account.

## Prerequisites

Log in to the Tencent Cloud console with the root account or a sub-account with the `QcloudCamFullAccess` permission and create a sub-account as instructed in [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).

## Custom policy

1. Use the root account or a sub-account with the `QcloudCamFullAccess` permission to log in to the **CAM** console and go to the [**Policies**](https://console.cloud.tencent.com/cam/policy) page.
2. Click **Create Custom Policy** > **Create by Policy Syntax** and select **Blank Template**. Edit the policy as instructed in [Policy Syntax](https://www.tencentcloud.com/document/product/1169/52015).
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/7tUI660_38intl_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.png)

## Policy authorization

>?CAT creates default permission policies `QcloudCATFullAccess` (full access to CAT) and `QcloudCATReadOnlyAccess` (read-only access to CAT) for you. You can search for a default policy for quick authorization. You can also use a custom policy for authorization. Then, the sub-account can access the relevant resources.

1. Use the root account or a sub-account with the `QcloudCamFullAccess` permission to log in to the **CAM** console and go to the [**Policies**](https://console.cloud.tencent.com/cam/policy) page.
2. Go to the policy management page and enter a policy name in the policy search box.
3. Select `QcloudRUMReadOnlyAccess` or `QcloudRUMFullAccess` and click **Associate Users/Groups** in the **Operation** column.
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/9s8U893_39intl_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.png)
4. In the pop-up window, select the target user and click **OK**.

