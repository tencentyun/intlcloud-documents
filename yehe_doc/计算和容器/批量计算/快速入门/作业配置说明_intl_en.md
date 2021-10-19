## 1. Introduction
The job configuration of Batch is provided in JSON format as described below. The job listed below consists of 2 tasks.

```
{
    "JobName": "TestJob",       // 作业名称
    "JobDescription": "for test ",    // 作业描述
    "Priority": "1",            // 作业优先级
    "Tasks": [                  // 任务列表（本例包含两个任务）
        {       
            // 任务1 （最简化的任务配置，去除所有非必选项） 
            "TaskName": "Task1",   // 任务1名称
            "Application": {        // 任务执行命令
                "DeliveryForm": "LOCAL",    // 应用程序的交付方式
                "Command": "echo hello"     // 命令具体内容（输出 hello）
                
            },
            "ComputeEnv": {         // 计算环境配置
                "EnvType": "MANAGED",   // 计算环境类型，托管型和非托管型
                "EnvData": {        // 具体配置（当前托管型，可参照CVM 创建实例说明）
                    "InstanceType": "S1.SMALL1",    // CVM 实例类型
                    "ImageId": "img-m4q71qnf",      // CVM 镜像 ID
                }
            },
            "RedirectInfo": {       // 标准输出重定向配置           
                "StdoutRedirectPath": "cos://dondonbatchv5- 1251783334.cosgz.myqcloud.com/logs/",  // 标准输出（需替换）
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"    // 标准错误（需替换）
            },
            "Authentications": [        // 鉴权相关信息（选填，访问非本人COS场景使用）
                {
                    "Scene": "COS",     // 场景（当前是 COS）
                    "SecretId": "***",  // SecretId（需替换）
                    "SecretKey": "***"  // SecretKey（需替换）
                }
            ]
        },
        {
            // 任务2
            "TaskName": "Task2",   // 任务2名称
            "TaskInstanceNum": 1,   // 任务2并发实例数目
            "Application": {        // 任务执行命令
                "DeliveryForm": "LOCAL",    // 执行本地命令
                "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "   // 命令具体内容（斐波拉契求和）
            },
            "ComputeEnv": {         // 计算环境配置
                "EnvType": "MANAGED",   // 计算环境类型，托管型和非托管型
                "EnvData": {        // 具体配置（当前托管型，可参照CVM 创建实例说明）
                    "InstanceType": "S1.SMALL1",    // CVM 实例类型
                    "ImageId": "img-m4q71qnf",      // CVM 镜像 ID（可替换）
                    "VirtualPrivateCloud": {        // CVM 网络配置（选填）
                        "VpcId": "vpc-cg18la4l",             // VpcId（需替换）
                        "SubnetId": "subnet-8axej2jc"           // SubnetId（需替换）
                    },
                    "SystemDisk": {                 // CVM 系统盘配置
                        "DiskType": "CLOUD_BASIC",
                        "DiskSize": 50
                    },
                    "DataDisks": [                  // CVM 数据盘配置
                        {
                            "DiskType": "CLOUD_BASIC",
                            "DiskSize": 50
                        }
                    ]
                }
            },
            "RedirectInfo": {       // 标准输出重定向配置           
                "StdoutRedirectPath": "cos://dondonbatchv5- 1251783334.cosgz.myqcloud.com/logs/",  // 标准输出（需替换）
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"    // 标准错误（需替换）
            },
            "MaxRetryCount": 1,         // 最大重试数目
            "Authentications": [        // 鉴权相关信息（选填，访问非本人COS场景使用）
                {
                    "Scene": "COS",     // 场景（当前是 COS）
                    "SecretId": "***",  // SecretId（需替换）
                    "SecretKey": "***"  // SecretKey（需替换）
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

Parameter | Type  | Required | Description
-----|------|-----|------
JobName | String | No | Job name
JobDescription | String | No | Job description
Priority | Integer | Yes | Job priority. Tasks (Task) and task instances (TaskInstance) inherit the job priority
Tasks.N | array of Task objects | Yes | Task details
Dependences.N | array of Dependence objects | No |  Dependency information

### II. Tasks
A job can contain multiple tasks. A task describes the environment (model, system, image) that the actual computing process depends on, the code package to be executed, command line, storage, network and other related information in batch data computing.

Parameter | Type  | Required | Description | Value
-----|------|-----|------|------
TaskName | String | Yes | Task name, which should be unique within a job | Example: Task 1
TaskInstanceNum | Integer | Yes | Number of instances launched | Example: 1
Application | Application object | Yes | Application information | -
ComputeEnv  | ComputeEnv object | Yes | Operating environment information |-
RedirectInfo | RedirectInfo object | Yes | Redirection path |-
InputMappings | array of InputMapping object | No | Input mapping |-
OutputMappings | array of OutputMapping object | No | Output mapping |-
Authentications | array of Authentication object | No | Information for authorization |-
MaxRetryCount | Integer | No | Maximum number of retries after a task fails | Example: 3
Timeout | Integer | No | Timeout period after the task is launched, in seconds | Example: 3600

#### Application
Parameter | Type  | Required | Description | Value
-----|------|-----|------|------
Command | String | Yes | Task execution command||
DeliveryForm | String | Yes | Delivery method of application | Values: **LOCAL** (local), **PACKAGE** (remote code package)
PackagePath | String | No | The path to remote code package. It should be in .tgz format. It’s only available when the delivery method is PACKAGE. | ```http://batchdemo-1251783334.cosgz.myqcloud.com/codepkg/codepkg.tgz```  

#### ComputeEnv
Parameter | Type  | Required | Description | Value
-----|------|-----|------|------
EnvType | String | Yes | Compute environment management types | Values: **MANAGED**, **UNMANAGED**
EnvData | EnvData object | Yes | Compute environment's parameters |-

#### EnvData
Parameter | Type  | Required | Description | Value
-----|------|-----|------|------
InstanceType | String | Yes | CVM instance type and managed type must be entered | Example: S1.SMALL1
ImageId | String | Yes | CVM image ID. It’s required for managed environments. | Example: img-m4q71qnf
others | others | No | Refer to the parameters provided in the CVM API documentation [Instance Creation](https://intl.cloud.tencent.com/zh/document/product/213/33237) | Values: `SystemDisk`, `DataDisks`, `VirtualPrivateCloud`, etc.

#### RedirectInfo
Parameter | Type  | Required | Description | Value
-----|------|-----|------|------
StdoutRedirectPath | String | No | Standard output redirection path | Example: cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/
StderrRedirectPath | String | No | Standard error redirection path | Example://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/

#### InputMapping
Parameter | Type  | Required | Description | Value
-----|------|-------|------|------
SourcePath | String | Yes | Source path | 	Example: cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/input/
DestinationPath | String | Yes | Destination path | Example: /data/input

#### OutputMapping

Parameter | Type  | Required | Description | Value
-----|------|-----|------|------
SourcePath | String | Yes | Source path | Example: /data/output
DestinationPath | String | Yes | Destination path | Example: cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/output/

#### Authentications 
Leave it blank if you’re the owner of the COS resource specified in storage mapping and log redirection. Otherwise please enter the secret to access the COS resource.

Parameter | Type  | Required | Description
-----|------|-----|------
Scene | String | Yes | Authentication scenario, such as `COS`
SecretId | String | Yes | ID of the secret
SecretKey | String | Yes | Key of the secret

### Dependences
It describes the execution order of tasks. If a job contains two tasks: StartTask for Task 1 and EndTask for Task 2, Task 2 is launched only after the execution of Task 1 is completed. When Task 2 is completed, the entire job is finished.

Parameter | Type  | Required | Description | Value
-----|------|-----|------|------
StartTask | String | Yes | The starting task of a dependency | Example: Task 1
EndTask | String | Yes | The ending task of a dependency | Example: Task 2


