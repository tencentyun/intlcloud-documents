## Overview

Tencent Cloud Security Token Service (STS) is a set of Web services for managing temporary access rights. You can use STS to create temporary security credentials for accessing Tencent Cloud resources and provide the credentials to a trusted user who can manage Tencent Cloud resources within the scope of the obtained privileges.

## Use Cases

### SAML 2.0-based federated identity 

You can create a federated identity for external users and grant them access to Tencent Cloud resources. If you have your own system and your users need access to Tencent Cloud resources, you can use the Identity Provider (IdP) function in CAM, in which you can assign Tencent Cloud access to users certified by IdP. For more details, see [Accessing Tencent Cloud Console as SAML 2.0 Federated Users](https://intl.cloud.tencent.com/document/product/598/32672).

### Cross-account access role

If you have more than one account, you can create an identity and use it to access all the resources in your accounts. For more details, see [Using Role](https://intl.cloud.tencent.com/document/product/598/19419).
