## Operation Scenarios
This document describes how to create a compute environment on TCCLI, submit a job to it, and then terminate it.

## Prerequisites
You can get prepared as instructed in [Preparations](https://intl.cloud.tencent.com/document/product/599/10807).


## Directions
### Installing and configuring TCCLI
1. Install TCCLI as instructed in [Installing TCCLI](https://intl.cloud.tencent.com/document/product/599/10548). 
2. Run the following command to verify whether TCCLI is successfully installed:
```
tccli batch help
```
If the following is returned, the installation is successful.
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
        This API is used to query compute environment details
        CreateTaskTemplate
        This API is used to create a task template
```
3. Configure TCCLI as instructed in [Configuring TCCLI](https://intl.cloud.tencent.com/document/product/599/10548).



### Creating COS bucket for result storage
In this example, the returned result is directly output to the standard output of the system. BatchCompute can collect `stdout` and `stderr` from the standard output and upload them to the specified COS bucket upon task completion. You need to create a bucket and a subfolder for storage in advance.

Create the COS bucket and subfolder as instructed in [Preparing COS Directory](https://intl.cloud.tencent.com/document/product/599/10548).



### Creating compute environment
You can get and modify the official sample to create a BatchCompute compute environment under your personal account. The configuration items in the compute environment are as described below:
You can also refer to APIs related to compute environment, such as [CreateComputeEnv](https://intl.cloud.tencent.com/document/product/599/30521).
```
tccli batch CreateComputeEnv --version 2017-03-12 --ComputeEnv '{
    "EnvName": "test compute env",          // Compute environment name
    "EnvDescription": "test compute env",   // Compute environment description
    "EnvType": "MANAGED",                   // Compute environment type, which is `managed` here
    "EnvData": {                            // Specific configuration (please see the CVM instance creation description)
        "InternetAccessible": {
            "PublicIpAssigned": "TRUE",
            "InternetMaxBandwidthOut": 50
        },
        "LoginSettings": {
            "Password": "*****"             // Login password (to be replaced)
        },
        "InstanceType": "S1.SMALL1",        // CVM instance type
        "ImageId": "img-xxxxyyyy"           // CVM image ID (to be replaced)
    },
    "DesiredComputeNodeCount": 2            // Number of desired compute nodes
}'
--Placement'{
    "Zone": "ap-guangzhou-2"                // AZ (to be replaced)
}'
```


#### Sample request
```
tccli batch CreateComputeEnv --version 2017-03-12  --ComputeEnv '{"EnvName": "test compute env", "EnvDescription": "test compute env", "EnvType": "MANAGED", "EnvData": {"InstanceType": "S1.SMALL2", "ImageId": "to be replaced", "LoginSettings": {"Password": "to be replaced"}, "InternetAccessible": {"PublicIpAssigned": "TRUE", "InternetMaxBandwidthOut": 50}, "SystemDisk": {"DiskType": "CLOUD_BASIC", "DiskSize": 50 } }, "DesiredComputeNodeCount": 2 }' --Placement '{"Zone": "ap-guangzhou-2"}'
```

#### Sample return
In the following returned value, `EnvId` indicates the unique ID of a BatchCompute compute environment.
```
{
    "EnvId": "env-jlatqfkn", 
    "RequestId": "297ed003-7373-4950-9721-242d3d40b3ca"
}
```

### Viewing compute environment list
#### Sample request
Run the following command to view the list of compute environments:
```
tccli batch DescribeComputeEnvs --version 2017-03-12
```

#### Sample return (some information omitted)
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


### Viewing specified compute environment
#### Sample request
Run the following command to view a specified compute environment:
```
tccli batch DescribeComputeEnv --version 2017-03-12 --EnvId env-jlatqfkn
```

#### Sample return (some information omitted)
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

### Submitting job to specified compute environment
#### Sample request
Replace related information in the command as needed and run the following command to submit a job to a specified compute environment.
```
tccli batch SubmitJob --version 2017-03-12  --Job '{"JobName": "test job", "JobDescription": "xxx", "Priority": "1", "Tasks": [{"TaskName": "hello2", "TaskInstanceNum": 1,  "Application": {"DeliveryForm": "LOCAL", "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "}, "EnvId": "to be replaced", "RedirectInfo": {"StdoutRedirectPath": "to be replaced", "StderrRedirectPath":  "to be replaced"} } ] }' --Placement '{"Zone": "ap-guangzhou-2"}'

```

#### Sample return
```
{
    "RequestId": "d6903404-5765-474b-b516-39137456fa5a", 
    "JobId": "job-qjq3mqp7"
}
```

### Terminating compute environment
#### Sample request
Run the following command to terminate a compute environment:
```
tccli batch DeleteComputeEnv --version 2017-03-12 --EnvId env-jlatqfkn
```

#### Sample return
```
{
    "RequestId": "029becda-2a4e-4989-aa77-6fbb5a873555"
}
```

