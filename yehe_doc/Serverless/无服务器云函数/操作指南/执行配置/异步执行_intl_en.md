## Use Cases

In single-task computation-intensive scenarios such as audio/video transcoding, massive data ETL, and AI reasoning, the runtime of a single function instance requires more computing power and longer stable execution. If the invoker of the function is jammed to wait for the execution result, this will not only continue to consume the invoker's resources but also raise the high requirements for the stability of the invocation linkage.
SCF provides a new function execution mechanism. You can use the async function execution mode provided by SCF to extend the execution timeout period and solve the problems with existing execution mechanisms.

## Directions
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=16&ns=default) and click **Function Service** on the left sidebar.
2. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
3. Select an **empty function** or **function template** to create a function.
4. On the **Function Configuration** page, expand **Advanced Settings** and select **Async Execution**.
5. Click **Complete**.




## Execution Mechanism

### How it works

After async execution is enabled for a function, after an event is invoked by a sync invoker (such as API Gateway) or async invoker (such as COS, CKafka, and Timer), the function will respond to the event asynchronously.
In other words, after event scheduling is completed, the event invocation identifier `RequestId` will be returned immediately, and the invocation operation will be ended, thus eliminating the need for the invoker to wait. When the `RequestId` is returned, the engine will concurrently deliver the event to the function runtime to start the execution of the function logic. After the function enters the async execution status, the execution log will be reported to the log service in real time to provide real-time feedback on the execution of the event executed asynchronously. It works as shown below:
![](https://main.qcloudimg.com/raw/8d22b6fdda30bfab2b67f1b4955b9822.png)

### Notes

- Due to differences in the execution mechanisms, you cannot switch between sync/async execution. You can choose whether to enable the "async execution" feature only when creating a function. This configuration item will be locked and cannot be modified or updated after the function is created.
- If the event is invoked successfully, the returned message will only contain `RequestId` and the event execution result. You need to configure the function code logic to call back specific APIs or send notification messages by yourself.
- Real-time logs rely strongly on the log service. The CLS log service is enabled by default. You need to select an existing logset and log topic in the advanced configuration of the function.
  - If no logsets or log topics are available, you need to create one.
  - If you don't enable CLS, you will not be able to get real-time logs.
- The maximum execution duration currently supported for async execution is 24 hours. If you need a longer execution duration, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
- If you use a function execution role to get the permission to access other components of Tencent Cloud services, the role's key is valid for up to 12 hours, and you need to consider extending the validity period or use a permanent key.

## Status Tracking

### How it works

After status tracking is enabled in the advanced configuration of a function, for an asynchronously executed event, the real-time status of the event response will be recorded and reported, and event management-related services such as event status statistics, query, and termination will be provided. It works as shown below:
![](https://main.qcloudimg.com/raw/fd4a61d180c6c7744999abaa842dab5d.png)

### Relevant APIs

APIs for event management-related services are provided through TencentCloud APIs:

<table>
<thead>
<tr>
<th>API</th>
<th>Description</th>
<th>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>GetAsyncEventOverview</td>
<td>This API is used to get an overview of the execution status of an asynchronously executed event. Event statuses include:
<li>Running: the event is being executed asynchronously.</li>
<li>Invoked successfully: the event is asynchronously executed successfully with a normal response.</li>
<li>Invocation failed: the event failed to be asynchronously executed with an exceptional response.</li>
<li>Invocation terminated: the user actively terminated the event in progress, and async execution stopped.</li>
</td>
<td>-</td>
</tr>
<tr>
<td>ListAsyncEvents</td>
<td>This API is used to list the information of an asynchronously executed event. It can query the information by conditions such as `RequestId`, function name, function version, event status, and event invocation/end time.
<dx-alert infotype="notice" title="">
Only data within three days after event tracking is enabled can be queried.
</dx-alert>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/39734">ListAsyncEvents</a></td>
</tr>
<tr>
<td>TerminateAsyncEvent</td>
<td>This API is used to terminate an asynchronously executed event in progress according to the returned `RequestId`.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/39733">TerminateAsyncEvent</a></td>
</tr>
</tbody>
</table>









### Notes

- The generated event status data is retained for only 3 days and will be cleared on a rolling basis in a time window of 3 days. If you want to keep all records, you need to periodically pull them and save them to your own storage.
- After status tracking is disabled, event management-related services such as recording, collecting, querying, and terminating asynchronously executed events will no longer be available, and the generated event status data will be cleared in 3 days.
- The limit on QPS of asynchronously executed events is one-tenth of the function concurrency, and any excess will be limited, resulting in response failures.
- If the limit on QPS is exceeded, or if your account falls into arrears, the corresponding exception will be returned by the scheduling engine directly after you invoke an event, and no event status records will be generated.


