The primary account allows its sub-account to assume roles. The following example shows how to create and assign policies to the roles

For example,  Company A wants to outsource its OPS Engineer position to Company B. The person who works on this position at Company B requires full access to all resources in Company A's CVM located in Guangzhou.

We assume that company A has an enterprise account 'CompanyExampleA' (ownerUin: 12345) while creating a role in Company B's enterprise account 'CompanyExampleB' (ownerUin is 67890).  Account 'CompanyExampleA' then calls the 'CreateRole' API to create and sets permissions to a role named 'DevOpsRole'. See [Create a role using API](https://cloud.tencent.com/document/product/598/19381#.E9.80.9A.E8.BF.87-api-.E5.88.9B.E5.BB.BA) to learn more about how to proceed with these steps.

After being granted the role, Company B's enterprise account (CompanyExampleB) wants its sub-account 'DevB' to perform the job. 'CompanyExampleB' needs to authorize 'DevB' to assume the 'DevOpsRole', which is a role CompanyExampleA.

1. Create a policy AssumeRole as shown below:
```
{
	"version": "2.0",
	"statement": [{
		"effect": "allow",
		"action": ["name/sts:AssumeRole"],
		"resource": ["qcs::cam::uin/12345:roleName/DevOpsRole"]
	}]
}
```
2. Authorize the policy to the sub-account 'DevB'. The sub-account is now assigned the permission to assume 'DevOpsRole'.

For how to use a role after the permission to assume it is assigned, see [Use Roles](https://cloud.tencent.com/document/product/598/19419).


