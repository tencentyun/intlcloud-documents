
The enterprise account, CompanyExample (ownerUIN: 12345678), has a sub-account, Developer, that requires read-only permission for VPC services under the CompanyExample enterprise account. This permission allows the sub-account to query VPCs and related resources, but will not permit the sub-account to create, update, or delete CLBs.

Solution A:

The enterprise account, CompanyExample, associates the Developer sub-account with the preset policy QcloudVPCReadOnlyAccess. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Step 1: create the following policy by using policy syntax.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "vpc:Describe*",
                "vpc:Inquiry*",
                "vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

