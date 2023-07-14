## Overview
After graceful scale-in is enabled, if the scale-in action is triggered when a node is executing tasks, the node will not be released immediately. Instead, it will be released after completing the tasks. Graceful scale-in is available for both automatic scaling and manual scale-in.
>? YARN, HBase, and Presto (renamed Trino in EMR v2.7.0 and v3.40 or later) support graceful scale-in. However, Presto cannot be scaled in gracefully in Ranger, Kerberos, and OpenLDAP integration scenarios.


## Directions
### Auto-scaling
Auto-scaling allows you to enable or disable graceful scale-in for all scale-in rules. This feature is called global graceful scale-in and is disabled by default. When you add or edit a single scale-in rule, graceful scale-in is enabled by default, and the default duration is 60 seconds (valid range: 60–1800 seconds).
>?When global graceful scale-in and a single rule are enabled, graceful scale-in takes effect for the rule.

1. Log in to the [EMR console](https://console.cloud.tencent.com/emr), click the **ID/name** of the target cluster to enter the cluster details page, and click **Auto-scaling**.
2. In the **Scaling rule management** section on the **Auto-scaling** page, click **Add rule** and add a scale-in rule.

### Manual scale-in
When you try to manually remove a node, graceful scale-in is disabled by default. When you enable this feature, the default duration is 60 seconds (valid range: 60–1800 seconds).
1. Click the **ID/name** of the target cluster to enter the cluster details page. Then, select **Cluster resources** > **Resources**.
2. Select the node to remove and click **Scale in**. In this case, graceful scale-in is disabled by default. You can enable it and set a duration.
3. After finishing your settings, click **Next**, confirm the node information, and click **Start termination**.
