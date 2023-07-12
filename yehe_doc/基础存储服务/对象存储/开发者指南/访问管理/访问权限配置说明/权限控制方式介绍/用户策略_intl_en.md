In the [CAM console](https://console.cloud.tencent.com/cam/overview), you can use your Tencent Cloud root account to create CAM users and grant them with Tencent Cloud resource permissions by associating them with policies.

## Overview

In [CAM](https://intl.cloud.tencent.com/document/product/598/10583), you can grant different permissions to different types of users under your root account. These permissions are described in the access policy language and are granted by user, so they are called **user policies**.

#### Differences between a user policy and a bucket policy

The biggest difference between a user policy and a bucket policy is that the user policy only describes effect, action, resource, and condition (optional), but not principal. Therefore, for a user policy:
- You need to write a user policy first, and then associate it manually with a sub-user, a user group or a role.
- A user policy **cannot grant anonymous users access to resources or operations**.

#### Preset policy and custom policy

User policies are classified into [preset policies and custom policies](https://intl.cloud.tencent.com/document/product/598/10601). You can [associate a preset policy for authorization](https://intl.cloud.tencent.com/document/product/598/10602) or [write a user policy](https://intl.cloud.tencent.com/document/product/598/35596) and associate it for authorization. For more information, see CAM's [Authorization Guide](https://intl.cloud.tencent.com/document/product/598/32668).

## Application Scenarios
If you want to specify what operations a user can perform, you are advised to configure user policy. You can search for a CAM user and check the permissions of the user's user groups to see what operations the user can perform. A user policy is recommended in scenarios where you want to:
- Configure COS service-level permissions such as the permissions for bucket creation (PutBucket) and bucket listing (GetService).
- Grant permissions on all COS buckets and objects under your root account.
- Grant the same permissions to a large number of CAM users under the root account.

## User Policy Syntax

### Policy syntax

Same as a bucket policy, a user policy is described in JSON language and its syntax complies with the unified specifications of the [access policy language](https://intl.cloud.tencent.com/document/product/436/18023). The access policy language contains the following basic elements: principal, effect, action, resource, and condition. However, a user policy is directly associated with a user or user group, and therefore you do not need to specify the principal element in a user policy.

The following table compares a user policy and a bucket policy:

| Element | User Policy | Bucket Policy |
|---|---|---|
| Principal | **No input** | Required |
| Effect | Required | Required |
| Action | Required | Required |
| Resource | Required |**Resources in the current bucket**|
| Condition | Optional | Optional |

### Policy examples

The following typical user policy example grants the permission to perform all COS operations on the bucket `examplebucket-1250000000` in Guangzhou. You need to save the policy and then associate it with a [CAM](https://intl.cloud.tencent.com/document/product/598/10583) sub-user, a user group or a role before it takes effect.

```
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["cos:*"],
      "Resource": [
          "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*",
          "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ],
  "Version": "2.0"
}
```

## Granting Sub-account COS Access Permission with User Policy

### Prerequisites

You have already created a CAM sub-account. If you haven't, see [Create a sub-account](https://intl.cloud.tencent.com/document/product/436/11714#step-1.-create-a-sub-account) to create one.

<span id="Custom Policy"></span>
### Directions

CAM provides [preset policies and custom policies](https://intl.cloud.tencent.com/document/product/598/10601). A preset policy is a policy preset in the system provided by CAM. For COS related preset policies, see [Preset Policy](https://intl.cloud.tencent.com/document/product/436/45236?lang=en&pg=#preset-policy). A custom policy allows users to customize elements such as resources and actions. The following describes how to create a custom policy to grant permissions to a sub-account:

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam).
2. Choose **Policy** > **Create Custom Policy** > **Create by Policy Syntax** to go to the policy creation page.
3. You can select **Blank Template** to customize a permission policy as needed or select a COS-associated **system template**. The following uses **Blank Template** as an example.

4. Select **Blank Template** and enter your policy syntax.The policy syntax must contain the following elements:
 - **resource: resource to authorize access to**
     - All resources (`"*"`)
     - Specified bucket (`"qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"`)
     - Specified directory or object in a bucket (`"qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/test/*"`)
 - **action: action to authorize**
 - **effect**: select `"Allow"` or `"Deny"`
 - **condition**: optional

 COS provides user policy examples. You can copy and paste the policy content in the following documents into the **Policy Content** box and click **Done**.
 - [Granting Sub-accounts Access to COS](https://intl.cloud.tencent.com/document/product/436/11714)
 - [Working with COS API Access Policies](https://intl.cloud.tencent.com/document/product/436/30580)
5. After creating the policy, you can go to **Policy** > **Custom Policy** in the [CAM console](https://console.cloud.tencent.com/cam) to view the created custom policy and associate it with sub-accounts.

6. Select the sub-account and click **Confirm** to complete the authorization.


<span id="Preset Policy"></span>
## Preset Policy
1. CAM provides some preset policies. You can view them (filtered by "COS") in **Policy** > **Preset Policy** in the [CAM console](https://console.cloud.tencent.com/cam).


2. Click a policy name and choose **Policy Syntax** > **JSON** to view the policy context. In a preset policy, `resource` is set to `"*"` (indicating all resources in COS) and its value cannot be modified. If you want to grant permissions on certain COS buckets or objects, you can copy the JSON preset policy to create a [Custom Policy](https://intl.cloud.tencent.com/document/product/436/45236?lang=en&pg=#directions).



Table 1 and Table 2 list the COS related preset policies provided by CAM and related descriptions.

**Table 1. COS Preset Policies**

<table>
<tr>
	<th>Preset Policy</th>
	<th>Description</th>
	<th>JSON Policy</th>
</tr>
<tr>
	<td>QcloudCOS<br>Bucket<br>ConfigRead</td>
	<td>Permission to read COS bucket configuration</td>
	<td>
	<pre>
	<code>
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:GetBucket*",
                "cos:HeadBucket"
            ],
            "resource": "*"
        }
    ]
}
	</code>
	</pre>
	</td>
</tr>
<tr>
	<td>QcloudCOS<br>Bucket<br>ConfigWrite</td>
	<td>Permission to modify COS bucket configuration</td>
	<td>
	<pre>
	<code>
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:PutBucket*"
            ],
            "resource": "*"
        }
    ]
}
	</code>
	</pre>
	</td>
</tr>
<tr>
	<td>QcloudCOS<br>Data<br>FullControl</td>
	<td>Permission to read, write, delete, and list data in the COS bucket (all access permissions)</td>
	<td>
	<pre>
	<code>
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:GetService",
                "cos:GetBucket",
                "cos:ListMultipartUploads",
                "cos:GetObject*",
                "cos:HeadObject",
                "cos:GetBucketObjectVersions",
                "cos:OptionsObject",
                "cos:ListParts",
                "cos:DeleteObject",
                "cos:PostObject",
                "cos:PostObjectRestore",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload",
                "cos:DeleteMultipleObjects",
                "cos:AppendObject"
            ],
            "resource": "*"
        }
    ]
}
	</code>
	</pre>
	</td>
</tr>

</table>

**Table 2. Relationships between COS actions and preset policies**

| Action Purpose | Action |QcloudCOS<br>Bucket<br>ConfigRead |QcloudCOS<br>Bucket<br>ConfigWrite |QcloudCOS<br>Data<br>FullControl |QcloudCOS<br>Data<br>ReadOnly |QcloudCOS<br>Data<br>WriteOnly |QcloudCOS<br>Full<br>Access |QcloudCOS<br>GetService<br>Access |QcloudCOS<br>ListOnly |QcloudCOS<br>Read<br>OnlyAccess |
|---|---|---|---|---|---|---|---|---|---|---|
| List buckets | GetService |❌ |❌ |✅ |❌ |❌ |✅ |✅ |✅ |✅ |
| Create a bucket |PutBucket |❌ |✅ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
| Delete a bucket |DeleteBucket |❌ |❌ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
| Get basic bucket information |HeadBucket |✅ |❌ |❌ |❌ |❌ |✅ |❌ |✅ |✅ |
| Get bucket configuration items |GetBucket* |✅ |❌ |❌ |❌ |❌ |✅ |❌ |❌ |✅ |
| Modify bucket configuration items |GetBucket* |❌ |✅ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
| Get bucket access permissions |GetBucketAcl |✅ |❌ |❌ |❌ |❌ |✅ |❌ |❌ |✅ |
| Modify bucket access permissions |PutBucketAcl |❌ |✅ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
| List objects in a bucket |GetBucket |✅ |❌ |✅ |❌ |❌ |✅ |❌ |✅ |✅ |
| List all objects in a bucket and their historical version information |GetBucketObjectVersions |✅ |❌ |✅ |❌ |❌ |✅ |❌ |✅ |✅ |
| Upload an object |PutObject |❌ |❌ |✅ |❌ |✅ |✅ |❌ |❌ |❌ |
| Multipart upload |ListParts<br>InitiateMultipartUpload<br>UploadPart<br>UploadPartCopy<br>CompleteMultipartUpload<br>AbortMultipartUpload<br>ListMultipartUploads |❌ |❌ |✅ |❌ |✅ |✅ |❌ |❌ |❌ |
| Append an object |AppendObject |❌ |❌ |✅ |❌ |❌ |✅ |❌ |❌ |❌ |
| Download an object |GetObject |❌ |❌ |✅ |✅ |❌ |✅ |❌ |❌ |❌ |
| View object metadata |HeadObject |❌ |❌ |✅ |✅ |❌ |✅ |❌ |❌ |✅ |
| Issue a preflight request for CORS |OptionsObject |❌ |❌ |✅ |✅ |❌ |✅ |❌ |❌ |✅ |


## More User Policy Examples

- [Granting Sub-accounts Access to COS](https://intl.cloud.tencent.com/document/product/436/11714)
- [Working with COS API Access Policies](https://intl.cloud.tencent.com/document/product/436/30580)

