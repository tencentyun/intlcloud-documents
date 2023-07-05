## Policy Configuration in Typical Scenarios
>!The following scenario policies are only used for TCR Individual use cases.
>
- Grant a sub-account the full read/write permissions for all resources in TCR Individual.
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
- Grant a sub-account the read-only permission for all resources in TCR Individual (former Image Repositories in TKE).
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
- Grant a sub-account permissions to manage the specific namespace in the specific region. For example, the namespace `team-01` in the default region.
```
{
	"version": "2.0",
	"statement": [{
			"action": [
				"tcr:*"
			],
			"resource": [
				"qcs::tcr:::repo/team-01",
				"qcs::tcr:::repo/team-01/*"
			],
			"effect": "allow"
		}
	]
}
```
- Grant a sub-account the read-only permission for an image repository, which means that the sub-account can only pull the images in the image repository instead of deleting the repository, modifying repository attributes, or pushing images. For example, the image repository `repo-demo` in the namespace `team-01` in the default region.
```
{
	"version": "2.0",
	"statement": [{
			"action": [
				"tcr:Describe*",
				"tcr:PullRepositoryPersonal"
			],
			"resource": [
				"qcs::tcr:::repo/team-01",
				"qcs::tcr:::repo/team-01/repo-demo",
				"qcs::tcr:::repo/team-01/repo-demo/*"
			],
			"effect": "allow"
		}
	]
}
```

