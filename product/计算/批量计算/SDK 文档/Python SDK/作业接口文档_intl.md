## Preparations for Development
- Download and install [Python SDK](https://cloud.tencent.com/document/sdk/Python).
- Before using Batch for the first time, see [Preparation](https://intl.cloud.tencent.com/document/product/599/10807).


```
#!/usr/bin/python
# -*- coding: utf-8 -*-

# Introducing the Cloud API Entry Module
from QcloudApi.qcloudapi import QcloudApi

# Common configuration
module = 'batch'

config = {
    'Region': 'ap-guangzhou',  # Destination region
    'secretId': 'Your secretId',
    'secretKey': 'Your secretKey',
}

service = QcloudApi(module, config)
```

## Submitting a Job

```
try:
    action = 'SubmitJob'
    action_params = {
        'Version': '2017-03-12',
        'Job': {
            'JobName': 'batch-job', # Job name
            'JobDescription': 'batch job',  # Job description
            'Priority': '1',  # Job priority
            'Tasks': [
                {
                    'TaskName': 'task1',  # Task name
                    'TaskInstanceNum':  1,  # Number of task instances
                    'FailedAction': 'FAST_INTERRUPT',  # Processing method for failing job
                    'Application': {
                        'DeliveryForm': 'LOCAL',  # Package source
                        'Command': 'echo hello',  # Command line
                        },
                    'EnvId': 'env-gbyctcy9',  # Compute environment ID
                    'RedirectInfo': {
                        'StdoutRedirectPath': 'cos://bucketgz-1251783334.cos.ap-guangzhou.myqcloud.com/stdout/',  # Standard output storage path
                        'StderrRedirectPath': 'cos://bucketgz-1251783334.cos.ap-guangzhou.myqcloud.com/stderr/',  # Standard error storage path
                        }
                    }
                ]
            },
        'Placement': {
            'Zone': 'ap-guangzhou-2'  # Availability zone
            },
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```

## Terminating a Job

```
try:
    action = 'TerminateJob'
    action_params = {
        'Version': '2017-03-12',
        'JobId': 'job-8kwnzki7',  # Job ID
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```


```
try:
    action = 'DeleteJob'
    action_params = {
        'Version': '2017-03-12',
        'JobId': 'job-8kwnzki7',  # Job ID
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```


## Viewing Job Submission Information

```
try:
    action = 'DescribeJobSubmitInfo'
    action_params = {
        'Version': '2017-03-12',
        'JobId': 'job-8kwnzki7',  # Job ID
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```

## Viewing Job Information

```
try:
    action = 'DescribeJob'
    action_params = {
        'Version': '2017-03-12',
        'JobId': 'job-8kwnzki7',  # Job ID
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```

## Viewing Job List

```
try:
    action = 'DescribeJobs'
    action_params = {
        'Version': '2017-03-12'
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```


## Viewing Task Information

```
try:
    action = 'DescribeTask'
    action_params = {
        'Version': '2017-03-12',
	'JobId': 'job-8kwnzki7',  # Job ID
	'TaskName': 'task A'  # Task name
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```


```
try:
    action = 'TerminateTaskInstance'
    action_params = {
        'Version': '2017-03-12',
	'JobId': 'job-8kwnzki7',  # Job ID
	'TaskName': 'task A',  # Task name
	'TaskInstanceIndex': 1  # The first instance
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
