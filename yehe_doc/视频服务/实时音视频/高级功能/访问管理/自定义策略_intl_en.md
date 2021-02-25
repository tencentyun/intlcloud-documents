>!This document describes the management of access to **TRTC**. For access management of other Tencent Cloud services, see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

It may be convenient to use a [preset policy](https://intl.cloud.tencent.com/document/product/647/39550) for access management in TRTC, but with preset policies, the granularity level of permissions is low, and permission granting cannot be specific to [TRTC applications](https://intl.cloud.tencent.com/document/product/647/37714) or [TencentCloud APIs](https://intl.cloud.tencent.com/product/api). To perform fine-grained authorization, you need to create custom policies.

## Custom Policy Creation

There are multiple ways to create a custom policy. The table below offers a comparison of different methods. For detailed directions, see the remaining part of the document.
<table>
<thead><tr><th width="20%%">Access</th><th>Tool</th><th>Effect</th><th>Resource</th><th>Action</th><th>Flexibility</th><th>Complexity</th></tr>
</thead>
<tbody><tr>
<td><a href="https://console.cloud.tencent.com/cam/policy">CAM console</a></td>
<td>Policy generator</td>
<td>Manual selection</td>
<td>Syntax conventions</td>
<td>Manual selection</td>
<td>Medium</td>
<td>Medium</td>
</tr>
<tr>
<td><a href="https://console.cloud.tencent.com/cam/policy">CAM console</a></td>
<td>Policy syntax</td>
<td>Syntax conventions</td>
<td>Syntax conventions</td>
<td>Syntax conventions</td>
<td>High</td>
<td>High</td>
</tr>
<tr>
<td>CAM server API</td>
<td><a href="https://intl.cloud.tencent.com/document/product/598/32248">CreatePolicy</a></td>
<td>Syntax conventions</td>
<td>Syntax conventions</td>
<td>Syntax conventions</td>
<td>High</td>
<td>High</td>
</tr>
</tbody></table>

> ?
>- TRTC does **not support** custom policy creation by product feature or project.
>- **Manual selection** means that you can select an object from a list of candidates offered in the console.
> - **Syntax conventions** means using the [permission policy syntax](#grammar) to describe an object.

<span id="grammar"></span>
## Permission Policy Syntax
<span id="s_grammar"></span>
### Resource syntax conventions

The granularity level of manageable resources in TRTC access management is applications. Syntax conventions of permission policies for applications are in line with the [Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606). In the example below, the developer (root account ID: `12345678`) has created three applications, whose `SDKAppIDs` are `1400000000`, `1400000001`, and `1400000002`.

- Syntax convention of permission policy for all TRTC applications
```
  "resource": [
    "qcs::trtc::uin/12345678:sdkappid/*"
  ]
```
- Syntax convention of permission policy for single TRTC applications
```
  "resource": [
    "qcs::trtc::uin/12345678:sdkappid/1400000001"
  ]
```
- Syntax convention of permission policy for multiple TRTC applications
```
  "resource": [
    "qcs::trtc::uin/12345678:sdkappid/1400000000",
    "qcs::trtc::uin/12345678:sdkappid/1400000001"
  ]
```
<span id="c_grammar)"></span>
### Action syntax conventions

The granularity level of authorizable actions in TRTC access management is TencentCloud APIs. For details, see [Manageable Resources and Actions](https://intl.cloud.tencent.com/document/product/647/39549). The examples below use TencentCloud APIs such as `DescribeAppList` (gets application list) and `DescribeAppInfo` (gets application information).
- Syntax convention of permission policy for all TencentCloud APIs
```
  "action": [
    "name/trtc:*"
  ]
```
- Syntax convention of permission policy for single TencentCloud APIs
```
  "action": [
    "name/trtc:DescribeAppStatList"
  ]
```
- Syntax convention of permission policy for multiple TencentCloud APIs
```
  "action": [
    "name/trtc:DescribeAppStatList",
    "name/trtc:DescribeTrtcAppAndAccountInfo"
  ]
```

## Examples of Using Custom Policies

### Using the policy generator

In the example below, we create a custom policy that allows all actions under TRTC application `1400000001` except calling the server API `RemoveUser`.

1. Go to the [**Policy**](https://console.cloud.tencent.com/cam/policy) page of the CAM console using a Tencent Cloud [root account](https://intl.cloud.tencent.com/document/product/598/32633) and click **Create Custom Policy**.
2. Select **Create by Policy Generator**.
3. Select the service and action.
   - For **Effect**, select **Allow**.
   - For **Service**, select **TRTC** .
   - For **Action**, check all the items.
   - For **resource**, enter `qcs::trtc::uin/12345678:sdkappid/1400000001`, which aligns with the syntax described in [Resource syntax conventions](#s_grammar).
   - No configuration is needed for **Condition**.
   - Click **Add Statement**, and a statement indicating that any action is allowed under TRTC application `1400000001` appears below.
4. Add another statement on the same page.
   - For **Effect**, select **Deny**.
   - For **Service**, select **TRTC**.
   - For **Action**, select `RemoveUser`. You can use the search feature to quickly locate the action.
   - For **Resource**, enter `qcs::trtc::uin/12345678:sdkappid/1400000001`, which aligns with the syntax described in [Resource syntax conventions](#s_grammar).
   - No configuration is needed for **Condition**.
   - Click **Add Statement**, and a statement indicating that calling `RemoveUser` is forbidden under TRTC application `1400000001` appears below.
5. Click **Next** and rename the policy if necessary.
6. Click **Done** to complete the creation.

You can then grant the policy to other sub-accounts as described in [Granting read-and-write permission to existing sub-account](https://intl.cloud.tencent.com/document/product/647/39550#FullRW).


### Using the policy syntax

In the example below, we create a custom policy that allows all actions under TRTC application `1400000002` and all actions but calling `RemoveUser` under `1400000001`.

1. Go to the **[Policy](https://console.cloud.tencent.com/cam/policy)** page of the CAM console using a Tencent Cloud [root account](https://intl.cloud.tencent.com/document/product/598/32633) and click **Create Custom Policy**.
2. Select **Create by Policy Syntax**.
3. In the **Select a template type** section, select **Blank Template**.
   
   >?A policy template allows you to create a policy by modifying a copy of an existing policy (preset or custom). You can choose a policy template that fits your actual conditions to reduce the complexity and workload of writing permission policies.
4. Click **Next** and rename the policy if necessary.
5. Enter the following content in the **Policy Content** box.
```
   {
    "version": "2.0",
    "statement":[
        {
            "effect": "allow",
            "action": [
                "name/trtc:*"
            ],
            "resource": [
                "qcs::trtc::uin/12345678:sdkappid/1400000001",
                "qcs::trtc::uin/12345678:sdkappid/1400000002"
            ]
        },
        {
            "effect": "deny",
            "action": [
                "name/trtc:RemoveUser"
            ],
            "resource": [
                "qcs::trtc::uin/12345678:sdkappid/1400000001"
            ]
        }
    ]
   }
```
> ?  Policy content must align with the [Syntax Logic](https://intl.cloud.tencent.com/document/product/598/10603). About the syntax of the resource and action elements, see [Resource syntax conventions](#s_grammar) and [Action syntax conventions](#c_grammar) above.
6. Click **Create Policy** to complete the creation.

You can then grant the policy to other sub-accounts as described in [Granting read-and-write permission to existing sub-account](https://intl.cloud.tencent.com/document/product/647/39550#FullRW).

### Using server APIs provided by CAM

Managing access in the console can meet the business needs of most developers, but to automate and systematize your access management, you need to use server APIs.
Permission policy-related server APIs belong to CAM. For details, see [CAM documentation](https://intl.cloud.tencent.com/document/product/598). Only a few main APIs are listed below:

- [CreatePolicy](https://intl.cloud.tencent.com/document/product/598/32248)
- [DeletePolicy](https://intl.cloud.tencent.com/document/product/598/32247)
- [AttachUserPolicy](https://intl.cloud.tencent.com/document/product/598/32249)
- [DetachUserPolicy](https://intl.cloud.tencent.com/document/product/598/32245)
