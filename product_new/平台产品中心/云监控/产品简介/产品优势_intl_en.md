

### Automatic Activation

You do not need to purchase or activate Cloud Monitoring (CM). After you [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985), the Cloud Monitor service is automatically activated, and you can go to the [Cloud Monitoring console](https://console.cloud.tencent.com/monitor/overview) to view the product running status and configure alarms after purchasing or using a Tencent Cloud product.

### Monitoring multiple metrics

CM provides various cloud service load and performance metrics, such as CPU utilization, memory utilization, disk utilization of Cloud Virtual Machine (CVM), and high-speed storage of TencentDB for Memcached. These metrics are displayed in charts.

### Monitoring at granularity level

Most cloud products, including CVM, CDB, VPC, and Cloud Block Storage (CBS), are monitored at one-minute granularity.
We are gradually offering seconds-level monitoring for certain products, with TencentDB for MySQL already supporting five-second granularity.

### Custom alarm thresholds

You can configure alarm triggering thresholds for various metrics, and each policy can be associated with different cloud products. A default alarm policy is automatically associated with newly purchased cloud products. You can also customize alarm recipients and transmission channels.

### Alarm channel service

CM also provides a custom alarm channel service, allowing you to use monitoring scripts to generate custom alarms and report them to the API. The API then reports the alarms to CM, which then pushes the alarm information to you.
