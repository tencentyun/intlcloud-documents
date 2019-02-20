Tencent Cloud supports identity federation based on SAML 2.0 (Security Assertion Markup Language 2.0). SAML 2.0 is an open standard used by many identity providers (IdPs). IdP enables federated single sign-on (SSO), so you can authorize users that have been successfully authenticated to log in to the Tencent Cloud console or call the Tencent Cloud APIs without you having to create a CAM sub-user for everyone in your enterprise or organization. By using SAML 2.0, the generic open protocol, you can simplify the process of federated authentication in Tencent Cloud, because you can use the IdP's service instead of writing custom identity proxy code.

## SAML IdP

IdP is an entity in CAM, which can be deemed as a collection of external trusted accounts. SAML 2.0-based identity providers are the SAML 2.0-compliant IdPs. If you want to build trust between SAML 2.0 protocol-compatible IdPs (such as Microsoft Active Directory Federation Service) and Tencent Cloud for your enterprise or organization members to access Tencent Cloud resources, you need to create SAML IdPs. For more information, see [Creating IdP](https://cloud.tencent.com/document/product/598/30290).

## IdP Role

After creating an SAML IdP, you must create one or more IdP roles with the SAML IdP as the role entity. A role is a virtual identity with a group of permissions, and uses temporary security credentials to access resources. In the context of SAML 2.0 assertions, a role can be assigned to a federated user authenticated by an IdP. This role allows the IdP to request for temporary security credentials to access the Tencent Cloud resources. The policy associated with the role determines the scope of Tencent Cloud resources that can be accessed by the federated user. For more information on how to create SAML 2.0-based federated IdP roles, see [Creating Role](https://cloud.tencent.com/document/product/598/19381).
![](https://main.qcloudimg.com/raw/86f82050ccb875c96864b11561acea9a.png)

## Accessing Tencent Cloud APIs via SAML 2.0-Based Federation

![](https://main.qcloudimg.com/raw/65eb02712b75d7bfcbba509b8f10be7c.png)
1.	A user in your enterprise or organization uses a client app to request authentication from your organization's IdP.
2.	The IdP authenticates the user against your enterprise's identity authorization system .
3.	The authentication result is returned.
4.	The IdP constructs a standard SAML 2.0 assertion with the above result and sends the assertion to the client app.
5.	The client app requests for a temporary security key from sts:AssumeRoleWithSAML, passing the SAML 2.0 assertion, the resource description of IdP and the resource description of IdP role.
6.	The SAML 2.0 assertion is authenticated by STS.
7.	The authentication result is returned.
8.	The API applies for and returns a temporary credential to the client.

## Realizing Federated Single Sign-on (SSO) via SAML 2.0-Based Federation
![](https://main.qcloudimg.com/raw/10d90eb5e5f91927e873cec8dc0e5823.png)
1. A user in your enterprise or organization uses a browser to access a Tencent Cloud service.
2. The Tencent Cloud service returns an authentication request to the browser.
3. The browser redirects the authentication request to the IdP of your enterprise or organization.
4. Your enterprise authenticates the user.
5. After the user has been authenticated successfully, the user information is returned to the IdP.
6. The IdP generates a standard SAML 2.0 assertion and returns it to the browser.
7. The browser redirects the SAML 2.0 assertion to Tencent Cloud.
8. Tencent Cloud starts the Tencent Cloud SSO login service, requests cAuth, and authenticates the user.
9. The authentication result is returned from Tencent Cloud.
10. Once the user is authenticated successfully, the login status is returned.
11. The user is redirected to the Tencent Cloud console.





