You can create a role via the CAM console or by using the CAM API. The procedures vary, depending on whether you are creating the role for Tencent Cloud accounts, Tencent Cloud services or identity providers.

## Creating a Role via Console

### Creating a role for Tencent Cloud primary account
1. Log in to the CAM console and go to the [Role Management](https://intl.cloud.tencent.com/login.tencent.com/cam/role).
2. Click **Create Role** and go to **Select Role Entity**, and then select **Tencent Cloud Account**.
3. In the **Account ID** box, enter the ID of the primary account that you allow to assume a role to access your Tencent Cloud resources. Enter your primary account ID by default.
If you want to grant roles to other Tencent Cloud sub-accounts, see [Assigning Role Assuming Policy to a Sub-User](https://intl.cloud.tencent.com/document/product/598/19422).
4. For permission configuration, select the policy you want to assign to the role in the policy list.
5. Create a name for your role, review and click **Done**.

### Creating a role for a Tencent Cloud product service
1. Log in to the CAM console and go to the [Role Management](https://intl.cloud.tencent.com/login.tencent.com/cam/role).
2. Click **Create Role** and go to **Select Role Entity**, and then select **Tencent Cloud Product Service**.
To find out which Tencent Cloud product services support roles, see [Cloud Services Supporting CAM](https://intl.cloud.tencent.com/document/product/598/10588).
3. Select the service you need as the role entity in the list of services that support roles.
4. In the policy list, select the policy you want to assign to the role to configure the policy for the role.
5. Enter the role name, review the information of the role to be created, and then click **Done** to create a custom role.

### Creating a role for an identity provider
1. Log in to the CAM console to go to the [Role Management](https://intl.cloud.tencent.com/login.tencent.com/cam/role) page.
2. Click **Create Role** to go to **Select Role Entity**, and then select **Identity Providers**.
**Identity Providers** refer to the identity providers you have created successfully, from which you can select the identity provider for which you want to create a role.
3. (Optional) You can configure whether the role is allowed to log in to the Tencent Cloud Console. A role can access the Tencent Cloud Console programmatically by default.
4. (Optional) In **Conditions**, you can manage the conditions to be met before the identity provider can use the role.
> Supported conditions are listed as below:
>  - saml:aud: Recipient. The URL of the terminal to which SAML assertion is submitted. The value of this key comes from the SAML Recipient field in the assertion, instead of the Audience field.
>  - saml:iss: Sender (URN). The value of this key comes from the SAML Issuer field in the assertion.
>  - saml:sub: External account ID. This is the subject of the statement, which contains a value that uniquely identifies a user within the organization. The value of this key comes from the SAML NameID field in the assertion.
>  - saml:sub_type: Type of external user. The value of this key comes from the Format attribute in SAML NameID field in the assertion.
5. In the policy list, select the policy you want to assign to the role to configure the permission for the role.
6. Enter the custom role name. You can enter the remarks for the role in **Remarks**.
7. Review the information of the role to be created, and then click **Done** to create a custom role.

## Creating a role using API

### Creating a role for Tencent Cloud account

You can create a role using a CAM API in Tencent Cloud. The following example shows how to quickly create roles using API.

For example,  Company A wants to outsource its OPS Engineer position to Company B. The person who works on this position at Company B requires full access to all resources in Company A's CVM located in Guangzhou.


Company A's enterprise account CompanyExampleA (ownerUin:12345) creates a role and sets the role entity to Company B's enterprise account CompanyExampleB (ownerUin: 67890).

1. CompanyExampleA (ownerUin: 12345) calls the API CreateRole to create a role with DevOpsRole as the roleName. The parameter policyDocument (role's trust policy) is configured as below.
```
{
	"version": "2.0",
	"statement": [{
		"action": "name/sts:AssumeRole",
		"effect": "allow",
		"principal": {
			"qcs": ["qcs::cam::uin/67890:root"]
		}
	}]
}
```

2. CompanyExampleA (ownerUin: 12345) needs to add permissions for the created role.
 (1). CompanyExampleA (ownerUin: 12345) creates the policy DevOpsPolicy. The policy syntax is as below.
```
{
	"version": "2.0",
	"statement": [{
		"effect": "allow",
		"action": "cvm:*",
		"resource": "qcs::cvm:ap-guangzhou::*"
	}]
}
```
 (2) CompanyExampleA (ownerUin: 12345) calls [AttachRolePolicy](https://intl.cloud.tencent.com/document/product/598/13889) to bind the policy created in Step 1 to the role DevOpsRole. Input parameters: policyName=DevOpsPolicy and roleName=DevOpsRole.

Now, Company A's enterprise account CompanyExampleA (ownerUin: 12345) has created the role and granted permissions to the role.

### Creating a role for an identity provider

You need to create an SAML identity provider in CAM before you can create a role for the identity provider. For more information about how to create an SAML identity provider, see [Creating an SAML Identity Provider]().

1. Prepare a trust policy for the role to be created.
> The fields in a trust policy are specified as below:
>  - action: Defines the API for which SAML Federation is allowed to use the role. `sts:AssumeRoleWithSAML` is used.
>  - principal: Defines the identity provider that is allowed to use the role. `{"federated": [ IdPArn ]}` string is used, for example, qcs::cam::uin/10001:saml-provider/idp_name.
>  - condition: Defines the condition to be met to use the role. ` {"StringEquals": {"SAML:aud": "https://intl.cloud.tencent.com/login/saml"}}` is used by default. Based on this condition, only the identity providers whose SAML Federation terminal is Tencent Cloud are allowed to use this role.

 Example of a role's trust policy:
```
{
  "version": "2.0",
  "statement": [
    {
      "action": "name/sts:AssumeRoleWithSAML",
      "effect": "allow",
      "principal": {
        "federated": [
          "qcs::cam::uin/10001:saml-provider/idp_name"
        ]
      },
      "condition": {
        "string_equal": {
          "saml:aud": "https://intl.cloud.tencent.com/login/saml"
        }
      }
    }
  ]
}
```

2. Prepare the permission policy for the role to be created. For more information about permission policy, see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
3. Call the API [cam:CreateRole](https://intl.cloud.tencent.com/document/api/598/13886) to create a role for the identity provider.





