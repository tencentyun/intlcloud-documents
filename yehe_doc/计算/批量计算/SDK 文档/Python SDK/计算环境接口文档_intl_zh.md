
## 开发准备
- 下载和安装 [Python SDK](https://intl.cloud.tencent.com/zh/document/product/494/7244) 。
- 首次使用批量计算，参考 [开始前的准备](https://intl.cloud.tencent.com/document/product/599/10807)。

## 快速入门

```
#!/usr/bin/python
# -*- coding: utf-8 -*-

# 引入云API入口模块
from QcloudApi.qcloudapi import QcloudApi

# 公共配置
module = 'batch'

config = {
    'Region': 'ap-beijing',
    'secretId': '您的secretId',
    'secretKey': '您的secretKey',
}

service = QcloudApi(module, config)
```

## 创建计算环境

```
try:
    action = 'CreateComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        "ComputeEnv": {
            "EnvName": "Cluster-A",  # 计算环境名称
            "EnvDescription": "first cluster",  # 计算环境描述
            "EnvType": "MANAGED",
            "MountDataDisks": [
                {
                    "FileSystemType": "NTFS",
                    "LocalPath": J://",  # 数据盘挂载点
                    }
                ],
            "EnvData": {
                "InstanceType": "S2.SMALL1",  # 实例类型
                "ImageId": "img-er9shcln",  # 镜像标识
                "LoginSettings": {
                    "Password": "B1[habcdB1[habcd"  # 登录密码
                    },
                "InternetAccessible": {
                    "PublicIpAssigned": "TRUE",  # 公网IP
                    "InternetMaxBandwidthOut": 50  # 公网带宽
                    },
                "SystemDisk": {
                    "DiskType": "LOCAL_BASIC",  # 系统盘类型
                    "DiskSize": 50  # 系统盘大小
                    },
                "DataDisks": [
                    {
                        "DiskType": "LOCAL_BASIC",  # 数据盘类型
                        "DiskSize": 50  # 数据盘大小
                        }
                    ]
                },
            "DesiredComputeNodeCount": 1  # 计算节点数量
            },
        "Placement": {
            "Zone": "ap-beijing-2"  # 可用区
            },
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```

## 修改计算环境

```
try:
    action = 'ModifyComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "env-cc44pzme",  # 计算环境标识
        'DesiredComputeNodeCount': 100,  # 期望节点数目
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```


 ## 删除计算集群

```
try:
    action = 'DeleteComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "env-cc44pzme",  # 计算环境标识
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```


 ## 查看计算环境的创建信息

```
try:
    action = 'DescribeComputeEnvCreateInfo'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "",  # 计算环境标识
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```


 ## 查看计算环境信息

```
try:
    action = 'DescribeComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "",  # 计算环境标识
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```


## 查看计算环境列表

```
try:
    action = 'DescribeComputeEnvs'
    action_params = {
        'Version': '2017-03-12',
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```

