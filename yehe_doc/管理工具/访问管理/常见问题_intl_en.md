### How do I grant a sub-account specific operation permissions of specific products?

You can [create a custom policy](https://intl.cloud.tencent.com/document/product/598/35596), select the products and operations you need, and [associate the policy with the user](https://intl.cloud.tencent.com/document/product/598/10602). After association, your sub-account will be able to manage the resources under the root account within the scope of permissions you set.

### How do I reset a sub-account’s password?

For more information on how to change a sub-user’s password, please see [Resetting Login Passwords for Sub-Users](https://intl.cloud.tencent.com/document/product/598/32656). For more information on how to change a collaborator’s password, please see [Account Password](https://intl.cloud.tencent.com/document/product/378/36001).


### Why can’t a sub-account access certain Tencent Cloud products after it has been authorized with the read-only policy (ReadOnlyAccess)?

The read-only policy (ReadOnlyAccess) only covers read APIs of Tencent Cloud products where the authorization granularity is operation level or resource level. If you access service-level products or the write APIs of operation-level/resource-level products, the prompt for no access will be displayed. For the authorization granularity of Tencent Cloud products, please see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

 ### After a sub-account is authorized, which account owns the resources purchased by the sub-account?

 Resources purchased by the sub-account are owned by the root account.

 ### How will the fees incurred by resource purchases made by a sub-account be paid?

 Fees incurred by the sub-account will be deducted from the balance of the root account.

### Why do I get a prompt saying that "The account is not on the allowlist" when creating a policy?

Some of Tencent Cloud products are still in beta, and a few products do not support CAM yet. See [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588) to check whether and at what granularity you can manage permissions of a product in CAM.

If you want to use CAM to manage permissions of a product in beta, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### How do I implement fine-grained permissions management for project resources?

You can implement fine-grained permissions management by using [tags](https://intl.cloud.tencent.com/document/product/651). 


### How should I grant permissions to allow a sub-account to only view part of my resources?

The following example describes how to allow a sub-account to view only part of the resources:

The enterprise account `CompanyExample` (ownerUin: 12345678) has a sub-account `Developer`. `CompanyExample` wants to allow the sub-account to view only part of its resources in the console.

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

2. Associate the policy with the sub-account. For more information on authorization, see [Authorization Management](https://cloud.tencent.com/document/product/598/10602).

The products that **support** read-only permission at the resource level include CVM, TencentDB for MySQL, and TKE.
Currently, other products do not support granting read-only access to specific resources. A sub-account either has the permission to view all the resources or has no permission to view any.

### How can I view the RoleArn of the role?
You can go to [Roles](https://console.cloud.tencent.com/cam/role) in the CAM console, click the name of the desired role to go to the role detail page, and query in the **Role Info** area.

### What is an API key?
An API key is an important identity credential for making Tencent Cloud API requests. You can use APIs to manage resources under your Tencent Cloud account. For the security of your assets and services, store your keys safely and change them regularly.

### Where can I view the API key?

 The API key is the access key. For more information on how to view the root account API key, please see [Root Account Access Key](https://intl.cloud.tencent.com/document/product/598/34228). For more information on how to view the sub-account API Key, please see [Access Key](https://intl.cloud.tencent.com/document/product/598/32675).

### Which Tencent Cloud services support limiting access via IP?

| Service | Limiting Access via IP |
| -------------------------- | ------------ |
| TKE - CI | ✔ |
| TKE - Cluster | ✔ |
| CLB | ✔ |
| COS | ✔ |
| Dayu Anti-DDoS - Anti-DDoS Advanced | ✔ |

