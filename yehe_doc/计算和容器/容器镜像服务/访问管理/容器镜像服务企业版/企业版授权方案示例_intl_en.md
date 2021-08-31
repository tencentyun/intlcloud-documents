
## Configuring Preset Policies
- **QcloudTCRFullAccess**: full read/write permission of TCR.
After the policy is bound to a sub-account, the sub-account has all operation permissions for all TCR resources, including the Enterprise Edition and the Personal Edition instances in TCR TKE.
```
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
After the policy is bound to a sub-account, the sub-account has the read-only permission for all TCR resources, including the enterprise edition and the personal edition instances in TCR TKE.
```
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

## Configuring Policies in Typical Scenarios
>! The policies in the following use cases are used only for the Enterprise Edition.
>
- Grant a sub-account all read/write operation permissions for all resources in the TCR Enterprise Edition instance.
```
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
```
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
- Authorize a sub-account to manage the specified instance, for example, dev-guangzhou whose instance ID is ins-xxxxxxxx.
```
	{
		"version": "2.0",
		"statement": [{
			"action": [
				"tcr:*"
			],
			"resource": [
				"qcs::tcr:::instance/ins-xxxxxxxx/*"
			],
			"effect": "allow"
		}]
	}
```
- Authorize a sub-account to manage the specified namespace in the specified instance, for example, team-01 under the instance ins-xxxxxxxx.
```
	{
		"version": "2.0",
		"statement": [{
				"action": [
					"tcr:*"
				],
				"resource": [
					"qcs::tcr:::repository/ins-xxxxxxxx/team-01/*"
				],
				"effect": "allow"
			},
			{
				"action": [
					"tcr:DescribeInstances",
					"tcr:DescribeInstanceStatus"
				],
				"resource": [
					"qcs::tcr:::repository/ins-xxxxxxxx/*"
				],
				"effect": "allow"
			}
		]
	}
```
- Authorize a sub-account to read only an image repository and pull only images in the image repository instead of deleting a repository, modifying repository attributes, or pushing images, for example, repo-demo in the namespace team-01 under the instance ins-xxxxxxxx.
```
	{
		"version": "2.0",
		"statement": [{
				"action": [
					"tcr:DescribeRepository",
					"tcr:PullRepository"
				],
				"resource": [
					"qcs::tcr:::repository/ins-xxxxxxxx/team-01/repo-demo/*"
				],
				"effect": "allow"
			},
			{
				"action": [
					"tcr:DescribeInstances",
					"tcr:DescribeInstanceStatus",
					"tcr:DescribeNamespace"
				],
				"resource": [
					"qcs::tcr:::repository/ins-xxxxxxxx/*"
				],
				"effect": "allow"
			}
		]
	}
```
