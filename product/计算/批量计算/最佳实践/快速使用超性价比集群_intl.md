## How to Quickly Create a Cluster?
A CVM cluster can be easily and efficiently maintained using the compute environment of Batch which can meet general cluster needs with ease. The following example illustrates how to use a compute environment to quickly create and terminate a cost-effective resource cluster. Currently, the compute environment only supports calling through command line. Please see Preparations for more information about CLI installation.

## Preparations
Please complete the preparations as detailed in checklist in [Preparation](/doc/product/599/10807). This example will use the command line tool (CLI). You need to install and configure CLI first.

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

## Creating a Compute Environment

You can create a Batch compute environment that can be executed under your account by modifying the configuration in the official example. Before you do this, please look at what the configuration items of the compute environment mean.
You can also see the documentation for compute environment-related APIs such as [Creating a Compute Environment](/document/api/599/12691).

The example below is to quickly create a cluster of 10 BS1.LARGE8 (Universal Batch model with 4 CPU cores and 8 GB memory) instances in Guangzhou Zone 2

```
qcloudcli batch CreateComputeEnv --Version 2017-03-12 --ComputeEnv '{
    "EnvName": "batch-env",          // Compute environment name
    "EnvDescription": "batch env demo",   // Compute environment description
    "EnvType": "MANAGED",                   // Compute environment type, managed
    "EnvData": {                            // Specific configuration (see the instructions on CVM instance creation)
        "InstanceType": "BS1.LARGE8",       // Type of CVM instance in the compute environment
        "ImageId": "img-m4q71qnf",          // ID of the CVM image in the compute environment (probably to be replaced with a custom image)
        "LoginSettings": {
            "Password": "B1[habcd"          // Login password of the CVM instance in the compute environment
        },
        "InternetAccessible": {
            "PublicIpAssigned": "TRUE",     // Whether a public IP is needed in the compute environment
            "InternetMaxBandwidthOut": 10   // Upper limit of CVM bandwidth in the compute environment
        },
        "SystemDisk": {
            "DiskType": "CLOUD_BASIC",      // Type of CVM disk in the compute environment (HDD cloud disk currently)
            "DiskSize": 50                  // Size of CVM disk in the compute environment
        }
    },
    "DesiredComputeNodeCount": 10           // Number of desired compute nodes
}'
--Placement'{
    "Zone": "ap-guangzhou-2"                // Availability zone (Guangzhou Zone 2 currently; probably to be replaced)
}'
```

#### Request example
```
qcloudcli batch CreateComputeEnv --Version 2017-03-12 --ComputeEnv '{"EnvName":"batch-env","EnvDescription":"batch env demo","EnvType":"MANAGED","EnvData":{"InstanceType":"BS1.LARGE8","ImageId":"img-m4q71qnf","LoginSettings":{"Password":"B1[habcd"},"InternetAccessible":{"PublicIpAssigned":"TRUE","InternetMaxBandwidthOut":50},"SystemDisk":{"DiskType":"CLOUD_BASIC","DiskSize":50}},"DesiredComputeNodeCount":1}' --Placement '{"Zone": "ap-guangzhou-2"}'
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
The created instances can be viewed in he CVM Console or viewed and managed using Batch's compute environment API. The following describes how to use Batch's command line API to view the compute environment and information about the instances in it. As EnvId will be used, please note down the returned EnvId.

## Viewing Compute Environment List

You can view a list of all the created compute environments using Batch's command line API.

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
The compute environment created just now will be included in the returned result which will include compute node information too.

## Viewing a Specified Compute Environment and the List of Nodes Contained There
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

It includes details about the compute environment and all the nodes in it

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

After the call, the compute environment will automatically terminate all the CVM instances in the cluster.
