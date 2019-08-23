## 1. API Description
This API (ListTrigger) gets a list of trigger.
API domain name: `ccr.api.qcloud.com`

## 2. Input Parameters
The following parameters are action-specific. For common parameters required for all API requests, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter Name | Description | Type | Required |
|---------|---------|---------|---------|
| triggerName | Specify this parameter to get details of a trigger. You can perform an exact match search. | String | No |
| offset | Data offset. Default is 0 | Int | No |
| limit | Maximum number of returned data entries. Default is 20 | Int | No |
| reponame | Name of the repository bound with the trigger | String | No |

## 3. Output Parameters

| Parameter Name | Description | Type |
|---------|---------|---------|
| code | Common error code. 0: Successful; other values: Failed. | Int |
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |
| message | Description of the Module error related to this API | String |
| totalCount | Number of query results | Int |
| triggerInfo | Trigger information | Object Array |

"triggerInfo" is composed as follows:

| Parameter Name | Description | Type |
|---------|---------|---------|
| triggerName | Name of the trigger to be updated | String |
| repoName | Name of the repository bound with the trigger | String |
| invokeSource | Cause of trigger. The value is always set to "IMAGE_PUSH", which means the trigger is initiated by image push | String |
| invokeAction | Trigger action. The value is always set to "SERVICE_UPDATE", which means to update the service | String |
| createTime | Time when the trigger is created | String |
| updateTime | Time when the trigger is updated | String |
| invokeCondition | Triggering condition | Object |
| invokePara | Trigger parameter | Object |

"invokeCondition" is composed as follows:

| Parameter Name | Description | Type |
|---------|---------|---------|
| invokeMethod | Trigger <br>all: All <br>taglist: Specified tag <br>regex: Regular expression | String | No |
| invokeExpr | The expression of the trigger. <br>If invokeMethod is "all", this parameter is empty <br>If invokeMethod is "taglist", this parameter is the tag list, where multiple values are separated with ";", such as v1;v2;v3 <br>If invokeMethod is "regex", this parameter is a regular expression, such as ^test* | String | No |

"invokePara" is composed as follows:

| Parameter Name | Description | Type |
|---------|---------|---------|
| serviceName | Name of the service to be updated | String |
| clusterId | ID of the cluster for the service to be updated | String |
| namespace | Namespace of the service to be updated | String |
| containerName | Name of the container for the service to be updated | String |
| clusterRegion   | Region of the cluster for the service to be updated. <br>Region Codes: <br>1: Guangzhou <br>4: Shanghai <br>5: Hong Kong, China <br>7: Shanghai Finance <br>8: Beijing <br>9: Singapore <br>16: Chengdu | Int |

## 4. Samples
Input

```
  https://domain/v2/index.php?Action=ListTrigger
  &triggerName=trigger_test
  &offset=0
  &limit=20
  &reponame=test/kube_test
  &other common parameters
```
Output

```
{
    "code": 0,
    "message": "", 
    "codeDesc": "Success",
    "data": {
        "totalCount": 1,
        "triggerInfo": [
            {
                "triggerName": "trigger_test",
                "invokeSource": "IMAGE_PUSH",
                "invokeAction": "SERVICE_UPDATE",
                "repoName": "test/kube_test",
                "createTime": "2018-03-07 14:30:43",
                "updateTime": "2018-03-08 15:30:43",
                "invokeCondition": {
                    "invokeMethod": "all",
                    "invokeExpr": ""
                },
                "invokePara": {
                    "appId": "1254666666",
                    "clusterId": "cls-xxxxxxxx",
                    "namespace": "default",
                    "serviceName": "nginx-test",
                    "containerName": "nginx-test",
                    "clusterRegion": 1
                }
            }
        ]
    }
}

```
