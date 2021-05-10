## Container Model of Function Runtime

SCF will execute a function on your behalf when an event is triggered, allocate resources based on your configuration information (such as memory size), and launch and manage the container (i.e., the execution environment of the function). The SCF platform is responsible for the creation, management, and deletion of all function runtime containers, and you have no permissions to manage them.


It takes time for the container to start, which adds some delay each time a function is invoked. However, this delay is usually only perceivable when the function is invoked for the first time, updated, or invoked again after being idle for a long time, because the platform tries to reuse the container for subsequent invocations in order to minimize the container launch delay. After the function is invoked, the container will be retained for a period of time according to the platform conditions for use in the next invocation, during which a new invocation will directly reuse the container.

The significance of the container reuse mechanism lies in:
- All declarations outside the [execution method](https://intl.cloud.tencent.com/document/product/583/9210) part in your code remain initialized and can be reused directly when the function is invoked again. For example, if a database connection is established in your function code, the original connection can be used directly when the container is reused. You can add logic to your code to check whether a connection already exists before creating a new one.
- Each container provides some disk space in the `/tmp` directory. The contents of this directory are retained when the container is retained, providing a temporary cache that can be used for multiple invocations. It is possible to use the contents of the disk directly when the function is invoked again. You can add extra code to check whether such data is in the cache.

>! Do not assume that the container is always reused in the function code, because reuse is related to the single actual invocation, and it cannot be guaranteed whether a new container will be created or an existing one will be reused.

## Temporary Disk Space

Each function has a temporary disk space of 512 MB (`/tmp`) during execution. You can perform certain read and write operations on the space in the execution code or create subdirectories, but this part of data may **not** be retained after function execution is completed. Therefore, if you need to persistently store the data generated during execution, please use COS or external persistent storage services such as Redis/Memcached.

## Invocation Types

The SCF platform supports both sync and async invocations of functions.

### Sync invocation
 Sync invocation will wait for the execution result of the function after the invocation request is sent.

[](id:asynchronous)
### Async invocation
- Async invocation will only send the request and get the request ID of the current request but not wait for the result.
- When an async invocation occurs, the async event will be placed in the async queue built in SCF and then consumed by the event execution function in the async queue. Async queues have the following restrictions:
 - Async queues are at the trigger level, and one function trigger has one queue.
 - An async event can be retained in a queue for up to 6 hours.
 - There can be up to 100,000 messages in an async queue.
- The retry policy may vary by async queue. For more information, please see [Retry Policy](https://intl.cloud.tencent.com/document/product/583/34383).


### Defining function invocation type
The invocation type is independent of the configuration of the function itself and can only be controlled when the function is invoked.

In the following invocation scenarios, you can freely define the invocation type of the function:
- The SCF function is invoked by a written application. If you need to make a sync invocation, pass in the `invokeType=RequestResponse` parameter to the `InvokeFunction` API; if you need to make an async invocation, pass in the `invokeType=Event` parameter.
- The SCF function is manually invoked (with API or CLI) for testing. The parameters for the invocation are the same as above.

If you use another Tencent Cloud service as the event source, the invocation type of the cloud service is predefined.

* Sync invocation: by [API Gateway trigger](https://intl.cloud.tencent.com/document/product/583/12513) and [CKafka trigger](https://intl.cloud.tencent.com/document/product/583/17530), for example.
* Async invocation: by [COS timer trigger](https://intl.cloud.tencent.com/document/product/583/9707), [timer trigger](https://intl.cloud.tencent.com/document/product/583/9708), and [CMQ topic timer trigger](https://intl.cloud.tencent.com/document/product/583/11517), for example.







## Usage Restrictions

For the restrictions on function usage quotas and related environments, please see [Quota Limits](https://intl.cloud.tencent.com/document/product/583/11637).

## Function Concurrency

The function concurrency is the number of executions of the function code in any given period of time. For the current SCF function, the request is executed once each time an event is published. Therefore, the number of events (i.e., requests) published by the trigger affects the function concurrency. You can use the formula below to estimate the total number of concurrent function instances.

```
Requests per second * function execution duration (in seconds) 
```

For example, for a function that handles COS events, if the function takes an average of 0.2 seconds (i.e., 200 milliseconds) for execution and COS publishes 300 requests per second to the function, then 300 \* 0.2 = 60 function instances will be generated simultaneously.


## Concurrency Restrictions

Currently, SCF has a limit on the amount of concurrency for each function. You can view the limit for the current function in [Quota Limits](https://intl.cloud.tencent.com/document/product/583/11637). You can [contact us](https://intl.cloud.tencent.com/document/product/583/9712) to increase the limit.

If an invocation causes the function concurrency to exceed the default limit, the invocation will be blocked and not executed by SCF. Restricted invocations are handled differently depending on the function invocation type:
- Sync invocation: if the function is restricted when invoked synchronously, a 432 error will be returned directly.
- Async invocation: if the function is restricted when invoked asynchronously, SCF will [automatically retry](https://intl.cloud.tencent.com/document/product/583/34383) the restricted event according to a certain policy.

## Execution Environment and Available Libraries

The current SCF execution environment is built based on the following:
- Standard CentOS 7.2

If you need to include executable binaries, dynamic libraries, or static libraries in your code, make sure that they are compatible with this execution environment.
Based on different language environments, there are base libraries and additional libraries installed for the corresponding language in the SCF execution environment. You can view the additional libraries installed in the environment in the descriptions of each language:
- [Python](https://intl.cloud.tencent.com/document/product/583/11061)
- [Node.js](https://intl.cloud.tencent.com/document/product/583/11060)
- [Go](https://intl.cloud.tencent.com/document/product/583/18032)
- [PHP](https://intl.cloud.tencent.com/document/product/583/17531)
- [Java](https://intl.cloud.tencent.com/document/product/583/12214)


