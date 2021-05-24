## Overview

This document describes how to configure SASL authentication and ACL rules in the CKafka console to enhance access control in public/private network transfers and permission control in production and consumption of resources such as topic.

>?
>- Kafka offers various security authentication mechanisms, which mainly fall into the SSL and SASL2 categories. Among them, SASL/PLAIN is an authentication method based on account and password and more commonly used. CKafka supports SASL_PLAINTEXT authentication (for more information, please see [Adding Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555)).
>- An access control list (ACL) helps you define a set of permission rules to allow/deny users to read/write topic resources through IPs.


## Directions

### Configuring ACL policy

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. On the topbar, select a region and click the **ID/Name** of the target instance.
3. On the instance details page, click the **User Management** tab at the top.
4. On the user management page, click **Create** and enter the username and password to create a user.
5. Click **ACL Policy Management** at the top.
6. On the ACL policy details page, click **Batch Configuration** to grant permissions to the user.
   - **Instances on v2.4.2**: you can grant permissions to the user through **batch check** or **fuzzy match by prefix**.
     **Batch check**: select multiple topics that need to be configured with the same ACL policy. The batch check mode only supports configuring one policy.
     **Fuzzy match by prefix**: fuzzy match topics that need to be configured with the same ACL policy by topic name prefix. You need to specify the fuzzy matching rule name. After this is set, when a new topic whose name contains the specified prefix is added, the system will automatically configure the specified ACL policy for it.
     >?Up to five fuzzy matching rules can be set.


   - **Instances on other versions**: you can grant permissions to the user through **batch check**.
     Select multiple topics that need to be configured with the same ACL policy. The batch check mode only supports configuring one policy.

   > ?
   > - Enabling routing only affects the authentication method during access, while the set ACL policy takes effect globally.
   > - If you use the PLAINTEXT method to access Kafka while enabling public network access routing, the ACL previously set for the topics will still take effect.
   >   If you want PLAINTEXT access to be unaffected, please add the read/write permissions of all users for the topics that PLAINTEXT needs to access.
   > - If a topic is already being used by another Tencent Cloud service (e.g., log shipping in CLS, message dump in SCF, and component consumption in EMR), enabling ACL policy is equivalent to imposing restrictions on the permissions of these linked capabilities, and they will directly become unavailable. Therefore, please be sure to do so with caution. In such cases, we recommend you produce the same data to another topic for separate processing instead of configuring a unified ACL policy on the same topic.

### Viewing fuzzy matching rule

1. On the ACL policy management page, select **Fuzzy Matching Rule**.
2. In the fuzzy matching rule list, click **Details** in the **Operation** column to view the details of a rule.

### Deleting fuzzy matching rule

1. On the ACL policy management page, select **Fuzzy Matching Rule**.
2. In the fuzzy matching rule list, click **Delete** in the **Operation** column to delete a rule.

## Subsequent Steps

After the authorization is completed, the user can access CKafka through the SASL access point and consume messages by using the PLAIN mechanism.
