This document describes how to modify the audit rule in the console.

## Prerequisites
You have enabled the audit service as instructed in [Enabling Audit Service](https://intl.cloud.tencent.com/document/product/1098/44614).

## Feature overview
- The audit rule can be changed from full audit to rule-based audit or vice versa.
- After the audit rule is modified, the modification will be applied to the selected instance.
- You’re allowed to modify the rule type, parameter field, operator, and characteristic string for an audit rule. You can add or remove the items but must keep at least one of them. For detailed directions, see [Enabling Audit Service > Set the audit rule](https://intl.cloud.tencent.com/document/product/1098/44614).

## Modifying the audit rule for one instance
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/).
2. Click **Database Audit** on the left sidebar and select the region at the top.
3. Click **Enabled** after **Audit Status** to filter instances for which the audit service is enabled.
4. Find the target cluster/instance in the audit instance list, or search for it by resource attribute in the search box, and select **More** > **Modify Audit Rule** in the **Operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/r6AT201_7.png)
5. In the **Modify Audit Rule** window, modify the audit rule and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/nj6N350_8.png)

## Batch modifying the audit rule
>?
>- The audit rule can be changed from full audit to rule-based audit or vice versa.
>- After the audit rule is modified, the modification will be applied to the selected instance.
>- You’re allowed to modify the rule type, parameter field, operator, and characteristic string for an audit rule. You can add or remove the items but must keep at least one of them. For detailed directions, see [Enabling Audit Service > Set the audit rule](https://intl.cloud.tencent.com/document/product/1098/44614).

1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/).
2. Click **Database Audit** on the left sidebar and select the region at the top.
3. Click **Enabled** after **Audit Status** to filter instances for which the audit service is enabled.
4. Find the target clusters/instances in the audit instance list, or search for them by resource attribute in the search box, and select them. Then, click **Modify Audit Rule** above the list.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/UYwz495_9.png)
5. In the **Modify Audit Rule** window, modify the audit rule and click **OK**.
>!The **Modify Audit Rule** window displays the audit rules both before and after the modification to make comparisons easier. The new rules will be applied to the selected instances. Therefore, proceed with caution.
>

