## Scenario
This document describes how to create a computing environment in TCCLI, submit a job to the computing environment, and terminate the computing environment.

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



### Creating a COS Bucket to Store Results
In this example, the returned result is directly output to the standard output of the system. Batch can collect `stdout` and `stderr` from the standard output and upload them to the specified COS bucket upon task completion. You need to create a bucket and a subfolder for storage in advance.

Create the COS bucket and subfolder based on the instructions in [Prepare the COS Directory](http://intl.cloud.tencent.com/document/product/599/10548).



### Creating a Computing Environment
You can acquire and modify the official example to create a Batch computing environment under a personal account. Learn each configuration item in the computing environment by referring to the following information.
You can also refer to the APIs related to the computing environment, for example, [CreateComputeEnv](https://intl.cloud.tencent.com/document/api/599/30521).
```
tccli batch CreateComputeEnv --version 2017-03-12 --ComputeEnv '{
    "EnvName": "test compute env",          // Computing environment name
    "EnvDescription": "test compute env",   // Computing environment description
    "EnvType": "MANAGED",                   // Computing environment type: MANAGED
    "EnvData": {                            // Specific configuration (Refer to the CVM instance creation description.)
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
    "Zone": "ap-guangzhou-2"                // Availability zone (to be replaced)
}'
```


#### Sample Request
```
tccli batch CreateComputeEnv --version 2017-03-12  --ComputeEnv '{"EnvName": "test compute env", "EnvDescription": "test compute env", "EnvType": "MANAGED", "EnvData": {"InstanceType": "S1.SMALL2", "ImageId": "To be replaced", "LoginSettings": {"Password": "To be replaced"}, "InternetAccessible": {"PublicIpAssigned": "TRUE", "InternetMaxBandwidthOut": 50}, "SystemDisk": {"DiskType": "CLOUD_BASIC", "DiskSize": 50 } }, "DesiredComputeNodeCount": 2 }' --Placement '{"Zone": "ap-guangzhou-2"}'
```

#### Response Example
In the following return values, `EnvId` indicates the unique ID of a Batch computing environment.
```
{
    "EnvId": "env-jlatqfkn", 
    "RequestId": "297ed003-7373-4950-9721-242d3d40b3ca"
}
```

### Viewing the List of Computing Environments
#### Sample Request
Run the following command to view the list of computing environments:
```
tccli batch DescribeComputeEnvs --version 2017-03-12
```

#### Response Example (Some Information is Omitted)
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


### Viewing the Specified Computing Environment
#### Sample Request
Run the following command to view the specified computing environment:
```
tccli batch DescribeComputeEnv --version 2017-03-12 --EnvId env-jlatqfkn
```

#### Response Example (Some Information is Omitted)
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

### Submitting a Job to the Specified Computing Environment
#### Sample Request
Replace related information in the command as needed and run the command to submit a job to the specified computing environment.
```
tccli batch SubmitJob --version 2017-03-12  --Job '{"JobName": "test job", "JobDescription": "xxx", "Priority": "1", "Tasks": [{"TaskName": "hello2", "TaskInstanceNum": 1,  "Application": {"DeliveryForm": "LOCAL", "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "}, "EnvId": "To be replaced", "RedirectInfo": {"StdoutRedirectPath": "To be replaced", "StderrRedirectPath":  "To be replaced"} } ] }' --Placement '{"Zone": "ap-guangzhou-2"}'

```

#### Response Example
```
{
    "RequestId": "d6903404-5765-474b-b516-39137456fa5a", 
    "JobId": "job-qjq3mqp7"
}
```

### Terminating a Computing Environment
#### Sample Request
Run the following command to terminate the computing environment:
```
tccli batch DeleteComputeEnv --version 2017-03-12 --EnvId env-jlatqfkn
```

#### Response Example
```
{
    "RequestId": "029becda-2a4e-4989-aa77-6fbb5a873555"
}
```

