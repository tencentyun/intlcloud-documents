## Configuring Policies in Typical Scenarios
>! The policies in the following scenarios are only used for Personal Edition.
>
- Grant a sub-account all read/write operation permissions for all resources in the TCR Personal Edition instance (image repository in TKE of the original TCR).
```
{
	"version": "2.0",
	"statement": [{
		"action": [
			"tcr:*"
		],
		"resource": [
			"qcs::tcr:::repo/*"
		],
		"effect": "allow"
	}]
}
```
- Grant a sub-account the read-only operation permission for all resources in the TCR Personal Edition instance (image repository in TKE of the original TCR).
```
{
	"version": "2.0",
	"statement": [{
		"action": [
			"tcr:Describe*",
			"tcr:PullRepository*"
		],
		"resource": [
			"qcs::tcr:::repo/*"
		],
		"effect": "allow"
	}]
}
```
- Authorize a sub-account to manage the specified instance in the specified region, for example, namespace team-01 in the default region.
```
{
	"version": "2.0",
	"statement": [{
			"action": [
				"tcr:*"
			],
			"resource": [
				"qcs::tcr:ap-guangzhou:*:repo/team-01/*"
			],
			"effect": "allow"
		}
	]
}
```
- Authorize a sub-account to read only an image repository and pull only images in the image repository instead of deleting a repository, modifying repository attributes, or pushing images, for example, the image repository repo-demo in the namespace team-01 under the default region.
```
{
	"version": "2.0",
	"statement": [{
			"action": [
				"tcr:Describe*",
				"tcr:PullRepositoryPersonal"
			],
			"resource": [
				"qcs::tcr:ap-guangzhou:*:repo/team-01/repo-demo/*"
			],
			"effect": "allow"
		},
		{
			"action": [
				"tcr:Describe*"
			],
			"resource": [
				"qcs::tcr:ap-guangzhou:*:repo/team-01/*"
			],
			"effect": "allow"
		}
	]
}
```
