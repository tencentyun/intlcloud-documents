A primary account, as the role entity, allows its sub-accounts to assume roles. The following example provides an easy view of how to create and assign a role-assumption policy for sub-accounts.

Assuming Company A has an OPS Engineer position and wants to outsource the position to Company B. The person assuming this position is required to work with all the CVM resources of Company A in Guangzhou.

Company A's enterprise account CompanyExampleA (ownerUin: 12345) creates a role and sets Company B's enterprise account CompanyExampleB (ownerUin is 67890) as the role entity. CompanyExampleA calls the CreateRole API to create a role named DevOpsRole. CompanyExampleA adds permissions for the created role DevOpsRole. See [Create a role using API](https://cloud.tencent.com/document/product/598/19381#.E9.80.9A.E8.BF.87-api-.E5.88.9B.E5.BB.BA) for how to proceed with these steps.

After being granted the role, Company B's enterprise account (CompanyExampleB) wants its sub-account DevB to perform the job. CompanyExampleB needs to authorize DevB to assume the DevOpsRole role of CompanyExampleA.

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
2. Authorize the policy to the sub-account DevB. The sub-account is now assigned the permission to assume the DevOpsRole role.

For how to use a role after the permission to assume it is assigned, see [Use Roles](https://cloud.tencent.com/document/product/598/19419).


