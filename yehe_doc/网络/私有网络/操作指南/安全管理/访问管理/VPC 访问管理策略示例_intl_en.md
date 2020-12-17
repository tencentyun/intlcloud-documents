## Full Read-write Permission Policy for VPC
The following policy allows you to create and manage VPC instances. You can associate this policy with a group of network admins. The `Action` element specifies all VPC-related APIs.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/vpc:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
## Read-only Permission Policy for VPC
The following policy allows you to query your VPC and relevant resources. However, you cannot create, update, or delete them with this policy.
We recommend that you grant the VPC read-only permission for users, because they have to be able to view the resource in order to operate it in the console.

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/vpc:Describe*",
                "name/vpc:Inquiry*",
                "name/vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

## Allowing a Sub-Account to Manage Only a Single VPC
The following policy allows a user to view all VPC instances but only to be able to operate VPC A (for example, VPC A with an ID of vpc-d08sl2zr) and network resources in VPC A (such as subnets and route tables, but excluding cloud virtual machines (CVMs) and databases). In other words, the user is not allowed to manage other VPC instances.
This version does not support **allowing the user to view VPC A only**, which however will be supported in future versions.

```
{
    "version": "2.0",
    "statement": [
        {
            "action": "name/vpc:*",
            "resource": "*",
            "effect": "allow",
            "condition": {
                "string_equal_if_exist": {  //Conditional judgment: only eligible instances can be managed
                    "vpc:vpc": [
                    "vpc-d08sl2zr"
                    ],
                    "vpc:accepter_vpc": [
                     "vpc-d08sl2zr"
                    ],
                     "vpc:requester_vpc": [
                     "vpc-d08sl2zr"
                    ]
                }
            }
        }
    ]
}
```

## Allowing a User to Manage VPC Instances but Not Operate Route Tables
The following policy allows a user to read and write VPC instances and relevant resources, but disallows the user to operate route tables.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/vpc:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "name/vpc:AssociateRouteTable",
                "name/vpc:CreateRoute",
                "name/vpc:CreateRouteTable",
                "name/vpc:DeleteRoute",
                "name/vpc:DeleteRouteTable",
                "name/vpc:ModifyRouteTableAttribute"
            ],
            "resource": "*",
            "effect": "deny"
        }
    ]
}
```

## Allowing a User to Manage VPN Resources
The following policy allows a user to view all VPC resources, while only allows the user to create, read, update, and delete (CRUD) VPN resources.

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/vpc:Describe*",
                "name/vpc:Inquiry*",
                "name/vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "name/vpc:*Vpn*",
                "name/vpc:*UserGw*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
