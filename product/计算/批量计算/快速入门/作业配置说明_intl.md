## 1. Brief Description
The job configuration in Batch is provided in JSON format. A brief description of the configuration is given below. The following job contains 2 tasks.

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
                "DeliveryForm": "LOCAL",    // Delivery method of the application
                "Command": "echo hello"     // Command content (to output hello)
                
            },
            "ComputeEnv": {         // Compute environment configuration
                "EnvType": "MANAGED",   // Compute environment type: managed or non-managed
                "EnvData": {        // Specific configuration (managed currently; see the instructions on CVM instance creation)
                    "InstanceType": "S1.SMALL1",    // CVM instance type
                    "ImageId": "img-m4q71qnf",      // CVM image ID
                }
            },
            "RedirectInfo": {       // Standard output redirection configuration           
                "StdoutRedirectPath": "cos://dondonbatchv5- 1251783334.cosgz.myqcloud.com/logs/",  // Standard output (to be replaced)
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"    // Standard error (to be replaced)
            },
            "Authentications": [        // Authentication-related information (optional, for use in case of COS of others)
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
                "DeliveryForm": "LOCAL",    // Execute local command
                "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "   // Specific command content (summing the Fibonacci sequence)
            },
            "ComputeEnv": {         // Compute environment configuration
                "EnvType": "MANAGED",   // Compute environment type: managed or non-managed
                "EnvData": {        // Specific configuration (managed currently; see the instructions on CVM instance creation)
                    "InstanceType": "S1.SMALL1",    // CVM instance type
                    "ImageId": "img-m4q71qnf",      // CVM image ID (probably to be replaced)
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
            "RedirectInfo": {       // Standard output redirection configuration           
                "StdoutRedirectPath": "cos://dondonbatchv5- 1251783334.cosgz.myqcloud.com/logs/",  // Standard output (to be replaced)
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"    // Standard error (to be replaced)
            },
            "MaxRetryCount": 1,         // Maximum number of retries
            "Authentications": [        // Authentication-related information (optional, for use in case of COS of others)
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
A job is a unit of submission in Batch. In addition to its own information, it also contains information about one or more tasks and dependencies among the tasks.

Name | Type | Required | Description  
-----|------|-----|------
JobName | String | No | Job name
JobDescription | String | No | Job description
Priority | Integer | Yes | Job priority; task (Task) and task instance (TaskInstance) inherit priority of the job
Tasks.N | array of Task objects | Yes | Task information
Dependences.N | array of Dependence objects | No | Dependency

### II. Task
A job can contain multiple tasks. A task mainly describes the information about the environment (model, system, image) on which the actual computation process depends in Batch, code package and command line executed, storage and network.

Name | Type | Required | Description | Example
-----|------|-----|------|------
TaskName | String | Yes | Task name; unique within a job | Task1
TaskInstanceNum | Integer | Yes | Number of running task instances | 1
Application | Application object | Yes | Application information | 
ComputeEnv | ComputeEnv object | Yes | Compute environment information |
RedirectInfo | RedirectInfo object | Yes | Redirection path |
InputMappings | array of InputMapping object | No | Input mapping |
OutputMappings | array of OutputMapping object | No | Output mapping |
Authentications | array of Authentication object | No | Authentication Information |
MaxRetryCount | Integer | No| Maximum number of retries after a task fails | 3
Timeout | Integer | No | Timeout after the task starts in seconds | 3600

#### Application
Name | Type | Required | Description | Example
-----|------|-----|------|------
Command | String | Yes | Task execution command
DeliveryForm | String | Yes | Delivery method of the application | LOCAL for local method; PACKAGE for remote code package method
PackagePath | String | No | Remote code package path that has to be in .tgz format | ```http://batchdemo-1251783334.cosgz.myqcloud.com/codepkg/codepkg.tgz``` (only for PACKAGE)

#### ComputeEnv
Name | Type | Required | Description | Example
-----|------|-----|------|------
EnvType | String | Yes | Compute environment management type, including managed and non-managed | LOCAL for local method; PACKAGE for remote code package method
EnvData | EnvData object | Yes | Compute environment's specific parameters |

#### EnvData
Name | Type | Required | Description | Example
-----|------|-----|------|------
InstanceType | String | Yes | CVM instance type; required for managed ones | img-m4q71qnf
ImageId | String | Yes | CVM image ID; required for managed ones | S1.SMALL1
others | others | No | See the parameters provided in CVM API documentation [Creating Instances](https://cloud.tencent.com/document/api/213/9384) | SystemDisk, DataDisks, VirtualPrivateCloud and other parameters are supported

#### RedirectInfo
Name | Type | Required | Description | Example
-----|------|-----|------|------
StdoutRedirectPath | String | No | Standard output redirection path | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/
StderrRedirectPath | String | No | Standard error redirection path | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/

#### InputMapping
| Name            | Type   | Required | Description      | Example                                                  |
| --------------- | ------ | -------- | ---------------- | -------------------------------------------------------- |
| SourcePath      | String | Yes      | Source path      | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/input/ |
| DestinationPath | String | Yes      | Destination path | /data/input/                                             |

#### OutputMapping
| Name            | Type   | Required | Description      | Example                                                   |
| --------------- | ------ | -------- | ---------------- | --------------------------------------------------------- |
| SourcePath      | String | Yes      | Source path      | /data/output/                                             |
| DestinationPath | String | Yes      | Destination path | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/output/ |



#### Authentication 
If the COS path (storage mapping, log redirection) is a COS address you own, you don't need to enter it. If you need to access COS of others, you need to enter the corresponding access key.

Name | Type | Required | Description  
-----|------|-----|------
Scene | String | Yes | Authentication scenario such as COS
SecretId | String | Yes | SecretId
SecretKey | String | Yes | SecretKey 

### III. Dependency
It describe the relationship among the tasks. For example, if a job contains two tasks (Task1 as StartTask and Task2 as EndTask), Task2 will be started after Task1 is executed, and after Task2 is executed, it can be deemed that the job is completed.

Name | Type | Required | Description | Example
-----|------|-----|------|------
StartTask | String | Yes | Dependency start task name | Task1
EndTask | String | Yes | Dependency end task name | Task2

