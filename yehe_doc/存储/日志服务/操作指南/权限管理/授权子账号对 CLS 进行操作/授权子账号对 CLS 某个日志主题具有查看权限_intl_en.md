
The sub-account Developer of the master account CompanyExample needs to have permission to view the log topic TopicA (including log search, analysis, dashboard and alarm) under CompanyExample via the console and API.

## Preparations

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) and create the sub-account Developer. For more information, see [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
2. Click **Custom Create** on the **Create User** page to select **Access Resources and Receive Messages** for **User Type**.
3. Click **Next** to configure user information. Check **Programming access** and **Tencent Cloud console access**.


## Directions

You need to perform 3 steps: first use master account CompanyExample to create a custom policy and grant sub-account Developer permission to view the log topic TopicA, and then, use sub-account Developer to access CLS services.
1. Use the master account to create a custom policy

 1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) using master account CompanyExample.
 1. Click **Policies** on the left sidebar to enter the **Policy** page. Click **Create Custom Policy** -> **Create by Policy Syntax**, check **Blank Template** for **Select Policy Template**, and click **Next**. Enter the policy name such as CLS-TopicA-ReadAccess, and fill in **Policy Content** by referring to the following:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cls:get*",
                "cls:list*",
                "cls:GetHistogram",
                "cls:GetFastAnalysis",
                "cls:GetChart",
                "cls:GetDashboard",
                "cls:searchLog",
                "cls:downloadLog",
                "cls:pullLogs",
                "cls:GetAccount",
                "cls:GetResource",
                "cls:GetAlarm"
            ],
            "resource": "qcs::cls:ap-shanghai:uin/100004375281:topic/3ea3ea1c-64ad-47af-b92a-75a98d123456",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": [
                "monitor:Get*",
                "monitor:Describe*",
                "cam:ListAttachedRolePolicies",
                "cls:list*"
            ],
            "resource": "*"
        }
    ]
}
```
>?Replace the `resource` field with your actual region, master account UIN, and log topic ID.

2. Authorize by the master account

 1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) using master account CompanyExample.
 1. Click **Users** -> **User List** on the left sidebar to enter the **User List** Page. Locate the sub-account and click **Authorize**. On the **Associate Policy** page, select and associate the policy CLS-TopicA-ReadAccess created in Step 1, and click **Done**.
      
3. Access by the sub-account
The sub-account Developer can access CLS services via both the console and API. To make API calls, you need to provide UIN of master account CompanyExample, together with SecretId and SecretKey of sub-account Developer. See [Access Key](https://intl.cloud.tencent.com/document/product/598/32675) for sub-account API key.

