### Why do I get a prompt saying that “The account is not on the whitelist” when creating a policy?

Some of our products are still in beta test, and a few products do not support CAM. See [CAM-enabled Products](https://intl.cloud.tencent.com/document/product/598/10588) to check whether and at what granularity you can manage permissions on a service in CAM.

If you want to use CAM to manage permissions for products in beta test, please [submit a ticket](https://console.cloud.tencent.com/workorder).



### Why do I receive a prompt in the Console saying that I have no access to COS after full access to COS has been granted?

COS V4 Console does not support CAM. If you log in to COS V4 Console after you are associated with the `QcloudCOSFullAccess` policy, you may get a prompt saying that you have no access. We recommend that you use COS V5 Console. 



### Why am I still not able to access Tencent Cloud services even though I have already been granted read-only access to the services?

Read-only access to Tencent Cloud services takes effect when either of the following conditions is met.
 - The service you are using is fully integrated with CAM.
 - The service you are using is in beta test, and your account is on the whitelist.



### How do I implement fine-grained permissions management for project resources?

You can implement fine-grained permissions management by using [tags](https://intl.cloud.tencent.com/document/product/651). 


### How should I grant permissions to allow a sub-account to only view part of my resources?

The following example describes how to allow a sub-account to only view part of the resources:

The enterprise account, `CompanyExample`, (ownerUin: 12345678), has a sub-account, `Developer`. `CompanyExample` wants to allow the sub-account to view only part of its resources in the Console.

For example, to allow the sub-account to view in the Console two CVM instances whose ID is `ins-xxx1` and `ins-xxx2` in the `gz` region:

1. Create the following policy by using policy syntax:
```
{
	"version": "2.0",
	"statement": [
	{
		"action": [
			"cvm:DescribeInstances"
		],
		"resource": ["qcs::cvm:gz::instance/ins-xxx1",
		    "qcs::cvm:gz::instance/ins-xxx2"
		],
		"effect": "allow"
	}
    ]
}
```
You can also grant the sub-account a wider permission, such as full access. To grant the sub-account full access to CVM instances in the Guangzhou region, create the following policy:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cvm:*"
                ],
            "resource": "qcs::cvm:gz::*",
            "effect": "allow"
        }
    ]
}
```

2. Associate the policy with the sub-account. For more information on authorization, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

The products that **support** read-only permission at the resource level include: CVM, TencentDB for MySQL, and TKE.
Currently, other products do not support granting read-only access to specific resources. A sub-account either has the permission to view all the resources or has no permission to view any.



### Which Tencent Cloud services support limiting access via IP?

| Service | Limiting Access via IP |
| -------------------------- | ------------ |
| CPM | ✔ |
| TKE - CI | ✔ |
| TKE - Cluster | ✔ |
| CLB | ✔ |
| COS | ✔ |
| Dayu Anti-DDoS - Anti-DDoS Advanced | ✔ |
