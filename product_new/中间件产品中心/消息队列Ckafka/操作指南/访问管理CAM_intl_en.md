
## Basic CAM Concepts
The root account authorizes sub-accounts by binding policies. The policy setting can be specific to the level of **API, Resource, User/User Group, Allow/Deny, and Condition**.

#### Accounts
- **Root account**: A root accounts owns all the resources in Tencent Cloud and can access any of these resources.
- **Sub-account**: This includes sub-users and collaborators.
 - **Sub-user**: Sub-users created and fully owned by the root account.
 - **Collaborator**: When a root account is added as the collaborator of the current root account, it becomes one of the sub-accounts of the current root account. The account can be switched from collaborator back to root account.
- **Identity credential**: Includes login credentials and access certificates. **Login credential** refers to a user’s login name and password. **Access certificate** refers to Cloud API keys (SecretID and SecretKey).

#### Resources and Permissions

- **Resource**: An object that Tencent Cloud services operate on, such as a CVM instance, a COS bucket, or a VPC instance.
- **Permission**: An authorization to allow or forbid users to perform certain operations. By default, **a root account has full access to all resources under the account**, while **a sub-account does not have access to any resources under its root account**.
- **Policy**: Syntax rule to define and describe one or more permissions. **A root account** performs authorization by **associating policies** with users/user groups.

[Click here to view more CAM documents >>](https://intl.cloud.tencent.com/document/product/598/10583)

## Related Documents
| Document Description | Link |
|---------|---------|
| Relationship between policy and user | [Policy Management](https://intl.cloud.tencent.com/document/product/598/10601) |
| Basic policy structure | [Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10603) |
| More CAM-compatible products | [List of Tencent Cloud CAM-compatible Products](https://intl.cloud.tencent.com/document/product/598/10588)|


## CAM Policy Examples 

#### Full Read/Write Permission Policy for CKafka
Granting a sub-user full permission to manage CKafka services (creating, managing, etc.).
```
{
  "version": "2.0",
  "statement": [
    {
      "action": [
            "name/ckafka:*",
            "name/monitor:GetMonitorData"
      ],
      "resource": "*",
      "effect": "allow"
    }
  ]
}
```

You can also configure the system’s [full read/write policy](https://console.cloud.tencent.com/cam/policy/createV2) to support this permission.
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview). 
2. On the left sidebar, click **[Policy](https://console.cloud.tencent.com/cam/policy)**.
3. In the policy list, click **Create Custom Policy**.
4. Select **Create by Policy Syntax** in the pop-up window.
5. In the Template Type field, search for "CKafka", select **QcloudCKafkaFullAccess** (for full read/write permission in CKafka), and click **Next**.
6. Click **Create a Policy**.



### Read-only Policy for a CKafka Instance
1. Create a policy with the Policy Generator and grant permission for lists and product monitoring.
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/ckafka:ListInstance",
                "name/monitor:GetMonitorData"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```

2. Grant read-only permission for a single instance.
> List* API does not support authentication at the resource level.

 ```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/monitor:GetMonitorData",
                "name/ckafka:Get*"
            ],
            "resource": [
                "qcs::ckafka:gz::ckafkaId/uin/$createUin/$instanceId" 
            ]
        }
    ]
}
 ```

You can also configure the system’s [read-only policy](https://console.cloud.tencent.com/cam/policy/createV2) to support this permission.
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview). 
2. On the left sidebar, click **[Policy](https://console.cloud.tencent.com/cam/policy)**.
3. In the policy list, click **Create Custom Policy**.
4. Select **Create by Policy Syntax** in the pop-up window.
5. In the Template Type field, search for "CKafka", select **QcloudCkafkaReadOnlyAccess** (for read-only permission in CKafka), and click **Next**.
6. Click **Create a Policy**.


