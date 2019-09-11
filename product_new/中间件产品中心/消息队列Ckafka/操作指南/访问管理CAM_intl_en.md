
## Basic Concepts in CAM
The root account authorizes sub-accounts by binding policies. The policy setting can be accurate down to **API, Resource, User/User Group, Allow/Deny, and Condition**.

#### Account
- **Root account**: It owns all Tencent Cloud resources and can access any of its resources.
- **Sub-account**: This includes sub-users and collaborators.
 - **Sub-user**: It is created and fully owned by a root account.
 - **Collaborator**: It has the identity of a root account. After it is added as a collaborator of the current root account, it becomes one of the sub-accounts of the current root account and can switch back to its root account identity.
- **Identity credential**: It includes login credentials and access certificates. **Login credential** refers to user login name and password. **Access certificate** refers to the Cloud API keys (SecretID and SecretKey).

#### Resources and Permissions

- **Resource**: A resource is an object that is manipulated in Tencent Cloud services, such as a CVM instance, a bucket in COS, or a VPC instance.
- **Permission**: Permission is an authorization to allow or forbid certain users to perform certain operations. By default, **a root account has the full access to all the resources under it**, while **a sub-account does not have access to any resources under its root account**.
- **Policy**: Policy is the syntax rule used to define and describe one or more permissions. **A root account** performs authorization by **associating policies** with users/user groups.

[Click here to view more CAM documents >>](https://intl.cloud.tencent.com/document/product/598/10583)

## Related Documents
| Document Description | Link |
|---------|---------|
| Relationship between policy and user | [Policy Management](https://intl.cloud.tencent.com/document/product/598/10601) |
| Basic structure of policy | [Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10603) |
| More products that support CAM | [List of Tencent Cloud Products that Support CAM](https://intl.cloud.tencent.com/document/product/598/10588)|


## Sample ACL 

#### Full Read/Write Permission Policy for CKafka
Grants a sub-user full permission to manage the CKafka service (creating, managing, etc.).
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

You can also do so by setting the [full read/write policy](https://console.cloud.tencent.com/cam/policy/createV2) for the system.
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview). 
2. On the left sidebar, click **[Policy](https://console.cloud.tencent.com/cam/policy)**.
3. In the policy list, click **Create a Custom Policy**.
4. Select **Create by Policy Syntax** in the pop-up window.
5. In the Template Type field, search for "CKafka", select **QcloudCKafkaFullAccess** (for full read/write permission in CKafka), and click **Next**.
6. Click **Create a Policy**.



### Read-Only Policy for a CKafka Instance
1. Create a policy by Policy Builder and grant the permission for lists and product monitoring.
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

2. Grant read-only permission of a single instance.
> The List* API does not support authentication at the resource level.

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

You can also do so by setting the [read-only policy](https://console.cloud.tencent.com/cam/policy/createV2) for the system.
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview). 
2. On the left sidebar, click **[Policy](https://console.cloud.tencent.com/cam/policy)**.
3. In the policy list, click **Create a Custom Policy**.
4. Select **Create by Policy Syntax** in the pop-up window.
5. In the Template Type field, search for "CKafka", select **QcloudCkafkaReadOnlyAccess** (for read-only permission in CKafka), and click **Next**.
6. Click **Create a Policy**.


