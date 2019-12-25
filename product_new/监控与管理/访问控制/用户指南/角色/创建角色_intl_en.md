## Introduction
This document describes how to create a role via the CAM Console or CAM APIs. After being created, the role can manage resources under the root account within the scope of permissions.
## Prerequisites
Log in to the CAM Console and go to the [Roles](https://console.cloud.tencent.com/cam/role) page.
## Directions
### Creating via the console

#### Creating a role for a Tencent Cloud root account
1. On the Roles page, click **Create Role**.
2. In the pop-up window, select **Tencent Cloud Account** as the role entity.
3. In the next page, enter the ID of the root account to which you want to grant access to your Tencent Cloud account resources. Your root account ID is entered by default.
If you want to create roles for Tencent Cloud sub-accounts, see [Assigning role policies to sub-accounts](https://intl.cloud.tencent.com/document/product/598/19422).
4. For permission configuration, select the policies you want to grant the role from the policy list.
5. Enter a name for your role, review the information, and click **Done** to complete the creation.

#### Creating a role for a Tencent Cloud service
1. On the Roles page, click **Create Role**.
2. In the pop-up window, select **Tencent Cloud Product Service** as the role entity.
To check whether a Tencent Cloud service supports using roles, see [CAM-enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).
3. Select the service you need as the role entity from the list of services that support roles.
4. For permission configuration, select the policies you want to grant the role from the policy list.
5. Enter a name for your role, review the information, and click **Done** to complete the creation.

#### Creating a role for an identity provider
1. On the Roles page, click **Create Role**.
2. In the pop-up window, select **Identity Provider** as the role entity.
**Identity Provider** refers to the identity providers you created. You can choose one from them as the role entity.
3. (Optional) You can configure whether the role is allowed to log in to the Tencent Cloud Console in the **Console Access** area. A role can access the Tencent Cloud Console programmatically by default.
4. (Optional) In the **Conditions** area, you can manage the conditions to be met before the identity provider can use the role.
> Supported conditions are listed below:
>  - saml:aud: recipient. The URL of the endpoint to which SAML assertion is submitted. The value of this key comes from the SAML Recipient field in the assertion, instead of the Audience field.
>  - saml:iss: issuer (URN). The value of this key comes from the SAML Issuer field in the assertion.
>  - saml:sub: external account ID. This is the subject of the statement, which contains a value that uniquely identifies a user within the organization. The value of this key comes from the SAML NameID field in the assertion.
>  - saml:sub_type: external user type. The value of this key comes from the Format attribute in SAML NameID field in the assertion.
5. For permission configuration, select the policies you want to grant the role from the policy list.
6. Enter a name for the role. You can enter the description of the role in **Description**.
7. Review the information and click **Done** to complete the creation.

### Creating via APIs

#### Creating a role for a Tencent Cloud account

You can create a role using CAM APIs in Tencent Cloud. Here we explain the process with a typical use case.

For example, Company A wants to outsource its OPS Engineer position to Company B. The person taking this position needs the access to all Company A’s CVM resources located in the Guangzhou region.

Company A's enterprise account CompanyExampleA (ownerUin:12345) creates a role and sets the role entity to Company B's enterprise account CompanyExampleB (ownerUin: 67890).

1. CompanyExampleA (ownerUin: 12345) calls the `CreateRole` API to create a role with `DevOpsRole` as the `roleName`. The parameter `policyDocument` (the role trust policy) is configured as follows:
```
{
	"version": "2.0",
	"statement": [
	{
		"action": "name/sts:AssumeRole",
		"effect": "allow",
		"principal": {
			"qcs": ["qcs::cam::uin/67890:root"]
		}
	}
]
}
```

2. CompanyExampleA (ownerUin: 12345) needs to add permissions to the new role.
 (1) CompanyExampleA (ownerUin: 12345) creates a new policy `DevOpsPolicy`. The policy syntax is as follows:
```
{
	"version": "2.0",
	"statement": [
	{
		"effect": "allow",
		"action": "cvm:*",
		"resource": "qcs::cvm:ap-guangzhou::*"
	}
]
}
```
 (2) CompanyExampleA (ownerUin: 12345) calls [AttachRolePolicy](https://intl.cloud.tencent.com/document/product/598/13889) to associate the new policy with the role `DevOpsRole`. Input parameters: policyName=DevOpsPolicy, roleName=DevOpsRole.

At this point, Company A's enterprise account CompanyExampleA (ownerUin: 12345) has created a new role and granted permissions to the role.

#### Creating a role for an identity provider

You need to create a SAML identity provider in CAM before you can create a role for it. For more information on how to create an SAML identity provider, see [Creating SAML IdP](https://intl.cloud.tencent.com/document/product/598/19381).

1. Prepare a trust policy for the role to be created.
> The fields in a trust policy are specified as follows:
>  - action: defines the API for which SAML Federation is allowed to use the role. Use `sts:AssumeRoleWithSAML`.
>  - principal: defines the identity provider that is allowed to use the role. Use `{"federated": [ IdPArn ]}` string, such as `"qcs::cam::uin/10001:saml-provider/idp_name"`.
>  - condition: defines the conditions to be met before an identity provider can use the role. ` {"StringEquals": {"SAML:aud": "https://intl.cloud.tencent.com/login/saml"}}` is used by default, specifying that only the identity providers whose SAML Federation endpoint is Tencent Cloud are allowed to use this role.

 Sample trust policy:
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

2. Prepare permission policies for the role to be created. For more information on permission policies, see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
3. Call the [cam:CreateRole](https://intl.cloud.tencent.com/document/api/598/13886) API to create a role for the identity provider.




