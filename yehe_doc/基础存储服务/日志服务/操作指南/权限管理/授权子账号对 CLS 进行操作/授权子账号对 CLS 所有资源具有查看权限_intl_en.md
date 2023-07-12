
The sub-account Developer of the master account CompanyExample needs to have permission to read all CLS resources (including logset, log topic, server group, etc.) under CompanyExample via the console and API. For example, the sub-account can see log search, log collection, dashboard, and alarm, etc.

## Preparations

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) and create the sub-account Developer. For more information, see [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
2. Click **Custom Create** on the **Create User** page to select **Access Resources and Receive Messages** for **User Type**.
3. Click **Next** to configure user information. Check **Programming access** and **Tencent Cloud console access**.

## Directions

You need to perform 2 steps: use master account CompanyExample to grant sub-account Developer permission, and access CLS services using sub-account Developer.
1. Authorize by the master account
 1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) using master account CompanyExample.
 3. Click **Users** -> **User List** on the left sidebar to enter the **User List** Page. Locate the sub-account and click **Authorize**. On the **Associate Policy** page, select and associate the policy CLS-TopicA-ReadAccess created in Step 1, and click **Done**.
2. Access by the sub-account
   The sub-account Developer can access CLS services via both the console and API. To make API calls, you need to provide UIN of master account CompanyExample, together with SecretId and SecretKey of sub-account Developer. See [Access Key](https://intl.cloud.tencent.com/document/product/598/32675) for sub-account API key.

