### A function can run normally in the local system, but I am prompted that some dependencies cannot be found when I try to run it online. What should I do?

A common reason is that third-party dependencies have not been packaged and uploaded to the online environment. You need to put the third-party libraries that the function depends on into the function directory and package and upload them along with the function code.

- For more information on how to deploy a function, please see [Deploying Functions](https://intl.cloud.tencent.com/document/product/583/32741).

### After SCF is deployed to a VPC, how do I configure public network access?

There are several ways for a VPC to access the public network. For more information, please see the [NAT Gateway documentation](https://intl.cloud.tencent.com/document/product/1015).

### Is the IP used for SCF to access the public network random or fixed?

It is random by default. You can also set a fixed public IP. For more information, please see [Fixed Public Outbound IP](https://intl.cloud.tencent.com/document/product/583/38106).

### What is the time zone in the SCF environment? How do I eliminate the impact of time zone differences?

UTC (GMT+0) is used in the SCF operating environment, which is 8 hours behind Beijing time.
You can use a time processing library or code package in your programming language to identify UTC time zone and convert it to Beijing time (GMT+8). You can also set the `TZ=Asia/Shanghai` environment variable to specify the time zone.

### Is there any space in the environment for write operations?

Yes. A function has a temporary disk space of 500 MB (`/tmp`) during execution. You can perform read and write operations or create subfolders in this space while executing the code, but data written in this space will not be retained after the function is executed.

> ?
> - The temporary disk spaces of different instances are isolated, i.e., each instance has its own independent temporary space.
> - In the operating environment, all directories are read-only except for `/tmp`.

### What should I do if SCF returns a 504 error?

1. Check the timeout period configured for the function and gateway and try to increase the gateway timeout period.
2. Configure logging as instructed in [API Gateway Log Management](https://intl.cloud.tencent.com/document/product/628/34636) and analyze logs to identify specific causes.

### My TencentDB for Redis instance has only private network access. How do I connect SCF to it?

To access resources in a VPC, please configure as instructed in [VPC Communication](https://intl.cloud.tencent.com/document/product/583/19703).

### Why does the returned data format have extra quotation marks?

API Gateway considers the returned result from SCF as in JSON format by default. You can select integration response in function configuration as instructed in [Overview of API Gateway Trigger](https://intl.cloud.tencent.com/document/product/583/12513) to solve this problem. Please note that after integration response is enabled, the data structure needs to be returned according to the specification.

### Can the root account restrict a sub-account's permission to manipulate certain functions?

Yes. For more information, please see [Sub-user and Authorization](https://intl.cloud.tencent.com/document/product/583/38178).

### How can SCF logs be delivered to COS?

Forward logs to CLS as instructed in [Connecting SCF Logs to CLS](https://intl.cloud.tencent.com/document/product/583/34876) and configure CLS to [deliver logs to COS](https://intl.cloud.tencent.com/document/product/614/31583).

### How does an application trigger a function directly?

The function can be triggered directly by calling the `Invoke` API of SCF. The owner of the function or an account that has the permission to call the function's `Invoke` API can make calls directly.

### Can a function be used when its code or configuration is changed?

Yes. There is a short window period of less than 1 minute in general when the function is updated, during which the request will be implemented by either the old or new function code.

### Is there a limit to the number of functions that can be executed in a single run?

SCF supports high numbers of concurrent function instances. However, it has a default security threshold, that is, up to 300 concurrent executions are allowed per function. To increase the limit, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1).

### What should I do if a failure occurs when a function handles an event?

In case of failure, a function that makes sync invocations will return the exception information, while a function that makes async invocations will automatically retry 3 times on the backend.

### What should I do if an error occurs after there is no more space for write operations?

If data is written to the `/tmp` directory continuously and the instance is used constantly due to frequent invocations, the directory may be full and write is no longer possible.
If this happens, check the state of writes in the directory and use code to delete temporary files no longer needed to free up the space.

### Can I use threads and processes in my function code?

Yes. You can use normal programming language and operating system features, such as creating additional threads and processes. Resources allocated to the function, including memory, execution duration, disk, and network, are shared by the threads or processes it uses.

### Can I initiate network connections in my function code?

Yes. You can use normal programming language and operating system features, such as initiating TCP and UDP connections. Through relevant language libraries, you can also perform operations such as connecting to databases and accessing APIs.

### What restrictions apply to function code?

We try not to impose restrictions on normal activities at the programming language and operating system levels, but certain activities such as inbound network connection are disabled.

### A jar package of Java is deployed on the backend of SCF. How can a WeChat Mini Program on the frontend call the deployed code? 

API Gateway can be used to this end. Configure the backend of API Gateway as a function and then call the gateway API to trigger the function. For detailed directions, please see [Creating Triggers](https://intl.cloud.tencent.com/document/product/583/31441) and [Overview of API Gateway Trigger](https://intl.cloud.tencent.com/document/product/583/12513).

### What events can trigger SCF functions?

Currently, triggering by manual triggers (APIs), scheduled triggers, COS, CMQ, and API Gateway is supported, and more triggering methods will be available in the future.

### What languages does SCF support?

Currently, it supports Python 2.7 and 3.6, Node.js 6.10, 8.9, 10.15, and 12.16, Java 8, PHP 5 and 7, Go, and Custom Runtime. More programming languages will be supported in the future.

### Can I access the infrastructure where SCF runs?

No. SCF manages the computing infrastructure on your behalf.

### How does SCF isolate code?

Each function runs in its own unique environment and has its own resources and file system. SCF uses the same technology as CVM to provide security and isolation at the infrastructure and execution levels.

### Can SCF communicate with other Tencent Cloud products such as CVM or TencentDB?

Yes. When you create or modify a function, select VPC configuration and deploy the function in the same VPC as the CVM or TencentDB instance.

### Does SCF reuse function instances?

To improve performance, SCF will retain your function instance for a certain period of time and reuse it for subsequent requests. However, your code should not assume that this action always happens.

### Why should I keep an SCF function stateless?

Keeping the statelessness of the function allows the function to launch as many instances as needed to meet the requested rate.

### How do I troubleshoot?

SCF has a logging function. Each invocation will output its log to the logs window in the console. The log records the resources consumed by the function during each use, the log in the code, and the platform invocation information. You can easily insert troubleshooting-related log statements into your code.

### I uploaded a zip file to create function, and saw a message saying "Unable to create the function. Please try again". What should I do?

A common reason is that the function's execution method cannot find the corresponding executable file or function entry in the zip package, or an outer folder is included during compression. The execution method format is `a.b`, where `a` is the name of the `py` file and `b` is the method name in the code.
If a file named `a.py` cannot be found in the root directory of the unzipped folder, the system will prompt that "The function code cannot be displayed as the file specified by the execution method cannot be found in the zip package of the code".
For example, if a folder structure is as follows:
```bash
--RootFolder
----SecondFolder
------a.py
------thirdfolder
--------sth.json
```

When you create the zip package, if `SecondFolder` is zipped, the error above will occur; instead, you should select `a.py` and `thirdfolder` for compression.


### What should I do if timeout occurs?

Please set the timeout period to a larger value (up to 900) and test the function again. If it still times out, please check whether there are excessive input data and computation, loops that cannot be jumped out, or prolonged sleeps in the log of your code.

### How do I scale a function?

You do not have to care about function scaling as the SCF platform will automatically do so on your behalf. Whenever a function request is received, SCF will quickly locate the free capacity and execute your code. Since your code is stateless, as many instances as needed can be launched without lengthy delays in deployment and configuration.

### How do I allocate function computation resources?

You can select the amount of memory allocated to a function, and the CPU and other resources will be allocated proportionally. For example, if you select 256 MB of memory, the CPU allocated to the function will be approximately twice that allocated for 128 MB of memory.


### Can I use a local library?

Yes. You can include your own code base in the function code and upload it to the platform as a zip package.

### What should I do if the error "Resource limit exceeded for function" is reported during function invocation?

A common reason is that the function concurrency exceeds the quota limit. You can calculate the required amount of function concurrency with the formula "function concurrency = QPS (number of requests per second) * function execution duration (in seconds)".
For example, if QPS = 100 and function execution duration = 100 ms, then the actual required function concurrency will be 100 * 0.1 = 10; if the concurrency exceeds the upper limit, you can increases the limit by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1).


### What should I do if the error "Account Arrears, Operation not Allowed" is reported during function creation?

There are overdue payments in your account. Please top up and try again.


### What should I do if the error "The SCF_QcsRole role does not exist. Please visit https://console.cloud.tencent.com/scf to create it" is reported during function creation?

Function creation requires the `SCF_QcsRole` role. Please log in to the [SCF console](https://console.cloud.tencent.com/scf) with your root account and follow the prompts to complete the authorization.

### What should I do if "xxx you are not authorized to perform operation xxx" is reported during function creation?

Please click `SCF_QcsRole` on the [Role](https://console.cloud.tencent.com/cam/role) page in the CAM console and confirm whether it has been associated with the preset policy `QcloudAccessForScfRole`, and if not, click **Add Policy** to associate `QcloudAccessForScfRole` and try again.

