You can use roles with CAM APIs in Tencent Cloud. The following example shows how to use roles with APIs.

For example,  Company A wants to outsource its OPS Engineer position to Company B. The person who works on this position at Company B requires full access to all resources in Company A's CVM located in Guangzhou.

Company A's enterprise account CompanyExampleA (ownerUin: 12345) creates a role and sets Company B's enterprise account CompanyExampleB (ownerUin: 67890) as the role entity. CompanyExampleA then calls the API CreateRole to create a role named DevOpsRole and gives permissions to DevOpsRole. For more information, see [Creating a role using API](https://intl.cloud.tencent.com/document/product/598/19381#.E9.80.9A.E8.BF.87-api-.E5.88.9B.E5.BB.BA).

After being granted the role, CompanyExampleB wants its sub-account DevB to do this job. So CompanyExampleB authorizes DevB to assume DevOpsRole which is owned by CompanyExampleA. For more information, see [Assigning Role Policy to a Sub-Account](https://intl.cloud.tencent.com/document/product/598/19422).

After creating the role, granting permissions to the role and assigning the role assuming policy to the sub-account, sub-account DevB can use the role.

1. Call the API [AssumeRole](https://intl.cloud.tencent.com/document/product/598/13895) to apply for temporary credentials for the role DevOpsRole. Input parameters are as follows: 
```
roleArn=qcs::cam::uin/12345:roleName/DevOpsRole,
roleSessionName=DevBAssumeTheRole,
durationSeconds=7200
```
2. The API is successfully called and the following result is returned: 
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
3. After roleDevB gets the role temporary credentials, it now can perform operations within the scope of its permissions during the validity period of the temporary credentials . For example, roleDevB is allowed to view the CVM list via API, replace the values of SecretId and SecretKey with the values of tmpSecretId and tmpSecretKey when calling the API [DescribeInstances](https://intl.cloud.tencent.com/document/product/213/15728), and set the Token in [Common Parameters](https://intl.cloud.tencent.com/document/api/213/15692) to the value of sessionToken. CompanyExampleB can also apply for the role's temporary credentials to work with CompanyExampleA's resources.
>**Note:**
>If CompanyExampleA wants to terminate the authorization to CompanyExampleB, it can delete the role DevOpsRole.


