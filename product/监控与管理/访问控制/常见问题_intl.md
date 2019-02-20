### Why do I receive a prompt saying that I am not on the whitelist appears when I create a policy?

Many products are under beta test, and some products do not support CAM. See [CAM-enabled Cloud Services](https://cloud.tencent.com/document/product/598/10588) to determine whether and at what granularity you can manage product permissions in CAM.

To manage permissions in CAM for the products in beta test, [submit a ticket](https://console.cloud.tencent.com/workorder).



### Why do I receive a prompt saying no permission after full COS read/write permission is authorized?

The reason the console COS V4 gives a prompt saying no permission after the preset policy QcloudCOSFullAccess is associated is because that console COS V4 is not integrated with CAM. We recommend that you use console COS V5. 



### Why do I have no access to the cloud services after the read-only permission is authorized?

The read-only access to cloud services takes effect when either of the following conditions is met.
 - The service you are using is fully integrated with CAM.
 - The service you are using is integrated with CAM in beta test, and your account is on the whitelist.



### How can I implement refined permission management for the project resources?

You can do so by using [labels](https://cloud.tencent.com/document/product/651). 


### How can I grant a sub-account the permission to view the list of partial resources?

See the following example:

A sub-account Developer under the enterprise account CompanyExample (ownerUin is 12345678) needs to be granted the permission to view only part of the resources of the enterprise account CompanyExample in the console.

We take CVM instance as an example. To grant the sub-account the access to CVM instances with IDs of ins-xxxxxx1 and ins-xxxxxx2 in the region of gz in the console:

1. Create the following policy using policy syntax
```
{
	"version": "2.0",
	"statement": [{
		"action": [
			"cvm:DescribeInstances"
		],
		"resource": ["qcs::cvm:gz:instance:ins-xxxxxx1",
			"qcs::cvm:gz:instance:ins-xxxxxx2"
		],
		"effect": "allow"
	}]
}
```
You can also grant the sub-account a higher permission as needed, such as the full read/write permission. To grant the sub-account the full read/write access to CVM instances in the region of Guangzhou, you can write the policy syntax as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cvm:*"
                ],
            "resource": "qcs::cvm:gz:instance:*",
            "effect": "allow"
        }
    ]
}
```

2. Authorize the policy to the sub-account. For more information on authorization, see [Authorization Management](https://cloud.tencent.com/document/product/598/10602).

The products that **support** read-only permission at resource level include: CVM, TencentDB for MySQL, and TKE.
For other products, the read-only access to specific resources is not available. The sub-accounts can only be authorized to view all resources or unable to view all resources.



### What cloud services support limiting access via IP?

| Service Name | Limiting Access via IP |
| -------------------------- | ------------ |
| CPM | ✔ |
| TKE - CI | ✔ |
| TKE - Cluster | ✔ |
| CLB | ✔ |
| COS | ✔ |
| Dayu Anti-DDoS - Anti-DDoS Advanced | ✔ |

