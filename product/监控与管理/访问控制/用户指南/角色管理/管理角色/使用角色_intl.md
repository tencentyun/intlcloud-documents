You can use roles with CAM APIs in Tencent Cloud. The following example shows how to use roles with APIs.

Assuming Company A has an OPS Engineer position and wants to outsource the position to Company B. The person assuming this position is required to work with all the CVM resources of Company A in Guangzhou.

Company A's enterprise account CompanyExampleA (ownerUin: 12345) creates a role and sets Company B's enterprise account CompanyExampleB (ownerUin: 67890) as the role entity. CompanyExampleA calls the API CreateRole to create a role named DevOpsRole (roleName). CompanyExampleA adds permissions for the created role DevOpsRole. For more information, see [Creating a role using API](https://cloud.tencent.com/document/product/598/19381#.E9.80.9A.E8.BF.87-api-.E5.88.9B.E5.BB.BA).

After being granted the role, CompanyExampleB wants its sub-account DevB to do this job. CompanyExampleB authorizes DevB to apply for the role DevOpsRole of CompanyExampleA. For more information, see [Assigning Role Policy to a Sub-Account](https://cloud.tencent.com/document/product/598/19422).

After creating the role, granting permissions to the role and assigning the role assuming policy to the sub-account, sub-account DevB can use the role.

1. Call the API [AssumeRole](https://cloud.tencent.com/document/product/598/13895) to apply for temporary credentials for the role DevOpsRole. Input parameters are as follows: 
```
roleArn=qcs::cam::uin/12345:roleName/DevOpsRole,
roleSessionName=DevBAssumeTheRole,
durationSeconds=7200
```
2. The API is called successfully and returns the following result: 
```
{
	"credentials": {
		"sessionToken": "5e776c4216ff4d31a7c74fe194a978a3ff2a42864",
		"tmpSecretId": "AKIDcAZnqgar9ByWq6m7ucIn8LNEuY2MkPCl",
		"tmpSecretKey": "VpxrX0IMCpHXWL0Wr3KQNCqJix1uhMqD"
	},
	"expiredTime": 1506433269,
	"expiration": "2018-09-26T13:41:09Z"
}
```
3. DevB can perform operations allowed by its permissions within the validity period of the temporary credentials after obtaining the temporary credentials of the role. For example, to view the CVM list via API, replace the values of SecretId and SecretKey with the values of tmpSecretId and tmpSecretKey when calling the API [DescribeInstances](https://cloud.tencent.com/document/product/213/15728), and set the Token in [Common Parameters](https://cloud.tencent.com/document/api/213/15692) to the value of sessionToken. CompanyExampleB can also apply for the role's temporary credentials to work with CompanyExampleA's resources.
>**Note:**
>If CompanyExampleA wants to terminate the authorization to CompanyExampleB, it can delete the role DevOpsRole.


