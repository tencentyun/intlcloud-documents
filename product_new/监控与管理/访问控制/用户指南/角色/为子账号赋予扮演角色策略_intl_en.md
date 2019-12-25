A root account as the entity of a role can allow its sub-accounts to assume the role. The following example shows how to create and assign policies for role assumption.

For example, Company A wants to outsource its OPS Engineer position to Company B. The person taking the position needs the access to all Company A’s CVM resources located in the Guangzhou region.

Company A’s enterprise account `CompanyExampleA` (ownerUin: 12345) creates a role with the `CreateRole` API. The entity and name of the role are set to Company B's enterprise account `CompanyExampleB` (ownerUin: 67890) and `DevOpsRole` respectively. CompanyExampleA adds permissions to `DevOpsRole`. For more information, see [Creating roles > Creating via APIs](https://intl.cloud.tencent.com/document/product/598/19381).

After being granted the role, Company B's enterprise account (`CompanyExampleB`) wants its sub-account, `DevB`, to perform the job. `CompanyExampleB` needs to authorize `DevB` to assume the `DevOpsRole` role.

1. Create a policy, `AssumeRole`, as follows:
```
{
	"version": "2.0",
	"statement": [
	{
		"effect": "allow",
		"action": ["name/sts:AssumeRole"],
		"resource": ["qcs::cam::uin/12345:roleName/DevOpsRole"]
	}
	]
}
```
2. Associate the policy with the sub-account `DevB`. The sub-account is now granted permissions to assume the `DevOpsRole` role.

3. For more information on how a sub-account can use a role after being granted the permissions, see [Using roles](https://intl.cloud.tencent.com/document/product/598/19419).

