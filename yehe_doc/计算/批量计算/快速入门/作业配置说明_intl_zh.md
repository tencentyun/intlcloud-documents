## 1. 简要说明
批量计算 Batch 的作业配置以 JSON 格式提供，下面给出这个配置的简要说明，下面的作业包含2个任务：

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
## 2. 详细说明

### I. 作业（Job）
作业是 Batch 提交的单元，除了本身信息，还包含了一个或者多个任务（Task）的信息以及 Task 之间的依赖关系。

名称 | 类型  | 是否必选 | 描述  
-----|------|-----|------
JobName | String | 否 | 作业名称
JobDescription | String | 否 | 作业描述
Priority | Integer | 是 | 作业优先级，任务（Task）和任务实例（TaskInstance）会继承作业优先级
Tasks.N | array of Task objects | 是 | 任务信息
Dependences.N | array of Dependence objects | 否 |  依赖信息

### II. 任务（Task）
一个作业可以包含多个任务，任务主要描述了批处理数据计算中，实际计算过程依赖的环境（机型、系统、镜像）、执行的代码包和命令行、存储、网络等相关信息。

名称 | 类型  | 是否必选 | 描述 | 示例
-----|------|-----|------|------
TaskName | String | 是 | 任务名称，在一个作业内部唯一 | Task1
TaskInstanceNum | Integer | 是 | 任务实例运行个数 | 1
Application | Application object | 是 | 应用程序信息 | -
ComputeEnv  | ComputeEnv object | 是 | 运行环境信息 |-
RedirectInfo | RedirectInfo object | 是 | 重定向路径 |-
InputMappings | array of InputMapping object | 否 | 输入映射 |-
OutputMappings | array of OutputMapping object | 否 | 输出映射 |-
Authentications | array of Authentication object | 否 | 授权信息 |-
MaxRetryCount | Integer | 否 | 任务失败后的最大重试次数 | 3
Timeout | Integer | 否 | 任务启动后的超时时间，单位秒 | 3600

#### Application
名称 | 类型  | 是否必选 | 描述 | 示例
-----|------|-----|------|------
Command | String | 是 | 任务执行命令
DeliveryForm | String | 是 | 应用程序的交付方式 | LOCAL 本地，PACKAGE 远程代码包
PackagePath | String | 否 | 远程代码包路径，必须 .tgz 格式 | ```http://batchdemo-1251783334.cosgz.myqcloud.com/codepkg/codepkg.tgz``` （仅 PACKAGE 方式）

#### ComputeEnv
名称 | 类型  | 是否必选 | 描述 | 示例
-----|------|-----|------|------
EnvType | String | 是 | 计算环境管理类型，包括托管和非托管两种 | MANAGED 托管，UNMANAGED 非托管
EnvData | EnvData object | 是 | 计算环境具体参数 |-

#### EnvData
名称 | 类型  | 是否必选 | 描述 | 示例
-----|------|-----|------|------
InstanceType | String | 是 | CVM实例类型，托管类型必填 | S1.SMALL1
ImageId | String | 是 | CVM镜像 ID，托管类型必填 | img-m4q71qnf
others | others | 否 | 参考 CVM API文档 [创建实例](https://intl.cloud.tencent.com/zh/document/product/213/33237) 提供的参数 | 支持 SystemDisk、DataDisks、VirtualPrivateCloud 等

#### RedirectInfo
名称 | 类型  | 是否必选 | 描述 | 示例
-----|------|-----|------|------
StdoutRedirectPath | String | 否 | 标准输出重定向路径 | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/
StderrRedirectPath | String | 否 | 标准错误重定向路径 | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/

#### InputMapping
名称 | 类型  | 是否必选 | 描述 | 示例
-----|------|-------|------|------
SourcePath | String | 是 | 源端路径 | 	cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/input/
DestinationPath | String | 是 | 目的端路径 | /data/input/

#### OutputMapping

名称 | 类型  | 是否必选 | 描述 | 示例 
-----|------|-----|------|------
SourcePath | String | 是 | 源端路径 | /data/output/
DestinationPath | String | 是 | 目的端路径 | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/output/

#### Authentication 
如果填写的 COS 路径（存储映射、日志重定向）是本人 COS 地址，无需填写。需要访问其他人的 COS 时，需要填写对应的访问密钥。

名称 | 类型  | 是否必选 | 描述  
-----|------|-----|------
Scene | String | 是 | 授权场景，例如COS
SecretId | String | 是 | SecretId
SecretKey | String | 是 | SecretKey 

### III. 任务依赖（Dependence）
描叙任务之间的先后关系，假设作业包含 2 个任务， StartTask 为 Task1，EndTask 为 Task2，则会在执行完 Task1 之后才会启动 Task2，Task2 执行完则作业执行完毕。

名称 | 类型  | 是否必选 | 描述 | 示例
-----|------|-----|------|------
StartTask | String | 是 | 依赖关系的起点任务名称 | Task1
EndTask | String | 是 | 依赖关系的终点任务名称 | Task2

