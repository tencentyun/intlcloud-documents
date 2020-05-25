When a Tencent Cloud user accesses Tencent Cloud resources, CAM determines whether to allow or deny the request by using the following evaluation logic:
![](https://mc.qcloudimg.com/static/img/9f6a095cb693996d0653b488e67d1234/CAM-User+Guide-Policy+Syntax-Evalution+Logic.png)    
1. All requests will be denied by default.
    
2. CAM will check all the policies currently associated with the user.
 1. It will determine whether any policies match, and if so, it will proceed to the next step. If not, the final result is "deny", and access to Tencent Cloud resources is not permitted.
 2. It will determine whether any "deny" policies match, and if so, the final result will be "deny", and access to Tencent Cloud resources is not permitted. If not, it will proceed to the next step.
 3. It will determine whether any "allow" policies match, and if so, the final result will be "allow", and access to Tencent Cloud resources will be permitted. If not, the final result is "deny", and access to Tencent Cloud resources is not permitted.
    
> **Note:**
- A root account has full access to all resources it owns by default. At present, cross-account resource access is only supported for COS.
- There are some general policies that are associated with all CAM users by default. For more information, please see the [General Policy Table](https://intl.cloud.tencent.com/document/product/598/10605) below.
- Other policies need to be explicitly specified. This applies to both `allow` and `deny` policies.
- For services that support cross-account resource access, permission propagation applies. For example, if root account A grants a sub-account under root account B access to its resources, CAM will verify whether root account A has granted root account B access and whether root account B has granted the sub-account access. Both must be true for the sub-account of root account B to be allowed to access root account A's resources.

<span id="dsa"></span>
The following table lists currently supported general policies:

| Policy Description | Policy Definition |
|---|---|
| MFA verification is required for querying keys |{<br>"principal":"*",<br>"action":"account:QueryKeyBySecretId",<br>"resource":"*",<br>"condition":{"string_equal":{"mfa":"0"}}<br>}|
| MFA verification is required for sensitive configurations |{<br>"principal":"*",<br>"action":"account:SetSafeAuthFlag",<br>"resource":"*",<br>"condition":{"string_equal":{"mfa":"0"}}<br>}|
| MFA verification is required for binding tokens |{<br>"principal":"*",<br>"action":"account:BindToken",<br>"resource":"*",<br>"condition":{"string_equal":{"mfa":"0"}}<br>}|
| MFA verification is required for unbinding tokens |{<br>"principal":"*",<br>"action":"account:UnbindToken",<br>"resource":"*",<br>"condition":{"string_equal":{"mfa":"0"}}<br>}|
| MFA verification is required for modifying email addresses |{<br>"principal":"*",<br>"action":"account:ModifyMail",<br>"resource":"*",<br>"condition":{"string_equal":{"mfa":"0"}}<br>}|
| MFA verification is required for modifying mobile numbers |{<br>"principal":"*",<br>"action":"account:ModifyPhoneNum",<br>"resource":"*",<br>"condition":{"string_equal":{"mfa":"0"}}<br>}|
