In addition to the standard runtime environments for supported programming languages and versions, to satisfy personalized needs of function implementation in more custom programming languages and versions, SCF also provides the Custom Runtime service, which allows you to customize runtime environments. It can implement custom function runtime by opening up its capabilities, enable you to use any programming language on any version to write functions as needed, and implement global operations in function invocation, such as extension load, security plugin, and monitoring agent. SCF and Custom Runtime respond to and process events over HTTP.

## Custom Runtime Deployment File Description
**Bootstrap file**: fixed executable bootstrap file of Custom Runtime. You need to create an executable file with the same name and implement it with a custom programming language and version. It can be directly processed or start another executable file to initialize and invocate the function runtime.
**Function file**: function program file developed and implemented with a custom programming language and version.
**Library files or executable files dependent on by the runtime**: relevant dependent library files or executable files required by the runtime in the custom programming language and version.

The function is published in the form of deployment package, which consists of the following files:

- Bootstrap file (required)
- Function file (required)
- Library files or executable files dependent on by runtime (optional)

As the deployment package size is limited, if a library file or executable file dependent on by the runtime is large, we recommend you publish the function by binding the deployment package to applicable layers, which involves the following files:
- Deployment package:
  - Bootstrap file (required)
  - Function file (required)
- Layer
  - Library files or executable files dependent on by runtime (optional)

>! Before publishing the executable files among the above deployment files to SCF, you should set the file executable permission for them, package the deployment files into a ZIP package, and upload the package directly or through COS.

## Custom Runtime Operating Mechanism
Custom Runtime divides the function runtime into initialization stage and invocation stage. Initialization is executed only once during the instance cold start, while invocation is the execution process called for every event response.
The start time and execution time vary by programming language and version. The **initialization timeout period** and **execution timeout period** configuration items are added to SCF specially for Custom Runtime to manage the runtime lifecycle.

### Loading function bootstrap
SCF first searches for the executable bootstrap file in the deployment package and performs the following operations based on the search result:
- If the bootstrap file is found and executable, SCF will load and execute it to enter the function initialization stage.
- If the bootstrap file cannot be found or is not executable, a message indicating that the bootstrap file does not exist and the start failed will be returned.

### Initializing function
The bootstrap file is executed to start function initialization. You can customize the bootstrap to implement custom operations as needed and directly process it or call another executable file to complete initialization. We recommend you perform the following basic operations during initialization:
- Set the paths and environment variables of the runtime's dependent libraries.
- Load the dependent library files and extensions of the custom programming language and version. If there are dependent files that need to be pulled in real time, you can download them to the `/tmp` directory.
- Parse the function file and execute the global operations or initialization processes (such as initializing SDK client (HTTP client) and creating database connection pool) required before function invocation, so they can be reused during invocation.
- Start plugins such as security and monitoring.
- After initialization is completed, you need to proactively call the runtime API to access the initialization readiness API `/runtime/init/ready`, which informs SCF that Custom Runtime has been initialized and is ready; otherwise, SCF will keep waiting until the configured initialization timeout period elapses and then end Custom Runtime and return an initialization timeout error. If the notifications are repeated, the first access time will be used as the readiness time. 

#### Logs and exceptions
- SCF logs all standard outputs during initialization.
- If function initialization is executed and completed normally within the timeout period, the logs generated during initialization will be combined and returned together with the logs of the first invocation. If initialization failed due to an error or exception within the timeout period, an initialization timeout error will be returned as the execution result, and program errors written into the standard outputs and exception logs will be reported to SCF and displayed in logs and log query in the console.

### Function invocation
In the function invocation stage, you need to customize event acquisition, function invocation, and result return and loop this process.
- Get events through long polling. You can use the custom programming language and version to access the event acquisition API `/runtime/invocation/next` of the runtime API with HTTP client. The response body contains the event data. If this API is repeatedly accessed during an invocation, the same event data will be returned.
>! Do not set a timeout period for the GET method of the HTTP client.
>
- Construct function invocation parameters based on the environment variables, required information in the response header, and event information.
- Push parameter data such as event information and call the function processing program.
- Access the runtime response result API `/runtime/invocation/response` to push the processing result of the function. The first invocation success will be considered as the final event status, which will be locked by SCF, and the result cannot be changed after push.
- If an error occurs during function invocation, you can call the runtime invocation error API `/runtime/invocation/error` to push the error message. The current invocation will end, and the first invocation will be considered as the final event status, which will be locked by SCF, and the result cannot be changed in subsequent pushes.
- Release the resources that are no longer needed after the current invocation.

#### Logs and exceptions
- SCF logs all standard outputs during invocation.
- After SCF distributes an event, if Custom Runtime does not get it after the function execution timeout period elapses, SCF will end the instance and return an event acquisition wait timeout error.
- After SCF distributes an event, if Custom Runtime gets it but does not return the execution result after the function execution timeout period elapses, SCF will end the instance and return an execution timeout error.


## Custom Runtime API
You need to implement Custom Runtime with your custom programming language and version, and Custom Runtime and SCF need to communicate with each other over a standard protocol during processes such as event distribution and result returning. Therefore, SCF provides runtime APIs to meet the interaction needs in the lifecycle of Custom Runtime.

SCF has the following built-in environment variables:
- SCF_RUNTIME_API: runtime API address.
- SCF_RUNTIME_API_PORT: runtime API port.
- For more information, please see [Environment Variables](https://intl.cloud.tencent.com/document/product/583/32748).

Custom Runtime can access runtime APIs through `SCF_RUNTIME_API:SCF_RUNTIME_API_PORT`.
<table>
<thead>
<tr>
<th>Path</th>
<th>Method</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>/runtime/init/ready</td>
<td>post</td>
<td>Calls the API to mark the ready status after runtime initialization.</td>
</tr>
<tr>
<td>/runtime/invocation/next</td>
<td>get</td>
<td>Gets invocation event.<br>The response header contains the following information<ul><li>request_id: request ID, which identifies the request triggering function invocation.</li><li>memory_limit_in_mb: maximum function memory in MB</li><li>time_limit_in_ms: function timeout period in milliseconds</li></ul>For the structures of the event data contained in the response body, please see <a href="https://intl.cloud.tencent.com/document/product/583/31439">Trigger Event Message Structure Summary</a>.</td>
</tr>
<tr>
<td>/runtime/invocation/response</td>
<td>post</td>
<td>Function processing result.<br>After calling the function processing program, the runtime will push the response from the function to the invocation response API.</td>
</tr>
<tr>
<td>/runtime/invocation/error</td>
<td>post</td>
<td>A function return error will be pushed to the invocation error API to mark the current invocation failure.</td>
</tr>
</tbody></table>






