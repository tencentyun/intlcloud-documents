## Scenario
This document describes how to submit a simple job by using TCCLI. The following example shows how to add up the numbers in the Fibonacci sequence. The Python code is specified by the `Command` field of `Application`. The returned result is saved in the configured stdout output location.


## Prerequisites
You can get prepared by referring to the steps in [Preparation](http://intl.cloud.tencent.com/document/product/599/10807).


## Steps
### Installing and Configuring TCCLI
1. Install TCCLI by referring to [Preparation](http://intl.cloud.tencent.com/document/product/599/10548).
2. Run the following command to verify whether TCCLI is successfully installed:
```
tccli batch help
```
The returned result is as follows, indicating that TCCLI is successfully installed:
```
NAME
        batch
DESCRIPTION
        batch-2017-03-12
USEAGE
        tccli batch <action> [--param...]
OPTIONS
        help
        show the tccli batch help info
        --version
        specify a batch api version
AVAILABLE ACTION
        DescribeComputeEnv
        Used to query details of the computing environment
        CreateTaskTemplate
        Used to create a task template
```
3. Configure TCCLI by referring to [Preparation](http://intl.cloud.tencent.com/document/product/599/10548).


<span id="create"></span>
### Creating a COS Bucket to Store Results
In this example, the returned result is directly output to the standard output of the system. Batch can collect `stdout` and `stderr` from the standard output and upload them to the specified COS bucket upon task completion. You need to create a bucket and a subfolder for storage in advance.

Create the COS bucket and subfolder based on the instructions in [Prepare the COS Directory](http://intl.cloud.tencent.com/document/product/599/10548).

### Job Configuration
You can acquire and modify the official example to create a Batch computing environment under a personal account. Learn each configuration item in the computing environment by referring to the following information.
```
tccli batch SubmitJob --version 2017-03-12 --Job '{
    "JobName": "TestJob",       // Job name
    "JobDescription": "for test ",    // Job description
    "Priority": "1",            // Job priority
    "Tasks": [                  // Task list (this example only contains one task)
        {
            "TaskName": "Task1",   // Task 1 name
            "Application": {        // Task execution command
                "DeliveryForm": "LOCAL",    // Runs the local command.
                "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "   // Command content (Fibonacci summation)
            },
            "ComputeEnv": {         // Computing environment configuration
                "EnvType": "MANAGED",   // Computing environment types: MANAGED and UNMANAGED
                "EnvData": {        // Specific configuration (The current type is MANAGED. Refer to the CVM instance creation description)
                    "InstanceType": "S1.SMALL1",    // CVM instance type
                    "ImageId": "img-m4q71qnf",      // CVM image ID (o be replaced)
                }
            },
            "RedirectInfo": {       // Configuration of standard output redirection           
                "StdoutRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/",    // Standard output (to be replaced)
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"     // Standard error (to be replaced)
            }
        }
    ]
}'
--Placement'{
    "Zone": "ap-guangzhou-2"    // Availability zone (to be replaced)
}'
```

#### `SubmitJob` Command
Below is an example of the `SubmitJob` command in Batch:
```
tccli batch SubmitJob --version 2017-03-12  --Job '{"JobName": "TestJob",  "JobDescription": "for test", "Priority": "1", "Tasks": [{"TaskName": "Task1",  "TaskInstanceNum": 1,  "Application": {"DeliveryForm": "LOCAL", "Command":  "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "},  "ComputeEnv": {"EnvType":  "MANAGED", "EnvData": {"InstanceType": "S1.SMALL1",  "ImageId": "To be replaced" }  }, "RedirectInfo": {"StdoutRedirectPath": "To be replaced", "StderrRedirectPath":   "To be replaced"}, "MaxRetryCount":  1 } ] }' --Placement '{"Zone": "ap-guangzhou-2"}'
```
The `SubmitJob` command includes the following 3 parameters:

<table>
	<tr>
	<th>Parameter</th>
	<th>Description</th>
	</tr>
	<tr>
	<td>version</td>
	<td>Version, which is fixed to 2017-03-12.</td>
	</tr>
	<tr>
	<td>Job</td>
	<td>Job configuration (in JSON format). For more information, see the example.</td>
	</tr>
	<tr>
	<td>Placement</td>
	<td>Availability zone for job execution.</td>
	</tr>
</table>

- Replace the fields marked with **to be replaced** in the example with your actual information before running the command. Those parameters include the custom image ID, VPC-related information, COS bucket address, SecretId, and SecretKey. For more information, see [Modifying Configuration](#change).
- Copy the complete content by clicking the **Copy** button next to the example. Replace the **to be replaced** content with your actual information before running the command.
- For more information about job configuration, see [Configuring a Job](http://intl.cloud.tencent.com/document/product/599/11040).


<span id="change"></span>
### Modifying Configuration

#### Setting ImageId
```
"ImageId": "To be replaced"
```
Use a configured image based on the Cloud-init service. The following images are available for direct use:
- CentOS 6.5 image, with an ID of **img-m4q71qnf**
- Windows Server 2012 official image, with an ID of **img-er9shcln**.

#### Configuring StdoutRedirectPath and StderrRedirectPath
```
"StdoutRedirectPath": "To be replaced", "StderrRedirectPath": "To be replaced"
```
Enter the endpoint obtained in the **[Creating a COS Bucket to Store Results](#create)** step above to StdoutRedirectPath and StderrRedirectPath.

#### (Optional) Modifying the Availability Zone
```
--Placement '{"Zone": "ap-guangzhou-2"}'
```
This example applies for resources in Guangzhou Zone 2. You can select an availability zone based on the default region configured in TCCLI and apply for resources.
For more information about regions and availability zones, see [Regions and Availability Zones](http://intl.cloud.tencent.com/document/product/213/6091).

### Viewing the Result
The returned result is as follows, indicating successful execution:
```
{
    "RequestId": "db84b7f8-ff8e-4c11-81c1-9a3b02652a46", 
    "JobId": "job-cr8qyyh9"
}
```
- Run the following command to view the submitted job information through DescribeJob: 
```
$ tccli batch DescribeJob  --version 2017-03-12 --JobId job-cr8qyyh9
{
    "EndTime": "2019-10-08T07:28:07Z", 
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
    "RequestId": "0e5c5ea5-ef25-4f90-b355-cfaa8057d473", 
    "TaskSet": [
        {
            ...
        }
    ], 
    "StateReason": null, 
    "JobId": "job-cr8qyyh9", 
    "DependenceSet": [], 
    "CreateTime": "2019-10-08T07:27:17Z"
}
```
- Run the following command to view the job list of the current region through DescribeJobs:
```
$ tccli batch DescribeJobs  --version 2017-03-12
```


## More Features
The preceding example shows a single-task job and includes only the fundamental features, but does not include the mapping remote storage capability. For more information about Batch, see the following topics or the [API documentation](http://intl.cloud.tencent.com/document/product/599/30458):

* **Simplified operations**: Batch provides robust capabilities and diverse configuration items, with support for simple call through scripts. For more information, see [Preparations](http://intl.cloud.tencent.com/document/product/599/10548) and [Quick Start](http://intl.cloud.tencent.com/document/product/599/10551).

* **Running Remote Package**: Batch provides a set of **custom images and remote packages with command line support** to fully meet your technical requirements. For more information, see [Running Remote Package](http://intl.cloud.tencent.com/document/product/599/10552).

* **Remote storage mapping**: Batch optimizes storage access by simplifying access to the remote storage service in the form of operations on the local file system. For more information, see [Mapping Remote Storage](http://intl.cloud.tencent.com/document/product/599/10983).
