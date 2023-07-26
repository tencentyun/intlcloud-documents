This document describes how to modify the audit rule in the console.

## Prerequisite
You have enabled the audit service. For more information, see [Enabling Audit Service](https://www.tencentcloud.com/document/product/236/52086).

## Note
- The audit rule can be changed from full audit to rule-based audit or vice versa.
- After the audit rule is modified, the modification will be applied to the selected instance.
- You’re allowed to modify the rule type, parameter field, operator, and characteristic string for an audit rule. You can add or remove the items but must keep at least one of them. For detailed directions, see [Enabling Audit Service > Set the audit rule](https://www.tencentcloud.com/document/product/236/52086#SJGZSZ).

## Modifying the audit rule for one instance
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/instance).
2. On the left sidebar, click **Database Audit**.
3. Select **Region** at the top, click the **Audit Instance** tab, and click **Enabled** to filter audit-enabled instances.
4. Find the target instance in the audit instance list, or search for it by resource attribute in the search box, and select **More** > **Modify Audit Rule** in the **Operation** column.
5. In the **Modify Audit Rule** window, modify the audit rule and click **OK**.

## Batch modifying the audit rule
>?
>- The audit rule can be changed from full audit to rule-based audit or vice versa.
>- After the audit rule is modified, the modification will be applied to the selected instance.
>- You’re allowed to modify the rule type, parameter field, operator, and characteristic string for an audit rule. You can add or remove the items but must keep at least one of them. For detailed directions, see [Enabling Audit Service > Set the audit rule](https://www.tencentcloud.com/document/product/236/52086#SJGZSZ).

1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/instance).
2. On the left sidebar, click **Database Audit**.
3. Select **Region** at the top, click the **Audit Instance** tab, and click **Enabled** to filter audit-enabled instances.
4. Find the target instances in the audit instance list, or search for them by resource attribute in the search box. Then, click **Modify Audit Rule** above the list.
5. In the **Modify Audit Rule** window, modify the audit rule and click **OK**.
>!The **Batch Modify Audit Rule** window displays the audit rules both before and after the modification to make comparisons easier. The new rules will be applied to the selected instances. Therefore, proceed with caution.
>

