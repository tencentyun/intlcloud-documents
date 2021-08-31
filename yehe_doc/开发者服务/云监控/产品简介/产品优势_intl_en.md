
### Automatic activation

Cloud Monitor (CM) does not require additional purchase and activation. It will be automatically activated after you [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985). After you purchased and used Tencent Cloud services, go to the [Cloud Monitoring console](https://console.cloud.tencent.com/monitor/overview) to view the product running status and configure alarms.

### Comprehensive metric monitoring

CM allows you to monitor various load and performance metrics, such as CVM CPU utilization, memory utilization, disk utilization, high-speed storage of TencentDB for Memcached, etc. These metrics can be displayed in visual charts. If the basic metric monitoring cannot meet your needs, you can use custom monitoring to report metric data and view monitoring charts in multiple dimensions.

### Fine-grained monitoring

Most Tencent Cloud services (including CVM, CDB, VPC, and CBS) are monitored at 1-minute granuarity.
We are gradually offering seconds-level monitoring for certain services. TencentDB for MySQL now supports monitoring at 5-second granularity.

### Elastic alarm configuration

You can configure alarm thresholds for various metrics, and each policy can be associated with different Tencent Cloud services. After you configure a default alarm policy, newly purchased services will be automatically associated with it. You can customize alarm recipients and notification channels.

### Flexible alarm service

CM also provides a custom alarm channel service, allowing you to use the monitoring script to generate a custom alarm. The alarm will be reported to the API, which then reports the alarm to CM. CM will push the alarm notification to you.
