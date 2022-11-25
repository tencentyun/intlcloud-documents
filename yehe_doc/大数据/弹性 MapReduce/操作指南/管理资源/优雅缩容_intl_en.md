## Feature Overview
After graceful scale-in is enabled, if the scale-in action is triggered when a node is executing tasks, the node will not be released immediately. Instead, it will be released after completing the tasks. Graceful scale-in is available for both automatic scaling and manual scale-in.
>? YARN, HBase, and Presto (renamed Trino in EMR v2.7.0 and v3.40 or later) support graceful scale-in. However, Presto cannot be scaled in gracefully in Ranger, Kerberos, and OpenLDAP integration scenarios.


## Directions
### Automatic scaling
Automatic scaling allows you to enable or disable graceful scale-in for all scale-in rules. This feature is called global graceful scale-in and is disabled by default. When you add or edit a single scale-in rule, graceful scale-in is enabled by default, and the default duration is 60 seconds (valid range: 60–1800 seconds).
>?When global graceful scale-in and a single rule are enabled, graceful scale-in takes effect for the rule.

1. Log in to the [EMR console](https://console.cloud.tencent.com/emr), click the **ID/name** of the target cluster to enter the cluster details page, and click **Auto Scaling**.
![](https://main.qcloudimg.com/raw/db8087ecc04f71d9d7c06d4b16d51e3e.png)
2. In the **Scaling Rule Management** section on the **Auto Scaling** page, click **Add Rule** and add a scale-in rule.
![](https://main.qcloudimg.com/raw/e0b4831b2b7ae3b0f487e7a6a6d2903e.png)

### Manual scale-in
When you try to manually remove a node, graceful scale-in is disabled by default. When you enable this feature, the default duration is 60 seconds (valid range: 60–1800 seconds).
1. Click the **ID/name** of the target cluster to enter the cluster details page. Then, select **Cluster Resource** > **Resource Management**.
![](https://main.qcloudimg.com/raw/dfae5e3b402f1b2abbfba7fbb5d3e66a.png)
2. Select the node to remove and click **Terminate**. In this case, graceful scale-in is disabled by default. You can enable it and set a duration.
![](https://main.qcloudimg.com/raw/5e04a826ba73007c76223ed349521f48.png)
3. After finishing your settings, click **Next**, confirm the node information, and click **Start Termination**.
![](https://main.qcloudimg.com/raw/7883b7f3a0d47dfa8c03e4968b09e5f9.png)
