### Why are there new roles in my account?
When you perform a specific operation (such as authorizing the creation of a service role) for a Tencent Cloud service, the service will send you a request for the authorization. After you indicate your consent, a service role will be automatically created and be associated with related policies.

In addition, if you have used a service before it supports service-linked roles, a role will be automatically created under your account after we notify you of this via email or other notification channels.

### Was there a change in the policy associated with the service role?
After a Tencent Cloud service is authorized to create a service role and grant permissions to it, the service feature may be upgraded. During the upgrade, the permission to call other Tencent Cloud service APIs may be added.

To ensure you can enjoy complete Tencent Cloud service features, we will associate new policies with the created service role or add new API permissions to the policy associated with the service role.
This change only applies to the Tencent Cloud services you are using and won’t affect the authorization for other sub-users.

### How can I view the RoleArn of the role?

You can go to [Roles](https://console.cloud.tencent.com/cam/role) in the CAM console, click the name of the desired role to go to the role details page, and query in the **Role Info** area.


### How many types of CAM roles are there?
There are three types of CAM roles based on different role entities:
- **Tencent Cloud service**: Authorize a Tencent Cloud service to use your cloud resources with the role.
- **Tencent Cloud account**: Authorize the root account or other root accounts to use your cloud resources with the role.
- **Identity provider**: Authorize an external user identity (such as enterprise user pool) to use your cloud resources.
