## 1. API Description
This API (ModifyUpdateServiceTrigger) modifies the trigger for service updates.
API domain name: `ccr.api.qcloud.com`

## 2. Input Parameters
The following parameters are action-specific. For common parameters required for all API requests, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter Name | Description | Type | Required |
|---------|---------|---------|---------|
| triggerName | Name of the trigger to be modified | String | Yes |
| reponame | Name of the repository bound with the trigger | String | No |
| newTriggerName | Name of the new trigger | String | No |
| invokeMethod | Trigger <br>all: All <br>taglist: Specified tag <br>regex: Regular expression | String | No |
| invokeExpr | The expression of the trigger. <br>If invokeMethod is "all", this parameter is empty <br>If invokeMethod is "taglist", this parameter is the tag list, where multiple values are separated with ";", such as v1;v2;v3 <br>If invokeMethod is "regex", this parameter is a regular expression, such as ^test* | String | No |
| serviceName | Name of the service to be updated | String | No |
| clusterId | ID of the cluster for the service to be updated | String | No |
| namespace | Namespace of the service to be updated | String | No |
| containerName | Name of the container for the service to be updated | String | No |
| clusterRegion   | Region of the cluster for the service to be updated. <br>Region Codes: <br>1: Guangzhou <br>4: Shanghai <br>5: Hong Kong, China <br>7: Shanghai Finance <br>8: Beijing <br>9: Singapore <br>16: Chengdu | Int | No |

## 3. Output Parameters

| Parameter Name | Description | Type |
|---------|---------|---------|
| code | Common error code. 0: Successful; other values: Failed. | Int |
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |
| message | Description of the Module error related to this API | String |

## 4. Samples
Input

```
  https://domain/v2/index.php?Action=ModifyUpdateServiceTrigger
  &triggerName=trigger_test
  &reponame=test/kube_test
  &newTriggerName=trigger_test_new
  &invokeMethod=taglist
  &invokeExpr=v1;v2
  &serviceName=nginx-test
  &clusterId=cls-xxxxxxxx
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