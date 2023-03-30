>>! This document describes the Cloud Access Management (CAM) feature for IM. For more information about CAM for other Tencent Cloud services, see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).
>
>You can easily use [preset policies](https://intl.cloud.tencent.com/document/product/1047/38087) in the CAM console for authorization. However, preset policies only provide coarse-grained permission control and cannot be refined to IM applications and [Tencent Cloud APIs](https://intl.cloud.tencent.com/product/api). If you need refined permission control, you must create custom policies.
>
>
>## Custom Policy Creation Methods
>
>The table compares several custom policy creation methods with detailed instructions for using them.
>
><table class="table"><thead><tr><th>Entry</th><th>Method</th><th>Effect</th><th>Resource</th><th>Action</th><th>Flexibility</th><th>Difficulty</th></tr></thead>
><tbody><tr><td><a href="https://console.cloud.tencent.com/cam/policy" target="_blank">CAM console</a></td><td>Policy generator</td><td>Manual selection</td><td>Syntax description</td><td>Manual selection</td><td>Medium</td><td>Medium</td></tr>
><tr><td><a href="https://console.cloud.tencent.com/cam/policy" target="_blank">CAM console</a></td><td>Policy syntax</td><td>Syntax description</td><td>Syntax description</td><td>Syntax description</td><td>High</td><td>High</td></tr>
><tr><td>CAM server API</td><td><a href="https://intl.cloud.tencent.com/document/product/598/32248" target="_blank">CreatePolicy</a></td><td>Syntax description</td><td>Syntax description</td><td>Syntax description</td><td>High</td><td>High</td></tr></tbody></table>
>
>
>>?
>>- IM does not support custom policy creation by product feature or project.
>>- Manual selection indicates that you must select an object from the option list in the console.
>>- Syntax description indicates that the [authorization policy syntax](#.E6.8E.88.E6.9D.83.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95) is used to describe objects.
>
>## Authorization Policy Syntax
>
>### Resource syntax description
>
>As mentioned previously, the resource granularity for IM permission management is applications. Policy syntax description of applications comply with the [Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606). In the following example, the developer’s root account ID is 12345678, and the developer creates three applications whose SDKAppIDs are 1400000000, 1400000001, and 1400000002 respectively.
>
>- Policy syntax description for all IM applications
>```
>"resource": [
>  "qcs::im::uin/12345678:sdkappid/*"
>]
>```
>- Policy syntax description for a single application
>```
>"resource": [
>  "qcs::im::uin/12345678:sdkappid/1400000001"
>]
>```
>- Policy syntax description for multiple applications
>```
>"resource": [
>  "qcs::im::uin/12345678:sdkappid/1400000000",
>  "qcs::im::uin/12345678:sdkappid/1400000001"
>]
>```
>
>### Action syntax description
>As mentioned previously, the action granularity of TRTC permission management is Tencent Cloud APIs. In the following example, Tencent Cloud APIs such as `DescribeAppStatList` (for obtaining the application list) and `DescribeSdkAppInfo` (for obtaining application information) are used.
>- Policy syntax description for all Tencent Cloud APIs for IM
>```
>"action": [
>  "name/im:*"
>]
>```
>- Policy syntax description for a single Tencent Cloud API
>```
>"action": [
>  "name/im:DescribeAppStatList"
>]
>```
>- Policy syntax description for multiple Tencent Cloud APIs
>```
>"action": [
>  "name/im:DescribeAppStatList",
>  "name/im:DescribeTrtcAppAndAccountInfo"
>]
>```
>
>## Custom Policy Usage Example
>
>### Using the policy generator
>
>In the following example, we will create a custom policy that allows all operations on the IM application whose SDKAppID is 1400000001.
>1. Log in to the **[Policies](https://console.cloud.tencent.com/cam/policy)** page in the CAM console with the [root account](https://intl.cloud.tencent.com/document/product/598/32633). Then, click **Create Custom Policy**.
>2. Select **Create by Policy Generator** to go to the policy creation page.
>3. In the **Select Service and Action** step:
>	- Select **Allow** for **Effect**.
>	- Select **IM** for **Service**.
>	- Select all items for **Action**.
>	- Enter `qcs::im::uin/12345678:sdkappid/1400000001` for **Resource** based on the [resource syntax description](#.E8.B5.84.E6.BA.90.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0).
>	- **Condition** is optional.
>	- Click **Add Statement**. A statement that allows all operations for the IM application 1400000001 appears.
>4. Continue to add another statement on the same page by configuring the following settings:
>	- Select **Deny** for **Effect**.
>	- Select **IM** for **Service**.
>	- Select `RemoveUser` for **Action**. (You can quickly find `RemoveUser` with the search feature.)
>	- Enter `qcs::im::uin/12345678:sdkappid/1400000001` for **Resource** based on the [resource syntax description](#.E8.B5.84.E6.BA.90.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0).
>	- **Condition** is optional.
>	- Click **Add Statement**. A statement that rejects the `RemoveUser` operation for IM application 1400000001 appears.
>5. Click **Next** and rename the policy as needed (You can also retain the current policy name). 
>6. Click **Done**.
>
>
>The method for granting the policy to other sub-accounts is the same as [Granting IM Permissions to an Existing Sub-account](https://intl.cloud.tencent.com/document/product/1047/38087).
>
>
>### Using the policy syntax
>
>In the following example, we will create a custom policy that allows all operations for the IM applications whose SDKAppIDs are 1400000001 and 1400000002.
>
>
>1. Log in to the **[Policies](https://console.cloud.tencent.com/cam/policy)** page in the CAM console with the [root account](https://intl.cloud.tencent.com/document/product/598/32633). Then, click **Create Custom Policy**.
>2. Select **Create by Policy Syntax** to go to the creation page.
>3. In the **Select a template type** area, select **Blank Template**.
> >? A policy template is used to create a policy by copying an existing policy (a preset or custom policy) and then modifying the policy. You can select an appropriate policy template to reduce the difficulty and workload of policy definition. 
>4. Click **Next** and rename the policy as needed (You can also retain the current policy name). 
>5. Copy and paste the following content in the **Policy Content** box:
>```
>{
> "version": "2.0",
> "statement": [
>     {
>         "effect": "allow",
>         "action": [
>             "name/im:*"
>         ],
>         "resource": [
>             "qcs::im::uin/12345678:sdkappid/1400000001",
>             "qcs::im::uin/12345678:sdkappid/1400000002"
>         ]
>     },
>     {
>         "effect": "deny",
>         "action": [
>             "name/im:RemoveUser"
>         ],
>         "resource": [
>             "qcs::im::uin/12345678:sdkappid/1400000001"
>         ]
>     }
> ]
>}
>```
>>? The policy content must comply with the CAM policy syntax logic described in [Element Reference](https://intl.cloud.tencent.com/document/product/598/33415). For more information on the syntax for resource and action elements, see [Resource syntax description](#.E8.B5.84.E6.BA.90.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0) and [Action syntax description](#.E6.93.8D.E4.BD.9C.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0).
>6. Click **Done**.
>The method for granting the policy to other sub-accounts is the same as [Granting IM Permissions to an Existing Sub-account](https://intl.cloud.tencent.com/document/product/1047/38087).
>
>### Using server APIs provided by CAM
>
>For most developers, performing permission management operations in the console can meet their business needs. However, if you need to automate and systematize your permission management capabilities, you can use server APIs.
>Policy-related server APIs are included in CAM. For more information, see [CAM documentation](https://intl.cloud.tencent.com/document/product/598). Among these APIs, the major ones include:
>
>- [CreatePolicy](https://intl.cloud.tencent.com/document/product/598/32248)
>- [DeletePolicy](https://intl.cloud.tencent.com/document/product/598/32247)
>- [AttachUserPolicy](https://intl.cloud.tencent.com/document/product/598/32249)
>- [DetachUserPolicy](https://intl.cloud.tencent.com/document/product/598/32245)
