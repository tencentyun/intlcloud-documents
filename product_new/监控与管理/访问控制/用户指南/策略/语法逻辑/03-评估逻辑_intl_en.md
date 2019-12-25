When a Tencent Cloud user accesses cloud resources, CAM determines whether to allow or deny the request by using the following evaluation logic.
![](https://mc.qcloudimg.com/static/img/b2bd42353bee28c55cc1bb1c3e8bb35d/395.png)    
1. All requests are denied by default.
    
2. CAM checks all policies currently associated the user.
 1. It determines whether any policies match. If yes, it proceeds to the next step. If no, the final result is "deny", and access to cloud resources is not permitted.
 2. It determines whether any "deny" policies match. If yes, the final result is "deny", and access to cloud resources is not permitted. If no, proceed to the next step.
 3. It determines whether any "allow" policies match. If yes, the final result is "allow", and access to cloud resources is permitted. If no, the final result is "deny", and access to cloud resources is not permitted.
    
> **Notes:**
- Root accounts have full access permissions for all owned resources by default. At present, cross-account resource access is only supported for COS/CAS products.
- There are several general policies that are associated with all CAM users by default. For specific details, see the **General Policy Table** below.
- Other policies need to be explicitly specified. This applies for both `allow` and `deny` policies.
- For services that support cross-account resource access, permission propagation applies. For example, root account A grants a sub-account under root account B access permissions to its resources. CAM will verify whether root account A has granted root account B access permission, and whether root account B has granted the sub-account access permission. Both must be true for the sub-account of root account B to be allowed to access root account A’s resources.

<span id="dsa"></span>
The following table contains general policies that are presently supported:

| Policy Description | Policy Definition |
|---|---|
| MFA verification is required for querying keys |{<br>"principal":"*",<br>"action":"account:QueryKeyBySecretId",<br>"resource":"*",<br>"condition":{"string_equal":{"mfa":"0"}}<br>}|
| MFA verification is required for sensitive configurations |{<br>"principal":"*",<br>"action":"account:SetSafeAuthFlag",<br>"resource":"*",<br>"condition":{"string_equal":{"mfa":"0"}}<br>}|
| MFA verification is required for binding tokens |{<br>"principal":"*",<br>"action":"account:BindToken",<br>"resource":"*",<br>"condition":{"string_equal":{"mfa":"0"}}<br>}|
| MFA verification is required for unbinding tokens |{<br>"principal":"*",<br>"action":"account:UnbindToken",<br>"resource":"*",<br>"condition":{"string_equal":{"mfa":"0"}}<br>}|
| MFA verification is required for modifying email addresses |{<br>"principal":"*",<br>"action":"account:ModifyMail",<br>"resource":"*",<br>"condition":{"string_equal":{"mfa":"0"}}<br>}|
| MFA verification is required for modifying mobile phone numbers |{<br>"principal":"*",<br>"action":"account:ModifyPhoneNum",<br>"resource":"*",<br>"condition":{"string_equal":{"mfa":"0"}}<br>}|
