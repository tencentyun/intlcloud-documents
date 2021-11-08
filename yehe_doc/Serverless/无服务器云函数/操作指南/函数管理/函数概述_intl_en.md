A function is the basic unit of management and operation in SCF, which usually consists of a series of configuration items and executable code/packages. You can trigger a function through APIs. You can also pass different events to a function through different triggers to trigger it for event processing.

## Relevant Concepts of Function

- Region: a function resource must belong to a certain region. For regions supported by SCF, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/583/17299).
- Namespace: a function resource must be created under a certain namespace in a certain region. Each region has a `default` namespace. You can also create namespaces, whose names cannot be modified after creation.
- Function name: it is the unique identifier of a function, must be unique under the same namespace, and cannot be modified after creation.
- Function type: SCF supports two function types: event-triggered function and HTTP-triggered function.
  - Event-Triggered functions are triggered by events in a specified format, such as scheduled triggering events and COS triggering events. For more information on the event structure, please see [Trigger Overview](https://intl.cloud.tencent.com/document/product/583/9705).
  - HTTP-Triggered functions focus on optimizing web services and can directly accept and process HTTP requests. For more information, please see [Function Overview](https://intl.cloud.tencent.com/document/product/583/40688).
- Runtime environment: execution environment of the function code. Currently, SCF supports [Python](https://intl.cloud.tencent.com/zh/document/product/583/40323), [Node.js](https://intl.cloud.tencent.com/document/product/583/11060), [PHP](https://intl.cloud.tencent.com/document/product/583/17531), [Java](https://intl.cloud.tencent.com/document/product/583/12214), [Go](https://intl.cloud.tencent.com/document/product/583/18032), [Custom Runtime](https://intl.cloud.tencent.com/document/product/583/38129), and [image deployment](https://intl.cloud.tencent.com/zh/document/product/583/41076).
- Function execution method: it specifies the starting file and function while invoking the function. There are three ways as follows:
  - For Go programming, use the **"[FileName]"** format, such as `main`.
  - For Python, Node.js, or PHP programming, use the **"[FileName].[FunctionName]"** format, such as `index.main_handler`.
  <dx-alert infotype="explain" title="">
  Please note that FileName does not include the file name extension, and FunctionName is the name of the entry function. Make sure that the file name extension matches the programming language. For example, for Python programming, the file name extension is `.py`, and for Node.js programming, the file name extension is `.js`. 
  </dx-alert>
  - For Java programming, use the **"[package].[class]::[method]"** format, such as `example.Hello::mainHandler`.
- Function description: used to record information such as the purpose of the function, which is optional.






## Relevant Configurations of Function


In addition to the above configuration items, you can also modify the following configuration items for function execution by editing the function configuration in the console or [updating function configuration](https://intl.cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/583/19806):
- Memory: amount of memory available for the function during execution. It ranges from 64 to 3,072 MB in increments of 128 MB starting from 128 MB (default value). The CPU processing capacity of a function is directly proportional to its configured memory. You can increase or decrease the memory to control the configured memory and CPU processing capacity allocated to the function.
- Initialization timeout period: maximum initialization duration of the function between 3 and 300 seconds (90 seconds for image deployment-based functions and 60 seconds for other functions by default).
<dx-alert infotype="notice" title="">
- The function initialization phase includes the preparations of function code, image, layer, and other relevant resources and execution of the main process code of the function. If your function has a larger image or complex business logic, please increase the initialization timeout period appropriately.
- The initialization timeout period only takes effect in the scenario where the trigger container is cold started for invocation.
- The client waiting time is better to be slightly larger than the sum of the initialization timeout period and the execution timeout period.
</dx-alert>
- Execution timeout period: maximum execution duration of the function between 1 and 900 seconds (3 seconds by default).
- Environment variable: it can be defined in the configuration and obtained from the environment when the function is executed.
- Execution role: it grants the corresponding permissions of the policy contained in it to the function. For more information, please see [Role and Authorization](https://intl.cloud.tencent.com/document/product/583/38176). For example, to execute the action of writing an object into COS in the function code, you should configure an execution role with the permission to write COS.
- Log configuration: it delivers function invocation logs to the specified log topic. For more information, please see [Log Search Guide](https://intl.cloud.tencent.com/zh/document/product/583/39777).
- Network configuration: it configures the function network access permissions. For more information, please see [Network Configuration Management](https://intl.cloud.tencent.com/document/product/583/38377).
  - Public network: it is enabled by default. The function cannot access public network resources after it is disabled.
  - Fixed outbound IP: after it is enabled, the platform will assign a fixed public network outbound IP to the function.
  - VPC: after it is enabled, the function can access resources in the same VPC.
- File system: after it is enabled, the function can access resources of the mounted file system.
- [Execution Configurations](https://intl.cloud.tencent.com/zh/document/product/583/39466):
  - Async execution: after it is enabled, the function execution timeout period can be up to 24 hours. It cannot be modified after function creation.
  - Linkage trace: it can be enabled only for async execution. When it's enabled, it will keep the logs of real-time status of response for async function events. You can query and stop the event and check the related statistics. Data of event status will be retained for three days.
- [Async invocation configuration](https://intl.cloud.tencent.com/document/product/583/34383): you can use this configuration item to set the retry policy for async invocation. You can also configure the [dead letter queue](https://intl.cloud.tencent.com/zh/document/product/583/39704) to collect error event information and analyze the failure cause.

  

## Executable Operations for a Function
- [Creating function](https://intl.cloud.tencent.com/document/product/583/19806): creates a function.
- [Updating function](https://cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/583/19806):
   - Updating function configuration: updates the configuration items of the function.
   - Updating function code: updates the execution code of the function.
- [Getting details](https://intl.cloud.tencent.com/document/product/583/19809): gets function configuration, trigger, and code details.
- [Testing function](https://intl.cloud.tencent.com/document/product/583/14572): triggers the function in a sync or async manner as needed.
- [Getting log](https://intl.cloud.tencent.com/document/product/583/19810): gets the log of function execution and output.
- [Deleting function](https://intl.cloud.tencent.com/document/product/583/19807): deletes a function that is no longer needed.




Function trigger-related operations include:

- [Creating trigger](https://intl.cloud.tencent.com/document/product/583/31441): creates a trigger.
- [Deleting trigger](https://intl.cloud.tencent.com/document/product/583/31442): deletes an existing trigger.
- [Enabling/Disabling trigger](https://intl.cloud.tencent.com/document/product/583/31443): disables a trigger to temporarily prevent a function from being triggered by an event occurring at the event source.

