

You can use a bucket policy to grant the operation permissions of a bucket and the objects in the bucket to CAM sub-accounts, other root accounts, and even anonymous users.

## Overview

>!A Tencent Cloud root account has the highest permission on its resources (including buckets). Even if you can set limits on almost all operations in the bucket policy, the root account always has the permission for the PUT Bucket Policy operation, and can call this operation without checking the bucket policy.

A bucket policy is described in JSON language, and supports granting anonymous identities or any Tencent Cloud [CAM](https://intl.cloud.tencent.com/document/product/598/10583) account the permissions to access and perform operations on buckets and objects. In Tencent Cloud COS, the bucket policy can be used to manage almost all operations in the bucket. It is recommended that you use a bucket policy to manage access policies that cannot be described using ACLs.

## Application Scenarios

>!The permissions for the service-level operations of creating a bucket and querying a bucket list must be configured in the [CAM console](https://console.cloud.tencent.com/cam).

If you want to specify which users can access a COS bucket, you are advised to configure a bucket policy. You can search for a bucket and check the bucket's policy to see who can access the bucket. A bucket policy is recommended in scenarios where you want to:

- Authorize a specific bucket.
- Use higher flexibility than that of an ACL.
- Use cross-account authorization and anonymous user authorization, which are not supported by user policies.

## Bucket Policy Elements

A bucket policy is described in JSON language and its syntax complies with the unified specifications of the [access policy language](https://intl.cloud.tencent.com/document/product/436/18023). The access policy language contains the following basic elements: principal, effect, action, resource, and condition. For more information, see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023).
The resource scope of a bucket policy is restricted to the bucket, and you can perform authorization on the entire bucket, specified directories, or specified objects.

> !When adding an access policy, be sure to grant the minimum permissions needed to satisfy your business needs. There may be data security risks if you grant other users the permission to access all of your resources `(resource:*)` or all operations `(action:*)`.

## Console Configuration Examples

>?
> - When configuring a bucket policy in the COS console, you need to grant users appropriate permissions to the bucket, for example, the permissions to get bucket tags and list bucket permissions.
> - The bucket policy size is limited to 20 KB.

For example, if you want to grant a sub-account all permissions of a specified directory in a bucket, the corresponding configuration is as follows:

| Configuration Item | Description |
|------|------|
| Effect | Allow |
| Principal | UIN of the sub-account, which must be a sub-account under the current root account, such as 100000000011 |
| Resource | Specified directory prefix, such as `folder/sub-folder/*` |
| Action | All operations |
| Condition | None |

In the COS console, you can add and manage bucket policies in two modes: [Visual Editor](https://intl.cloud.tencent.com/document/product/436/45235?lang=en&pg=#visual-editor) and [JSON](https://intl.cloud.tencent.com/document/product/436/45235?lang=en&pg=#json).

<span id="Visual Editor"></span>
### Visual Editor
Click the target bucket and choose **Permission Management** > **Permission Policy Settings** > **Visual Editor**. On the **Visual Editor** tab page, click **Add Policy**. In the pop-up window, configure the policy in two steps:

#### Step 1: select a template (optional)

COS provides you with different templates depending on the combination of authorized users (grantees) and resource scope you choose to help you quickly configure bucket policies. If the templates provided by COS do not meet your requirements, you can skip this step and add or delete authorized operations in [Step 2: configure the policy](#configurePolicies).

<dx-accordion>
::: Grantee

 - **All users (allow anonymous access)**: Select this option if you want to grant operation permissions to anonymous users. If you select this option, all users (`*`) will be automatically selected for you during policy configuration in step 2.
 - **Specified user**: Select this option if you want to grant operation permissions to specified sub-accounts, root accounts, or cloud services. During policy configuration in step 2, you need to further specify the account UINs.
:::
::: Resource Scope

 - **The whole bucket**: if you want to grant bucket configuration permissions or set the resource scope to the entire bucket, you can select this option to automatically add the entire bucket as a resource for you during policy configuration in step 2.
 - **Specified directory**: select this option if you want to restrict the resource scope to a specified folder. During policy configuration in step 2, you need to further specify the specific directory.
:::
::: Template
A template is a collection of operations that you want to authorize. COS provides you with different recommended templates depending on the combination of authorized users and resource scope you choose. If the templates provided by COS do not meet your requirements, you can skip this step and add or delete authorized operations during policy configuration in step 2.

 - **Custom (no preset configuration)**: If you do not need to use a template, select this option and add policies as needed during policy configuration in step 2.
 - **Other templates**: COS provides you with different recommended templates depending on the combination of authorized users and resource scope you choose. After you select a template, COS automatically adds the corresponding operation permissions for you during policy configuration in step 2.


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
      <td rowspan=7>COS provides the most recommended templates for the combination of <b>Specified user</b> and <b>The whole bucket</b>. In addition to reading, writing, and listing files, COS provides the following sensitive permission templates for trusted users:<li>Read/Write buckets and object ACLs: get and modify buckets and object ACLs. Options include GetObjectACL, PutObjectACL, GetBucketACL, and PutBucketACL. <li>General bucket configuration items: non-sensitive permissions such as bucket tagging, CORS, and origin-pull. <li>Bucket sensitive configuration item: sensitive permissions such as bucket policies, bucket ACLs, and bucket deletion. Sensitive permissions should be used with caution.</td>
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
:::
</dx-accordion>


#### Step 2: configure the policy[](id:configurePolicies)

Based on the combination of authorized users, specified directories, and templates you select in step 1, COS automatically adds operations, authorized users, and resources to the configuration policy for you. If you specify a user and a directory, you need to specify the user UIN and directory during policy configuration.

>? To authorize the permissions of a directory, you need to add `/*` to the resource path entered. For example, to authorize the `test` directory, you need to enter `test/*`.

If the recommended templates provided by COS do not meet your requirements, you can add or delete authorized users, resources, and operations in this step.

The configuration items are described as follows:
- **Effect**: select **Allow** or **Deny**, corresponding to `allow` or `deny` in the policy syntax.
- **User**: add or delete authorized users. Options include **Everyone** (`*`), **Root account**, **Sub-account**, and **Cloud service**.
- **Resource**: add the whole bucket or a specific directory resource.
- **Operation**: add or delete authorized operations as needed.
- **Condition**: you can specify conditions for permission authorization. For example, you can specify a user access IP.


<span id="JSON"></span>
### JSON

If you are familiar with bucket policies, you can click the target bucket, choose **Permission Management** > **Permission Policy Settings** > **JSON**, and write the bucket policy in JSON language.

After writing the bucket policy, you can add it via [API](https://intl.cloud.tencent.com/document/product/436/8282) or [SDK](https://intl.cloud.tencent.com/document/product/436/6474).


#### JSON policy example 

The following policy is to allow root account 100000000001 (APPID: 1250000000) to grant sub-account 100000000011 with all operation permissions of the objects in the `folder/sub-folder` directory in the `examplebucket-bj` bucket of the Beijing region.
```JSON
{
  "Statement": [
    {
      "Principal": {
        "qcs": [
          "qcs::cam::uin/100000000001:uin/100000000011"
        ]
      },
      "Effect": "Allow",
      "Action": [
        "name/cos:*"
      ],
      "Resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-bj-1250000000/folder/sub-folder/*"
      ]
    }
  ],
  "version": "2.0"
}
```


## Operation Methods

COS allows you to add bucket policies by using the COS console, APIs, or SDKs. The COS console provides the Visual Editor configuration mode and common authorization templates to help users that are unfamiliar with the policy language to quickly add policies.

<table>
   <tr>
      <th colspan=2>Operation Method</td>
      <th>Description</td>
   </tr>
   <tr>
      <td colspan=2><a href="https://intl.cloud.tencent.com/document/product/436/30927">Console</a></td>
      <td>Web page, intuitive and easy to use</td>
   </tr>
   <tr>
      <td colspan=2><a href="https://intl.cloud.tencent.com/document/product/436/8282">API</a></td>
      <td>RESTful API, sending requests directly to COS</td>
   </tr>
   <tr>
      <td rowspan=3>SDK</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/35811">JavaScript</a></td>
      <td rowspan=3>Rich SDK demos, supporting various programming languages</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/35865">Node.js</a></td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/35854">Mini Program</a></td>
   </tr>
</table>


## More Bucket Policy Examples

- [Granting authorization through bucket policies](https://intl.cloud.tencent.com/document/product/436/12514#granting-authorization-through-bucket-policies)
- [Granting Sub-Account Under One Root Account Permission to Manipulate Buckets Under Another Root Account](https://intl.cloud.tencent.com/document/product/436/32971)

> !When adding an access policy, be sure to grant the minimum permissions needed to satisfy your business needs. There may be data security risks if you grant other users the permission to access all of your resources `(resource:*)` or all operations `(action:*)`.

The following are examples of bucket policies used to limit subnets, principals and VPC IDs.

### Example 1

Limit the IP range in the subnet to 10.1.1.0/24 and the VPC ID to aqp5jrc1:

```
{
  "Statement": [
    {
      "Action": [
        "name/cos:*"
      ],
      "Condition": {
        "ip_equal": {
          "qcs:ip": [
            "10.1.1.0/24"
          ]
        },
        "string_equal": {
          "vpc:requester_vpc": [
            "vpc-aqp5jrc1"
          ]
        }
      },
      "Effect": "deny",
      "Principal": {
        "qcs": [
          "qcs::cam::anyone:anyone"
        ]
      },
      "Resource": [
        "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
      ]
    }
  ],
  "version": "2.0"
}
```

### Example 2
Limit the VPC ID to aqp5jrc1 and specify the principal and bucket:

```
{
  "Statement": [
    {
      "Action": [
        "name/cos:*"
      ],
      "Condition": {
        "string_equal": {
          "vpc:requester_vpc": [
            "vpc-aqp5jrc1"
          ]
        }
      },
      "Effect": "allow",
      "Principal": {
        "qcs": [
          "qcs::cam::uin/100000000001:uin/100000000002"
        ]
      },
      "Resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*"
      ]
    }
  ],
  "version": "2.0"
}
```
