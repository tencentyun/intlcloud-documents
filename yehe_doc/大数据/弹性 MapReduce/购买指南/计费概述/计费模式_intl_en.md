Billing mode for EMR clusters:
- **Pay-as-you-go:** all nodes in a cluster are charged on a [pay-as-you-go](https://intl.cloud.tencent.com/document/product/555/30328) basis. This is suitable for clusters that exist for a short time or periodically.

For information on node types, see [Node Type Description](https://intl.cloud.tencent.com/document/product/1026/31094).

When you purchase an EMR cluster, the price will be listed as an hourly fee. However, you will be billed by the actual seconds of usage and the charge will be rounded to two decimal places. Billing starts from the second the cluster is created and stops the second the cluster is terminated. 

When you purchase a pay-as-you-go cluster, the fees for 2-hour usage under the current configuration will be frozen in your account balance as a deposit. You will then be billed by the hour (Beijing time) for your usage over the past hour. When you change the node configurations, the frozen amount will be unfrozen and a new 2-hour deposit will be frozen based on the unit price of the new configuration. Your deposit will be released back to your account when the cluster is terminated.

Other items that may incur costs include network traffic, metadata storage, and COS.

- **Network traffic**
Public network access is enabled for the Master.1 node in a cluster by default so that you can access the WebUI pages of various Hadoop components from outside the cluster. Traffic fees are incurred for data interactions when you visit these pages, which is very little in most cases. Therefore, the bill-by-traffic mode is used by default, which costs less than the bill-by-bandwidth mode.
- **Metadata storage**
The metadata storage such as Hive on EMR (v2.x and lower) uses TencentDB, the fee of which is included in the total cost on the purchase page.
- **COS**
When you separate compute and storage for a cluster via COS, data storage and request fees (see [COS Product Pricing](https://buy.intl.cloud.tencent.com/price/cos)) will be incurred when the cluster pulls data from COS for computing. In addition, new data may be generated for the storage or backup of compute results in COS.
