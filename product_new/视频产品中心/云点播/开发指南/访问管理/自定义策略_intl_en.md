It is convenient to use a [preset policy](https://intl.cloud.tencent.com/document/product/266/33971) in CAM to implement authorization, but its granularity of permission control is coarse and cannot be refined to the subapplication and API levels. If you require fine-grained permissions control, you need to create custom policies.


## Custom Policy Creation Method

There are multiple ways to create a custom policy. The table below shows a comparison of various methods. For detailed directions, please see further below.

| Creation Entry | Creation Method | Effect <br/> | Resource <br/> | Action <br/> | Flexibility | Difficulty |
| ---------- | ------------ | ------------------- | --------------------- | ------------------- | ------ | ---- |
| Console | Policy builder | Manual selection | Syntax description | Manual selection | Medium | Medium |
| Console | Policy syntax | Syntax description | Syntax description | Syntax description | High | High |
| Server API | CreatePolicy | Syntax description | Syntax description | Syntax description | High | High |

>
>- VOD does not support creating custom policies by product feature.
>- **Manual selection** means that you can select an object from the candidate list displayed in the console, while **syntax description** means that you can describe objects through policy syntax.

## <span id = "p1"></span>Policy Syntax Description for Resource

As mentioned above, the resource granularity of permission control in VOD is subapplication. The subapplication description in policy syntax follows the [CAM rules](https://intl.cloud.tencent.com/document/product/598/10606). In the example below, the developer's account ID is 12345678, APPID is 1250000001 (which is equivalent to the primary application ID), and the developer has created two VOD subapplications with IDs of 1400000001 and 1400000002 respectively.

- **Policy syntax description for all VOD resources**
```
"resouce": [
	"qcs::vod::uin/12345678:subAppId/*"
]
```
- **Policy syntax description for the primary application**
```
"resouce": [
	"qcs::vod::uin/12345678:subAppId/1250000001"
]
```
- **Policy syntax description for a single subapplication**
```
"resouce": [
	"qcs::vod::uin/12345678:subAppId/1400000001"
]
```
- **Policy syntax description for the primary application and a single subapplication**
```
"resouce": [
	"qcs::vod::uin/12345678:subAppId/1250000001",
	"qcs::vod::uin/12345678:subAppId/1400000001"
]
```

## <span id ="p3"></span>Policy Syntax Description for Action

As mentioned above, the action granularity of permission control in VOD is server API. Server APIs such as `DescribeMediaInfos` and `DescribeAllClass` are used as examples below.

- **Policy syntax description for all VOD server APIs**
```
"action": [
	"name/vod:*"
]
```
- **Policy syntax description for a single server API**
```
"action": [
	"name/vod:DescribeMediaInfos"
]
```
- **Policy syntax description for multiple server APIs**
```
"action": [
	"name/vod:DescribeMediaInfos",
	"name/vod:DescribeAllClass"
]
```

## Usage Examples of Custom Policy

### Using the policy builder

In the example below, we will create a custom policy, which allows all actions except the server API `ProcessMedia` to be performed on VOD subapplication 1400000001.

1. Access the **[Policy](https://console.cloud.tencent.com/cam/policy)** page in the CAM Console as a [root account](https://intl.cloud.tencent.com/document/product/598/32633) and click **Create Custom Policy**.
2. Select **Create by Policy Builder** to enter the policy creation page.
3. Select services and actions.
	- Select **Allow** for **Effect**.
	- Select **VOD** for **Service**.
	- Check **All** for **Action**.
	- Enter `qcs::vod::uin/12345678:subAppId/1400000001` for **Resource** according to the [syntax description for resource](#p1).
	- The **Condition** configuration item does not need to be configured.
	- Click **Add Statement** and a statement saying that "Any action is allowed on VOD subapplication 1400000001" will appear at the bottom of the page.
4. Continue adding another statement on the same page.
	- Select **Deny** for **Effect**.
	- Select **VOD** for **Service**.
	- Check `ProcessMedia` (which can be selected by search) for **Action**.
	- Enter `qcs::vod::uin/12345678:subAppId/1400000001` for **Resource** according to the [syntax description for resource](#p1).
	- The **Condition** configuration item does not need to be configured.
	- Click **Add Statement** and a statement saying that "The `ProcessMedia` action is denied on VOD subapplication 1400000001" will appear at the bottom of the page.
     ![](https://main.qcloudimg.com/raw/1ac34ffafb9719e36e46d4a5e7ccf1cf.png)
5. Click **Next** and rename the policy name as needed (or leave it unchanged).
6. Click **Create Policy** to create the custom policy. Subsequently, this policy can be granted to subusers in the same way as [granting full permissions of VOD to existing subusers](https://intl.cloud.tencent.com/document/product/266/33971#p2).


### Using policy syntax

In the example below, we will create a custom policy, which allows all actions to be performed on VOD subapplications 1400000001 and 1400000002 but denies `ProcessMedia` for subapplication 1400000001.

1. Access the **[Policy](https://console.cloud.tencent.com/cam/policy)** page in the CAM Console as a [root account](https://intl.cloud.tencent.com/document/product/598/32633) and click **Create Custom Policy**.
2. Select **Create by Policy Syntax** to enter the policy creation page.
3. In the **Select Template Type** box, select **Blank Template**.
>A policy template is used to create a policy by copying an existing policy (preset or custom) and then making adjustment to the copy. In actual use, you can choose an appropriate policy template based on the actual conditions to reduce the difficulty and workload of writing policy content.
4. Click **Next** and rename the policy name as needed (or leave it unchanged).
5. Enter the following policy content in the **Edit Policy Content** box:
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/vod:*"
            ],
            "resource": [
                "qcs::vod::uin/12345678:subAppId/1400000001",
                "qcs::vod::uin/12345678:subAppId/1400000002"
            ]
        },
        {
            "effect": "deny",
            "action": [
                "name/vod:ProcessMedia"
            ],
            "resource": [
                "qcs::vod::uin/12345678:subAppId/1400000001"
            ]
        }
    ]
}
```
> The policy content should follow the CAM [policy syntax](https://intl.cloud.tencent.com/document/product/598/10603) rules, where the syntax of "resource" and "action" is as shown above in [Policy Syntax Description for Resource](#p1) and [Policy Syntax Description for Action](#p3).
6. Click **Create Policy** to create the custom policy. Subsequently, this policy can be granted to subusers in the same way as [the example of granting full permissions of VOD to existing subusers](https://intl.cloud.tencent.com/document/product/266/33971#p2).

### Using server API

For most developers, performing permission management operations in the console can meet their business needs. However, if you need to automate and systematize your permission management capabilities, you can use server APIs.
The server APIs related to policies belongs to CAM. For more information, please see the [CAM documentation](https://intl.cloud.tencent.com/document/product/598). Only a few main APIs are listed below:

- [CreatePolicy](https://intl.cloud.tencent.com/document/product/598/32248)
- [DeletePolicy](https://intl.cloud.tencent.com/document/product/598/32247)
- [AttachUserPolicy](https://intl.cloud.tencent.com/document/product/598/32249)
- [DetachUserPolicy](https://intl.cloud.tencent.com/document/product/598/32245)
