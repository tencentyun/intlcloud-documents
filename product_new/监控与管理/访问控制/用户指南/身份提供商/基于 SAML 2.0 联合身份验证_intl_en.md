Tencent Cloud supports identity federation based on SAML 2.0 (Security Assertion Markup Language 2.0). SAML 2.0 is an open standard used by many identity providers (IdPs). IdP enables federated single sign-on (SSO), so you can authorize users that have been successfully authenticated to log in to the Tencent Cloud console or call the Tencent Cloud APIs without creating a CAM sub-user account for each of your members. In addition, as an open protocol, SAML 2.0 allows you use the proxy code directly instead of writing one by yourself, which has simplified federated authentication in Tencent Cloud.

## SAML IdP

IdP is an entity in CAM, which can be deemed as a collection of external trusted accounts. SAML 2.0-based identity providers are the SAML 2.0-compliant IdPs. If you want to build trust between SAML 2.0 protocol-compatible IdPs (such as Microsoft Active Directory Federation Service) and Tencent Cloud for your enterprise or organization members to access Tencent Cloud resources, you need to create SAML IdPs. For more information, see [Creating an IdP](https://intl.cloud.tencent.com/document/product/598/30391).

## IdP Role

After creating an SAML IdP, you must create one or more IdP roles with the SAML IdP as the role entity. A role is a virtual identity with a group of permissions, and uses temporary security credentials to access resources. In the context of SAML 2.0 assertions, a role can be assigned to a federated user authenticated by an IdP. This role allows the IdP to request for temporary security credentials to access the Tencent Cloud resources. The policy associated with the role determines the scope of Tencent Cloud resources that can be accessed by the federated user. For more information on how to create SAML 2.0-based federated IdP roles, see [Creating a Role](https://intl.cloud.tencent.com/document/product/598/19381).
![](https://main.qcloudimg.com/raw/b9acbbfd1f17b960a21185cd2f9c9ec6.png)

## Accessing Tencent Cloud APIs via SAML 2.0-Based Federation

![](https://main.qcloudimg.com/raw/65eb02712b75d7bfcbba509b8f10be7c.png)
1.	A user in your enterprise or organization uses a client app to request authentication from your organization's IdP.
2.	The IdP authenticates the user against your enterprise's identity authorization system.
3.	Return user authentication result
4.	The IdP generates a standard SAML 2.0 assertion document based on the user authentication result and sends it back to the client app.
5.The client app requests sts:AssumeRoleWithSAML a temporary security key based on the SAML 2.0 assertion document, the resource description of the IdP and IdP role.
6.	The SAML 2.0 assertion is authenticated by STS.
7.	Return user authentication result.
8.	The API applies for and returns a temporary credential to the client.

## Realizing Federated Single Sign-on (SSO) via SAML 2.0-Based Federation
![](https://main.qcloudimg.com/raw/10d90eb5e5f91927e873cec8dc0e5823.png)
1. A user in your enterprise or organization uses a browser to access a Tencent Cloud service.
2. The Tencent Cloud service returns an authentication request to the browser.
3. The browser redirects the authentication request to the IdP of your enterprise or organization.
4. Your enterprise authenticates the user.
5. After the user is authenticated successfully, the user information will be returned to the IdP.
6. The IdP generates a standard SAML 2.0 assertion and returns it to the browser.
7. The browser redirects the SAML 2.0 assertion to Tencent Cloud.
8. Start the Tencent Cloud SSO login, request cAuth and verify the user's identity.
9. Return to Tencent Cloud verification results.
10. The verification is successful and the login status is returned.
11. Redirect to the Tencent Cloud Console.




