### What is an SCF function?

The code running on SCF is uploaded as an "SCF function". Each function has its associated configuration information such as name, description, and resource requirements. The code must be written in a "stateless" style, which should be assumed to be unrelated to the underlying computing infrastructure. Local file system access and child processes are strictly controlled during the lifecycle of the function, and any persistent state should be stored in externally available storage such as COS or CDB. An SCF function can contain external libraries or even native libraries.

### Does SCF reuse function instances?

To improve performance, SCF will retain your function instance for a certain period of time and reuse it for subsequent requests. However, your code should not assume that this action always happens.

### Can SCF use temporary storage?

Yes. An SCF function has a temporary disk space of 500 MB (/tmp) during execution. You can perform some read and write operations in the space while executing the code, but this part of data will not be retained after the function is executed.

### Why should I keep an SCF function stateless?

Keeping the statelessness of the function allows the function to launch as many instances as needed to meet the requested rate.

### Can I use threads and processes in my function code?

Yes. You can use normal language and operating system features such as creating additional threads and processes. Resources allocated to the function, including memory, execution duration, disk, and network, are shared by the threads/processes it use.

### What restrictions apply to function code?

We try not to impose restrictions on normal activities at the language and operating system levels, but certain activities are disabled. For example, inbound network connections are blocked.

### How to create an SCF function using TCCLI?

You can package the code (and any dependent libraries) as a .zip file and upload it from your local environment using TCCLI, or upload it to a COS bucket and specify the bucket name and file name of the zip package when creating a function.

### How to troubleshoot?

SCF has a logging function. Each call will output its log to the logs window in the console. The log records the resources consumed by the function during each use, the log in the code, and the platform call information. You can easily insert troubleshooting-related log statements into your code.

### When I try to create a function by uploading a zip package, the system prompts "Function creation failed. Please try again". What should I do?

A common reason is that the function's execution method cannot find the corresponding executable file or function entry in the zip package, or an outer folder is included during compressing. The execution method is in `a.b` format, where a is the name of the .py file, and b is the name of the method in the code.
If a file named `a.py` cannot be found in the root directory of the unzipped folder, the system will prompt that "The function code cannot be displayed as the file specified by the execution method cannot be found in the zip package of the code".

For example, a folder structure is as follows:

--RootFolder
----SecondFolder
------a.py
------thirdfolder
--------sth.json

When you create the zip package, if SecondFolder is zipped, the error above will occur; instead, you should select `a.py` and `thirdfoler` for compression.

### Why is the execution duration of the same code snippet almost the same no matter how much memory is selected?

During the public trial, we uniformly allocate the same computing resources to each function instance (i.e., the number of container cores is fixed), and will proportionally allocate the resources based on the selected memory size after the public trial is over.

### What if a timeout occurs?

Please set the timeout to a larger value (up to 300) and test the function again. If it still times out, please check if there are excessive input data and computation, loops that cannot be jumped out, or prolonged sleeps in the log of your code.

### How to scale a function?

You do not have to worry about function scaling as the SCF platform will automatically do so on your behalf. Whenever a function request is received, SCF will quickly locate the free capacity and execute your code. Since your code is stateless, as many instances as needed can be launched without lengthy delays in deployment and configuration.

### How to allocate function computation resources?

You can select the amount of memory allocated to a function, and the CPU and other resources will be allocated proportionally. For example, if you select 256 MB of memory, the CPU allocated to the function is approximately twice tat allocated for 128 MB of memory.

### Can I use a local library?

Yes. You can include your own code base in the function code and upload it to the platform as a zip package.

### What if the system prompts that "Resource limit exceeded for function" when a function is called?

A common reason is that the function concurrency exceeds the quota limit. You can calculate the required amount of function concurrency using the formula "function concurrency = QPS (number of requests per second) x function execution duration (in seconds)"; for example, if QPS = 100 and function execution duration = 100 ms, then the actual required function concurrency = 100 x 0.1 = 10; if the concurrency exceeds the upper limit, you can increases the limit by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1).
