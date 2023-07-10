

There is a sub-account "Developer" under the corporate account "CompanyExample". This sub-account needs to have the permission to collect and upload logs to CLS log topic "TopicA" under "CompanyExample" through the console and API, including using LogListener and API for collection.

## Preparations

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) and create the sub-account "Developer". For detailed directions, please see [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
2. On the **Create User** page, click **Custom Create** to enter the user type selection page and click **Access Resources and Receive Messages**.
3. Click **Next** to enter the user information page and select **Programming access** and **Tencent Cloud console access**.






## Directions

This process is divided into three steps: the root account "CompanyExample" creates a custom policy, the root account grants preset permissions to the sub-account "Developer", and the sub-account accesses the CLS service.
1. <span id="step1"></span>Create a custom policy

   1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) as the root account "CompanyExample".
   1. On the left sidebar, select **Polices** > **Create Custom Policy** > **Create by Policy Syntax** > **Blank Template** to create a policy named "CLS-TopicA-Pushlog". Then, enter the specific policy content in **Policy Content** as shown below:
```plaintext
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cls:pushLog"
            ],
            "resource": "qcs::cls:ap-guangzhou:uin/100004375281:topic/002dbab1-fcf2-4ca7-b602-fda10d5e1731",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": [
                "cls:listLogset",
                "cls:getConfig",
                "cls:agentHeartBeat"
            ],
            "resource": "*"
        }
    ]
}
```
>?The `resource` field should be modified based on your real information, including `region`, `uin` (root account), and `topic` (log topic ID).
>- Region: go to [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940) to get the region information.
>- uin: enter the account ID, which can be obtained in the [Account Center](https://console.cloud.tencent.com/developer).
>- topic: enter the log topic ID, which can be obtained from the logset page by going to **CLS** > **[Logset Management](https://console.cloud.tencent.com/cls/logset)** and clicking the corresponding logset.

2. Grant permissions with the root account

 1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) as the root account "CompanyExample".
 1. On the left sidebar, click **Users** > **User List** > **Authorize**. Search for the policy "CLS-TopicA-Pushlog" created in [step 1](#step1) on the **Associate Policy** page, select and associate it, and click **Confirm**.
    
3. Access as the sub-account
The sub-account "Developer" can access the CLS service by logging in to the console or calling APIs. It should be noted that the `uin` of the root account "CompanyExample" and the `SecretId` and SecretKey` of the sub-account "Developer" are required for API calls. For more information on the API key of the sub-account, please see [Access Key](https://intl.cloud.tencent.com/document/product/598/32675).
