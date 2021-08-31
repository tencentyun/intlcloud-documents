### How do I upgrade/downgrade the configurations of CVMs?

You can only adjust the configurations of instances **whose system disks and data disks are both cloud disks**. 
- For more information about how to upgrade/downgrade instance configurations, see [Changing Instance Configurations](https://intl.cloud.tencent.com/document/product/213/2178).
- For more information about how to adjust bandwidth/network configurations, see [Adjusting Network Configurations](https://intl.cloud.tencent.com/document/product/213/15517).

If your configuration adjustments do not take effect, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.

### How do I check the records of configuration adjustments?

1. Log in to the [CloudAudit Console](https://console.cloud.tencent.com/cloudaudit).
2. On the **Event history** page, set filters such as the username, the resource type, and the resource name as needed to view the record list.
For more information, see [Getting Started](https://intl.cloud.tencent.com/document/product/1021/30338).

### Can I adjust the configurations of CVM instances?
Yes. You can adjust the configurations of instances whose system disks and data disks are both cloud disks. For pay-as-you-go instances, you can upgrade or downgrade their configurations as many times as you want.

### What is the maximum number of times I can downgrade the configurations of CVMs?
- You can upgrade or downgrade the configurations of pay-as-you-go instances as many times as you want.

### Can I upgrade the specifications and the configurations of pay-as-you-go instances?

Yes. You can upgrade the configurations of pay-as-you-go CVM instances by following the directions listed in [Changing Instance Configurations](https://intl.cloud.tencent.com/document/product/213/2178) or through the [ResetInstancesType](https://intl.cloud.tencent.com/document/product/213/33239) API.

### How long does it take to upgrade a CVM instance?

About 1 to 2 minutes.

### How is the cost incurred for a CVM instance upgrade calculated?

You can view the cost details at the [Billing Center](https://console.cloud.tencent.com/expense) after you upgrade the specifications or the configurations of the CVM instance.

### Will upgrading CVM instances affect my business configurations on the instance?

After you upgrade a CVM instance, you must restart it to validate the new configurations. The upgrade operation will interrupt your business for a short period of time. We recommend that you upgrade instances when business is slow. After being upgraded, instances will seamlessly resume your business and will not require environment reconfiguration.

### Why is the estimated refund of a CVM downgrade 0?

One possible reason is that you have purchased the instance at a discount but the downgraded configuration is calculated according to the original price of the instance. When the price of the instance purchased at a discount is lower than or equal to the original price of the instance, the estimated refund will be displayed as 0.

### Why did the instance upgrade not take effect?

After you upgrade an instance, you must restart it on the Console or through an API.


