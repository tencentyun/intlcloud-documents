A function is the basic unit of management and operation in SCF, which usually consists of a series of configuration items and executable code/packages. You can trigger a function through APIs. You can also pass different events to a function through different triggers to trigger it for event processing.

## Relevant Concepts of Function

#### Regions
A function resource must belong to a certain region. For regions supported by SCF, see [Billing Overview](https://intl.cloud.tencent.com/document/product/583/17299).

#### Namespace
A function resource must be created under a certain namespace in a certain region. Each region has a `default` namespace. You can also create namespaces, whose names cannot be modified after creation.

#### Function name
It is the unique identifier of a function, must be unique under the same namespace, and cannot be modified after creation.


#### Function type
SCF supports two function types: event-triggered function and HTTP-triggered function.
  - Event-triggered functions are triggered by events in a specified format, such as scheduled triggering events and COS triggering events. For more information on the event structure, see [Trigger Overview](https://intl.cloud.tencent.com/document/product/583/9705).
  - HTTP-triggered functions focus on optimizing web services and can directly accept and process HTTP requests. For more information, see [Function Overview](https://intl.cloud.tencent.com/document/product/583/40688).

#### Time zone
SCF uses the UTC time by default, which you can modify by configuring the `TZ` environment variable. After you select a time zone, the `TZ` environment variable corresponding to the time zone will be added automatically.

#### Runtime environment
Execution environment of the function code. Currently, SCF supports [Python](https://intl.cloud.tencent.com/document/product/583/40323), [Node.js](https://intl.cloud.tencent.com/document/product/583/11060), [PHP](https://intl.cloud.tencent.com/document/product/583/17531), [Java](https://intl.cloud.tencent.com/document/product/583/12214), [Go](https://intl.cloud.tencent.com/document/product/583/18032), [Custom Runtime](https://intl.cloud.tencent.com/document/product/583/38129), and [image deployment](https://intl.cloud.tencent.com/document/product/583/41076).

#### Function execution method
The execution method specifies the starting file and function while invoking the function. There are three ways as follows:
  - For Go programming, use the <b>"[FileName]"</b> format, such as `main`.
  - For Python, Node.js, or PHP programming, use the <b>"[FileName].[FunctionName]"</b> format, such as `index.main_handler`.
<dx-alert infotype="explain" title="">
Note that FileName does not include the file name extension, and FunctionName is the name of the entry function. Make sure that the file name extension matches the programming language. For example, for Python programming, the file name extension is `.py`, and for Node.js programming, the file name extension is `.js`.   
</dx-alert>
  - For Java programming, use the <b>"[package].[class]::[method]"</b> format, such as `example.Hello::mainHandler`.


#### Function description
It is used to record information such as the purpose of the function, which is optional.


## Relevant Configurations of Function


In addition to the above configuration items, you can also modify the following configuration items for function execution by editing the function configuration in the console or [updating function configuration](https://intl.cloud.tencent.com/document/product/583/19806):


#### Resource type
The computing power supported by SCF includes CPU and GPU.

#### Resource specification
It sets the specifications of resources, such as different memory sizes for CPU and different card types for GPU.

#### Initialization timeout period
Maximum initialization duration of the function between 3 and 300 seconds (90 seconds for image deployment-based functions and 60 seconds for other functions by default).
<dx-alert infotype="notice" title="">
- The function initialization phase includes the preparations of function code, image, layer, and other relevant resources and execution of the main process code of the function. If your function has a larger image or complex business logic, increase the initialization timeout period appropriately.
- The initialization timeout period only takes effect in the scenario where the triggered instance is cold started for invocation.
- The client waiting time is better to be slightly larger than the sum of the initialization timeout period and the execution timeout period.
</dx-alert>

#### Execution timeout period
Maximum execution duration of the function between 1 and 900 seconds (3 seconds by default).

#### Environment variable
It can be defined in the configuration and obtained from the environment when the function is executed. For more information, see [Environment Variables](https://intl.cloud.tencent.com/document/product/583/32748).

#### Execution role
It grants the corresponding permissions of the policy contained in it to the function. For more information, see [Role and Authorization](https://intl.cloud.tencent.com/document/product/583/38176). For example, to execute the action of writing an object into COS in the function code, you should configure an execution role with the permission to write COS.

#### Log configuration
It delivers function invocation logs to the specified log topic. For more information, see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/39777).

#### Network configuration
It configures the function network access permissions. For more information, see [Network Configuration Management](https://intl.cloud.tencent.com/document/product/583/38377).
  - Public network: It is enabled by default. The function cannot access public network resources after it is disabled.
  - Fixed outbound IP: After it is enabled, the platform will assign a fixed public network outbound IP to the function.
  - VPC: After it is enabled, the function can access resources in the same VPC.

#### File system
After it is enabled, the function can access resources of the mounted file system. For more information, see [Mounting CFS File System](https://intl.cloud.tencent.com/document/product/583/37497).

#### Execution configuration 
The execution configuration includes async execution, status tracking, and async execution event management. For more information, see [Execution Configuration](https://intl.cloud.tencent.com/document/product/583/39466).
  - Async execution: After it is enabled, the function execution timeout period can be up to 24 hours. It cannot be modified after function creation.
  - Linkage trace: It can be enabled only for async execution. When it's enabled, it will keep the logs of real-time status of response for async function events. You can query and stop the event and check the related statistics. Data of event status will be retained for three days.


#### Async invocation configuration
[Async invocation configuration](https://intl.cloud.tencent.com/document/product/583/39851): You can use this configuration item to set the retry policy for async invocation. You can also configure the [dead letter queue](https://intl.cloud.tencent.com/document/product/583/39704) to collect error event information and analyze the failure cause.


#### Application performance monitoring
After it is enabled, SCF will report the basic execution duration of the function to the specified APM system. You can also instrument the function code for custom reporting. This helps you better track and monitor the execution of the function.

#### DNS configuration
In SCF use cases, DNS delays may cause function execution timeouts, affecting the normal business logic. In case of frequent function invocations, the resolution of the DNS server may exceed the frequency limit, which also leads to function execution failures. SCF provides the DNS cache configuration to solve these problems, which can improve the DNS efficiency and mitigate the impact of various factors such as network jitter on the DNS success rate. For more information, see [DNS Caching Configuration](https://intl.cloud.tencent.com/document/product/583/47182).




## Executable Operations for a Function

- [Creating function](https://intl.cloud.tencent.com/document/product/583/19806): Creates a function.
- [Updating function](https://intl.cloud.tencent.com/document/product/583/19806):
  - Updating function configuration: Updates the configuration items of the function.
  - Updating function code: Updates the execution code of the function.
- [Getting details](https://intl.cloud.tencent.com/document/product/583/19809): Gets function configuration, trigger, and code details.
- [Testing function](https://intl.cloud.tencent.com/document/product/583/14572): Triggers the function in a sync or async manner as needed.
- [Getting log](https://intl.cloud.tencent.com/document/product/583/19810): Gets the log of function execution and output.
- [Deleting function](https://intl.cloud.tencent.com/document/product/583/19807): Deletes a function that is no longer needed.
- Copying function: Copies a function to the specified region, name, and configuration.

Function trigger-related operations include:

- [Creating trigger](https://intl.cloud.tencent.com/document/product/583/31441): Creates a trigger.
- [Deleting trigger](https://intl.cloud.tencent.com/document/product/583/31442): Deletes an existing trigger.
- [Enabling/Disabling trigger](https://intl.cloud.tencent.com/document/product/583/31443): Disables a trigger to temporarily prevent a function from being triggered by an event occurring at the event source.
