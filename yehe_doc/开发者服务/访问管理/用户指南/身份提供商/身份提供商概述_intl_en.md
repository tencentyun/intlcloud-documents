If you already have an account system for your organization, you can use the Identity Provider (IdP) feature to allow your organization members to access Tencent Cloud resources. This eliminates the need to create a CAM sub-user for each organization member. With IdP, you can also manage non-Tencent Cloud identities and grant them permissions to access your Tencent Cloud resources whenever needed.

A known IdP can verify external identities on your behalf, so there is no need to implement custom login code or authentication. Users with authenticated external identities can use a role to log in to Tencent Cloud. You can grant the IdP role permissions to use your Tencent Cloud resources within the limited authorization range. External users log in to Tencent Cloud by using roles and roles use temporary keys, which helps prevent security problems caused by persistent keys (such as TencentCloud API keys), because such keys makes key rotation difficult and may result in credential leakage.

## Use Cases

If you already have an account and user system for your organization, you can use the IdP feature of CAM to allow your users to access Tencent Cloud resources. This eliminates the need to create a CAM sub-user for each organization user. With the IdP feature, you can manage non-Tencent Cloud users and use the role feature to specify permissions to access Tencent Cloud resources for users whose identities are federated from an IdP.

## Features

- **No need to create Tencent Cloud accounts**
You don't need to create a Tencent Cloud account for each member in your organization, which helps avoid security issues caused by leakage of persistent access credentials (such as TencentCloud API keys) assigned to users.
- **Federated single sign-on (SSO)**
If you already have your own organizational authentication system, you can easily implement federated SSO by leveraging an IdP.
- **Simplified login authentication process**
With login codes provided by IdPs, identity federation with Tencent Cloud for enterprise customers is made simple and cost-effective.



