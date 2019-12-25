If you already have an account system for your organization, you can use the Identity Provider (IdP) to allow your organization members to access Tencent Cloud resources. This removes the need of creating a CAM sub-user for each organization member. With an identity provider, you can also manage your non-Tencent Cloud identities. You can grant those identities permissions to access your Tencent Cloud resources whenever needed.

A known IdP can verify external identities on your behalf, so there's no need for additional login authentication. Users with authenticated external identities can use a role to log in to Tencent Cloud. You can grant the IdP roles permissions to fully access your Tencent Cloud resources. These roles that external identities assume will have limited access dependent on the scope of permissions assigned. External users log in to Tencent Cloud using roles and roles use temporary keys, thus helping prevent security problems caused by persistent keys (such as cloud API keys). Persistent keys makes key rotation difficult and may result in credential leakage.

## Application Scenarios

If your users already have non-Tencent Cloud identities and need access to Tencent Cloud resources, you can use the Tencent CAM Identity Provider feature instead of creating CAM sub-users in your Tencent Cloud account. With the IdP feature, you can manage non-Tencent Cloud users, and use the role feature to specify permissions to access Tencent Cloud resources for users whose identities are federated from an Identity Provider (IdP).

## Features

- **No need to create Tencent Cloud accounts**
Enterprise customers do not need to create a Tencent Cloud account for each member, which can avoid security issues caused by leakage of long-term access credentials (such as cloud API keys) assigned to users.
- **Federated single sign-on (SSO)**
When enterprise customers already have its own authentication system, they are able to federate their user identities with IdPs (SSO)
- **Simplified login authentication process**
With log-in codes provided by IdPs, identity federation with Tencent Cloud for enterprise customers is simple and cost effective.



