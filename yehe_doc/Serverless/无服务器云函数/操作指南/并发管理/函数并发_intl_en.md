SCF uses concurrent instances (also called concurrency or instances) to process requests or events.

## Concepts
- **Concurrency quota**: the quota used to configure concurrency limit at the account, function, or version level. It is set or adjusted in the form of memory size. The function instances running simultaneously cannot exceed the concurrency quota. The actual number of concurrent instances that can be started is calculated by dividing the quota by the configured memory of the function.
-**Concurrent instance count**: the number of concurrent instances. Each concurrent instance can process one function event at any specific time point.
- **Account concurrency quota**: the concurrency quota of the current user account in a specific region.
- **Reserved concurrency quota**: the concurrency quota set for a specific function at the function level.
- **Provisioned concurrency**: the specific concurrency preset at the function version level. Instances in the provisioned concurrency will be started in advance and keep running continuously after the provisioned concurrency is configured.





## Concurrency Overview
Currently, an SCF concurrent instance processes only one event at a time. No matter whether it is a sync or async request, when the SCF platform receives a request and passes it to the concurrent instance for processing, this logic always applies. Subsequent events or requests will not be received by the instance if it is still processing the current event and has not received the returned information.

In case of async request, async events will first enter a queue on the SCF platform, where they will be processed in a FIFO manner. The system will select an appropriate concurrency processing method based on the conditions such as queue length and current number of concurrent instances of the function to pull sufficient concurrent instances and process the events in sequence.

In case of a sync request, after sync requests arrive at the SCF platform, the platform will check whether there are any idle concurrent instances, and if so, the events will be immediately sent to instances for processing; otherwise, the platform will start new concurrent instances to process them.




### Concurrency expansion
If the current number of concurrent instances of a function is insufficient to process request events, the SCF platform will start new ones to process them.

The maximum expansion speed of new concurrent instances in a region under one account is 500 instances/minute, that is, up to 500 new concurrent instances can be started in one minute. If the limit is reached in one minute, no more new instances will be started until the minute elapses, during which a limited expansion error will occur if new instance expansion requests are initiated.

### Instance reuse
After a concurrent instance processes a request event, it will not be repossessed immediately; instead, it will be retained for a certain period of time. During the retention duration, if there are new request events that need to be processed, the retained concurrent instance will be used first, so the events can be processed quickly with no need to wait for start of new concurrent instances. The concurrent instance retention duration is dynamically adjusted by the SCF platform as needed; therefore, you cannot assume a certain retention duration when writing the function business code.


### Concurrency monitoring

When a concurrent instance of a function is processing actual requests, it will be marked as running concurrent instance. In SCF monitoring information, you can query the running concurrent instances of a function, a specific function version, or an alias. As there are certain intervals in running instance information collection, if a function's execution time is very short and its number of concurrent instances is high, the current monitoring data may not be completely accurate.


## Concurrency Limit and Control

Currently, SCF allows concurrency quota management at three levels:

```
Account concurrency
    |- Function reserved concurrency
        |- Version provisioned concurrency
```

### Account concurrency

Account concurrency quota refers to the concurrency quota of a Tencent Cloud account in a specific region, which is reflected in the form of memory size. For more information, please see [Limits](https://intl.cloud.tencent.com/document/product/583/11637).

The current concurrency quota at the account level in a region is 128,000 MB, which can sustain the concurrent executions of 1,000 function instances with the 128 MB configuration. When the configured function memory increases, the number of instances that can run simultaneously will decrease accordingly. For example, if the configured function memory is changed to 256 MB, the number of instances that can run simultaneously will become 500.

Account concurrency quota is effective separately in each region, that is, the running status of instances in one region does not affect that of instances in another region.

By default, the account concurrency quota is shared by all functions in the current region. This means that at any specific time point, the sum of actual concurrently running instances of all functions can reach up to the concurrency quota of the account.

In case of insufficient account concurrency quota, an error may occur while invoking functions, which is reflected as an overrun (OverQuota) error. In this case, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for increasing the account quota.

At the same time, the available quota of the account, i.e., the concurrency quota shared by functions, will be reduced to 12,800 MB at least when the reserved concurrency and provisioned concurrency are set. This means that the configurable quota at the account level will reserve 12,800 MB, which cannot be allocated to reserved concurrency or provisioned concurrency and will be used to run functions that don't have such quotas set.

### Function reserved concurrency

Reserved concurrency is the concurrency quota set at the function level. Currently, it is configured in the form of memory size. It is exclusive to the function, that is, the sum of the actual concurrently running instances of all versions of a function can reach up to the reserved concurrency quota of the function.

Setting the reserved concurrency for a function can guarantee the available concurrency quota for the function, which doesn't need to share the account concurrency quota with other functions. The set quota will be deducted from the account concurrency quota. Meanwhile, other functions that don't have the reserved concurrency quota set will share the remaining concurrency quota of the account.

In addition, the reserved concurrency quota is also the upper limit of the function's concurrent instances. The sum of concurrently running instances of specific versions cannot exceed the reserved concurrency quota. When the reserved concurrency quota is used up, an error may occur while invoking functions, which is reflected as an overrun (OverQuota) error. In this case, you can increase the reserved concurrency quota to increase the upper limit.

For more information on the function reserved concurrency quota, please see [Reserved Concurrency](https://intl.cloud.tencent.com/document/product/583/39464).


### Version provisioned concurrency

Provisioned concurrency is the concurrency set at the version level. Currently, it is configured in the form of memory size. For a version that has the provisioned concurrency configured, it will start instances after the configuration instead of waiting for the arrival of triggering events. This way, you can prepare computing resources in advance and reduce the duration for cold start and initialization of business code.

The configured provisioned concurrency value should be a multiple of the configured memory of the function version. The number of instances started in advance equals to "configured provisioned concurrency/configured version memory".

For more information on the version provisioned concurrency quota, please see [Provisioned Concurrency](https://intl.cloud.tencent.com/document/product/583/37704).

## Use Cases

By using reserved concurrency and provisioned concurrency together, you can flexibly allocate resources among multiple functions and warm up functions as needed.

### Shared quota

If nothing is configured, all functions share the account quota by default. If a function generates a surge of business invocations, it can make full use of the unused quota to ensure that the surge will not cause overrun errors.

### Guaranteed concurrency

If the business features of a specific function are sensitive or critical, and you need to do your best to ensure a high request success rate, then you can use the reserved concurrency quota feature to this end. Reserved concurrency can give the function exclusive quota to guarantee the concurrency reliability and avoid overruns caused by concurrency preemption by multiple functions. In addition, if the function is expected to have a higher number of concurrent connections, then you also need to set a higher reserved quota.

### Provisioned concurrency

If a function is sensitive to cold start, the code initialization process takes a long time, or many libraries need to be loaded, then you can set the provisioned concurrency for a specific function version to start function instances in advance and ensure smooth execution.
