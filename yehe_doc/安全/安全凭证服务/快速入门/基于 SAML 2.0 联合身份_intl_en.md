
## Overview
Tencent Cloud supports federated authentication based on SAML 2.0 (Security Assertion Markup Language 2.0). If you already have your own account system and users, you can generate temporary security credentials for them to manage Tencent Cloud resources with limited permission, instead of creating a CAM sub-user.

## Prerequisite
You already had your own account system and users.

## How It Works
1. A user in your enterprise or organization uses a client app to request authentication from your organization's IdP.
2. The IdP authenticates the user against your enterprise's identity authorization system.
3. The user authentication result is returned.
4. The IdP generates a standard SAML 2.0 assertion document based on the user authentication result and sends it back to the client app.
5. The client passes the SAML 2.0 assertion and the resource description of the IdP and the assumed role to [sts:AssumeRoleWithSAML](https://intl.cloud.tencent.com/document/product/598/35839) for temporary credential.
6. STS verifies the SAML 2.0 assertion.
7. The verification result is returned.
8. The API constructs a temporary credential based on the result, and sends it to the client.
