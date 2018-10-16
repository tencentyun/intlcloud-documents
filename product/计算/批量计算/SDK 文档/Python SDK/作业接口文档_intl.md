## Preparations for Development
- Download and install [Python SDK](https://cloud.tencent.com/document/sdk/Python).
- Before using Batch for the first time, see [Preparation](https://cloud.tencent.com/document/product/599/10807).
- For more information about job configuration parameters, see the API documentation for [Submitting a Job](https://cloud.tencent.com/document/product/599/12683).

## Getting Started

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
For detailed parameter descriptions and error codes, see the API documentation for [Submitting a Job](https://cloud.tencent.com/document/product/599/12683).

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
For detailed parameter descriptions and error codes, see the API documentation for [Terminating a Job](https://cloud.tencent.com/document/product/599/12689).

## Deleting a Job

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
For detailed parameter descriptions and error codes, see the API documentation for [Deleting a Job](https://cloud.tencent.com/document/product/599/12682).

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
For detailed parameter descriptions and error codes, see the API documentation for [Viewing Job Submission Information](https://cloud.tencent.com/document/product/599/12687).

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
For detailed parameter descriptions and error codes, see the API documentation for [Viewing Job Information](https://cloud.tencent.com/document/product/599/12685).

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
For detailed parameter descriptions and error codes, see the API documentation for [Viewing Job List](https://cloud.tencent.com/document/product/599/12686).

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
For detailed parameter descriptions and error codes, see the API documentation for [Viewing Task Information](https://cloud.tencent.com/document/product/599/12684).

## Terminating a Task Instance

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
For detailed parameter descriptions and error codes, see the API documentation for [Terminating a Task Instance](https://cloud.tencent.com/document/product/599/12688).
