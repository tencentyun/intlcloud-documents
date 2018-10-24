## An Example of Using a Compute Environment
This example shows how to use the command line to create a compute environment, then submit a job to it, and finally terminate it.

## Preparations
Please complete the preparations as detailed in checklist in [Preparation](/doc/product/599/10807). This example will use the command line interface (CLI) and COS. You need to install and configure CLI and create a COS bucket first.

### Install and configure CLI
To configure CLI, see [Configuring CLI](/doc/product/440/6184). After the installation, check that it can properly run.
```
qcloudcli batch help

CreateComputeEnv                        	|DescribeJobSubmitInfo
CreateTaskTemplate                      	|DescribeJobs
DeleteComputeEnv                        	|DescribeTask
DeleteJob                               	|DescribeTaskTemplates
DeleteTaskTemplates                     	|ModifyTaskTemplate
DescribeAvailableCvmInstanceTypes       	|SubmitJob
DescribeComputeEnv                      	|TerminateJob
DescribeComputeEnvs                     	|TerminateTaskInstance
DescribeJob
```

### Create a COS bucket for result storage

In this simple example, the results are output directly to the system standard output. Batch can capture the system standard output "stdout" and "stderr" and upload the information to your specified COS bucket after the task is finished. You need to prepare the bucket and subfolders for saving the information in advance.

Create a corresponding COS bucket and subfolders according to the **Prepare the COS directory** section in [CLI - Preparation](/doc/product/599/10548).


## Creating a Compute Environment

You can create a Batch compute environment that can be executed under your account by modifying the configuration in the official example. Before you do this, please look at what the configuration items of the compute environment mean.
You can also see the documentation for compute environment-related APIs such as [Creating a Compute Environment](/document/api/599/12691).

```
qcloudcli batch CreateComputeEnv --Version 2017-03-12 --ComputeEnv '{
    "EnvName": "test compute env",          // Compute environment name
    "EnvDescription": "test compute env",   // Compute environment description
    "EnvType": "MANAGED",                   // Compute environment type, managed
    "EnvData": {                            // Specific configuration (see the instructions on CVM instance creation)
        "InternetAccessible": {
            "PublicIpAssigned": "TRUE",
            "InternetMaxBandwidthOut": 50
        },
        "LoginSettings": {
            "Password": "B1[habcd"
        },
        "InstanceType": "S1.SMALL1",        // CVM instance type
        "ImageId": "img-xxxxyyyy"           // CVM image ID (to be replaced)
    },
    "DesiredComputeNodeCount": 2            // Number of desired compute nodes
}'
--Placement'{
    "Zone": "ap-guangzhou-2"                // Availability zone (probably to be replaced)
}'
```


#### Request example
```
qcloudcli batch CreateComputeEnv --Version 2017-03-12  --ComputeEnv '{"EnvName": "test compute env", "EnvDescription": "test compute env", "EnvType": "MANAGED", "EnvData": {"InstanceType": "S1.SMALL2", "ImageId": "To be replaced", "LoginSettings": {"Password": "To be replaced"}, "InternetAccessible": {"PublicIpAssigned": "TRUE", "InternetMaxBandwidthOut": 50}, "SystemDisk": {"DiskType": "CLOUD_BASIC", "DiskSize": 50 } }, "DesiredComputeNodeCount": 2 }' --Placement '{"Zone": "ap-guangzhou-2"}'
```

#### Return example
This is the return value where EnvId is the unique ID of the Batch compute environment.
```
{
    "Response": {
        "EnvId": "env-c96rwhnf",
        "RequestId": "bead16d4-b33b-47b5-9b86-6a02b4bed1b2"
    }
}
```

## Viewing Compute Environment List
#### Request example
```
qcloudcli batch DescribeComputeEnvs --Version 2017-03-12
```

#### Return example
```
{
    "Response": {
        "TotalCount": 1,
        "ComputeEnvSet": [
            {
                "EnvId": "env-c96rwhnf",
                "Placement": {
                    "Zone": "ap-guangzhou-2"
                },
                "EnvType": "MANAGED",
                "EnvName": "test compute env",
                "ComputeNodeMetrics": {
                    "CreatedCount": 0,
                    "DeletingCount": 0,
                    "CreationFailedCount": 0,
                    "SubmittedCount": 0,
                    "CreatingCount": 0,
                    "AbnormalCount": 0,
                    "RunningCount": 2
                },
                "CreateTime": "2017-11-27T07:10:02Z"
            }
        ],
        "RequestId": "bac76f1c-06cd-4ef4-82a9-f230fa5a1992"
    }
}
```


## Viewing a Specified Compute Environment
#### Request example
```
qcloudcli batch DescribeComputeEnv --Version 2017-03-12 --EnvId env-c96rwhnf
```

#### Return example
```
{
    "Response": {
        "EnvId": "env-c96rwhnf",
        "Placement": {
            "Zone": "ap-guangzhou-2"
        },
        "EnvType": "MANAGED",
        "EnvName": "test compute env",
        "RequestId": "12dc7dba-f33b-4d5a-8cd6-ebd1df17ebf7",
        "ComputeNodeMetrics": {
            "CreatedCount": 0,
            "DeletingCount": 0,
            "CreationFailedCount": 0,
            "SubmittedCount": 0,
            "CreatingCount": 0,
            "AbnormalCount": 0,
            "RunningCount": 2
        },
        "ComputeNodeSet": [
            {
                "ComputeNodeId": "node-838udz1w",
                "ComputeNodeState": "RUNNING",
                "Mem": 2,
                "ResourceCreatedTime": "2017-11-27T07:10:46Z",
                "ComputeNodeInstanceId": "ins-q09nyg5g",
                "AgentVersion": "1.0.7",
                "TaskInstanceNumAvailable": 1,
                "Cpu": 1
            },
            {
                "ComputeNodeId": "node-c4z8f8xc",
                "ComputeNodeState": "RUNNING",
                "Mem": 2,
                "ResourceCreatedTime": "2017-11-27T07:10:41Z",
                "ComputeNodeInstanceId": "ins-fgqcau4q",
                "AgentVersion": "1.0.7",
                "TaskInstanceNumAvailable": 1,
                "Cpu": 1
            }
        ],
        "CreateTime": "2017-11-27T07:10:02Z"
    }
}
```

## Submitting a Task to a Specified Compute Environment
#### Request example
```
qcloudcli batch SubmitJob --Version 2017-03-12  --Job '{"JobName": "test job", "JobDescription": "xxx", "Priority": "1", "Tasks": [{"TaskName": "hello2", "TaskInstanceNum": 1,  "Application": {"DeliveryForm": "LOCAL", "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "}, "EnvId": "To be replaced", "RedirectInfo": {"StdoutRedirectPath": "cos://dondonbatch-1251783334.cosgz.myqcloud.com/hello2/logs/", "StderrRedirectPath":  "cos://dondonbatch-1251783334.cosgz.myqcloud.com/hello2/logs/"} } ] }' --Placement '{"Zone": "ap-guangzhou-2"}'

```

#### Return example
```
{
    "Response": {
        "RequestId": "cf821ae0-71d6-42b1-b878-6ecdeec15796",
        "JobId": "job-lhi5agkh"
    }
}
```

## Terminating a Compute Environment
#### Request example
```
qcloudcli batch DeleteComputeEnv --Version 2017-03-12 --EnvId env-c96rwhnf
```

#### Return example
```
{
    "Response": {
        "RequestId": "389f011a-7dbd-4993-82fe-334ac923ff88"
    }
}
```
