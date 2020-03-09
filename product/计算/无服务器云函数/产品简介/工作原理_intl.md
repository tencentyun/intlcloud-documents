## Container Model of the Function Runtime

SCF will execute a function on your behalf when an event is triggered, allocate resources based on your configuration information (such as memory size), and launch and manage the container (i.e., the execution environment of the function). The SCF platform is responsible for the creation, management, and deletion of all function runtime containers, and you have no permissions to manage them.

It takes some time to launch a container, which increases the delay slightly each time the function is called. However, this delay is usually only noticeable when the function is called for the first time, updated, or idle for a long time, because the platform tries to reuse the container for subsequent calls in order to minimize this launch delay. After the function is called, the container is retained for a period of time for use in the next call. Calls during this period will directly reuse the retained container.

The significance of the container reuse mechanism lies in:
- All declarations outside the [execution method](https://cloud.tencent.com/document/product/583/9210#.E6.89.A7.E8.A1.8C.E6.96.B9.E6.B3.95) part in your code remain initialized and can be reused directly when the function is called again. For example, if a database connection is established in your function code, the original connection can be used directly when the container is reused. You can add logic to your code to check whether a connection already exists before creating a new one.
- Each container provides some disk space in the `/tmp` directory. The contents of this directory are retained when the container is retained, providing a temporary cache that can be used for multiple calls. It is possible to use the contents of the disk directly when the function is called again. You can add extra code to check whether such data is in the cache.

>! Do not assume that the container is always reused in the function code, because reuse is related to the single actual call, and it cannot be guaranteed whether a new container will be created or an existing one will be reused.

## Temporary Disk Space

Each function has a temporary disk space of 512 MB (`/tmp`) during execution. You can perform certain read and write operations on the space in the execution code, but this part of the data may *not* be retained after function execution is completed. Therefore, if you need to persistently store the data generated during execution, please use COS or external persistent storage services such as Redis/Memcached.

## Call Types

The SCF platform supports both sync and async calls of functions. The call type is independent of the configuration of the function itself and can only be controlled when the function is called.
- Sync call will wait for the execution result of the function after the call request is sent.
- Async call will only send the request and get the request ID of the current request, but not wait for the result.

In the following call scenarios, you can freely define the call type of the function:
- The SCF function is called by a written application. If you need to make a sync call, pass in the parameter `invokeType=RequestResponse` to the InvokeFunction API; if you need to make an async call, pass in the parameter `invokeType=Event`.
- The SCF function is manually called (using API or TCCLI) for testing. The parameters for the call are the same as above.

However, if you use another Tencent Cloud service as the event source, the call type of the cloud service is predefined, and you cannot freely specify the call type in this case. For example, COS and timer triggers always call SCF functions asynchronously.

## Usage Restrictions

For the restrictions on function usage quotas and related environments, see [Quota Limits](https://cloud.tencent.com/document/product/583/11637).

## Function Concurrency

The amount of function concurrency is the number of executions of the function code in any given period of time. For the current SCF function, the request is executed once each time an event is published. Therefore, the number of events (i.e., requests) published by the trigger affects the amount of function concurrency. You can use the formula below to estimate the total number of concurrent function instances.

```
Requests per second * function execution duration (in seconds) 
```

For example, for a function that handles COS events, if the function takes an average of 0.2 seconds (i.e., 200 milliseconds) for execution and COS publishes 300 requests per second to the function, then 300 \ * 0.2 = 60 function instances will be generated simultaneously.


## Concurrency Restrictions

Currently, SCF has a limit on the amount of concurrency for each function. You can view the limit for the current function in [Quota Limits](https://cloud.tencent.com/document/product/583/11637). You can [contact us](https://cloud.tencent.com/document/product/583/9712) to increase the limit value.

If a call causes the function concurrency to exceed the default limit, the call will be blocked and not executed by SCF. Restricted calls are handled differently depending on the function call type:
- Sync call: If the function is restricted when called synchronously, a 429 error will be returned directly.
- Async call: If the function is restricted when called asynchronously, SCF will automatically retry the restricted event at a fixed frequency for a certain period of time.
 
## Retry Mechanism

In case that your function fails because it exceeds the maximum amount of concurrency or the internal resources on the platform are insufficient, if the function is called synchronously, an error will be returned directly (see the concurrency restrictions above). If the function is called asynchronously by an internal cloud service, the call will automatically enter a retry queue and SCF will automatically retry the call.

## Execution Environment and Available Libraries

The current SCF execution environment is built based on the following:
- Standard CentOS 7.2

If you need to include executable binaries, dynamic libraries, or static libraries in your code, make sure that they are compatible with this execution environment.
Based on different language environments, there are base libraries and additional libraries installed for the corresponding language in the SCF execution environment. You can view the additional libraries installed in the environment in the descriptions of each language:
- [Python](https://intl.cloud.tencent.com/document/product/583/11061)
- [Node.js](https://intl.cloud.tencent.com/document/product/583/11060)
- [Golang](https://cloud.tencent.com/document/product/583/18032)
- [PHP](https://intl.cloud.tencent.com/document/product/583/11060)
- [JAVA](https://cloud.tencent.com/document/product/583/12214)


