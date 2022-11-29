## Overview

This document describes how to configure SASL authentication and ACL (access control list) rules in the CKafka console to enhance access control in public/private network transfers and permission control in production and consumption of resources such as topics.

> ?
> 
>- Kafka offers various security authentication mechanisms, which mainly include SSL and SASL. SASL/PLAIN is a more commonly used authentication method that is based on account and password. CKafka supports SASL_PLAINTEXT authentication. For more information, see [Adding Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555).
> - An ACL helps you define a set of permission rules to allow/deny users to read/write topic resources through IPs.

## Directions

### Creating a user

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. On the topbar, select a region and click the **ID/Name** of the target instance.
3. On the instance details page, click the **ACL Policy Management** tab at the top.
4. On the **User Management** tab, click **Create** and enter the username and password to create a user.

### Configuring an ACL policy

1. On the **ACL Policy Management** page, select the **Policy List** tab.
2. Click **Batch Set** to grant permissions to the user.

> ?
> 
> - If only allow rules are configured, any IPs not in those rules cannot connect to the instance.
> - If only deny rules are configured, any IPs not in those rules can connect to the instance.
>- If both allow and deny rules are configured, only IPs in allow rules can connect to the instance.

<dx-tabs>
::: Instances on v2.4.1 or later
You can grant permissions to the user through the **Topics**, **Topic name prefix**, or **Preset Rule** option.
<dx-alert infotype="explain" title="">
You can enter multiple IPs or IP ranges and separate them by `;` when configuring the ACL policy. If the IP is empty, the permission will be added for **all IPs** by default.
</dx-alert>

- **Topics:** Select multiple topics that need to be configured with the same ACL policy.
- **Topic name prefix:** Fuzzy match topics that need to be configured with the same ACL policy by topic name prefix. You need to specify the fuzzy matching rule name. After this is set, when a new topic with a name containing the specified prefix is added, the system will automatically configure the specified ACL policy for it.
  <dx-alert infotype="explain" title="">
  Up to five fuzzy match rules can be set.  
  </dx-alert>

- **Preset Rule:** A set of rules can be preset and automatically applied during subsequent topic creation.
  <dx-alert infotype="explain" title="">
  Up to five preset rules can be set.  
  </dx-alert>

  :::
  ::: Instances on other versions
  You can grant permissions to the user through the **Topics** or **Preset Rule** option.

<dx-alert infotype="explain" title="">
You can enter multiple IPs or IP ranges and separate them by `;`. If the IP is empty, the permission will be added for **all IPs** by default.
</dx-alert>
- **Topics:** Select multiple topics that need to be configured with the same ACL policy.
- **Preset Rule:** A set of rules can be preset and automatically applied during subsequent topic creation.
  <dx-alert infotype="explain" title="">
  Up to five preset rules can be set.  
  </dx-alert>

  :::
  </dx-tabs>
  Next steps: After the authorization is completed, the user can access CKafka through the SASL access point and consume messages by using the PLAIN mechanism. For more information, see the <a href="https://www.tencentcloud.com/document/product/597/40049">SDK documentation</a>.
  

### Use limits

1. Enabling routing only affects the authentication method during access, while the set ACL policy takes effect globally.
2. If you use the PLAINTEXT method to access CKafka while enabling public network access routing, the ACL previously set for the topics will still take effect. If you want PLAINTEXT access to be unaffected, add the read/write permissions of all users for the topics that PLAINTEXT needs to access.

  <dx-alert infotype="explain" title="">
  When adding an ACL policy, you don't need to select any user, and read/write permissions are added to **all users** by default.
  </dx-alert>

3. If a topic is already being used by another Tencent Cloud service (e.g., log shipping in CLS, message dump in SCF, and component consumption in EMR), enabling ACL policy is equivalent to imposing restrictions on the permissions of these linked capabilities, and they will directly become unavailable. Therefore, be sure to do so with caution. In such cases, we recommend you produce the same data to another topic for separate processing instead of configuring a unified ACL policy on the same topic.

### Viewing a preset rule

1. On the ACL policy management page, select **Preset Rule**.
2. In the preset rule list, click **Details** in the **Operation** column to view the details of a rule.

### Deleting a preset rule

1. On the ACL policy management page, select **Preset Rule**.
2. In the preset rule list, click **Delete** in the **Operation** column to delete a rule.
    The impact of deleting the preset rule varies by the type of rule match:
  - If the rule is a fuzzy match rule, it will no longer be automatically applied to new topics or take effect for topics to which it is already applied.
  - If the rule is not a fuzzy match rule, it will no longer be automatically applied to new topics but will still take effect for topics to which it is already applied.
