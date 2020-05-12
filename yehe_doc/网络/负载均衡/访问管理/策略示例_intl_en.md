## Full Access Policy in CLB
- Grant a sub-account full access to the CLB service (creating, managing, etc.).
- Policy name: CLBResourceFullAccess
```
{
	"version": "2.0",
	"statement": [{
		"action": [
			"name/clb:*"
		],
		"resource": "*",
		"effect": "allow"
	}]
}
```

## Read-Only Policy in CLB
- Grant a sub-account read-only access to CLB (i.e., the permission to view but not to create, update, or delete all CLB resources). In the console, the prerequisite to manipulate a resource is the ability to view the resource; therefore, you are recommended to grant the sub-account full read access to CLB.
- Policy name: CLBResourceReadOnlyAccess
```
{
	"version": "2.0",
	"statement": [{
		"action": [
			"name/clb:Describe*"
		],
		"resource": "*",
		"effect": "allow"
	}]
}
```
