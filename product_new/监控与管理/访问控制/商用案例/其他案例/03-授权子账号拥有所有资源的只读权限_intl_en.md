
A sub-account, Developer, under the enterprise account, CompanyExample, requires read-only permissions for all resources belonging to the enterprise account.

Solution A:

The enterprise account, CompanyExample, associates the Developer sub-account with the preset policy ReadOnlyAccess. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Step 1: create the following policy by using policy syntax.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cvm:Describe*",
                "cvm:Inquiry*",
                "vpc:Describe*",
                "vpc:Inquiry*",
                "vpc:Get*",
                "clb:Describe*",
                "monitor:*",  
                "bm:Describe*",
                "bmeip:Describe*",
                "bmlb:Describe*",
                "bmvpc:Describe*",
                "bm:Get*",
                "bmlb:Get*",
                "cos:List*",
                "cos:Get*",
                "cos:Head*",
                "cos:OptionsObject",
                "cas:Describe*",
                "cas:List*",
                "cas:Get*",
                "kms:List*",
                "kms:Get*"                
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

