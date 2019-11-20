
### Why is the value of max_connections always displayed as 1,000 rather than the actual number of current maximum connections in MySQL instance monitoring?
max_connections represents the allowed maximum connections in instance monitoring. You can customize the maximum value up to 10,240. **Number of open connections** means the number of connections available at the current moment, a value that changes in real time.

### How can I get to know that the disk capacity is insufficient?
The monitoring center oversees the disk capacity of a TencentDB instance. When the disk utilization is over 90%, SMS and email alarms will be triggered. To receive such alarms, you only need to configure alarm recipients in Cloud Monitor. (For more information on how to configure, see [Alarming](https://intl.cloud.tencent.com/document/product/236/8457)).



