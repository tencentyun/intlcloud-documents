Concurrency refers to the number of requests that can be processed by a function concurrently at a moment. If it can be sustained by other services of your business, you can increase the function concurrency from several to tens of thousands with simple configuration.

## How Concurrency Works

When a function is invoked, SCF will assign a concurrent instance to process the request or event. After the function code is executed and its response is returned, the instance will process other requests. If all instances are running when a request arrives, SCF will assign a new concurrent instance.

SCF follows the execution logic that one concurrent instance processes only one event at any time so as to ensure the processing efficiency and stability of each event.

### Concurrent processing for async invocations

Async events will first enter a queue on the SCF platform, where they will be processed in a FIFO manner. The system will select an appropriate concurrency processing method based on the conditions such as queue length and current number of concurrent instances of the function to pull sufficient concurrent instances and process the events in sequence.

If an async invocation fails, SCF will retry according to certain rules. For more information, please see [Error Types and Retry Policies](https://intl.cloud.tencent.com/document/product/583/34383).

### Concurrent processing for sync invocations

After sync events arrive at the SCF platform, the platform will check whether there are any idle concurrent instances, and if so, the events will be immediately sent to instances for processing; otherwise, the platform will start new concurrent instances to process them.

If a sync invocation fails, you need to retry by yourself.




### [Concurrency calculation](id:computing)
SCF concurrency refers to the number of requests or invocations processed by the function code at a time, which can be estimated according to the following formula:

Concurrency = request rate * function execution duration = QPS * average time per request

You can view the average time per request in **execution duration** in the monitoring data.
For example, if the QPS of a business is 2,000, and the average time per request is 0.02 seconds, then the concurrency during function execution will be 2000 * 0.02 = 40.




## Concurrent Instance Reuse and Repossession

After a concurrent instance processes a request event, it will not be repossessed immediately; instead, it will be retained for a certain period of time for reuse. During the retention duration, if there are new request events that need to be processed, the retained concurrent instance will be used first, so the events can be processed quickly with no need to start new concurrent instances.

After the retention duration elapses, if there are no requests that need to be processed by the instance, the SCF platform will repossess it. For low concurrency scenarios, no retention duration is set, and the platform will enable the smart repossession mechanism for resource repossession.

The concurrent instance retention duration is dynamically adjusted by the SCF platform as needed; therefore, you cannot assume a certain retention duration when writing the function business code.


## Concurrency Expansion

If a request arrives, but no concurrent instances for that version can process it, the SCF platform will start a new concurrent instance for processing. After initialization, the new instance can process events, which is called expansion by elastic concurrency.

The **maximum expansion speed of new concurrent instances in a region under one account is 500 instances/minute by default**, that is, up to 500 new concurrent instances can be started in one minute. If the limit is reached in one minute, no more new instances will be started until the minute elapses, during which a limited expansion error (429 ResourceLimit) will occur if new instance expansion requests are initiated. For more information, please see [Function Status Code](https://intl.cloud.tencent.com/document/product/583/35311).

For example, the concurrency quota of an account in the Guangzhou region is 1,000 concurrent instances by default for a 128 MB function, and if many requests arrive, 500 concurrent instances can be started from 0 in the first minute. If there are still other requests to be processed, 500 more concurrent instances can be started to reach 1,000 instances in total in the second minute, until the number of concurrent instances is sufficient for the requests or reaches the upper limit.

The elastic concurrency expansion speed of 500 instances per minute can meet the requirements in most business scenarios. If your business is limited by this speed, please select provisioned concurrency for prefetch or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to increase the limit.

### Provisioned concurrency

Concurrent instances in elastic concurrency expansion in the SCF platform need to be initialized, which includes initialization of the runtime environment and the business code.
You can use the **provisioned concurrency** feature to configure concurrent instances in advance. **The SCF platform will start the concurrent instances after you configure them and will not actively repossess the provisioned instances, so as to guarantee a certain number of concurrent instances as much as possible.** If errors such as code memory leak occur on a concurrent instance, the SCF platform will replace it with a new instance. For more information, please see [Provisioned Concurrency](https://intl.cloud.tencent.com/document/product/583/37704).

### Concurrency service level

#### Elastic concurrency expansion limit
| Individual User | Organizational User | Additional Quota Available for Application |
|---------|---------|---------|
| Elastic concurrency expansion limit | 500 concurrent instances/minute | 1,000 concurrent instances/minute | Concurrency expansion speed at the 10,000 concurrent instances/minute level is supported, which you can apply for by submitting a ticket. |

At the region level, the elastic concurrency expansion speed is limited to 500 concurrent instances/minute for individual users and 1,000 concurrent instances/minute for organizational users by default. For example, if you need 100,000 concurrent instances, it will take 100000/1000 = 100 minutes to complete the expansion at the maximum elastic concurrency expansion speed. If you need to increase the quotas, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

#### Concurrency quota
<table>
<th>Region</th>
<th>Individual User</th>
<th>Organizational User</th>
<th>Additional Quota Available for Application</th>
<tr>
<td rowspan=2>Concurrency quota</td>
<td>Guangzhou, Shanghai, Beijing, Chengdu, and Hong Kong (China)</td>
<td>128,000 MB</td>
<td>256,000 MB</td>
</tr>
<tr>
<td>Mumbai, Singapore, Tokyo, Toronto, Silicon Valley, Frankfurt, Shenzhen Finance, and Shanghai Finance</td>
<td>64,000 MB</td>
<td>128,000 MB</td>
</td>
</tr>
</table>      


Each account has concurrency restrictions at the region level, and you cannot modify the regional quotas. The SCF platform configures different concurrency quotas in different regions for individual and organizational users as detailed in the table. If you need to increase the quotas, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.





## Concurrency Management

The SCF platform provides concurrency management capabilities at the function granularity for you to flexibly control the concurrency of different functions. For more information, please see [Concurrency Management System](https://intl.cloud.tencent.com/zh/document/product/583/39464).


Each account has a total concurrency quota limit at the region level. The default value is 128,000 MB or 64,000 MB. For more information, please see [Quota Limits](https://intl.cloud.tencent.com/document/product/583/11637). The concurrency quotas between regions are independent of each other.

### Concurrent memory and concurrency

To help you manage concurrency more precisely, the SCF concurrency quota is calculated by memory; for example, a 256 MB concurrency quota represents one concurrent instance with 256 MB memory or two instances with 128 MB memory each.

### Reserved quota

When you set a reserved quota for a function, it will have the following two effects:

- The reserved quota is the **upper limit of the concurrency quota of this function**. The sum of the concurrency quotas of all versions is less than or equal to the reserved quota.
- After the concurrency quota is allocated to this function, it will be **exclusive to** this function and will no longer be provided to other functions.


## Concurrency Monitoring

When a concurrent instance of a function is processing actual requests, it will be marked as running concurrent instance. In SCF monitoring information, you can query the running concurrent instances of a function, a specific function version, or an alias. As there are certain intervals in running instance information collection, if a function's execution time is very short and its number of concurrent instances is high, the current monitoring data may not be completely accurate.



## Use Cases

By using reserved quota and provisioned concurrency together, you can flexibly allocate resources among multiple functions and warm up functions as needed.

### Shared quota

If nothing is configured, all functions share the account quota by default. If a function generates a surge of business invocations, it can make full use of the unused quota to ensure that the surge will not cause overrun errors.

### Guaranteed concurrency

If the business features of a specific function are sensitive or critical, and you need to do your best to ensure a high request success rate, then you can use the reserved quota feature to this end. Reserved quota can give the function exclusive quota to guarantee the concurrency reliability and avoid overruns caused by concurrency preemption by multiple functions.

### Provisioned concurrency

If a function is sensitive to cold start, the code initialization process takes a long time, or many libraries need to be loaded, then you can set the provisioned concurrency for a specific function version to start function instances in advance and ensure smooth execution.
