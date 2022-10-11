### How do I migrate from self-built Prometheus to TMP?[](id:question1)

In the configuration file of self-built Prometheus, add a remote write configuration pointing to TMP for migration. For more information, see [Migration from Self-Built Prometheus](https://intl.cloud.tencent.com/document/product/1116/43213).

### Can I batch import/export dashboards into/from Grafana?

You can do so through APIs as instructed in [HTTP API reference](https://grafana.com/docs/grafana/latest/http_api/).

### What should I do if one exporter has too much data?

You can use Prometheus in this scenario, but we recommend you not expose too many metrics in the exporter, as the exporter itself and the Prometheus agent consume a lot of memory. Only expose key metrics, and do not use parameters such as user ID and URL in metric labels.

### How do I use TMP to monitor clusters in two different VPCs?
1. You can interconnect the VPCs of the two clusters through [CCN](https://intl.cloud.tencent.com/document/product/215/40089) and then integrate the clusters into Prometheus .
2. Install the [agent](https://intl.cloud.tencent.com/document/product/1116/43180) in one of the clusters, and then use the Nginx proxy to remotely write the target address to the TMP instance.

### How do I integrate native container services with TMP?  
You can't integrate them directly. However, you can create data and add a remote write configuration pointing to TMP in the configuration file of your self-built Prometheus. For detailed directions, see [Migration from Self-Built Prometheus](https://intl.cloud.tencent.com/document/product/1116/43213).

### How do I set the parameters of the alarm cycle when creating an alarm rule through Prometheus APIs?

Add `key=_interval_  value=1m/5m/10m/15m/30m/60m` to the new `Labels` parameter.


### Will data get lost during instance rebooting?
Data will not get lost during instance rebooting, as it is stored in TencentDB for CTSDB. However, because data cannot be reported normally during rebooting, data breakpoints may occur.

### Is it normal to see a rise in generated data after the TMP instance is rebooted?
Retries will be performed after instance rebooting, so it is normal if the data volume seems to fluctuate greatly in a short period of time.


### Can I batch add MySQL instances when integrating MySQL with Prometheus in the integration center?
No. You can only add instances one by one.

### Where can I view the security group of the EKS cluster created by Prometheus?
Go to **Security** > **Security Group** in the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and search by the current TMP instance ID.

### Can I configure multiple scrape tasks for a PodMonitor?
Yes, but you should ensure that the tasks have the same port name and label.

### (TMP Pushgateway usage) If the clients of multiple instances push the same job with different label metrics, metrics will be overwritten. What should I do?
You can use `groupingkey` to solve this problem. Below is the sample code:

```
if err := push.New("http://$IP:$PORT", "db_backup").
        BasicAuth("$APPID", "$TOKEN").
        Collector(completionTime).
        Grouping("instance", "$INSTANCE"). 
```
