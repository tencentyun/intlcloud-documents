When you already have an account system for your organization, you can use the Identity Provider (IdP), instead of creating a CAM sub-user for each member, to allow your organization members to access Tencent Cloud resources. With an identity provider, you can also manage your non-Tencent Cloud identities, whom you can grant permissions to access your Tencent Cloud resources whenever needed.

A known IdP can verify external identities on your behalf, so there's no extra login authentification needed. Users with authenticated external identities can use a role to log in to Tencent Cloud. You can grant the IdP roles permissions to fully access your Tencent Cloud resources, while roles that external identities assume will have limited access according to the permissions that are assigned to them. Because external users log in to Tencent Cloud using roles and roles use temporary keys, this can help prevent security problems caused by long-term access credentials (such as cloud API keys) leakage.

## Application Scenarios

If your users already have non-Tencent Cloud identities and need access to Tencent Cloud resources, you can use the Tencent CAM Identity Provider feature rather than creating CAM sub-users in your Tencent Cloud account for these users. With this feature, you can manage non-Tencent Cloud users, and use the role feature to specify permissions to access Tencent Cloud resources for users whose identity is federated from an Identity Provider (IdP).

## Features

- **No need to create Tencent Cloud accounts**
Enterprise customers do not need to create a Tencent Cloud account for each member, which can avoid security problems caused by leakage of long-term access credentials (such cloud API keys) assigned to users.
- **Federated single sign-on (SSO)**
When enterprise customers already have its own authentication system, they are able to federate their user identities with IdPs (SSO)
- **Simplified login authentication**
With log-in codes provided by IdPs, enterprise customers can simplify the identity federation with Tencent Cloud at a low cost.

