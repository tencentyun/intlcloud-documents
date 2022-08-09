
The enterprise account, CompanyExample (ownerUin: 12345678), has a sub-account, Developer, that requires permissions to operate a specific CVM (ID: ins-1) in Guangzhou region belonging to the enterprise account CompanyExample.

Step 1: create the following policy according to policy syntax.
```json
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cvm:*",
                "vpc:DescribeVpcEx",
                "vpc:DescribeNetworkInterfaces"
            ],
            "resource": "*",
            "condition": {
                "for_any_value:string_equal": {
                    "qcs:resource_tag": [
                        "game&webpage"
                    ]
                }
            }
        }
    ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
