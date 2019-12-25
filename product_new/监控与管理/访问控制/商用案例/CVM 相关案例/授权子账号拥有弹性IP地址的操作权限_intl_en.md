
The enterprise account, `CompanyExample` (ownerUin: 12345678), has a sub-account, `Developer`, that requires permissions for the CVM service under the `CompanyExample` enterprise account. The sub-account needs to view Elastic IPs (EIPs) in the CVM Console, and use the EIPs.

Step 1: create the following policy by using policy syntax.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cvm:AllocateAddresses",
                "cvm:AssociateAddress",
                "cvm:DescribeAddresses",
                "cvm:DisassociateAddress",
                "cvm:ModifyAddressAttribute",
                "cvm:ReleaseAddresses"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
Step 2: associate the policy with the sub-account. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

The following policy allows a sub-account to view the EIPs and associate them with instances. The sub-account can modify the attributes of the EIPs, disassociate them from instances, and release the EIPs.

Step 1: create the following policy by using policy syntax.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cvm:DescribeAddresses",
                "cvm:AllocateAddresses",
                "cvm:AssociateAddress"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
Step 2: associate the policy with the sub-account. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

