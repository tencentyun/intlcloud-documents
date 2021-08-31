## Introduction

You can use Cloud Access Management (CAM) policies to manage user access to resources using the Cloud Virtual Machine (CVM) console. This document provides examples to help you understand how to use the pre-defined CAM policies using the CVM console.

## Examples
### Read and write (CVM)
If you want to allow a user to create and manage CVM instances, associate the user with the policy named QcloudCVMFullAccess. This policy is designed to grant users the permissions to access all the resources in CVM, Virtual Private Cloud (VPC), Cloud Load Balancer (CLB), and Cloud Monitor.
The detailed steps are as follows:
Refer to [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602) for instructions on how to grant the preset policy QcloudCVMFullAccess to a user.

### Read-only (CVM)
If you want to allow a user to only query, but not create, delete or start/shutdown CVM instances, associate the user with the policy named QcloudCVMInnerReadOnlyAccess. This policy is designed to grant users the permissions to perform all operations starting with "Describe" and "Inquiry" in CVM. The detailed steps are as follows:
Refer to [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602) for instructions on how to grant the preset policy QcloudCVMInnerReadOnlyAccess to a user.

### Read-only (CVM and associated resources)
If you want to to allow a user to only query, but not create, delete or start/shut down CVM instances and associated resources (VPC and CLB), associate the user with the policy named QcloudCVMReadOnlyAccess. This policy is designed to grant users the permissions to perform the following operations:
- All operations starting with "Describe" and "Inquiry" in CVM.
- All operations starting with "Describe", "Inquiry", and "Get" in VPC.
- All operations starting with "Describe" in CLB.
- All operations in the Monitor.

The detailed steps are as follows:
Refer to [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602) for instructions on how to grant the preset policy QcloudCVMReadOnlyAccess to a user.

### CBS policies

If you want to allow a user to view, create, and use cloud disks on the CVM console, add the following operations to your policy and associate the policy with the user.
- **CreateCbsStorages:** create a cloud disk.
- **AttachCbsStorages:** mount the specified cloud disk to the specified CVM.
- **DetachCbsStorages:** unmount the specified cloud disk.
- **ModifyCbsStorageAttributes:** modify the name or the project ID of the specified cloud disk.
- **DescribeCbsStorages:** query the details of a cloud disk.
- **DescribeInstancesCbsNum:** query the number of mounted cloud disks of a CVM and the maximum number of cloud disks that are allowed to be mounted to the CVM.
- **RenewCbsStorage:** renew the specified cloud disk.
- **ResizeCbsStorage:** resize the specified cloud disk.

The detailed steps are as follows:
1. Refer to [Policies](https://intl.cloud.tencent.com/document/product/598/10601) for information and create a custom policy that grants the permissions to view cloud disk information on the CVM console and to create and use cloud disks.
Use the following as a syntax reference:
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/cvm:CreateCbsStorages",
                "name/cvm:AttachCbsStorages",
                "name/cvm:DetachCbsStorages",
                "name/cvm:ModifyCbsStorageAttributes",
                "name/cvm:DescribeCbsStorages"
            ],
            "resource": [
                "qcs::cvm::uin/1410643447:*"
            ]
        }
    ]
}
```
2. Find the created policy, and in the “Action” column of the row, click **Associate User/Group**.
3. In the “Associate User/Group” window, select the user/group you want to associate, and click **OK**.


### Security group policies

To allow a user to view and use security groups on the CVM console, add the following operations to your policy, and associate the policy with the user.
- **DeleteSecurityGroup:** delete a security group.
- **ModifySecurityGroupPolicys:** replace all the policies of a security group.
- **ModifySingleSecurityGroupPolicy:** modify a single policy of a security group.
- **CreateSecurityGroupPolicy:** create a security group policy.
- **DeleteSecurityGroupPolicy:** delete a security group policy.
- **ModifySecurityGroupAttributes:** modify the attributes of a security group.

The detailed steps are as follows:
1. Refer to [Policies](https://intl.cloud.tencent.com/document/product/598/10601) for information and create a custom policy that grants the permissions to create, delete, and modify security groups on the CVM console.
Use the following as a syntax reference:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:ModifySecurityGroupPolicys",
                "name/cvm:ModifySingleSecurityGroupPolicy",
                "name/cvm:CreateSecurityGroupPolicy",
                "name/cvm:DeleteSecurityGroupPolicy"
            ],
            "resource": "*",
            “effect": "allow"
        }
    ]
}
```
2. Find the created policy, and in the “Action” column of the row, click **Associate User/Group**.
3. In the “Associate User/Group” window, select the user/group you want to authorize, and click **OK**.


### Policy for EIPs

If you want to allow a user to view and use EIPs on the CVM console, add the following operations to your policy, and associate the policy with the user.
- **AllocateAddresses:** assign an EIP to a VPC or CVM instance.
- **AssociateAddress:** associate an EIP with an instance or a network interface.
- **DescribeAddresses:** view EIPs on the CVM console.
- **DisassociateAddress:** disassociate an EIP from an instance or a network interface.
- **ModifyAddressAttribute:** modify the attributes of an EIP.
- **ReleaseAddresses:** release an EIP.

The detailed steps are as follows:
1. Refer to [Policies](https://intl.cloud.tencent.com/document/product/598/10601) for information and create a custom policy.
This policy allows users to view an EIP and assign it to and associate it with an instance on the CVM console. Users cannot modify the attributes of the EIP, disassociate it from an instance, or release the EIP. Use the following as a syntax reference:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:DescribeAddresses",
                "name/cvm:AllocateAddresses",
                "name/cvm:AssociateAddress"
            ],
            "resource": "*",
            “effect": "allow"
        }
    ]
}
```
2. Find the created policy, and in the “Action” column of the row, click **Associate User/Group**.
3. In the “Associate User/Group” window, select the user/group you want to authorize, and click **OK**.

### Policy for authorizing users to perform operations on specific CVMs
If you want to authorize a user to perform operations on a specific CVM, associate the following policy with the user. The detailed steps are as follows:
1. Refer to [Policies](https://intl.cloud.tencent.com/document/product/598/10601) for information and create a custom policy.
This policy authorizes the user to operate a CVM instance with the ID of ins-1 in the Guangzhou region. Use the following as a syntax reference:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cvm:*",
            "resource": "qcs::cvm:ap-guangzhou::instance/ins-1",
            “effect": "allow"
        }
    ]
}
```
2. Find the created policy, and in the “Action” column of the row, click **Associate User/Group**.
3. In the “Associate User/Group” window, select the user/group you want to authorize, and click **OK**.


### Policy for authorizing users to perform operations on the CVMs in a specific region
If you want to authorize a user to perform operations on the CVMs in a specific region, associate the following policy with the user. The detailed steps are as follows:
1. Refer to on [Policies](https://intl.cloud.tencent.com/document/product/598/10601) for information and create a custom policy.
This policy authorizes the user to operate CVM instances in the Guangzhou region. Use the following as a syntax reference:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cvm:*",
            "resource": "qcs::cvm:ap-guangzhou::*",
            “effect": "allow"
        }
    ]
}
```
2. Find the created policy, and in the “Action” column of the row, click **Associate User/Group**.
3. In the “Associate User/Group” window, select the user/group you want to authorize, and click **OK**.


### Granting a sub-account all permissions to CVM instances except payment

Assume that the account CompanyExample, whose ownerUin is 12345678, has a sub-account called Developer. Developer requires full management permissions (including all operations such as creation and management) for the CVM instance, except payment, which means Developer can make orders but cannot pay for them.
You can do this by using one of the following two solutions:
- **Solution A**
The account owner of CompanyExample associate the preset policy QcloudCVMFullAccess with Developer. For more information, refer to [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
- **Solution B**
 1. Use the following as a syntax reference and create a [custom policy](#CAMCustomPolicy).
```
 {
    "version": "2.0",
    "statement":[
         {
             "effect": "allow",
             "action": "cvm:*",
             "resource": "*"
         }
    ]
}
```
 2. Associate the policy to the sub-account. For more information, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).


### Granting a sub-account the permission to manage projects
Assume that the enterprise account, CompanyExample, with ownerUin of 12345678, has a sub-account called Developer. The owner of CompanyExample wants to allow Developer to manage projects, including assigning and removing resources, on the console.
The detailed steps are as follows:
1. Create a custom policy for project management.
For more information, refer to [Policies](https://intl.cloud.tencent.com/document/product/598/10601).
2. Refer to [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602) for information on how to associate the custom policy with the sub-account.
If you run into permission issues when attempting to view snapshots, images and EIPs, associate preset policies QcloudCVMAccessForNullProject, QcloudCVMOrderAccess, and QcloudCVMLaunchToVPC with the sub-account. For more information on authorization, refer to [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

<span id="CAMCustomPolicy"></span>
### Custom policy

If preset policies cannot meet your requirements, you can create custom policies.
For detailed instructions, refer to [Policies](https://intl.cloud.tencent.com/document/product/598/10601).
For more information on CVM policy syntax, refer to [Authorization Policy Syntax](https://intl.cloud.tencent.com/document/product/213/10313).

