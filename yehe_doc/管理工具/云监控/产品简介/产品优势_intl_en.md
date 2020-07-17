
### Automatic activation

You do not need to purchase or activate Cloud Monitor (CM). After you [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985), the Cloud Monitor service is automatically activated, and you can go to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/overview) to view the product running status and configure alarms after purchasing or using a Tencent Cloud product.

### Comprehensive metric monitoring

CM provides various basic metrics, such as CPU utilization, memory utilization, and disk utilization of Cloud Virtual Machines (CVMs), high-speed storage of TencentDB for Memcached, and other cloud service load and performance metrics. These metrics are displayed in visual charts. If the basic metric monitoring cannot meet your needs, you can use the custom monitoring feature to report metric data and view additional data in the corresponding monitoring charts.

### Fine-grained monitoring

Most cloud products (including CVM, CDB, VPC, and CBS) are monitored at one-minute intervals.
We are gradually offering seconds-level monitoring for certain products, with TencentDB for MySQL already supporting five-second intervals.

### Elastic alarm settings

You can configure alarm trigger thresholds for various metrics, and each policy can be associated with different cloud products. After setting a default alarm policy, it will be automatically associated with newly purchased cloud products. You can also create custom alarm recipient groups and transmission channels.

### Flexible alarm service

CM also provides a custom alarm channel service, allowing you to generate custom alarms using monitoring scripts. These alarms are reported to the API, which reports the alarm content to CM. CM then pushes the alarm information to you.
