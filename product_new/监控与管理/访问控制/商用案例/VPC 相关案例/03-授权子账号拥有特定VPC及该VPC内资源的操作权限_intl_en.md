
The enterprise account, CompanyExample (ownerUin: 12345678), has a sub-account, Developer, that requires operating permissions for a specific VPC (ID: vpc-id1) and relevant resources (e.g., subnets, routing tables, but not CVMs and databases) of the VPC service belonging to the CompanyExample enterprise account.

Step 1: create the following policy according to policy syntax.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "vpc:*",
            "resource": "*",
            "effect": "allow",
            "condition": {
                "string_equal_if_exist": {
                    "vpc:vpc": [
                    "vpc-id1"
                    ],
                    "vpc:accepter_vpc": [
                     "vpc-id1"
                    ],
                     "vpc:requester_vpc": [
                     "vpc-id1"
                    ]
                }
            }
        }
    ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
