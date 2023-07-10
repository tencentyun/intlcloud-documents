## Overview

CFS（Cloud File Storage） supports access management at the resource level, i.e., allowing the root account to grant users and user groups permissions to manipulate specified resources. After authorization, the CFS Console and APIs will allow or forbid operations performed by specified users based on permissions granted.
This document describes how to configure read-only, read/write, and custom policies for CFS users. For more information on how Cloud Access Management (CAM) works and can be used, please see [CAM Overview](https://intl.cloud.tencent.com/document/product/598/10583).



## Creating an Access Control Policy

Log in to the [CAM Console](https://console.cloud.tencent.com/cam/policy) and enter the policy management page.

- To grant users permissions quickly, do a search for CFS, select the preset read-only or read/write permissions and associate them with the specified user group.
- If you need to grant users permissions for specific operations, you can create a custom policy and associate it with the specified user group.

#### Full read/write permission policy

If you want to authorize users to perform all operations such as CRUD, you can associate them with the `QcloudCFSFullAccess` policy. Below is the policy syntax for using the preset `QcloudCFSFullAccess` policy to grant collaborators or subusers full read/write access to all CFS resources and VPC/subnet query permission:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cfs:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:DescribeVpcEx",
                "vpc:DescribeSubnetEx"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

#### Read-only permission policy

If you want to grant users permission to query but not create, modify, or delete resources, you can associate them with the `QcloudCFSReadOnlyAccess` policy. Below is the policy syntax for using the preset `QcloudCFSReadOnlyAccess` policy to grant collaborators or subusers read-only access to all CFS resources and VPC/subnet query permission:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cfs:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:DescribeVpcEx",
                "vpc:DescribeSubnetEx"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

#### Custom policy

Custom policies allow more flexibility in permission management. The CAM Console offers multiple methods for generating custom policies. This example shows you how to create a custom policy by using a **Policy Generator**. For other methods, please see [Creating Custom Policies](https://intl.cloud.tencent.com/document/product/598/35596).

The CAM policy generator is very user friendly. You simply need to select the desired parameters, and policy code will be generated automatically. This is especially suitable for first-time CAM users.

Log in to the [CAM Policies Console](https://console.cloud.tencent.com/cam/policy), and select **Create Custom Policy** > **Create by policy generator**. Use the policy generator to create a custom policy to which you can add multiple statements. The configurations are described as below:

| Parameter | Options and Effect |
| ---- |  ----------- |
| Effect        | Allow or Reject    |
| Service      | Select CFS here  |
| Action      | All CFS-supported actions   |
| Resource     | All resources that can be manipulated: <br><li>For all resources in CFS, enter `*`<br><li>For all resources in a specified region, use the format: `qcs::cfs:ap-guangzhou::*`<br><li>For all resources in all regions under a specified user account, use the format `qcs::cfs::uin/27700000:*` <br><li>For all file systems in a specified region under a specified user account, use the format `qcs::cfs:ap-guangzhou:uin/27700000:filesystem/*` <br><li>For file systems in a specified user group under a specified user account, use the format `qcs::cfs::uin/27700000:pgroup/pgroup-doxpcqh` <br><li>Note: the UIN in a policy must be a root account UIN. The file systems or permission group resources must belong to the root account.</li>   |
| Condition    | Sets the condition that must be met for the created policy to take effect, please see [Condition](https://intl.cloud.tencent.com/document/product/598/10608) |

The APIs, API features, and notes for authorization are listed in the table below. You can set your resource permissions accordingly.

<table>
   <tr>
      <th>API Category</th>
      <th>API Name</th>
      <th>API Description</th>
      <th>Permission Type</th>
      <th>Note</th>
   </tr>
   <tr>
      <td rowspan="2">Service APIs</td>
      <td>SignUpCfsService</td>
      <td>Activates the CFS service</td>
      <td>Write permission</td>
      <td>You do not need to specify resources when authorizing this API</td>
   </tr>
   <tr>
      <td>DescribeCfsServiceStatus</td>
      <td>Queries whether the CFS service is activated</td>
      <td>Read permission</td>
      <td>You do not need to specify resources when authorizing this API</td>
   </tr>
   <tr>
      <td rowspan="9">File system APIs</td>
      <td>DescribeCfsFileSystems</td>
      <td>Lists file systems</td>
      <td>Read permission</td>
      <td>You need to specify the resources as <code>*</code> when authorizing this API</td>
   </tr>
   <tr>
      <td>CreateCfsFileSystem</td>
      <td>Creates a file system</td>
      <td>Write permission</td>
      <td>You do not need to specify file system resources when authorizing this API</td>
   </tr>
   <tr>
      <td>UpdateCfsFileSystemName</td>
      <td>Updates the file system name</td>
      <td>Write permission</td>
      <td>You need to specify file system resources when authorizing this API</td>
   </tr>
   <tr>
      <td>UpdateCfsFileSystemPGroup</td>
      <td>Updates the permission group for a file system</td>
      <td>Write permission</td>
      <td>You need to specify file system resources when authorizing this API</td>
   </tr>
   <tr>
      <td>UpdateCfsFileSystemSizeLimit</td>
      <td>Updates the file system quota</td>
      <td>Write permission</td>
      <td>You need to specify file system resources when authorizing this API</td>
   </tr>
   <tr>
      <td>DeleteCfsFileSystem</td>
      <td>Deletes a file system</td>
      <td>Write permission</td>
      <td>You need to specify file system resources when authorizing this API</td>
   </tr>
   <tr>
      <td>DescribeMountTargets</td>
      <td>Queries mount targets</td>
      <td>Read permission</td>
      <td>You need to specify file system resources when authorizing this API</td>
   </tr>
   <tr>
      <td>AddMountTarget</td>
      <td>Creates a mount target</td>
      <td>Write permission</td>
      <td>You need to specify file system resources when authorizing this API</td>
   </tr>
   <tr>
      <td>DeleteMountTarget</td>
      <td>Deletes a mount target</td>
      <td>Write permission</td>
      <td>You need to specify file system resources when authorizing this API</td>
   </tr>
   <tr>
      <td rowspan="8">Permission group APIs</td>
      <td>DescribeCfsPGroups</td>
      <td>Lists permission groups</td>
      <td>Read permission</td>
      <td>You need to specify the resources as <code>*</code> when authorizing this API</td>
   </tr>
   <tr>
      <td>CreateCfsPGroup</td>
      <td>Creates a permission group</td>
      <td>Write permission</td>
      <td>You do not need to specify resources when authorizing this API</td>
   </tr>
   <tr>
      <td>UpdateCfsPGroup</td>
      <td>Updates the information of a permission group</td>
      <td>Write permission</td>
      <td>You need to specify permission group resources when authorizing this API</td>
   </tr>
   <tr>
      <td>DeleteCfsPGroup</td>
      <td>Deletes a permission group</td>
      <td>Write permission</td>
      <td>You need to specify permission group resources when authorizing this API</td>
   </tr>
   <tr>
      <td>DescribeCfsRules</td>
      <td>Lists permission group rules</td>
      <td>Read permission</td>
      <td>You need to specify permission group resources when authorizing this API</td>
   </tr>
   <tr>
      <td>CreateCfsRule</td>
      <td>Creates a permission group rule</td>
      <td>Write permission</td>
      <td>You need to specify permission group resources when authorizing this API</td>
   </tr>
   <tr>
      <td>UpdateCfsRule</td>
      <td>Updates the information of a permission group rule</td>
      <td>Write permission</td>
      <td>You need to specify permission group resources when authorizing this API</td>
   </tr>
   <tr>
      <td>DeleteCfsRule</td>
      <td>Deletes a permission group rule</td>
      <td>Write permission</td>
      <td>You need to specify permission group resources when authorizing this API</td>
   </tr>
   <tr>
      <td>Key APIs</td>
      <td>DescribeKmsKeys</td>
      <td>Queries KMS keys</td>
      <td>Read permission</td>
			<td>You need to specify the resources as <code>*</code> when authorizing this API</td>
   </tr>
</table>

>! As CFS file systems use the VPC IPs, permissions for "vpc:DescribeVpcEx" and "vpc:DescribeSubnetEx" APIs are needed to create, list and query file systems. We strongly recommend granting all VPC resources permissions for these two APIs in all your CFS authorization polices. See the `QcloudCFSReadOnlyAccess` policy statement to learn how to write the policy.

After setting the above parameters, click **Add Statement** to add a statement to the custom policy. Repeat these steps to add multiple statements. If the policy already exists or conflicts with other policies, see [Syntax Structure](https://intl.cloud.tencent.com/document/product/598/10604).

A policy should be written in the following format. There can be multiple statements in one policy.

```
{
    "version": "2.0",
    "statement": [{
        "effect": "Effect",
        "action": [
            "Action"
        ],
        "resource": "Resource"

    }]
}
```

For example, the policy syntax for prohibiting users from deleting certain file systems and updating quotas is as follows:

```
{
    "version": "2.0",
    "statement": [{
        "effect": "deny",
        "action": [
            "name/cfs:DeleteCfsFileSystem",
            "name/cfs:UpdateCfsFileSystemSizeLimit"
        ],
        "resource": [
            "qcs::cfs::uin/2779643970:filesystem/cfs-11111111",
            "qcs::cfs::uin/2779643970:filesystem/cfs-22222222",
            "qcs::cfs::uin/2779643970:filesystem/cfs-33333333"
        ]
    }]
}
```

## Authorizing a User/User Group

If you wish to grant an existing permission, you can do a search for `QcloudCFSFullAccess`, `QcloudCFSReadOnlyAccess`, or a custom policy and click **Bind User/Group** in the "Operation" column. Then, locate and select the user or user group that needs to be authorized and click **OK**.

## Deauthorizing a User/User Group

If you need to deauthorize a user/user group, click the policy name to go to the policy details page. Select the user or user group under the **User/User Group** tab and click **Remove User** or **Remove Group**. Click **OK** in the pop-up confirmation box. The user/user group’s CFS permissions will be revoked. 
