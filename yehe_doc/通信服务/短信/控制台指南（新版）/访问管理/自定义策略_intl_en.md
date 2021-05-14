>!This document describes the access management feature of **SMS**. For more information on access management for other Tencent Cloud services, please see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

It is convenient to use a [default policy](https://intl.cloud.tencent.com/document/product/382/38455) in SMS access control to implement authorization, but its granularity of permission control is coarse and cannot be refined to the SMS application and the [TencentCloud API](https://intl.cloud.tencent.com/product/api) levels. If you need fine-grained permissions control, you need to create custom policies.

## Custom Policy Creation Methods
There are multiple ways to create a custom policy. The table below shows a comparison of various methods. For detailed directions, please see further below.

| Creation Entry | Creation Method | Effect | Resource | Action | Flexibility |
|--------------|---------------|-------------|----------------|--------------|------|
| [CAM console](https://console.cloud.tencent.com/cam/policy) | Policy generator | Manual selection | Syntax description | Manual selection | Medium |
| [CAM console](https://console.cloud.tencent.com/cam/policy) | Policy syntax | Syntax description | Syntax description | Syntax description | High |
| CAM server API | [CreatePolicy](https://intl.cloud.tencent.com/document/product/598/32248) | Syntax description | Syntax description | Syntax description | High |

>?
>- SMS does not support creating custom policies by product feature or project.
>- Manual selection means that you can select an object from the candidate list displayed in the console.
>- Syntax description means that you can describe objects through the [authorization policy syntax](#.E6.8E.88.E6.9D.83.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95).

## Authorization Policy Syntax
### Resource syntax description
As mentioned above, the resource granularity of permission management in SMS is the application. The application description in the policy syntax follows the [CAM resource description method](https://intl.cloud.tencent.com/document/product/598/10606). In the example below, the developer's root account ID is 12345678, and the developer has created three applications with an `App` of 1400000000, 1400000001, and 1400000002, respectively.
- **Policy syntax description for all SMS applications**
```
"resource": ["qcs::sms::uin/12345678:app/*"]
```
- **Policy syntax description for a single SMS application**
```
"resource": [ "qcs::sms::uin/12345678:app/1400000001"]
```
- **Policy syntax description for multiple SMS applications**
```
"resource": [ "qcs::sms::uin/12345678:app/1400000000","qcs::sms::uin/12345678:app/1400000001"]
```

### Action syntax description
As mentioned above, the action granularity of permission management in SMS is the TencentCloud API. For more information, please see [Authorizable Resources and Actions](https://intl.cloud.tencent.com/document/product/382/38454). TencentCloud APIs such as `DescribeAppList` (getting application list) and `DescribeAppInfo` (getting application information) are used as examples below.
- **Policy syntax description for all SMS TencentCloud APIs**
```
"action": [
"name/sms:*"
]
```
- **Policy syntax description for a single TencentCloud API**
```
"action": [
"name/sms:DescribeAppList"
]
```
- **Policy syntax description for multiple TencentCloud APIs**
```
"action": [
"name/sms:DescribeAppList",
"name/sms:DescribeAppInfo"
]
```

## Custom Policy Use Cases
### Using the policy generator
In the example below, we will create a custom policy, which allows all actions except the console API `DeleteAppInfo` to be performed on the SMS application 1400000001.
1. Access the **[Policy](https://console.cloud.tencent.com/cam/policy)** page in the CAM console using a Tencent Cloud [root account](https://intl.cloud.tencent.com/document/product/598/32633) and click **Create Custom Policy**.
2. Select **Create by Policy Generator** to access the policy creation page.
3. Select the service and action.
	● Select **Allow** for **Effect**.
	● Select **Short Message Service** for **Service**.
	● Check all items for **Action**.
	● Enter `qcs::sms::uin/12345678:app/1400000001` for **Resource** according to the [resource syntax description](#.E8.B5.84.E6.BA.90.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0).
	● The **Condition** configuration item does not need to be configured.
	● Click **Add Statement** and a statement saying that "Any action is allowed on the SMS application 1400000001" will appear at the bottom of the page.
4. Continue adding another statement on the same page.
	● Select **Deny** for **Effect**.
	● Select **Short Message Service** for **Service**.
	● Check `DeleteAppInfo` (which can be quickly found using the search engine) for **Action**.
	● Enter `qcs::sms::uin/12345678:app/1400000001` for **Resource** according to the [resource syntax description](#.E8.B5.84.E6.BA.90.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0).
	● The **Condition** configuration item does not need to be configured.
	● Click **Add Statement** and a statement saying that "The `DeleteAppInfo` action is denied on the SMS application 1400000001" will appear at the bottom of the page.
5. Click **Next** and rename the policy as needed (or leave it unchanged).
6. Click **Done** to create the custom policy.
Subsequently, this policy can be granted to other sub-accounts in the same way as [granting full access to SMS to an existing sub-account](https://intl.cloud.tencent.com/document/product/382/38455#.E5.B0.86-sms-.E5.85.A8.E8.AF.BB.E5.86.99.E8.AE.BF.E9.97.AE.E6.9D.83.E9.99.90.E6.8E.88.E4.BA.88.E5.B7.B2.E5.AD.98.E5.9C.A8.E7.9A.84.E5.AD.90.E8.B4.A6.E5.8F.B7).

### Using the policy syntax
In the example below, we will create a custom policy, which allows all actions to be performed on SMS applications 1400000001 and 1400000002 but denies `DeleteAppInfo` for application 1400000001.
1. Access the **[Policy](https://console.cloud.tencent.com/cam/policy)** page in the CAM console using a Tencent Cloud [root account](https://intl.cloud.tencent.com/document/product/598/32633) and click **Create Custom Policy**.
2. Select **Create by Policy Syntax** to access the policy creation page.
3. In the **Select a template type** box, select **Blank Template**.
>?A policy template is used to create a policy by copying an existing policy (preset or custom) and then making adjustments to the copy. During actual use, you can choose an appropriate policy template based on the actual conditions to reduce the difficulty and workload of writing the policy content.
4. Click **Next** and rename the policy as needed (or leave it unchanged).
5. Enter the following policy content in the **Policy Content** box:
```
{
 "version": "2.0",
 "statement": [
     {
          "effect": "allow",
          "action": [
              "name/SMS:*"
          ],
          "resource": [
              "qcs::sms::uin/12345678:app/1400000001",
              "qcs::sms::uin/12345678:app/1400000002"
          ]
      },
      {
          "effect": "deny",
          "action": [
              "name/SMS: DeleteAppInfo "
          ],
          "resource": [
              "qcs::SMS::uin/12345678:app/1400000001"
          ]
      }
  ]
}
```
>?The policy content should follow the [CAM policy syntax logic](https://intl.cloud.tencent.com/document/product/598/10603), where the syntax of "resource" and "action" is as shown above in the [Resource syntax description](#.E8.B5.84.E6.BA.90.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0) and the [Action syntax description](#.E6.93.8D.E4.BD.9C.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0).
6. Click **Create Policy** to create the custom policy.
Subsequently, this policy can be granted to other sub-accounts in the same way as [granting full access to SMS to existing sub-accounts](https://intl.cloud.tencent.com/document/product/382/38455#.E5.B0.86-sms-.E5.85.A8.E8.AF.BB.E5.86.99.E8.AE.BF.E9.97.AE.E6.9D.83.E9.99.90.E6.8E.88.E4.BA.88.E5.B7.B2.E5.AD.98.E5.9C.A8.E7.9A.84.E5.AD.90.E8.B4.A6.E5.8F.B7).
