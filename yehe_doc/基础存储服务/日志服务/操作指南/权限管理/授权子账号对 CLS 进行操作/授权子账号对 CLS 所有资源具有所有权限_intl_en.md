
The sub-account Developer of the master account CompanyExample needs to have full permissions for all CLS resources (including logset, log topic, server group, etc.) under CompanyExample via the console and API. For example, the sub-account can operate log collection, search and analysis, dashboard, and alarm, etc.

## Preparations

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) and create the sub-account Developer. For more information, see [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
2. Click **Custom Create** on the **Create User** page to select **Access Resources and Receive Messages** for **User Type**.
3. Click **Next** to configure user information. Check **Programming access** and **Tencent Cloud console access**.

## Directions

You need to perform 3 steps: use master account CompanyExample to create a custom policy (the policy is used to configure bucket list for shipping logs to COS, and configure Ckafka instance and topic list for shipping logs to Ckafka. Skip this step if you do not need the log shipping feature), grant the sub-account Developer permissions, and then access CLS services using sub-account Developer.

1. Create a custom policy (required for shipping logs to COS and Ckafka; otherwise skip to Step 2).
 1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) using master account CompanyExample.
 1. Click **Policies** on the left sidebar to enter the **Policy** page. Click **Create Custom Policy** -> **Create by Policy Syntax**, check **Blank Template** for **Select Policy Template**, and click **Next**. Enter the policy name such as CLSListCosCKafka, and paste the following content in **Policy Content**.
	```plaintext
{
	 "version": "2.0",
	 "statement": [
		{
			"effect": "allow",
			"action": [
			    "cos:GetService",
				"ckafka:ListInstance",
				"ckafka:ListTopic"
		   ],
           "resource": "*"
        }
      ]
}
	```
   
   
2. Authorize by the master account
	1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) using master account CompanyExample.
	2. Click **Users** -> **User List** on the left sidebar to enter the **User List** Page. Locate the sub-account and click **Authorize**. On the **Associate Policy** page, select and associate QcloudCLSFullAccess and the policy CLSListCosCKafka created in Step 1, and click **Done**.
   
3. Access by the sub-account
   The sub-account Developer can access CLS services via both the console and API. To make API calls, you need to provide UIN of master account CompanyExample, together with SecretId and SecretKey of sub-account Developer. See [Access Key](https://intl.cloud.tencent.com/document/product/598/32675) for sub-account API key.

