
## Development Preparations
- For downloading and installing Python SDK, see [Python](https://intl.cloud.tencent.com/zh/document/product/494/7244).
- If this is your first time using BatchCompute, please see [Preparation](https://intl.cloud.tencent.com/document/product/599/10807).

## Getting Started

```
#!/usr/bin/python
# -*- coding: utf-8 -*-

# Introduce the Cloud API entry module
from QcloudApi.qcloudapi import QcloudApi

# Common Configuration
module = 'batch'

config = {
    'Region': 'ap-beijing',
    'secretId': 'Your secretId',
    'secretKey': 'Your secretKey',
}

service = QcloudApi(module, config)
```

## Creating a Computing Environment

```
try:
    action = 'CreateComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        "ComputeEnv": {
            "EnvName": "Cluster-A",  # Compute environment name
            "EnvDescription": "first cluster",  # Description of compute environment
            "EnvType": "MANAGED",
            "MountDataDisks": [
                {
                    "FileSystemType": "NTFS",
                    "LocalPath": J://",  # Data disk mount target
                    }
                ],
            "EnvData": {
                "InstanceType": "S2.SMALL1",  # Instance type
                "ImageId": "img-er9shcln",  # Image ID
                "LoginSettings": {
                    "Password": "B1[habcdB1[habcd"  # Login password
                    },
                "InternetAccessible": {
                    "PublicIpAssigned": "TRUE",  # Public IP
                    "InternetMaxBandwidthOut": 50  # Public bandwidth
                    },
                "SystemDisk": {
                    "DiskType": "LOCAL_BASIC",  # System disk type
                    "DiskSize": 50  # System disk capacity
                    },
                "DataDisks": [
                    {
                        "DiskType": "LOCAL_BASIC",  # Data disk type
                        "DiskSize": 50  # Data disk capacity
                        }
                    ]
                },
            "DesiredComputeNodeCount": 1  # Number of compute nodes
            },
        "Placement": {
            "Zone": "ap-beijing-2"  # Availability zone
            },
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```

## Modifying a Compute Environment

```
try:
    action = 'ModifyComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "env-cc44pzme",  # Compute environment ID
        'DesiredComputeNodeCount': 100,  # Number of desired compute nodes
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```


 ## Deleting a Compute Cluster

```
try:
    action = 'DeleteComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "env-cc44pzme",  # Compute environment ID
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```


 ## Viewing the Creation Information of the Compute Environment

```
try:
    action = 'DescribeComputeEnvCreateInfo'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "",  # Compute environment ID
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```


 ## Viewing the Compute Environment Information

```
try:
    action = 'DescribeComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "",  # Compute environment ID
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```


## Viewing the List of Compute Environments

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

