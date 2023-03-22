Tencent Cloud EventBridge uses [Tencent Cloud Access Management (CAM)](https://intl.cloud.tencent.com/zh/document/product/598) to manage permissions. CAM is a permission and access management service that helps you securely manage the access permissions to resources under your Tencent Cloud account. With CAM, you can create, manage and terminate users and user groups and use identity and policy management to control user access to Tencent Cloud resources. Before using EventBridge, you need to activate it on the product page. This document describes how to activate and use EventBridge.

## Directions

<dx-steps>
- Log in to the [EventBridge console](https://console.cloud.tencent.com/eb) and activate the service and create a role as prompted (these operations must be performed with the **root account**).
- (Optional) Log in to the [CAM console](https://console.cloud.tencent.com/cam) to assign permission to the sub-account.
- After creating a service role, you can use the EventBridge features to create relevant resources.
</dx-steps>


## Access Management

### Activating EventBridge[](id:EB_QCSRole)

If this is the first time that you use EventBridge with your root account, according to CAM requirements, you need to enable the EventBridge service role **EB_QCSRole** and grant permissions related to the service role to call other services. To do so, go to the [EventBridge console](https://console.cloud.tencent.com/eb?regionId=1) and grant permissions as instructed:
![](https://qcloudimg.tencent-cloud.cn/raw/692b51a3b5633bc16d00670bd63212f9.png)
![](https://qcloudimg.tencent-cloud.cn/raw/151896257f99feef8b10ed1afe67aaa4.png)

### Granting permissions to sub-account
>! Before a sub-account can use EventBridge, you need to log in to the [CAM console](https://console.cloud.tencent.com/cam/role) with the root account to check whether the `EB_QCSRole` role is created successfully. If not, create the role and grant permissions to it according to [Grant permissions with the root account](#EB_QCSRole). Otherwise, the sub-account cannot use the EventBridge console properly nor call other resources on the cloud via EventBridge.

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) with the root account, select a corresponding sub-account, and select **Associate Policy**.
![](https://qcloudimg.tencent-cloud.cn/raw/8fd31bc5f13cd7334f87225602ab118d.png)

2. Select **Select policies from the policy list** > **Create Custom Policy**.
![](https://qcloudimg.tencent-cloud.cn/raw/24be8712c315ec7e9e35c9538f52193d.png)

3. Select **Create by Policy Syntax** > **Blank Template**. Enter the policy name and enter the following syntax content in **Policy Content**:
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/cbUz634_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230322161459.png" width="450">
```json
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "apigw:DescribeServicesStatus",
                "apigw:DescribeApi",
                "apigw:DescribeService",
                "apigw:CreateService",
                "cam:ListGroups",
                "cam:DescribeSubAccountContacts",
                "cam:GetRole",
                "cam:GetGroup",
                "scf:ListNamespaces",
                "scf:ListFunctions",
                "scf:ListVersionByFunction",
                "scf:ListAliases",
                "scf:CreateFunction",
                "scf:GetFunction",
                "tdmq:CreateSubscription",
                "tdmq:ResetMsgSubOffsetByTimestamp",
                "tdmq:DescribeClusters",
                "tdmq:DescribeEnvironments",
                "tdmq:DescribeTopics",
                "tdmq:DescribeSubscriptions",
                "ckafka:DescribeInstanceAttributes",
                "ckafka:DescribeInstances",
                "ckafka:DescribeTopic",
                "ckafka:DescribeRoute",
                "cls:DescribeTopics",
                "cls:DescribeLogsets",
                "cls:SearchLog",
                "cls:DescribeLogsets",
                "cls:DescribeTopics",
                "monitor:GetMonitorData",
                "monitor:DescribeAlarmNotices",
                "cam:CreateRole",
                "cloudaudit:*",
                "dts:DescribeSubscribes",
                "es:DescribeInstances",
                "tag:DescribeTagKeys",
                "tag:DescribeTagValues"
            ],
            "resource": "*"
        }
    ]
}
```


4. Bind the custom policy and the preset policy `QcloudEBFullAccess` with the sub-account. Then the sub-account can use the service properly.
