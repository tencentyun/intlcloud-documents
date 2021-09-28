## Overview

This document describes how to configure SASL authentication and ACL (access control list) rules in the CKafka console to enhance access control in public/private network transfers and permission control in production and consumption of resources such as topics.

>?
>- Kafka offers various security authentication mechanisms, which mainly include SSL and SASL. SASL/PLAIN is an authentication method based on account and password and is more commonly used. CKafka supports SASL_PLAINTEXT authentication (for more information, please see [Adding Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555)).
>- An ACL helps you define a set of permission rules to allow/deny users to read/write topic resources through IPs.


## Directions

### Configuring ACL policy

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. On the topbar, select a region and click the **ID/Name** of the target instance.
3. On the instance details page, click the **User Management** tab at the top.
4. On the user management page, click **Create** and enter the username and password to create a user.
5. Click **ACL Policy Management** at the top.
6. On the ACL policy details page, click **Batch Configuration** to grant permissions to the user.

>?
>- If allow rules are configured only, any IPs other than those configured with allow rules cannot connect to the instance.
>- If deny rules are configured only, any IPs other than those configured with deny rules can connect to the instance.
>- If allow and deny rules are simultaneously configured, only IPs with allow rules can connect to the instance. 

<dx-tabs>
::: Instances on v2.4.1 or above
You can grant permissions to the user through **Topics** or **Topic name prefix**.

- **Topics:** select multiple topics that need to be configured with the same ACL policy. The "Topics" mode only supports configuring one policy.
- **Topic name prefix:** fuzzy match topics that need to be configured with the same ACL policy by topic name prefix. You need to specify the fuzzy matching rule name. After this is set, when a new topic whose name contains the specified prefix is added, the system will automatically configure the specified ACL policy for it.

>?
>- Up to five fuzzy match rules can be set.  
>- You can enter multiple IPs or IP ranges and separate them by `;`.

![](https://main.qcloudimg.com/raw/302ef1adfcd93b5fcae7ebaed583c7f9.png)
:::
::: Instances on other versions
You can grant permissions to the user through **Topics**.

> ?
> - The "Topics" mode only supports configuring one policy.
> - You can enter multiple IPs or IP ranges and separate them by `;`.		

![](https://main.qcloudimg.com/raw/d1294464da0efc600c01bc183c62d0b8.png)
:::
</dx-tabs>
    

### Use limits

1. Enabling routing only affects the authentication method during access, while the set ACL policy takes effect globally.

2. If you use the PLAINTEXT method to access CKafka while enabling public network access routing, the ACL previously set for the topics will still take effect. If you want PLAINTEXT access to be unaffected, please add the read/write permissions of all users for the topics that PLAINTEXT needs to access.
>?When adding an ACL policy, you don't need to select any user, and read/write permissions are added to **all users** by default.
>
 ![](https://main.qcloudimg.com/raw/27e8e0b9b20da5f123eaee2212633dba.png)

   The effect after addition is as follows:
   ![](https://main.qcloudimg.com/raw/6d1b4b5dd89343530deae827e76d38ab.png)

3. If a topic is already being used by another Tencent Cloud service (e.g., log shipping in CLS, message dump in SCF, and component consumption in EMR), enabling ACL policy is equivalent to imposing restrictions on the permissions of these linked capabilities, and they will directly become unavailable. Therefore, please be sure to do so with caution. In such cases, we recommend you produce the same data to another topic for separate processing instead of configuring a unified ACL policy on the same topic.

### Viewing fuzzy match rule

1. On the ACL policy management page, select **Fuzzy Match Rule**.
2. In the fuzzy match rule list, click **Details** in the **Operation** column to view the details of a rule.

### Deleting fuzzy match rule

1. On the ACL policy management page, select **Fuzzy Match Rule**.
2. In the fuzzy match rule list, click **Delete** in the **Operation** column to delete a rule.

## Subsequent Operations

After the authorization is completed, you can access CKafka through the SASL access point and consume messages by using the PLAIN mechanism as instructed in the [SDK documentation](https://intl.cloud.tencent.com/document/product/597/40049).
