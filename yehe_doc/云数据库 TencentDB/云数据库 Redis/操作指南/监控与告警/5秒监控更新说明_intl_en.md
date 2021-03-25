## Update Description
TencentDB for Redis has been updated with optimized monitoring features in the latest version.
- The monitoring granularity is now narrowed from one minute to five seconds.
- The monitoring data delay is now reduced to less than 20 seconds.
- Monitoring, data collection, and alarms are now supported for replica nodes.
- Monitoring, data collection, and alarms are now supported for Proxy nodes.
- You can now compare monitoring metric values among multiple nodes.
- New monitoring metrics are supported.

## Notes
- By default, new instances (excluding CKV instances) support five-second granularity.
- In the future, you can modify the monitoring granularity of existing instances from one minute to five seconds in the [TencentDB for Redis console](https://console.cloud.tencent.com/redis). Please pay attention to the notices and pop-up notifications in the console.
- In the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/policylist/create), alarm policies for five-second granularity are of a different policy type from those for one-minute granularity. You can replicate the alarm policies for one-minute granularity and change their policy types to **Memory Edition (5-second granularity)**, so that these alarm policies can be associated with new instances supporting five-second granularity.
![](https://main.qcloudimg.com/raw/9bfa0b792d4c0ddc4b262ea5357575e3.png)
## FAQs
#### How do I tell whether an instance supports five-second or one-minute monitoring granularity?
- Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance name/ID and enter the instance management page, select **System Monitoring** > **Monitoring Metrics**, and click the **Period** drop-down list at the top. If you can select **5 seconds** from the drop-down list, this instance supports the monitoring granularity of five seconds, or else it supports only the monitoring granularity of one minute.
![](https://main.qcloudimg.com/raw/e7833ebba07a4dd949c911c58940a4d0.png)
- Check the value of the `InstanceSet.MonitorVersion` field returned by the [DescribeInstances](https://intl.cloud.tencent.com/document/product/239/32065) API. If the value is `5s`, this instance supports the monitoring granularity of five seconds; if the value is `1m`, it supports only the monitoring granularity of one minute.

#### How do I get information of Proxy or Redis nodes?
Use the [DescribeInstanceNodeInfo](https://intl.cloud.tencent.com/document/product/239/38627) API to get the IDs of Proxy nodes and Redis nodes.
>!The IDs of Proxy and Redis nodes will change when node failover, instance capacity expansion/reduction, data migration, etc., occur. Therefore, we recommend that you get the latest node information from the API in a timely manner.

