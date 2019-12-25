
The enterprise account, CompanyExample (ownerUin: 12345678), has a sub-account, Developer, that requires permissions to view, create and use cloud disks in the CVM Console belonging to the CompanyExample enterprise account.

Solution A:

The enterprise account, CompanyExample, associates the Developer sub-account with the preset policy QcloudCBSFullAccess. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Step 1: create the following policy by using policy syntax.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cvm:CreateCbsStorages",
                "cvm:AttachCbsStorages",
                "cvm:DetachCbsStorages",
                "cvm:ModifyCbsStorageAttributes",
                "cvm:DescribeCbsStorages",
                "cvm:DescribeInstancesCbsNum",
                "cvm:RenewCbsStorage",
                "cvm:ResizeCbsStorage"
                ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Note: If the sub-account is not allowed to modify cloud disk properties, remove `cvm:ModifyCbsStorageAttributes` from the policy syntax.
