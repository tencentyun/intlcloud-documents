## Scenario
This document describes the usage methods and computing capability of Batch. 

## Prerequisites
Complete preparations based on the instructions in [Preparation](http://intl.cloud.tencent.com/document/product/599/10548), and learn how to configure the general part of the custom information.

### Viewing the Demo
>Modify the general part of the custom information in `1_SimpleStart.py` based on the instructions in [Preparation](http://intl.cloud.tencent.com/document/product/599/10548).
>
Open `1_SimpleStart.py` in an editor.
```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "LOCAL",
    "Command": " python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "
}
StdoutRedirectPath = "your cos path"
StderrRedirectPath = "your cos path"
```
All information except `Application` in the custom part is described in Preparation. Set the parameters of `Application` based on the following table.

<table>
	<tr>
	<th>Configuration Item</th>
	<th>Description</th>
	</tr>
	<tr>
	<td>DeliveryForm</td>
	<td>Three delivery methods of applications are available: software packaging, container image, and direct running within the CVM. In this case, LOCAL indicates direct running within the CVM.</td>
	</tr>
	<tr>
	<td>Command</td>
	<td>Task startup command. In this case, a Python script is executed. Starting from 1, add up the first 20 numbers of the Fibonacci sequence and output the result to StdOutput.</td>
	</tr>
</table>

<span id="commit"></span>
### Submitting a Job
Run the following command to run the Python script.
The demo encapsulates the job submission process by using Python scripts and the Batch command line tool.
```
python 1_SimpleStart.py
```
The returned result is as follows, indicating that the job is successfully submitted:
```
{
    "RequestId": "393292f4-5583-48ad-a9f5-f673138ea637", 
    "JobId": "job-o0xxxxxq7"
}
```
If the submit operation fails, check the returned value or [Contact Us](http://intl.cloud.tencent.com/document/product/599/10806).

### Viewing State
- Run the following command to view the execution status through DescribeJob:
```
$ tccli batch DescribeJob --version 2017-03-12 --JobId job-xxx
```
>--Replace job-xxx with the JobId acquired after [Submitting a Job](#commit).
>
The returned result is as follows (some information is omitted):
```
{
    "EndTime": "2019-10-08T04:06:58Z", 
    "JobState": "SUCCEED", 
    "TaskInstanceMetrics": {
        ...
    }, 
    "Zone": "ap-guangzhou-2", 
    "TaskMetrics": {
        ...
    }, 
    "JobName": "TestJob", 
    "Priority": 1, 
    "RequestId": "7a5f4c94-1357-486c-9c48-8286ba01b5b2", 
    "TaskSet": [
        ...
    ], 
    "StateReason": null, 
    "JobId": "job-o0xxxxxq7", 
    "DependenceSet": [], 
    "CreateTime": "2019-10-08T04:05:54Z"
}
```
- The returned result includes the following common execution statuses:
 * STARTING: Launching
 * RUNNING: Running
 * SUCCEED: Running successfully
 * FAILED: Failed to run

### Viewing the Result
1. Log in to the COS console and click **[Bucket List](https://console.cloud.tencent.com/cos5/bucket)** in the left sidebar.
2. Select the ID of the created bucket, click **Objects**, and select the **logs**, which stores the execution results. See the figure below:
![](https://main.qcloudimg.com/raw/e6ffa709b7e843c44d00bedfd072f367.png)
 - View the standard output in stdout.job-xxx.xxxx.0.log for a successful operation. The content is as follows:
```
6765
```
 - View the standard error in stderr.job-xxx.xxxx.0.log in case of a failure. The content may be:
```
/bin/sh: -c: line 0: syntax error near unexpected token `('
/bin/sh: -c: line 0: ` python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" '
```



