Before implementing the OpenID Connect (OIDC)-based role-based single sign-on (SSO), you need to create an identity provider (IdP) and create a role for it in the Tencent Cloud console, and then use the OIDC token issued by the IdP to obtain the Tencent Cloud STS token (the role’s temporary key).

## Creating an OIDC IdP

1. On the left sidebar in the CAM console, select **Identity Providers** > **Role-Based SSO**.
2. On the **Role-Based SSO** page, click **Create IdP**.
3. On the page you enter, select “OIDC” as the IdP type and enter the following IdP information:
	○ **IdP Name**: The custom IdP name that is unique under a Tencent Cloud account.
	○ **IdP URL**: The OIDC IdP identifier provided by an external IdP. It must be a standard URL that starts with “http”.
	○ **Client ID**: The client ID registered in the OIDC IdP. You can configure multiple client IDs if multiple applications need to access Tencent Cloud.
	○ **Public Key for Signature**: The public key used to verify the signature of the OIDC IdP ID token. It corresponds to the value of the `jwks_uri` field in the OIDC metadata document. Please open the URL in your browser to obtain the public key. We suggest you rotate it timely.
	○ **Remarks**: Remarks for the IdP.
4. Click **Next** to enter the information review page.
5. Confirm the information you entered and click **Complete** to save it.


## Creating a role for the IdP
1. On the left sidebar in the CAM console, click **Roles**.
2. On the role management page, click **Create Role**.
3. Select **IdPs** as the role entity.
4. On the page you enter, select “OIDC” as the IdP type.
5. Select an IdP you created.
6. Set conditions for the role:
	○ **oidc:iss**: The OIDC issuer, which is required. The conditional operator must be `string_equal`, and the value must be the IdP URL you entered for the selected OIDC IdP. The role can be assumed only if the value of the `iss` field in the OIDC token meets this condition.
	○ **oidc:aud**： The OIDC audience, which is required. The conditional operator must be `string_equal`, and the value(s) must be the client ID(s) you configured for the selected IdP. The role can be assumed only if the value of the `aud` field in the OIDC token meets this condition.
	○ **oidc:sub**: The OIDC subject, which is optional. The conditional operator can be a string of all types, and you can specify up to 10 values for this condition. The role can be assumed only if the value of the `sub` field in the OIDC token meets this condition.
7. Click **Next**.
8. On the page you enter, associate permissions policies with the role and click *Next**.
9. On the review page, enter the role name and role description (optional) and click **Complete** to save the above configurations.

## Obtaining the OIDC token issued by the IdP
You cannot log in to the Tencent Cloud console using OIDC. Instead, you must implement OIDC-based SSO through programmatic access, that is, you need to call an API to obtain the temporary key and use the temporary key to access Tencent Cloud. As the OIDC token generation process is essentially based on OAuth, you need to use OAuth 2.0 to obtain the OIDC token from an OIDC IdP such as Okta. For more information, see the IdP-related documentation.

## Using the OIDC token to obtain the STS token
After you get the OIDC token from the IdP, you can directly call the `[AssumeRoleWithWebIdentity](https://intl.cloud.tencent.com/zh/document/product/598/47141)` API to obtain the STS token to access Tencent Cloud.
Sample request:
```
POST / HTTP/1.1
Host: sts.tencentcloudapi.com
Content-Type: application/json
X-TC-Action: AssumeRoleWithWebIdentity
<Common request parameters>

{
    "DurationSeconds": "5000",
    "RoleSessionName": "test_OIDC",
    "WebIdentityToken": "eyJraWQiOiJkT**********CNOQ",
    "RoleArn": "qcs::cam::uin/798950673:roleName/OneLogin-Role",
    "ProviderId": "OIDC"
}
```
Sample response:
```
{
  "Response": {
    "ExpiredTime": 1543914376,
    "Expiration": "2018-12-04T09:06:16Z",
    "Credentials": {
      "Token": "1siMD5r0tPAq9xpR******6a1ad76f09a0069002923def8aFw7tUMd2nH",
      "TmpSecretId": "AKID65zyIP0mp****qt2SlWIQVMn1umNH58",
      "TmpSecretKey": "q95K84wrzuE****y39zg52boxvp71yoh"
    },
    "RequestId": "f6e7cbcb-add1-47bd-9097-d08cf8f3a919"
  }
}
```
## Using the STS token to access Tencent Cloud resources
You can now use the STS token you obtained in the above steps to access Tencent Cloud resources for which you have permissions.

