## 1. Introduction
The job configuration of BatchCompute is provided in JSON format as described below. The job listed below consists of 2 tasks.

```
{
    "JobName": "TestJob",       // Job name
    "JobDescription": "for test ",    // Job description
    "Priority": "1",            // Job priority
    "Tasks": [                  // Task list (this example has two tasks)
        {       
            // Task 1 (the simplest task configuration without any non-mandatory options) 
            "TaskName": "Task1",   // Task 1 name
            "Application": {        // Task execution command
                "DeliveryForm": "LOCAL",    // Delivery method of application
                "Command": "echo hello"     // Command content (output hello)
                
            },
            "ComputeEnv": {         // Compute environment configuration
                "EnvType": "MANAGED",   // Compute environment types: managed and unmanaged
                "EnvData": {        // Specific configuration (current type is managed. Refer to the CVM instance creation description)
                    "InstanceType": "S1.SMALL1",    // CVM instance type
                    "ImageId": "img-m4q71qnf",      // CVM image ID
                }
            },
            "RedirectInfo": {       // Configuration of standard output redirection           
                "StdoutRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/",  // Standard output (to be replaced)
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"     // Standard error (to be replaced)
            },
            "Authentications": [        // Authentication information (optional, used when visiting others' COS scenarios).
                {
                    "Scene": "COS",     // Scenario (currently in COS)
                    "SecretId": "***",  // SecretId (to be replaced)
                    "SecretKey": "***"  // SecretKey (to be replaced)
                }
            ]
        },
        {
            // Task 2
            "TaskName": "Task2",   // Task 2 name
            "TaskInstanceNum": 1,   // Number of Task 2 concurrent instances
            "Application": {        // Task execution command
                "DeliveryForm": "LOCAL",    // Run the local command
                "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "   // Command content (Fibonacci summation)
            },
            "ComputeEnv": {         // Compute environment configuration
                "EnvType": "MANAGED",   // Compute environment types: managed and unmanaged
                "EnvData": {        // Specific configuration (current type is managed. Refer to the CVM instance creation description)
                    "InstanceType": "S1.SMALL1",    // CVM instance type
                    "ImageId": "img-m4q71qnf",      // CVM image ID (replaceable)
                    "VirtualPrivateCloud": {        // CVM network configuration (optional)
                        "VpcId": "vpc-cg18la4l",             // VpcId (to be replaced)
                        "SubnetId": "subnet-8axej2jc"           // SubnetId (to be replaced)
                    },
                    "SystemDisk": {                 // CVM system disk configuration
                        "DiskType": "CLOUD_BASIC",
                        "DiskSize": 50
                    },
                    "DataDisks": [                  // CVM data disk configuration
                        {
                            "DiskType": "CLOUD_BASIC",
                            "DiskSize": 50
                        }
                    ]
                }
            },
            "RedirectInfo": {       // Configuration of standard output redirection           
                "StdoutRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/",  // Standard output (to be replaced)
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"     // Standard error (to be replaced)
            },
            "MaxRetryCount": 1,         // Maximum number of retry attempts
            "Authentications": [        // Authentication information (optional, used when visiting others' COS scenarios).
                {
                    "Scene": "COS",     // Scenario (currently in COS)
                    "SecretId": "***",  // SecretId (to be replaced)
                    "SecretKey": "***"  // SecretKey (to be replaced)
                }
            ]
        }
    ],
    "Dependences": [
        {
            "StartTask": "Task1", 
            "EndTask": "Task2"
        }
    ]
}
```
## 2. Details

### I. Job
A job is a unit submitted by Batch. It contains its own information and the information about one or more tasks as well as the dependencies between tasks.

Name | Type | Required | Description  
-----|------|-----|------
JobName | String | No | Job name
JobDescription | String | No | Job description
Priority | Integer | Yes | Job priority. Task (Task) and task instance (TaskInstance) inherit the job priority
Task.N | array of Task objects | Yes | Task details
Dependences.N | array of Dependence objects | No | Dependency information

### II. Tasks
A job can contain multiple tasks. A task describes the environment (model, system, image) that the actual computing process depends on, the code package to be executed, command line, storage, network and other related information in batch data computing.

Parameter | Type | Required | Description | Value
-----|------|-----|------|------
TaskName | String | Yes | A unique task name in a job | Task1
TaskInstanceNum | Integer | Yes | Number of instances launched | 1
Application | Application object | Yes | Application information | -
ComputeEnv | ComputeEnv object | Yes | Operating environment information |-
RedirectInfo | RedirectInfo object | Yes | Path for Redirection |-
InputMappings | array of InputMapping object | No | Input mapping |-
OutputMappings | array of OutputMapping object | No | Output mapping |-
Authentications | array of Authentication object | No | Information for authorization |-
MaxRetryCount | Integer | No | The maximum number of retry attempts after a task failed | 3
Timeout | Integer | No | Timeout after a task is launched (in sec) | 3,600

#### Application
Parameter | Type | Required | Description | Example
-----|------|-----|------|------
Command | String | Yes | Task execution command
DeliveryForm | String | Yes | Delivery method of application | **LOCAL** (local), **PACKAGE** (remote code package)
PackagePath | String | No | The path to remote code package. It should be in .tgz format. | ```http://batchdemo-1251783334.cosgz.myqcloud.com/codepkg/codepkg.tgz``` | It’s only available when the delivery method is PACKAGE.

#### ComputeEnv
Parameter | Type | Required | Description | Example
-----|------|-----|------|------
EnvType | String | Yes | Compute environment management types | **MANAGED**, **UNMANAGED**
EnvData | EnvData object | Yes | Compute environment's parameters |-

#### EnvData
Parameter | Type | Required | Description | Example
-----|------|-----|------|------
InstanceType | String | Yes | CVM instance type, required for managed environments | S1.SMALL1
ImageId | String | Yes | CVM image ID, required for managed environments | img-m4q71qnf
others | others | no | Refer to the parameters provided in the CVM API document [Instance Creation](https://intl.cloud.tencent.com/zh/document/product/213/33237) | SystemDisk, DataDisks, and VirtualPrivateCloud are supported

#### RedirectInfo
Parameter | Type | Required | Description | Example
-----|------|-----|------|------
StdoutRedirectPath | String | No | Path for standard output redirection | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/
StderrRedirectPath | String | No | Path for standard error redirection | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/

#### InputMapping
Parameter | Type | Required | Description | Example
-----|------|-------|------|------
SourcePath | String | Yes | Source path | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/input/
DestinationPath | String | Yes | Destination path | /data/input/

#### OutputMapping

Parameter | Type | Required | Description | Example 
-----|------|-----|------|------
SourcePath | String | Yes | Source path | /data/output/
DestinationPath | String | Yes | Destination path | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/output/

#### Authentication 
Leave it blank if you’re the owner of the COS resource specified in storage mapping and log redirection. Otherwise please enter the secret to access the COS resource.

Name | Type | Required | Description  
-----|------|-----|------
Scene | String | Yes | Authentication scenario, such as `COS`
SecretId | String | Yes | SecretId
SecretKey | String | Yes | SecretKey 

### III. Task Dependence
It describes the execution order of tasks. If a job contains two tasks: StartTask for Task 1 and EndTask for Task 2, Task 2 is launched only after the execution of Task 1 is completed. When Task 2 is completed, the entire job is finished.

Parameter | Type | Required | Description | Example
-----|------|-----|------|------
StartTask | String | Yes | Name of start task in a dependency | Task1
EndTask | String | Yes | Name of end task in a dependency | Task2

