## Update Description
TencentDB for Redis has been updated with optimized monitoring features in the latest version.
- The monitoring granularity is now narrowed from one minute to five seconds.
- The monitoring data delay is now reduced to less than 20 seconds.
- Monitoring, data collection, and alarms are now supported for replica nodes.
- Monitoring, data collection, and alarms are now supported for proxy nodes.
- You can now compare monitoring metric values among multiple nodes.
- New monitoring metrics are added.

## Update Notes
- In the future, you can modify the monitoring granularity of existing instances from one minute to five seconds in the TencentDB for Redis console. We will notify you of when the modification becomes supported by notices and pop-up notifications in the [console](https://console.cloud.tencent.com/redis).
- In the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/policylist/create), alarm policies for five-second granularity are of a different policy type from those for one-minute granularity, as shown below. You can replicate the alarm policies for one-minute granularity and change their policy types to **Memory Edition (5-second granularity)**, so that these alarm policies can be associated with new instances supporting five-second granularity.
![](https://main.qcloudimg.com/raw/1f1078e7d1676425b20bc8849d242ac4.png)
  
## FAQs
#### How do I tell whether an instance supports five-second or one-minute monitoring granularity?
- Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance name/ID and enter the instance management page, select **System Monitoring** > **Monitoring Metrics**, and click the **Period** drop-down list at the top. If you can select **5 seconds** from the drop-down list, this instance supports the monitoring granularity of five seconds, or else it supports the monitoring granularity of one minute.
![](https://main.qcloudimg.com/raw/19e0babb73bd59d10993c76ac295b197.png)
- Check the value of the `InstanceSet.MonitorVersion` field returned by the [DescribeInstances](https://intl.cloud.tencent.com/document/product/239/32065) API. If the value is `5s`, this instance supports the monitoring granularity of five seconds; if the value is `1m`, it supports the monitoring granularity of one minute.

#### How do I get information on proxy or Redis nodes?
Use the [DescribeInstanceNodeInfo](https://intl.cloud.tencent.com/document/product/239/38627) API to get the IDs of proxy and Redis nodes.
>!The IDs of proxy and Redis nodes will change when node failover, instance capacity expansion/reduction, data migration, etc., occur. Therefore, we recommend that you get the latest node information from the API in a timely manner.

