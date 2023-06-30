This document describes how to enable sub-accounts to view and use the TCR related resources through the CAM policy, including specific operation steps and common policy configuration examples.

>! If you need the permissions of other Tencent Cloud services when using some features in TCR console such as VPC, CloudAudit, Tag, please see the corresponding CAM Guide in [CAM-Enabled Products](https://intl.cloud.tencent.com/ Document/product/598/10588).



## Directions
This document takes the example of "granting the sub-account the read-only permission of an image repository" to introduce how to create a policy.

- **Instance ID**: tcr-xxxxxxxx
- **Namespace**: team-01
- **Image repository**: repo-demo

<dx-tabs>
::: Creating by policy generator (recommended)
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. Click **Policies** on the left sidebar to access the **Policies** page.
3. Click **Create Custom Policy** in the upper-left corner.
4. In the selection window that pops up, click **Create by Policy Generator** to go to the **Edit Policy** page.
5. Select the service in the Visual Policy Generator, enter the following information, and edit an authorization statement. 
 - **Effect**: select **Allow** or **Deny**. Here we select **Allow**.
 - **Service**: select the service you want to authorize. Here we select **Tencent Container Registry (tcr)**.
 - **Action**: select the operations you want to authorize. Here we select **Read**.
 - **Resource**: select all resources or specific resources you want to authorize. Here we select **Specific resources**, and add the following six-segment resource to restrict the access.
	 - **repository**: select the region where the repository resides, and enter the resource path of the repository, for example, `tcr-xxxxxxxx/team-01/repo-demo/*`. You can get the resource path in [Image Repository](https://console.cloud.tencent.com/tcr/repository).
	 - **repo**: it is left empty.
	 - **instance**: select the region where the repository resides, and enter the ID of the instance to which the repository belongs, for example, `tcr-xxxxxxxx`. You can get the instance ID in the [Instance List](https://console.cloud.tencent.com/tcr/instance?rid=1).
 - **Condition**: it is left empty.
6. Click **Next** to go to the **Associate Users/User Groups** page.
7. In the **Associate Users/User Groups** page, add the policy name and description, and you can associate users or user groups for quick authorization at the same time.
8. Click **Done** to complete the custom policy creation.


:::
::: Creating by policy syntax
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. Click **Policies** on the left sidebar to access the **Policies** page.
3. Click **Create Custom Policy** in the upper-left corner.
4. In the selection window that pops up, click **Create by Policy Syntax** to go to the **Select Policy Template** page.
5. In **Select a template type** section, select **Blank Template**.
6. Click **Next** to go to the **Edit Policy** page.
7. In the **Edit Policy** page, enter the policy name and description, and add the following policy content.
```
	{
		"version": "2.0",
		"statement": [{
				"action": [
					"tcr:DescribeRepositories",
					"tcr:PullRepository",
					"tcr:DescribeNamespaces"
				],
				"resource": [
					"qcs::tcr:::repository/tcr-xxxxxxxx/team-01/repo-demo/*"
				],
				"effect": "allow"
			},
			{
				"action": [
					"tcr:DescribeInstance*"				
				],
				"resource": [
					"qcs::tcr:::instance/tcr-xxxxxxxx"
				],
				"effect": "allow"
			}
		]
	}
```
6. Click **Done** to complete the custom policy creation.


:::
</dx-tabs>


















## Common Policy Configuration

If you need to customize the policy JSON, please see [CAM APIs for Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/39860) and [Syntax Logic](https://intl.cloud.tencent.com/document/product/598/33415).

### Preset policy configuration
- **QcloudTCRFullAccess**: full read/write permission of TCR.
After the policy is bound to a sub-account, the sub-account has all operation permissions for all TCR resources, including the Enterprise Edition and the Personal Edition in TKE.
```json
	{
		"version": "2.0",
		"statement": [{
			"action": [
				"tcr:*"
			],
			"resource": "*",
			"effect": "allow"
		}]
	}
```
- **QcloudTCRReadOnlyAccess**: read-only permission of TCR.
After the policy is bound to a sub-account, the sub-account has the read-only permission for all TCR resources, including the Enterprise Edition and the Personal Edition in TKE.
```json
	{
		"version": "2.0",
		"statement": [{
			"action": [
				"tcr:Describe*",
				"tcr:PullRepository*"
			],
			"resource": "*",
			"effect": "allow"
		}]
	}
```

### Policy configuration in typical scenarios
>!The policies in the following use cases are used only for the Enterprise Edition. For the policies used for Personal Edition, please see [Example of Authorization Solution of the Personal Edition](https://intl.cloud.tencent.com/document/product/1051/37250).
>
- Grant a sub-account all read/write operation permissions for all resources in the TCR Enterprise Edition instance.
```json
	{
		"version": "2.0",
		"statement": [{
			"action": [
				"tcr:*"
			],
			"resource": [
				"qcs::tcr:::instance/*",
				"qcs::tcr:::repository/*"
			],
			"effect": "allow"
		}]
	}
```
- Grant a sub-account the read-only operation permission for all resources in the TCR Enterprise Edition instance.
```json
	{
		"version": "2.0",
		"statement": [{
			"action": [
				"tcr:Describe*",
				"tcr:PullRepository*"
			],
			"resource": [
				"qcs::tcr:::instance/*",
				"qcs::tcr:::repository/*"
			],
			"effect": "allow"
		}]
	}
```
- Authorize a sub-account to manage the specified instance, for example, dev-guangzhou whose instance ID is tcr-xxxxxxxx.
```json
	{
		"version": "2.0",
		"statement": [{
			"action": [
				"tcr:*"
			],
			"resource": [
				"qcs::tcr:::instance/tcr-xxxxxxxx"
			],
			"effect": "allow"
		}]
	}
```
- Authorize a sub-account to manage the specified namespace in the specified instance, for example, team-01 under the instance tcr-xxxxxxxx.
```json
	{
		"version": "2.0",
		"statement": [{
				"action": [
					"tcr:*"
				],
				"resource": [
					"qcs::tcr:::repository/tcr-xxxxxxxx/team-01/*"
				],
				"effect": "allow"
			},
			{
				"action": [
					"tcr:DescribeInstance*"
				],
				"resource": [
					"qcs::tcr:::repository/tcr-xxxxxxxx"
				],
				"effect": "allow"
			}
		]
	}
```
- Authorize a sub-account the read-only permission of an image repository, which means that the sub-account can only pull the images in the image repository instead of deleting a repository, modifying repository attributes, or pushing images, for example, repo-demo in the namespace team-01 under the instance tcr-xxxxxxxx.
```json
	{
		"version": "2.0",
		"statement": [{
				"action": [
					"tcr:DescribeRepositories",
					"tcr:PullRepository",
					"tcr:DescribeNamespaces"
				],
				"resource": [
					"qcs::tcr:::repository/tcr-xxxxxxxx/team-01/repo-demo/*"
				],
				"effect": "allow"
			},
			{
				"action": [
					"tcr:DescribeInstance*"
					
				],
				"resource": [
					"qcs::tcr:::instance/tcr-xxxxxxxx"
				],
				"effect": "allow"
			}
		]
	}
```
