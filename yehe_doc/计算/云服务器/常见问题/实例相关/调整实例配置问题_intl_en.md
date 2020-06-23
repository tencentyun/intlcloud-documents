### How do I upgrade/downgrade the configuration of a CVM?

You can only adjust the configurations of instances **whose system disk and data disk are both cloud disks**. 
- For more information about how to upgrade/downgrade instance configuration, see [Adjusting Instance Configuration](https://intl.cloud.tencent.com/document/product/213/2178).
- For more information about how to adjust bandwidth/network configuration, see [Adjusting Network Configuration](https://intl.cloud.tencent.com/document/product/213/15517).

If your configuration adjustment does not take effect, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.

### How do I check the records of configuration adjustments?

1. Log in to the [CloudAudit Console](https://console.cloud.tencent.com/cloudaudit).
2. On the **Event history** page, set the filters such as username, resource type, and resource name as needed to view the record list.
For more information, see [Getting Started](https://intl.cloud.tencent.com/document/product/1021/30338).

### Can I adjust the configuration of a CVM instance?
Yes, you can adjust the configurations of instances whose system disk and data disk are both cloud disks. Moreover, you can freely upgrade or downgrade the configurations of pay-as-you-go instances.

### How many times can I downgrade the configuration of one CVM at most?
- You can upgrade or downgrade the configuration of pay-as-you-go instances as many times as you want.

### Can I upgrade the specification and configuration of pay-as-you-go instances?

Yes. You can upgrade the configurations of pay-as-you-go CVM instances using methods in [adjusting instance configuration](https://intl.cloud.tencent.com/document/product/213/2178) or through the [ResetInstancesType](https://intl.cloud.tencent.com/document/product/213/33239) API.

### How long does it take to upgrade a CVM instance?

It takes about 1 to 2 minutes to complete the upgrade.

### How is the cost incurred for a CVM instance upgrade calculated?

You can view the cost details on the [Billing Center](https://console.cloud.tencent.com/expense/overview) after you upgrade the specification or configuration of the CVM instance.

### Does upgrading CVM instances affect my service configurations on the instance?

After you upgrade a CVM instance, you must restart it to validate new configurations. The upgrade operation will cause short interruption of services. We recommend that you upgrade instances when the business is slow. Instances can seamlessly resume services after upgrades without environment reconfiguration.

### Why is the estimated refund of a CVM downgrade to be 0?

The possible reason is that you have purchased the instance at a discount and the downgraded configuration is calculated according to the original price. When the former is lower than or equal to the latter, the estimated refund will be displayed as 0.

### Why did the instance upgrade not take effect?

After you upgrade an instance, you must restart it on the Console or through API.


