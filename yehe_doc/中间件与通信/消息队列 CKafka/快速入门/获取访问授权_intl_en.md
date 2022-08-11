## Basic CAM Concepts

A root account authorizes sub-accounts by binding policies. The policy settings can be specific to the level of **API, Resource, User/User Group, Allow/Deny, and Condition**.

#### Account

- **Root account**: It owns all Tencent Cloud resources and can access any of its resources.
- **Sub-account**: It includes sub-users and collaborators.
    - **Sub-user**: It is created and fully owned by a root account.
    - **Collaborator**: It has the identity of a root account. After it is added as a collaborator of the current root account, it becomes one of the sub-accounts of the current root account and can switch back to its root account identity.
- **Identity credential**: It includes login credentials and access certificates. **Login credential** refers to a user's login name and password. **Access certificate** refers to Tencent Cloud API keys (`SecretId` and `SecretKey`).

#### Resource and permission

- **Resource**: An object that is operated in Tencent Cloud services, such as a CVM instance, a COS bucket, or a VPC instance.
- **Permission**: It is an authorization that allows or forbids users to perform certain operations. By default, **a root account has full access to all resources under it**, while **a sub-account does not have access to any resources under its root account**.
- **Policy**: It is a syntax rule that defines and describes one or more permissions. The **root account** performs authorization by **associating policies** with users/user groups.

## Using CKafka with Sub-Account

A sub-account needs to be authorized in the following two aspects before it can use CKafka:

1. CKafka needs to get permissions to access other Tencent Cloud service resources, such as viewing VPCs and tags. Therefore, a role (and its permission policy) should be passed to the CKafka service by associating the `ckafka_PassRole` policy with the sub-account. For detailed directions, see [Step 1. Grant the `ckafka_PassRole` policy](#step1). For details of use cases of the policy, see [Appendix](#msg).
2. For the sub-account to use CKafka, the root account needs to grant it the **full access** or **permissions of specified resources**. Based on your business needs, you can choose the scope of permissions to be granted. For detailed directions, see [Step 2. Grant full access or the permissions of specified resources](#step2).


[](id:step1)
### Step 1. Grant the `ckafka_PassRole` policy

#### Creating `ckafka_PassRole` policy
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) as the root account.
2. On the left sidebar, click **Policies** to enter the policy management page.
3. Click **Create Custom Policy**.
4. In the **Select Policy Creation Method** pop-up window, select **Create by Policy Generator** to enter the **Create by Policy Generator** page.
5. Enter the services, operations, resources, and other information in the policy as needed. You can refer to the figure below to generate the `ckafka_PassRole` policy. Then, click **Next**.
6. Enter the policy name `ckafka_PassRole`, associate it with the target **user**, **user group** or **role**, and click **Complete**.


[](id:step2)
### Step 2. Grant full access or the permissions of specified resources
<dx-tabs>
::: Full access

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) as the root account.
2. On the left sidebar, click **Policies** to enter the policy management page.
3. Search for `QcloudCKafkaFullAccess` on the right. 
4. In the search results, click the **Associated Users/Groups** of `QcloudCKafkaFullAccess` and select the sub-account to be authorized.

:::
::: Permissions of specified resources

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka/) and find the CKafka instance resource that needs to be authorized.
2. Get the ID of the instance.
3. Log in to the [CAM console](https://console.cloud.tencent.com/cam) and click **Policies** on the left sidebar to enter the policy management list page.
4. Click **Create Custom Policy**. In the **Select Policy Creation Method** pop-up window, select **Create by Policy Generator** to enter the **Create by Policy Generator** page.
5. Enter the services, operations, resources, and other information in the policy as needed. Then, click **Add a six-segment resource description**.
6. Enter the ID of the specified instance in the six-segment resource description.
7. Click **Next**, specify users or user groups for the policy, and click **Complete**.
:::
</dx-tabs>

[](id:msg)
## Appendix

Using CKafka involves calling the following Tencent Cloud services. The root account needs to authorize sub-accounts separately for them to use CKafka features.

| Tencent Cloud Service | Operations Involved in CKafka |
| ----------------|---------------------|
| VPC  | Select the access VPC when creating an instance |
| Tag     | Select the tag when creating an instance      |



