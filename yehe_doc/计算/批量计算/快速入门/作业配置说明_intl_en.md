## 1. Brief Description
The job configuration in BatchCompute is provided in JSON format. A brief description of the configuration is given below. The following job contains 2 tasks.

```
{
    "JobName": "TestJob",       // Job name
    "JobDescription": "for test ",    // Job description
    "Priority": "1",            // Job priority
    "Tasks": [                  // Task list (two tasks in this example)
        {       
            // Task 1 (the most simplified task configuration with all non-essential options removed) 
            "TaskName": "Task1",   // Task 1 name
            "Application": {        // Task execution command
                "DeliveryForm": "LOCAL",    // Application delivery method
                "Command": "echo hello"     // Command content (to output hello)
                
            },
            "ComputeEnv": {         // Compute environment configuration
                "EnvType": "MANAGED",   // Compute environment types: MANAGED or UNMANAGED
                "EnvData": {        // Specific configuration (the current type is MANAGED. For more information, please see CVM instance creation description)
                    "InstanceType": "S1.SMALL1",    // CVM instance type
                    "ImageId": "img-m4q71qnf",      // CVM image ID
                }
            },
            "RedirectInfo": {       // Configuration of standard output redirection           
                "StdoutRedirectPath": "cos://dondonbatchv5- 1251783334.cosgz.myqcloud.com/logs/",  // Standard output (to be replaced)
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"    // Standard error (to be replaced)
            },
            "Authentications": [        // Authentication information (optional, for use in case of COS of others)
                {
                    "Scene": "COS",     // Scenarios (COS currently)
                    "SecretId": "***",  // SecretId (to be replaced)
                    "SecretKey": "***"  // SecretKey (to be replaced)
                }
            ]
        },
        {
            // Task 2
            "TaskName": "Task2",   // Task 2 name
            "TaskInstanceNum": 1,   // Number of concurrent instances in task 2
            "Application": {        // Task execution command
                "DeliveryForm": "LOCAL",    // Run the local command
                "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "   // Command content (Fibonacci summation)
            },
            "ComputeEnv": {         // Compute environment configuration
                "EnvType": "MANAGED",   // Compute environment types: MANAGED or UNMANAGED
                "EnvData": {        // Specific configuration (the current type is MANAGED. For more information, please see CVM instance creation description)
                    "InstanceType": "S1.SMALL1",    // CVM instance type
                    "ImageId": "img-m4q71qnf",      // CVM image ID (to be replaced)
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
                "StdoutRedirectPath": "cos://dondonbatchv5- 1251783334.cosgz.myqcloud.com/logs/",  // Standard output (to be replaced)
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"    // Standard error (to be replaced)
            },
            "MaxRetryCount": 1,         // Maximum number of retries
            "Authentications": [        // Authentication information (optional, for use in case of COS of others)
                {
                    "Scene": "COS",     // Scenarios (COS currently)
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
## 2. Detailed Description

### I. Job
A job is a unit of submission in BatchCompute. In addition to its own information, it also contains information about one or more tasks and dependencies among the tasks.

Name | Type | Required | Description  
-----|------|-----|------
JobName | String | No | Job name
JobDescription | String | No | Job description
Priority | Integer | Yes | Job priority; task (Task) and task instance (TaskInstance) inherit priority of the job
Tasks.N | array of Task objects | Yes | Task information
Dependences.N | array of Dependence objects | No | Dependency

### II. Task
A job can contain multiple tasks. A task mainly describes the information about the environment (model, system, image) on which the actual computation process depends in BatchCompute, code package and command line executed, storage and network.

Name | Type | Required | Description | Example
-----|------|-----|------|------
TaskName | String | Yes | Task name, which should be unique within a job | Task1
TaskInstanceNum | Integer | Yes | Number of running task instances | 1
Application | Application object | Yes | Application information | -
ComputeEnv | ComputeEnv object | Yes | Running environment information | -
RedirectInfo | RedirectInfo object | Yes | Redirection path | -
InputMappings | array of InputMapping object | No | Input mapping | -
OutputMappings | array of OutputMapping object | No | Output mapping | -
Authentications | array of Authentication object | No | Authentication information | -
MaxRetryCount | Integer | No| Maximum number of retries after a task fails | 3
Timeout | Integer | No | Timeout period after a task starts in seconds | 3600

#### Application
Name | Type | Required | Description | Example
-----|------|-----|------|------
Command | String | Yes | Task execution command
DeliveryForm | String | Yes | Application delivery method | LOCAL: local method; PACKAGE: remote code package method
PackagePath | String | No | Remote code package path, which must be in .tgz format | ```http://batchdemo-1251783334.cosgz.myqcloud.com/codepkg/codepkg.tgz``` (only for `PACKAGE`)

#### ComputeEnv
Name | Type | Required | Description | Example
-----|------|-----|------|------
EnvType | String | Yes | Compute environment management type, including MANAGED and UNMANAGED | LOCAL: local method; PACKAGE: remote code package method
EnvData | EnvData object | Yes | Compute environment's specific parameters | -

#### EnvData
Name | Type | Required | Description | Example
-----|------|-----|------|------
InstanceType | String | Yes | CVM instance type, which is required for the MANAGED type | S1.SMALL1
ImageId | String | Yes | CVM image ID, which is required for the MANAGED type | img-m4q71qnf
others | others | No | Please see the parameters provided in CVM API document [Creating Instances](https://intl.cloud.tencent.com/document/product/213/33237) | `SystemDisk`, `DataDisks`, `VirtualPrivateCloud` and other parameters are supported

#### RedirectInfo
Name | Type | Required | Description | Example
-----|------|-----|------|------
StdoutRedirectPath | String | No | Standard output redirection path | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/
StderrRedirectPath | String | No | Standard error redirection path | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/

#### InputMapping
Name | Type | Required | Description | Example
-----|------|-------|------|------
SourcePath | String | Yes | Source path | 	cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/input/
DestinationPath | String | Yes | Destination path | /data/input/

#### OutputMapping

Name | Type | Required | Description | Example 
-----|------|-----|------|------
SourcePath | String | Yes | Source path | /data/output/
DestinationPath | String | Yes | Destination path | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/output/

#### Authentication 
If the COS path (storage mapping, log redirection) is a COS address you own, you don't need to enter this parameter. If you need to access COS of others, you need to enter the corresponding access key.

Name | Type | Required | Description  
-----|------|-----|------
Scene | String | Yes | Authentication scenario such as COS
SecretId | String | Yes | SecretId
SecretKey | String | Yes | SecretKey 

### III. Dependency
It describes the relationship between tasks. For example, if a job contains two tasks (Task1 as `StartTask` and Task2 as `EndTask`), Task2 will be started after Task1 is executed, and after Task2 is executed, it can be deemed that the job is completed.

Name | Type | Required | Description | Example
-----|------|-----|------|------
StartTask | String | Yes | Dependency start task name | Task1
EndTask | String | Yes | Dependency end task name | Task2

