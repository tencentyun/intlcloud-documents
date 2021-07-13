SCF uses concurrent instances (also called concurrency or instances) to process requests or events.

## Key Concepts

- **Concurrency quota**: the concurrency limit at the account or function level. It is set or adjusted in the form of memory size. The function’s running concurrent instances cannot exceed the concurrency quota. The actual number of concurrent instances that can be started is calculated by dividing the quota by the configured memory of the function.
-**Concurrent instance count**: the number of concurrent instances. Each concurrent instance can process one function event at any specific time point.
- **Account concurrency quota**: the concurrency quota of the current user account in a specific region.
- **Reserved concurrency quota**: the concurrency quota set for a specific function at the function level.
- **Provisioned concurrency**: the specific concurrency preset at the function version level. Once you configure the provisioned quota of a version, instances will start in advance and keep running.





## Concurrency Overview
Currently, a SCF concurrent instance processes only one event at a time. When the SCF platform receives and passes a request, regardless of sync or async, to the concurrent instance, only one event will be processed. The concurrent instance will start processing subsequent events or requests only after the current event is completed and returned to the instance.

In case of an async request, async events will first enter a queue on the SCF platform, where they will be processed in a FIFO manner. The system will select an appropriate concurrency processing method based on the conditions such as queue length and the current number of concurrent instances of the function to start sufficient concurrent instances and process the events in sequence.

In case of a sync request, after sync requests arrive at the SCF platform, the platform will check whether there are any idle concurrent instances, and if so, the events will be immediately sent to instances for processing; otherwise, the platform will start new concurrent instances to process them.




### Concurrency expansion
When concurrent instances of a function are insufficient to process request events, the SCF platform will start new ones to process them.

This expansion is subject to 500 instances per minute in a region for each account. If the limit is reached in one minute, no more new instances will be started until the minute elapses, during which initiating a new instance expansion request will return an error.

### Instance reuse
After a concurrent instance processes a request event, it will not be repossessed immediately; instead, it will be retained for a certain period of time. During the retention duration, if there are new request events that need to be processed, the retained concurrent instance will be used first, so the events can be processed quickly with no need to wait for starting new concurrent instances. The retention duration is dynamically adjusted by the SCF platform as needed, which cannot be specified in your business code snippets.


### Concurrency monitoring

When a concurrent instance of a function is processing actual requests, it will be marked as running concurrent instance. In SCF monitoring information, you can query the running concurrent instances of a function, a specific function version, or an alias. Because of the time difference between function execution and data collection, if a function has a large number of concurrent instances running in a very short time, the current monitoring data may not be completely accurate.


## Concurrency Limit and Control

Currently, SCF allows concurrency quota management at three levels:

```
Account concurrency
    |- Function reserved concurrency
```
>? The **version-level provisioned concurrency quota** is a capability that supports starting instances in advance, rather than quota management. For more information, see [Provisioned Concurrency](https://intl.cloud.tencent.com/document/product/583/37704).

### Account concurrency

Account concurrency quota refers to the total concurrency quota of a Tencent Cloud account in a specific region, which is reflected in the form of memory size. For more information, please see [Quota Limits](https://intl.cloud.tencent.com/document/product/583/11637).

The account concurrency quota is currently 128,000 MB in each region, which supports 1,000*128 MB concurrent instances. When the configured function memory increases, the number of concurrent instances will decrease accordingly. For example, if the function memory is configured to 256 MB, the number of concurrent instances will become 500.

The account concurrency quota is region-specific; that is, the running status of instances in one region does not affect that of instances in another region.

By default, the account concurrency quota is shared by all functions in the current region. This means that at any specific time point, the sum of actually running concurrent instances of all functions can reach up to the account concurrency quota.

In case of insufficient account concurrency quota, function invocation may fail and return an overrun (OverQuota) error. In this case, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to raise the account quota.

The available quota at the account level, i.e., the concurrency quota shared by all functions, decreases with the configuration of the reserved concurrency quota, to an extreme of 12,800 MB. This means a quota of 12,800 MB will be reserved at the account level for functions with no reserved or provisioned concurrency configured.

### Function reserved concurrency

Reserved concurrency is a function-level concurrency quota, and only used for the given function. Currently, it is configured in the form of memory size. The sum of the actually running concurrent instances of all versions of a function can reach up to the reserved concurrency quota of the function.

You can configure the reserved concurrency for a function to ensure the execution of concurrent instances without sharing the account concurrency quota with other functions. The reserved concurrency will take up the account concurrency quota, and other functions with no reserved concurrency quota configured will share the remaining concurrency quota of the account.

In addition, the reserved concurrency quota is also the upper limit of the function's concurrent instances. The sum of concurrently running instances of specific versions cannot exceed the reserved concurrency quota. When the reserved concurrency quota is used up, function invocation may fail and return an overrun (OverQuota) error. In this case, you can raise the reserved concurrency quota.

For more information on the function reserved concurrency quota, please see [Reserved Concurrency](https://intl.cloud.tencent.com/document/product/583/39464).



## Use Cases

By using reserved concurrency and provisioned concurrency together, you can flexibly allocate resources among multiple functions and warm up functions as needed.

### Shared quota

If nothing is configured, all functions share the account quota by default. If a function generates a surge of business invocations, it can make full use of the unused quota to ensure that the surge will not cause overrun errors.

### Guaranteed concurrency

If the business features of a specific function are sensitive or critical, and you need a high request success rate, then you can configure the reserved concurrency quota. Reserved concurrency is only used for a given function to guarantee the concurrency reliability and avoid overruns caused by concurrency preemption by multiple functions. In addition, if the function is expected to have a higher number of concurrent instances, then you also need to set a higher reserved quota.

### Provisioned concurrency

If a function is sensitive to cold start, the code initialization process takes a long time, or many libraries need to be loaded, then you can set the provisioned concurrency for a specific function version to start function instances in advance and ensure smooth execution.
