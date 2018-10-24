
## A Simple Example
This example shows how to use the command line to submit a simple job. It is to sum the Fibonacci sequence in Python. The code is directly input by the task command configuration provided by Batch, and the result is directly output to the stdout output address in the task configuration.

## Preparations
Please complete the preparations as detailed in checklist in [Preparation](/doc/product/599/10807). This example will use the command line interface (CLI) and COS. You need to install and configure CLI and create a COS bucket first.


### Install and configure CLI
To configure CLI, see [Configuring CLI](/doc/product/440/6184). After the installation, check that it can properly run.
```
qcloudcli batch help

DescribeAvailableCvmInstanceTypes       	|DescribeTask
DescribeJob                             	|SubmitJob
DescribeJobs                            	|TerminateTaskInstance
```

### Create a COS bucket for result storage

In this simple example, the results are output directly to the system standard output. Batch can capture the system standard output "stdout" and "stderr" and upload the information to your specified COS bucket after the task is finished. You need to prepare the bucket and subfolders for saving the information in advance.

Create a corresponding COS bucket and subfolders according to the **Prepare the COS directory** section in [CLI - Preparation](/doc/product/599/10548).

## Job Configuration Overview

You can create the configuration of a Batch job that can be executed under your account by modifying the configuration in the official example. Before you do this, please look at what the configuration items of the job mean.

```
qcloudcli batch SubmitJob --Version 2017-03-12 --Job '{
    "JobName": "TestJob",       // Job name
    "JobDescription": "for test ",    // Job description
    "Priority": "1",            // Job priority
    "Tasks": [                  // Task list (only one task in this example)
        {
            "TaskName": "Task1",   // Task 1 name
            "Application": {        // Task execution command
                "DeliveryForm": "LOCAL",    // Execute local command
                "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "   // Specific command content (summing the Fibonacci sequence)
            },
            "ComputeEnv": {         // Compute environment configuration
                "EnvType": "MANAGED",   // Compute environment type: managed or non-managed
                "EnvData": {        // Specific configuration (managed currently; see the instructions on CVM instance creation)
                    "InstanceType": "S1.SMALL1",    // CVM instance type
                    "ImageId": "img-m4q71qnf",      // CVM image ID (to be replaced)
                }
            },
            "RedirectInfo": {       // Standard output redirection configuration           
                "StdoutRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/",    // Standard output (to be replaced)
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"     // Standard error (to be replaced)
            }
        }
    ]
}'
--Placement'{
    "Zone": "ap-guangzhou-2"    // Availability zone (probably to be replaced)
}'
```

Batch's SubmitJob command contains 3 parameters:
* **Version**: Version number; currently, it is fixed to 2017-03-12
* **Job**: Job configuration in JSON format; for detailed meanings of the fields, see the example
* **Placement**: Availability zone where the job is executed

``* 1. The fields marked with "to be replaced" in the job need to be replaced with your own information, such as the custom image Id, VPC-related information, COS bucket address and the corresponding SecretId and SecretKey. ``

``* 2. Comments are added to the example above which therefore cannot be executed directly in CLI. Please copy the example below and enter the "to be replaced" fields before executing. The command is lengthy, so please use the copy button at the end to ensure complete copying. ``

``* 3. For detailed job configuration instructions, see ``[Job Configuration Instructions](https://cloud.tencent.com/document/product/599/11040) ``. ``

```
qcloudcli batch SubmitJob --Version 2017-03-12  --Job '{"JobName": "TestJob",  "JobDescription": "for test", "Priority": "1", "Tasks": [{"TaskName": "Task1",  "TaskInstanceNum": 1,  "Application": {"DeliveryForm": "LOCAL", "Command":  "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "},  "ComputeEnv": {"EnvType":  "MANAGED", "EnvData": {"InstanceType": "S1.SMALL1",  "ImageId": "To be replaced" }  }, "RedirectInfo": {"StdoutRedirectPath": "To be replaced", "StderrRedirectPath":   "To be replaced"}, "MaxRetryCount":  1 } ] }' --Placement '{"Zone": "ap-guangzhou-2"}'
```

### Modifying Configuration

#### 1. Enter the ImageId
```"ImageId": "To be replaced"```

An image based on the Cloud-init service with proper configuration is required during the internal trial period. Tencent Cloud provides a CentOS 6.5 image (image ID: img-m4q71qnf) that can be directly used. The image ID of the official Windows Server 2012 image is img-er9shcln.

#### 2. Configure StdoutRedirectPath and StderrRedirectPath
```"StdoutRedirectPath": "To be replaced", "StderrRedirectPath":   "To be replaced"```

Enter the COS bucket access addresses created during preparations into StdoutRedirectPath and StderrRedirectPath.

#### 3. Modify the availability zone (optional)
```
--Placement '{"Zone": "ap-guangzhou-2"}'
```

The example specifies Guangzhou Zone 2 for resource application. You can select the corresponding availability zone for resource applicable according to the default region configured in CLI. For more information about region and availability zone, see [Regions and Availability Zones >>](/doc/product/213/6091).

#### 4. Modify the JSON data for CLI on Windows (optional)
The JSON data entered in CLI on Windows is different from that on Linux. For example, " should be replaced with \". For details, see the "Input Parameters in JSON Format" section in [CLI Quick Start](/doc/product/440/6185).

## Viewing the Result

```
{
    "Response": {
        "RequestId": "5d928636-bba2-4ab3-bef3-cf17d7c73c51",
        "JobId": "job-1rqdgnqn"
    }
}
```
If JobId is returned, the execution succeeds.

```
$ qcloudcli batch DescribeJob  --Version 2017-03-12 --JobId job-1z4yl2bp
{
    "Response": {
        "JobState": "STARTING",
        "Zone": "ap-guangzhou-2",
        "JobName": "test job",
        "Priority": 1,
        "RequestId": "b116f9b5-410c-4a69-bbe8-b695a2d6a869",
        "TaskSet": [
            {
                "TaskName": "hello2",
                "TaskState": "STARTING"
            }
        ],
        "JobId": "job-1z4yl2bp",
        "DependenceSet": []
    }
}
```
You can view the information about the task just submitted through DescribeJob.

```
$ qcloudcli batch DescribeJobs  --Version 2017-03-12
```
You can also view the list of jobs in the current region through DescribeJobs.

## What Can I Do Next?

This document illustrates a simple single-task job with no remote storage mapping involved to show the most basic capabilities of Batch. You can continue to test the advanced capabilities according to the API documentation.

* **Easier operation methods**: Batch is very powerful with a lot of configuration items. It can be called more easily and quickly using scripts. For more information, see [Preparations](/doc/product/599/10548) and [1_Quick Start](/doc/product/599/10551).

* **Running remote code package**: Batch provides a **custom image + remote code package + command line** method for execution that technically meets your different business needs in all aspects. For more information, see [2_Running Remote Package](/doc/product/599/10552).

* **Remote storage mapping**: Batch optimizes storage access and simplifies access to remote storage services into local file system operations. For more information, see [3_Remote Storage Mapping](/doc/product/599/10983).
