TDSQL-C Serverless Edition adopts the serverless architecture for cloud native database services. It is billed based on the actual computing and storage resource usage, so you only need for pay for what you use while enjoying the cloud native technologies of Tencent Cloud.

## Service Features
- Autopilot: the database can automatically start/stop according to the business load and scale in an imperceptible manner without causing disconnections.
- Utility pricing: the database is billed based on the actual computing and storage usage which is calculated by second and settled by hour.

## Use Cases
- Low-Frequency database usage scenarios such as development and test environments.
- Scenarios where the load is uncertain, such as IoT and edge computing.
- SaaS application scenarios such as Mini Program Cloud Base and SME website development.

## Billing Modes
Computing and storage are billed separately: computing is billed by the number of CCUs, while storage is billed by the usage in GB. The billing system calculates the usage by second and settles fees by hour. For detailed prices, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/1098/40620)

CynosDB Compute Unit (CCU) is the computing and billing unit for the Serverless Edition. A CCU is approximately equal to 1 CPU core and 2 GB memory. The number of CCUs used in each billing cycle is the greater of the number of CPU cores used by the database and 1/2 of the memory size.

You can select the maximum and minimum CCUs your database requires on the [purchase page](https://buy.cloud.tencent.com/cynosdb) according to your business conditions. You can also change them in the [console](https://console.cloud.tencent.com/cynosdb).
![](https://main.qcloudimg.com/raw/e260eb868b7e1a5c0d63ba6303e1af69.png)

## Service Management
### Pausing service
- You can enable/disable the auto-pause feature in the [console](https://console.cloud.tencent.com/cynosdb) according to your business needs.
 - After this feature is enabled, you need to set the auto-pause time, which is one hour by default. The database will be automatically paused if it has no active connections and CPU usage after this time elapses. After the pause, the computing resources will not be billed, and the storage resources will be billed by the actual usage.
 - If this feature is disabled, the database will keep running. When there are no active connections and CPU usage, the database will be billed based on the minimum CCU you configure. This is suitable for scenarios where your business has a heartbeat connection.
![](https://main.qcloudimg.com/raw/713ab08ea390726aa4c1b30a3a20b658.png)
- You can also manually pause specified databases in the console.
![](https://main.qcloudimg.com/raw/237185fbb0522d99ae062c2c376d2974.png)

### Starting service
You cannot use the features in the [console](https://console.cloud.tencent.com/cynosdb) for a paused serverless database. If needed, you can wait until the database is automatically started or manually start it the console.
![](https://main.qcloudimg.com/raw/af1ea0bb0607126fdcc8f3f7e6b70bfe.png)

When a paused database is accessed, the system will automatically start it in seconds. During the short startup process, the application may receive the following error messages; therefore, the business should have a reconnection mechanism.
```
ERROR 9449 (08S01): CynosDB serverless instance is resuming, please try connecting again
ERROR 2003 (HY000): Can't connect to MySQL server on  'xxxx' (111)
```
![](https://main.qcloudimg.com/raw/938b717a6d5282ab386b0b33237645a8.png)

