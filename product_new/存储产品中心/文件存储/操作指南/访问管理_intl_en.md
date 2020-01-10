## Operation Scenarios

CFS supports access management at the resource level, i.e., allowing the root account to grant users and user groups certain permissions to manipulate the specified resources. After the authorization is completed, the CFS Console and APIs will allow or forbid operations performed by the specified users based on the permissions granted to them.
This document describes how to configure read-only, read/write, and custom policies for CFS users. For more information on how Cloud Access Management (CAM) works and can be used, please see [CAM Overview](https://intl.cloud.tencent.com/document/product/598/10583).



## Creating an Access Control Policy

Log in to the [CAM Console](https://console.cloud.tencent.com/cam/policy) and enter the policy management page.

- If you need to grant users permissions quickly, you can search for CFS in the search box on the right of the policy management page, select the preset read-only or read/write permissions, and associate them with the specified user group.
- If you need to grant users permissions to specific operations, you can create a custom policy and associate it with the specified user group.

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

Custom policy is a more flexible way to authorize users. Multiple policy generation methods are available in the CAM Console. This example shows you how to create a custom policy by using the method of "Create by Policy Generator". For other methods, please see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).

The policy generator page provides visual policy configuration items. You just need to select the desired parameters, and policy code will be generated automatically. This is especially suitable if you use the CAM for the first time.

Log in to the [Policy Management Console](https://console.cloud.tencent.com/cam/policy), enter the policy page, and select **Create Custom Policy** > **Create by Policy Generator**. On the "Create Policy" page, use the policy generator to create a policy, and you can add multiple statements to the custom policy. The configurations are described as below:

| Parameter | Corresponding Parameter Policy | Option and Effect |
| ---- | ------------ | ------------------------------------------------------------ |
| Effect  | Effect       | Allow or deny    |
| Service | Service      | Select CFS here  |
| Operation | Action       | All operation types supported by CFS   |
| Resource | Resource     | All resources that can be manipulated: <br><li>For all resources in CFS, enter `*`<br><li>For all resources in the specified region, enter `qcs::cfs:ap-guangzhou::*` for example <br><li>For all resources in all regions under the specified user account, enter `qcs::cfs::uin/27700000:*` for example <br><li>For all file systems in the specified region under the specified user account, enter `qcs::cfs:ap-guangzhou:uin/27700000:filesystem/*` <br><li>For file systems in the specified user group under the specified user account, enter `qcs::cfs::uin/27700000:pgroup/pgroup-doxpcqh` <br><li>Note: the UIN in a policy must be a root account UIN (the file systems or permission group resources after it must belong to this root account)  |
| Condition | Condition    | Specifies under which condition this policy will take effect. For more information, please see [Conditions](https://intl.cloud.tencent.com/document/product/598/10608) |

The APIs, API features, and precautions during authorization are listed in the table below. You can configure resource options accordingly.

<table>
   <tr>
      <th>API Category</th>
      <th>API Name</th>
      <th>API Description</th>
      <th>Permission Type</th>
      <th>Precautions</th>
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
      <td>Queries mount points</td>
      <td>Read permission</td>
      <td>You need to specify file system resources when authorizing this API</td>
   </tr>
   <tr>
      <td>AddMountTarget</td>
      <td>Creates a mount point</td>
      <td>Write permission</td>
      <td>You need to specify file system resources when authorizing this API</td>
   </tr>
   <tr>
      <td>DeleteMountTarget</td>
      <td>Deletes a mount point</td>
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

> As CFS file systems use the VPC IPs, the permissions to the "vpc:DescribeVpcEx" and "vpc:DescribeSubnetEx" APIs need to be obtained for creating a file system, listing file systems, and querying file system details; otherwise, these operations cannot be performed. You are strongly recommended to grant the two APIs the permission to all VPC resources in all your authorization polices for CFS. For the detailed policy writing method, please see the policy statement of `QcloudCFSReadOnlyAccess`.

After the above parameters are configured, click **Add Statement** to add a statement to the custom policy. You can repeat this operation to add multiple statements. In case that a policy already exists or is in conflict with other policies, for more information on whether and how they will take effect, please see [Syntax Structure](https://intl.cloud.tencent.com/document/product/598/10604).

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

If you choose the permissions provided by the system, you can search for `QcloudCFSFullAccess`, `QcloudCFSReadOnlyAccess`, or a custom policy directly in the policy list and click **Associate User/User Group** in the "Operation" column on the right of the list. Then, locate and select the user or user group that needs to be authorized and click **OK**.

## Deauthorizing a User/User Group

If you need to deauthorize a user/user group, you can select them in the **Associated Users/User Groups** list on the corresponding policy details page and then click **Dissociate User**. After confirming the deauthorization, the user/user group will be deprived of the permission to manipulate CFS resources.
