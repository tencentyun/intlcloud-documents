## Overview

You can add a policy for a bucket via the COS console to allow/deny access to specified COS resources from an account, IP, or IP range. For more information on bucket policy and examples, see [Overview](https://intl.cloud.tencent.com/document/product/436/18023) and [Bucket Policy](https://intl.cloud.tencent.com/document/product/436/45235). The following describes how to add a bucket policy.

>! Each root account can create up to 1,000 bucket ACL rules.
>

## Prerequisites

You have created a bucket. For more information, see [Creating Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the target bucket to enter the configuration page.
3. On the left sidebar, click **Permission Management** > **Permission Policy Settings**. COS allows you to add bucket policies through **[Visual Editor](#1)** or **[JSON](#2)** as needed in the following steps:
![](https://qcloudimg.tencent-cloud.cn/raw/c0cde183414d0a01ee1cd14d84483613.png)
For more information on configuration items, see [Overview](https://intl.cloud.tencent.com/document/product/436/18023).
4. After confirming that the configuration information is correct, click **OK** or **Save**. In this way, if a sub-account logs in to the COS console, it can only access resources allowed by the policy.

<span id=1></span>

## Visual Editor
On the **Visual Editor** tab page, click **Add Policy**. In the pop-up window, configure the policy in two steps: **select a template** and **configure the policy**.

### Step 1. Select a template

COS provides you with different templates depending on the combination of authorized users (grantees) and resource scope you choose to help you quickly configure bucket policies.

- Grantee
 - **All users (allow anonymous access)**: Select this option if you want to grant operation permissions to anonymous users. If you select this option, all users (`*`) will be automatically selected for you during policy configuration in step 2. Because it is risky to grant permissions on operations such as listing buckets (`ListBucket`) and configuring bucket configuration permissions to anonymous users, COS does not provide corresponding templates when this option is selected. You can add policies during policy configuration in step 2 if necessary.
 - **Specified user**: Select this option if you want to grant operation permissions to specified sub-accounts, root accounts, or cloud services. During policy configuration in step 2, you need to further specify the specific account UINs.
![](https://qcloudimg.tencent-cloud.cn/raw/ee012d2b26a9670e1e876a243e6a26ae.png)

- Resource Scope
 - **The whole bucket**: If you want to configure bucket configuration permissions or set the resource scope to the entire bucket, you can select this option to automatically add the entire bucket as a resource for you during policy configuration in step 2.
 - **Specified directory**: Select this option if you want to restrict the resource scope to a specified folder. During policy configuration in step 2, you need to further specify the specific directory. When this option is selected, COS does not provide policy templates related to bucket configuration, because for such permissions, the entire bucket must be specified as the resource.
![](https://qcloudimg.tencent-cloud.cn/raw/ee012d2b26a9670e1e876a243e6a26ae.png)

- Template: Collection of operations that you want to authorize.
 - **Custom (no preset configuration)**: If you do not need to use a template, select this option and add policies as needed during policy configuration in step 2.
 - **Other templates**: COS provides you with different recommended templates depending on the combination of authorized users and resource scope you choose. After you select a template, COS automatically adds the corresponding operation permissions for you during policy configuration in step 2.
![](https://qcloudimg.tencent-cloud.cn/raw/d7b01ebbfd480190b02e6af986ca4972.png)
>?If the authorized operations provided by the template do not meet your requirements, you can add or delete authorized operations during policy configuration in step 2.

Templates are described in the following table.
<table>
   <tr>
      <th>Grantee</td>
      <th>Resource Scope</td>
      <th>Policy Template</td>
      <th>Description</td>
   </tr>
   <tr>
      <td colspan=2>All combinations</td>
      <td>Custom</td>
      <td>For any combination of authorized users and resource scopes, this template does not provide any preset policies. You can add policies during policy configuration in step 2.</td>
   </tr>
   <tr>
      <td rowspan=4>All users (allow anonymous access)</td>
      <td rowspan=2>The whole bucket</td>
      <td>Read-Only objects (listing objects is not included)</td>
      <td rowspan=4>For anonymous users, COS provides you with recommended templates for reading files (such as downloading files) and writing files (such as uploading and modifying files).<br><br>COS's recommended templates do not list all objects in your bucket, and sensitive permissions, such as read and write permissions and bucket configuration permissions, are not allowed to improve data security. <br><br>You can add or delete operation permissions during policy configuration in step 2 as needed.</td>
   </tr>
   <tr>
      <td>Read/Write objects (listing objects is not included)</td>
   </tr>
   <tr>
      <td rowspan=2>Specified directory</td>
      <td>Read-Only objects (listing objects is not included)</td>
   </tr>
   <tr>
      <td>Read/Write objects (listing objects is not included)</td>
   </tr>
   <tr>
      <td rowspan=11>Specified user</td>
      <td rowspan=7>The whole bucket</td>
      <td>Read-Only objects (listing objects is not included)</td>
      <td rowspan=7>COS provides the most recommended templates for the combination of <b>Specified user</b> and <b>The whole bucket</b>. In addition to reading, writing, and listing files, COS provides the following sensitive permission templates for trusted users:<li>Read/Write buckets and object ACLs: Get and modify buckets and object ACLs. Options include GetObjectACL, PutObjectACL, GetBucketACL, and PutBucketACL. <li>General bucket configuration items: Non-sensitive permissions such as bucket tagging, CORS, and origin-pull. <li>Bucket sensitive configuration item: Sensitive permissions such as bucket policies, bucket ACLs, and bucket deletion. Sensitive permissions should be used with caution.</td>
   </tr>
   <tr>
      <td>Read-Only objects (listing objects is included)</td>
   </tr>
   <tr>
      <td>Read/Write objects (listing objects is not included)</td>
   </tr>
   <tr>
      <td>Read/Write objects (listing objects is included)</td>
   </tr>
   <tr>
      <td>Read/Write buckets and object ACLs</td>
   </tr>
   <tr>
      <td>General bucket configuration items</td>
   </tr>
   <tr>
      <td>Bucket sensitive configuration item</td>
   </tr>
   <tr>
      <td rowspan=4>Specified directory</td>
      <td>Read-Only objects (listing objects is not included)</td>
      <td rowspan=4>For the combination of <b>Specified user</b> and <b>Specified directory</b>, COS provides you with recommended templates for reading files (such as downloading files) and writing files (such as uploading and modifying files), as well as recommended templates for listing objects.<br><br>If you need to grant read, write, and list permissions to a specified folder to a specified user, this combination is recommended.<br><br>You can add or delete operation permissions during policy configuration in step 2 as needed.</td>
   </tr>
   <tr>
      <td>Read-Only objects (listing objects is included)</td>
   </tr>
   <tr>
      <td>Read/Write objects (listing objects is not included)</td>
   </tr>
   <tr>
      <td>Read/Write objects (listing objects is included)</td>
   </tr>
</table>

### Step 2. Configure a policy
Based on the combination of authorized users, specified directories, and templates you select in step 1, COS automatically adds operations, authorized users, and resources to the configuration policy for you. If you specify a user and a directory, you need to specify the user UIN and directory during policy configuration.

If the recommended templates provided by COS do not meet your requirements, you can add or delete authorized users, resources, and operations in this step. The configuration items are described as follows:
- Effect: Select **Allow** or **Deny**, corresponding to **allow** or **deny** in the policy syntax.
- User: Add or delete authorized users. Options include **Everyone** (`*`), **Root account**, **Sub-account**, and **Cloud service**.
- Resource: Add the whole bucket or a specific directory resource.
- Operation: Add or delete authorized operations as needed.
- Condition: You can specify conditions for permission authorization. For example, you can specify a user access IP.
![](https://qcloudimg.tencent-cloud.cn/raw/60015ffb067decd0cdfda05a740efb24.png)


<span id=2></span>
## Policy Syntax

Click **Edit** to enter the user-defined policy syntax. COS provides policy syntax for various scenarios. For more information, see [Bucket Policy](https://intl.cloud.tencent.com/document/product/436/45235).
![](https://main.qcloudimg.com/raw/b4e280ccbd67b081dcb59c4039f4d3b0.png)

