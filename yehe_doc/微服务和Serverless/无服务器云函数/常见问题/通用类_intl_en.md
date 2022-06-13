### What should I do if the error "Cannot find module" or "No module named" is reported or the dependencies can't be found during function execution? How do I install dependencies?

This problem is usually caused by the fact that the dependency file for code execution is not uploaded to the cloud environment. You can troubleshot as follows:
1. Check whether the path of the dependency file referenced in the code is correct. If a relative path is used, **the dependency file must be placed in the same root directory as the function code file** and packaged and uploaded to the cloud together with the function code. If an absolute path is used, make sure that the path is accessible to SCF, and the specified dependency file exists under the path.
2. If you have uploaded the dependency file to a layer in advance, check whether the binding relationship between the layer version and the function runtime version is as expected.
3. If you have used the [online dependency installation](https://intl.cloud.tencent.com/document/product/583/38105) feature, check whether all dependencies are successfully installed.

>?
>- For more information on function deployment, see [Deploying Functions](https://intl.cloud.tencent.com/document/product/583/32741).
>- For more information on dependency installation, see [Dependency Installation](https://intl.cloud.tencent.com/document/product/583/34879).


### What is the time zone in the SCF environment? How do I eliminate the impact of time zone differences?

UTC (GMT+0) is used in the SCF operating environment, which is 8 hours behind Beijing time.
You can use a time processing library or code package in your programming language to identify the UTC time zone and convert it to Beijing time (GMT+8). You can also set the `TZ=Asia/Shanghai` environment variable to specify the time zone.

### Why am I prompted the "no permission" error while writing a file? Is there any space in the environment for write operations?

SCF function has a temporary disk space of 500 MB (`/tmp`) during execution. You can perform read and write operations in this space or create subdirectories while executing the code, but data written in this space will not be retained after the function is executed.

>?
>- The temporary disk spaces of different instances are isolated, i.e., each instance has its own independent temporary space.
>- In the operating environment, all directories are read-only except for `/tmp`.

### What should I do if an error occurs after there is no more space for write operations?

If data is written to the `/tmp` directory continuously and the instance is constantly used due to frequent invocations, the directory may be full and data cannot be written into.
In this case, check the writes in the directory and use codes to delete obsolete temporary files to free up space.


### Why does the returned data format have extra quotation marks?

API Gateway parses the returned result from SCF into JSON format by default. To solve this problem, you can select integration response in function configuration as instructed in [Integration response and passthrough response](https://intl.cloud.tencent.com/document/product/583/12513). Note that after integration response is enabled, the required data structure needs to be returned.

### Can the root account restrict a sub-account's permission to manipulate certain functions?

Yes. For more information, see [Sub-user and Authorization](https://intl.cloud.tencent.com/document/product/583/38178).

### How can SCF logs be delivered to COS?

Upload logs to CLS as instructed in [Log Delivery Configuration (Legacy)](https://intl.cloud.tencent.com/document/product/583/34876) and configure CLS to [ship logs to COS](https://intl.cloud.tencent.com/zh/document/product/614/31581).

### How does an application trigger a function directly?

The function can be triggered directly by calling the `Invoke` API of SCF. The owner of the function or an authorized account can call this API directly.

### Can a function still be used when its code or configuration changed?

Yes. There is a short window period of less than 1 minute in general when the function is updated, during which the request will be implemented by either the old or new function code.

### Is there a limit to the number of concurrency instances for a single function?

SCF supports large numbers of concurrent function instances. For the total function concurrency quota per region, see [Quota Limits](https://intl.cloud.tencent.com/document/product/583/11637). For the function concurrency management, see [Function Concurrency](https://intl.cloud.tencent.com/document/product/583/37040).


### What should I do if a failure occurs when a function handles an event?

In case of failure, a function that makes sync invocations will return the exception information, while a function that makes async invocations will automatically retry. For more information, see [Error Types and Retry Policies](https://intl.cloud.tencent.com/document/product/583/39851).



### Can I use threads and processes in my function code?

Yes. You can use general programming language and operating system features, such as creating additional threads and processes. Resources allocated to the function, including memory, execution duration, disk, and network, are shared by the threads or processes it uses.



### What restrictions apply to function code?

We try not to impose restrictions on normal activities at the programming language and operating system levels, but certain activities such as inbound network connection are disabled.

### A jar package of Java is deployed on the backend of SCF. How can a WeChat Mini Program on the frontend call the deployed code? 

API Gateway can be used to this end. Configure the backend of API Gateway as a function and then call the gateway API to trigger the function. For detailed directions, see [Creating Triggers](https://intl.cloud.tencent.com/document/product/583/31441) and [Overview](https://intl.cloud.tencent.com/document/product/583/12513).



### What events can trigger SCF functions?

Currently, SCF functions can be triggered by manual triggers (APIs), timer triggers, COS, CMQ, and API Gateway, and more triggering methods will be supported soon.

### What languages does SCF support?

Currently, it supports Python 2.7 and 3.6, Node.js 6.10, 8.9, 10.15, and 12.16, Java 8, PHP 5 and 7, Go, and Custom Runtime. More programming languages will be supported soon.

### Can I access the infrastructure where SCF runs?

No. SCF manages the computing infrastructure on your behalf.

### How does SCF isolate code?

Each function runs in its own unique environment and has its own resources and file system. SCF uses the same technology as CVM to provide security and isolation at the infrastructure and execution levels.

### Can SCF interconnect with other Tencent Cloud services such as CVM or TencentDB?

Yes. When you create or modify a function, select VPC configuration and deploy the function in the same VPC as the CVM or TencentDB instance.



### Does SCF reuse function instances?

To improve performance, SCF will retain your function instance for a certain period of time and reuse it for subsequent requests. However, do not rely on this reuse.

### Why should I keep an SCF function stateless?

Keeping the statelessness of the function allows the function to launch as many instances as needed to meet the requested rate.

### How do I troubleshoot?

SCF provides a logging feature. Each invocation will output its log to the logs window in the console. The log records the resources consumed by the function during each use, the log in the code, and the platform invocations. You can easily insert troubleshooting log statements into your code.





### I uploaded a zip file to create function, and I was prompted that "Unable to create the function. Try again" or "Function execution entry point file not found. Confirm that the filename matches with the handler setting or the code package is correct". What should I do?

A possible reason is that the function's execution method cannot find the corresponding executable file or function entry in the zip package, because an outer folder is compressed together.
The execution method format is `a.b`, where `a` is the name of the `.py` file, and `b` is the method name in the code.
If a file named `a.py` cannot be found in the root directory of the unzipped folder, the system will prompt that "The function code cannot be displayed. The file name specified by the execution method cannot be found in the code zip package".
For example, if a folder structure is as follows:
```bash
--RootFolder
----SecondFolder
------a.py
------thirdfolder
--------sth.json
```

If you compress `SecondFolder` when creating the zip package, the above error will occur; instead, you should only compress `a.py` and `thirdfolder`.


### What should I do if timeout occurs?

Set the timeout period to a larger value (up to 900) and test the function again. If it still times out, check whether there are excessive input data and computation, loops that cannot be jumped out, or prolonged sleeps in the log of your code.

### How do I scale a function?

You don't need to care about function scaling as the SCF platform will automatically do so on your behalf. Whenever a function request is received, SCF will quickly locate the free capacity and execute your code. Since your code is stateless, as many instances as needed can be launched without lengthy delays in deployment and configuration.

### How do I allocate computing resources to a function?

You can select the amount of memory allocated to a function, and the CPU and other resources will be allocated proportionally. For example, if you select 256 MB of memory, the CPU allocated to the function will be approximately twice that allocated for 128 MB of memory.


### Can I use a local library?

Yes. You can add your own code repository to the function code and upload it to the platform as a zip package.

### What should I do if the error "Resource limit exceeded for function" is reported during function invocation?

A common reason is that the function concurrency exceeds the quota limit. You can calculate the required amount of function concurrency with the formula "function concurrency = QPS (number of requests per second) * function execution duration (in seconds)".
For example, if QPS = 100 and function execution duration = 100 ms, then the actual required function concurrency will be 100 * 0.1 = 10. If the result exceeds the quota limit, you can [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to increase the limit.


### What should I do if the error "Account Arrears, Operation not Allowed" is reported during function creation?

There are overdue payments in your account. Top up and try again.


### What should I do if the error "The SCF_QcsRole role does not exist. Visit https://console.cloud.tencent.com/scf to create it" is reported during function creation?

The `SCF_QcsRole` role is required for creating a function. Log in to the [SCF console](https://console.cloud.tencent.com/scf) with your root account and follow the instructions to complete the authorization.

### What should I do if the error "xxx you are not authorized to perform operation xxx" is reported during function creation?

Click `SCF_QcsRole` on the [Role](https://console.cloud.tencent.com/cam/role) page in the CAM console and confirm whether it has been associated with the preset policy `QcloudAccessForScfRole`, and if not, click **Add Policy** to associate `QcloudAccessForScfRole` and try again.

### How do I get the `DemoId` when creating a function with a template?

Select **Template** as the creation method when creating a function in the SCF console, select the template you want to use, click **View Details** in the top-right corner of the template, and click **Click to download template function** on the template details page. The template code will be downloaded to the local system with the name `DemoId`.
> ! The `DemoId` of the same function template varies by region. Pay attention to the region when getting the `DemoId`.

