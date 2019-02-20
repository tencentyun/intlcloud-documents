If your organization already has its own account system and you want to manage the use of Tencent Cloud resources by the organization members, you can use Identity Provider (IdP) feature, rather than creating a CAM sub-user in your Tencent Cloud account for each member. With an identity provider, you can manage your non-Tencent Cloud user identities, and give these external user identities permissions to access your Tencent Cloud resources.

You don't have to create custom login code or complete login authentication, for IdP provides the authentication service. Once authenticated by a well-known identity provider, users with external identities can use a role to log in to Tencent Cloud. You can grant the IdP role permissions to access your Tencent Cloud resources, and externally authenticated users can access resources within the limited scope of the role's permissions. Since externally authenticated users log in to Tencent Cloud via a role that uses a temporary key, the problem of being difficult to rotate keys and security problems caused by data interception as a result of using long-term keys (such as cloud API keys) can be avoided.

## Application Scenarios

If your users already have non-Tencent Cloud identities and need access to Tencent Cloud resources, you can use the Tencent CAM Identity Provider feature rather than creating CAM sub-users in your Tencent Cloud account for these users. With this feature, you can manage non-Tencent Cloud users, and use the role feature to specify permissions to access Tencent Cloud resources for users whose identity is federated from an Identity Provider (IdP).

## Features

- **No need to create Tencent Cloud accounts**
Enterprise customers do not need to create a Tencent Cloud account for each member, which can avoid security problems caused by leakage of long-term access credentials (such cloud API keys) assigned to users.
- **Federated single sign-on (SSO)**
If an enterprise customer already has an authentication system, SSO can be implemented using the IdP feature.
- **Simplified login authentication process**
Since the IdP feature provides login code, enterprise customers can complete the identity federation with Tencent Cloud at a low cost, thus facilitating cloudification.




