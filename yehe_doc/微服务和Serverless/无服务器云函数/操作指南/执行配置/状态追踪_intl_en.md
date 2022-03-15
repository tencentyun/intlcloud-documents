## Use Cases

Asynchronously executed functions are usually used to process a large number of async time-consuming tasks. In order to better manage such tasks, SCF provides a status trace feature, which records and reports the real-time status of event responses and provides event management services such as event status statistics collection and query.

## Execution Mechanism

### How it works

After the status trace feature is enabled for asynchronously executed functions, the platform will start recording and reporting the real-time status of events. It works as shown below:
![](https://main.qcloudimg.com/raw/fd4a61d180c6c7744999abaa842dab5d.png)

### Notes

- The status data of asynchronously executed events is retained for only 3 days and will be cleared on a rolling basis in a time window of 3 days. If you want to keep all records, you need to periodically pull them and save them to your own storage.
- After status trace is disabled, event management services such as recording, collecting, and querying asynchronously executed events will no longer be available, and the generated event status data will be cleared in 3 days.
- If the limit on QPS is exceeded, or if your account falls into arrears, the corresponding exception will be returned by the scheduling engine directly after you invoke an event, and no event status records will be generated.

## Directions

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=16&ns=default) and click **Function Service** on the left sidebar.
2. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
3. Select an **empty function** or **function template** to create a function.
4. On the **Function Configuration** page, expand **Advanced Settings**, select **Async Execution** > **Status Trace**, and click **Complete**.
5. After the function is created, you can click **Event Management** to view the list of async events.
![](https://qcloudimg.tencent-cloud.cn/raw/91118500ac76440f1c6c4ff7a7b20c69.png)

