## 1. API Description
This API (AddUpdateServiceTrigger) adds a trigger.
API domain name: `ccr.api.qcloud.com`

## 2. Input Parameters
The following parameters are action-specific. For common parameters required for all API requests, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter Name | Description | Type | Required | 
|---------|---------|---------|---------
| triggerName | Trigger name | String | Yes |
| reponame | Name of the repository bound with the trigger | String | Yes |
| invokeMethod | Trigger | String | Yes |
| invokeExpr | The expression of the trigger | String | No |
| serviceName | Service name | String | Yes |
| clusterId | Cluster ID | String | Yes |
| namespace | Namespace | String | Yes |
| containerName | Container name | String | Yes |
| clusterRegion | Region of the cluster | Int | Yes |

## 3. Output Parameters
 
| Parameter Name | Description | Type | 
|---------|---------|---------|
| code | Common error code. 0: Successful; other values: Failed. | Int | 
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |
| message | Description of the Module error related to this API | String |

## 4. Samples
Input

```
  https://domain/v2/index.php?Action=AddUpdateServiceTrigger
  &triggerName=trigger_test
  &reponame=test/kube_test
  &invokeMethod=taglist
  &invokeExpr=v1;v2
  &serviceName=nginx-test
  &clusterId=cls-xxxxxx
  &namespace=default
  &containerName=nginx-test
  &clusterRegion=1
  &other common parameters
```
Output

```
{
    "code": 0,
    "message": "", 
    "codeDesc": "Success"
}

```
