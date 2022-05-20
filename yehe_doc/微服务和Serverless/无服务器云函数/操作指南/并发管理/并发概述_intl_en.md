Concurrency refers to the number of requests that can be processed by a function concurrently at a moment. If it can be sustained by other services of your business, you can increase the function concurrency from several to tens of thousands with simple configuration.

## How Concurrency Works

When a function is invoked, SCF will assign a concurrent instance to process the request or event. After the function code is executed and its response is returned, the instance will process other requests. If all instances are running when a request arrives, SCF will assign a new concurrent instance.

SCF follows the execution logic that one concurrent instance processes only one event at any time so as to ensure the processing efficiency and stability of each event.

### Concurrent processing for async invocations

Async events enter a queue on SCF, where they will be processed in a FIFO manner. The system will select an appropriate concurrency processing method based on the conditions such as queue length and current number of concurrent instances of the function to pull sufficient concurrent instances and process the events in sequence.

If an async invocation fails, SCF will retry according to certain rules. For more information, see [Error Types and Retry Policies](https://intl.cloud.tencent.com/document/product/583/39851).

### Concurrent processing for sync invocations

When sync events arrive, SCF checks for idle concurrent instances. If yes, the events are immediately sent to idle instances; otherwise, new concurrent instances are started to process them.

When a sync invocation fails, you need to retry on your own.




### [Concurrency calculation](id:computing)
SCF concurrency refers to the number of requests or invocations processed by the function code at a time, which can be estimated according to the following formula:

Concurrency = request rate * function execution duration = QPS * average time per request

You can view the average time per request in **execution duration** in the monitoring data.
For example, if the QPS of a business is 2,000, and the average time per request is 0.02 seconds, then the concurrency during function execution will be 2000 * 0.02 = 40.




## Concurrent Instance Reuse and Repossession

After a concurrent instance processes a request event, it will not be repossessed immediately; instead, it will be retained for a certain period of time for reuse. During the retention duration, if there are new request events that need to be processed, the retained concurrent instance will be used first, so the events can be processed quickly with no need to start new concurrent instances.

After the retention duration elapses, if there are no requests that need to be processed by the instance, the SCF platform will repossess it. For low concurrency scenarios, no retention duration is set, and the platform will enable the smart repossession mechanism for resource repossession.

The concurrent instance retention duration is dynamically adjusted by SCF as needed; therefore, you cannot assume a certain retention duration when writing the function business code.


## Concurrency Scale-out

When a request arrives, but no concurrent instance for that version is available, a new concurrent instance is automatically launched and initialized for it. This is called elastic concurrency scale-out, and its speed limit is called **function burst**.

The **default upper limit of scale-out speed (function burst) per region under each account is 500 instances/minute**, that is, up to 500 new concurrent instances can be started in one minute for all functions in this region. If the limit is hit in one minute, no more new instances will be started until the minute elapses, during which a over-limit error (429 ResourceLimit) occurs if new scale-out requests are initiated. For more information, see [Function Status Code](https://intl.cloud.tencent.com/document/product/583/35311).

For example, the concurrency quota of an account in the Guangzhou region is 1,000 concurrent instances by default for a 128 MB function, and if many requests arrive, 500 concurrent instances can be started from 0 in the first minute. If there are still other requests to be processed, 500 more concurrent instances can be started to reach 1,000 instances in total in the second minute, until the number of concurrent instances is sufficient for the requests or reaches the upper limit.

Currently, the function burst of 500 instances/minute can meet the requirements in most business scenarios. If your business is limited by this scale-out speed, or you need to add namespace-level function burst management capabilities, you can select provisioned concurrency for prefetch or purchase a [function package](https://console.cloud.tencent.com/scf/buy?rid=1&ns=default) to increase the limit.

### Provisioned concurrency

Concurrent instances launched for elastic concurrency scale-out need to be initialized, which includes initialization of the runtime environment and the business code.
You can configure the **provisioned concurrency** to get concurrent instances ready in advance. **When the provisioned concurrency is configured, SCF will start the concurrent instances, and will not actively repossess the provisioned instances, so as to guarantee the number of concurrent instances.** If errors such as code memory leak occur on a concurrent instance, it will be replaced by a new one. For more information, see [Provisioned Concurrency](https://intl.cloud.tencent.com/document/product/583/37704).

### Concurrency service level

#### Concurrency scale-out limit
| Limit on Concurrency Scale-out | Default Limit | Additional Quota Available for Application |
|-|---------|---------|
| Elastic concurrency scale-out speed limit (function burst) | 500 concurrent instances/minute | Concurrency scale-out speed at the 10,000 concurrent instances/minute level is supported, which you can get by purchasing a function package. |
| Provisioned concurrency scale-out speed limit (provisioned burst) | 100 concurrent instances/minute | The speed of starting provisioned concurrency can be automatically adjusted according to business conditions. |


At the region level, the function burst is limited to 500 concurrent instances/minute by default. For example, if you need 50,000 concurrent instances, it will take 50000/500 = 100 minutes to complete the scale-out at the maximum function burst speed. If you need to increase function burst, you can directly purchase a [function package](https://console.cloud.tencent.com/scf/buy?rid=1&ns=default). SCF will adjust the provisioned burst based on your business, which is 100 concurrent instances/minute by default.

#### Concurrent function quota
SCF provides concurrency management capabilities at the function granularity by default for you to flexibly control the concurrency of different functions. Each account has a limit on the quota of total concurrent functions in different regions as detailed below. If you want to increase the quotas or add concurrency quota management capabilities at the namespace granularity, you can directly purchase a [function package](https://console.cloud.tencent.com/scf/buy?rid=1&ns=default).


<table>
<th></th>
<th>Region</th>
<th>Default Quota</th>
<th >Additional Quota Available for Application</th>
<tr>
<td rowspan=2>Concurrent function quota</td>
<td>Guangzhou, Shanghai, Beijing, Chengdu, and Hong Kong (China)</td>
<td>128,000 MB</td>
<td rowspan=2>At the one million MB level, which can be increased by purchasing a function package</td>
</tr>
<tr>
<td>Mumbai, Singapore, Tokyo, Toronto, Silicon Valley, Frankfurt, Shenzhen Finance, and Shanghai Finance</td>
<td>64,000 MB</td>
</td>
</tr>
</table>      


 




## Concurrency Management

SCF provides concurrency management capabilities at the function granularity. For more information, see [Concurrency Management System](https://intl.cloud.tencent.com/document/product/583/39464).


### Concurrent memory and concurrency

To help you manage concurrency more precisely, the SCF concurrency quota is calculated by memory; for example, a 256 MB concurrency quota represents one concurrent instance with 256 MB memory or two instances with 128 MB memory each.

### Reserved quota

What a reserved quota does:

- The reserved quota is the upper limit of the concurrency quota for all versions of this function. The sum of the concurrency quotas of all versions cannot exceed this limit.
- The concurrency quota is allocated **exclusively** to this function and will not be shared by other functions.


## Concurrency Monitoring

A concurrent instance is marked as running when it’s processing requests. In SCF monitoring information, you can query the running concurrent instances of a function, a specific function version, or an alias. Because of the time difference between function execution and data collection, if a function has a large number of concurrent instances running in a very short time, the current monitoring data may not be completely accurate.



## Use Cases

By using reserved quota and provisioned concurrency together, you can flexibly allocate resources among multiple functions and warm up functions as needed.

### Shared quota

If nothing is configured, all functions share the account quota by default. When the requests to a function increase, it can make full use of the unused quota to prevent overrun errors.

### Guaranteed concurrency

For functions used for key business, a high request success rate is required. We can set up the reserved quota to allocate dedicated resources for the function, so as to guarantee the concurrency reliability and avoid overruns caused by concurrency preemption by multiple functions.

### Provisioned concurrency

If a function is sensitive to cold start, the code initialization process takes a long time, or many libraries need to be loaded, then you can set the provisioned concurrency for a specific function version to start function instances in advance and ensure smooth execution.
