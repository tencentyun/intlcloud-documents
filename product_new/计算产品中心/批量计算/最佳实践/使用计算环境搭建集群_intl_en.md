## Scenario
With the capabilities of BatchCompute (Batch), you can easily and efficiently maintain the Cloud Virtual Machine (CVM) cluster. The Batch computing environment corresponds to common cluster concepts. This document describes how to use the capabilities of the Batch computing environment to create or terminate an ultra cost-effective resource cluster.

## Prerequisites

You can get prepared as instructed by [Preparation](http://intl.cloud.tencent.com/document/product/599/10807).


## Steps
### Installing and Configuring TCCLI
>In the current computing environment, you can only call command lines. Install TCCLI by referring to the following steps:
>
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

### Creating a Computing Environment
You can acquire and modify the official example to create a Batch computing environment under a personal account. Learn each configuration item in the computing environment by referring to the following information.
You can also refer to the APIs related to the computing environment, for example, [CreateComputeEnv](https://intl.cloud.tencent.com/document/api/599/30521).

The following example shows how to create a cluster with ten BS1.LARGE8 instances (Standard  BatchCompute model, 4-core CPU and 8 GB memory) in Guangzhou Zone 2:
```
tccli batch CreateComputeEnv --version 2017-03-12 --ComputeEnv '{
    "EnvName": "batch-env",          // Computing environment name
    "EnvDescription": "batch env demo",   // Computing environment description
    "EnvType": "MANAGED",                   // Computing environment type: MANAGED
    "EnvData": {                            // Specific configuration (Refer to the CVM instance creation description.)
        "InstanceType": "BS1.LARGE8",       // CVM instance type in a computing environment
        "ImageId": "img-m4q71qnf",          // CVM image ID in a computing environment, which can be replaced by a custom image ID
        "LoginSettings": {
            "Password": "B1[habcd"          // CVM login password in a computing environment
        },
        "InternetAccessible": {
            "PublicIpAssigned": "TRUE",     // Whether the CVM requires a public IP address in a computing environment
            "InternetMaxBandwidthOut": 10   // CVM bandwidth cap in a computing environment
        },
        "SystemDisk": {
            "DiskType": "CLOUD_BASIC",      // Type of a CVM disk in a computing environment (HDD cloud disk is used now)
            "DiskSize": 50                  // Size of a CVM disk in a computing environment
        }
    },
    "DesiredComputeNodeCount": 10           // Number of desired compute nodes
}'
--Placement'{
    "Zone": "ap-guangzhou-2"                // Availability zone (Guangzhou Zone 2 now, you can change it if necessary)
}'
```

#### Sample Request
```
tccli batch CreateComputeEnv --version 2017-03-12 --ComputeEnv '{"EnvName":"batch-env","EnvDescription":"batch env demo","EnvType":"MANAGED","EnvData":{"InstanceType":"BS1.LARGE8","ImageId":"img-m4q71qnf","LoginSettings":{"Password":"B1[habcd"},"InternetAccessible":{"PublicIpAssigned":"TRUE","InternetMaxBandwidthOut":50},"SystemDisk":{"DiskType":"CLOUD_BASIC","DiskSize":50}},"DesiredComputeNodeCount":1}' --Placement '{"Zone": "ap-guangzhou-2"}'
```

#### Response Example
In the following return values, `EnvId` indicates the unique ID of a Batch computing environment.
The following will describe how to use Batch command line interface (CLI) to check the computing environment and instance information within it, and `EnvId` will be used. You need to record the returned value of `EnvId`.
```
{
    "EnvId": "env-jlatqfkn", 
    "RequestId": "297ed003-7373-4950-9721-242d3d40b3ca"
}
```
You can view the created CVM in [CVM Console](https://console.cloud.tencent.com/cvm/index) or view and manage the CVM by using the [CreateComputeEnv](https://intl.cloud.tencent.com/document/api/599/30521) API.

### Viewing the List of Computing Environments
You can use the Batch CLI to view the list of all created computing environments.
#### Sample Request
Run the following command to view the list of computing environments:
```
tccli batch DescribeComputeEnvs --version 2017-03-12
```

#### Response Example
The following result contains information about the computing environment to be queried (some information is omitted):
```
{
    "TotalCount": 1, 
    "ComputeEnvSet": [
        {
            "EnvId": "env-jlatqfkn", 
            "ComputeNodeMetrics": {
                ...
            }, 
            "EnvType": "MANAGED", 
            "DesiredComputeNodeCount": 2, 
            "EnvName": "test compute env", 
            "Placement": {
                ...
            }, 
            "CreateTime": "2019-10-08T08:55:12Z"
        }
    ], 
    "RequestId": "7a1f9338-0118-46bf-b59f-60ace9f154f5"
}
```


### Viewing the Specified Computing Environment and Its Node List
#### Sample Request
Run the following command to view the specified computing environment and its node list:
```
tccli batch DescribeComputeEnv --version 2017-03-12 --EnvId env-jlatqfkn
```

#### Response Example
The following result contains the overall computing environment and details of each node (some information is omitted):
```
{
    "EnvId": "env-jlatqfkn", 
    "ComputeNodeMetrics": {
        ...
    }, 
    "EnvType": "MANAGED", 
    "DesiredComputeNodeCount": 2, 
    "ComputeNodeSet": [
        ...
    ], 
    "RequestId": "407de39c-1c3d-489e-9a35-5257ae561e87", 
    "Placement": {
        ...
    }, 
    "EnvName": "test compute env", 
    "CreateTime": "2019-10-08T08:55:12Z"
}
```


### Terminating a Computing Environment
#### Sample Request
Run the following command to terminate the computing environment. After you run the command, the computing environment automatically terminates all CVMs in the cluster.
```
tccli batch DeleteComputeEnv --version 2017-03-12 --EnvId env-jlatqfkn
```

#### Response Example
```
{
    "RequestId": "029becda-2a4e-4989-aa77-6fbb5a873555"
}
```


