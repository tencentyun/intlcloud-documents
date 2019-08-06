## Preparations for Development
- Download and install [Python SDK](https://cloud.tencent.com/document/sdk/Python).
- Before using Batch for the first time, see [Preparation](https://cloud.tencent.com/document/product/599/10807).


##Getting Started

```
#!/usr/bin/python
# -*- coding: utf-8 -*-

# Introducing the Cloud API Entry Module
from QcloudApi.qcloudapi import QcloudApi

# Common configuration
module = 'batch'

config = {
    'Region': 'ap-beijing',
    'secretId': 'Your secretId',
    'secretKey': 'Your secretKey',
}

service = QcloudApi(module, config)
```

##Creating a Compute Environment

```
try:
    action = 'CreateComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        "ComputeEnv": {
            "EnvName": "Cluster-A",  # Compute environment name
            "EnvDescription": "first cluster",  # Compute environment description
            "EnvType": "MANAGED",
            "MountDataDisks": [
                {
                    "FileSystemType": "NTFS",
                    "LocalPath": J://",  # Data disk mounting point
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
                    "InternetMaxBandwidthOut": 50  # Internet bandwidth
                    },
                "SystemDisk": {
                    "DiskType": "LOCAL_BASIC",  # System disk type
                    "DiskSize": 50  # System disk size
                    },
                "DataDisks": [
                    {
                        "DiskType": "LOCAL_BASIC",  # Data disk type
                        "DiskSize": 50  # Data disk size
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
        'DesiredComputeNodeCount': 100,  # Number of desired nodes
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

 
## Viewing Compute Environment Creation Information
 
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
 
 
## Viewing Compute Environment Information
 
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


## Viewing Compute Environment List

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
