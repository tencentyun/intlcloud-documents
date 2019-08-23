## API Description
This API (ListTriggerLog) gets the triggering log.
API domain name:

````
ccr.api.qcloud.com
````

## Input Parameters
The following parameters are action-specific. For common parameters required for all API requests, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter Name | Description | Type | Required |
|---------|---------|---------|---------|
| reponame | Repository name | String | Yes |
| offset | Data offset. Default is 0 | Int | No |
| limit | Maximum number of returned data entries. Default is 20 | Int | No |
| order   | If sorted by time, desc means descending order, while asc means ascending order | String | No |
| orderby   | Sorting rule for returned entries. Supported sorting fields include `invoke_time`, `trigger_name`, and `repo_name` | String | No |

## Output Parameters

| Parameter Name | Description | Type |
|---------|---------|---------|
| code | Common error code. 0: Successful; other values: Failed. | Int |
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |
| message | Description of the Module error related to this API | String |
| totalCount | Total number of query results | Int |
| logInfo | Information of the triggering action|Object Array |

"logInfo" is composed as follows:

| Parameter Name | Description | Type |
|---------|---------|---------|
| triggerName | Trigger name | String |
| repoName | Name of the repository bound with the trigger | String |
| tagName   | Image repository tag | String |
| invokeSource | Cause of trigger. The value is always set to "IMAGE_PUSH", which means the trigger is initiated by image push | String |
| invokeAction | Trigger action. The value is always set to "SERVICE_UPDATE", which means to update the service | String |
| invokeTime | Triggering time | String |
| invokeCondition   | Trigger condition | Object |
| invokePara | Trigger parameter | Object |
| invokeResult | Trigger result | Object |

"invokeCondition" is composed as follows:

| Parameter Name | Description | Type |
|---------|---------|---------|
| invokeMethod | Trigger <br>all: All <br>taglist: Specified tag <br>regex: Regular expression | String |
| invokeExpr | The expression of the trigger. <br>If invokeMethod is "all", this parameter is empty <br>If invokeMethod is "taglist", this parameter is the tag list, where multiple values are separated with ";", such as v1;v2;v3 <br>If invokeMethod is "regex", this parameter is a regular expression, such as ^test* | String |

"invokePara" is composed as follows:

| Parameter Name | Description | Type |
|---------|---------|---------|
| appId   | User APPID | String |
| serviceName | Name of the service to be updated | String |
| clusterId | ID of the cluster for the service to be updated | String |
| namespace | Namespace of the service to be updated | String |
| containerName | Name of the container for the service to be updated | String |
| clusterRegion   | Region of the cluster for the service to be updated. <br>Region Codes: <br>1: Guangzhou <br>4: Shanghai <br>5: Hong Kong, China <br>7: Shanghai Finance <br>8: Beijing <br>9: Singapore <br>16: Chengdu | Int |

"invokeResult" is composed as follows:

| Parameter Name | Description | Type |
|---------|---------|---------|
| returnCode | Trigger result. 0: Successful; Other values: Failed | Int |
| returnMsg | Trigger result message | String |
## Samples
### Input

```
  https://domain/v2/index.php?Action=ListTriggerLog
  &offset=0
  &limit=20
  &reponame=test/kube_test
  &other common parameters
```
### Output

```
{
    "code": 0,
    "message": "", 
    "codeDesc": "Success",
    "data": {
			"logInfo": [{
				"repoName": "kubetest/kubetest",
				"tagName": "latest",
				"triggerName": "trigger_test",
				"invokeSource": "IMAGE_PUSH",
				"invokeAction": "SERVICE_UPDATE",
				"invokeTime": "2018-07-23 23:13:27",
				"invokeCondition": {
					"invokeMethod": "regex",
					"invokeExpr": "test*"
				},
				"invokePara": {
					"appId": "1254119589",
					"clusterId": "cls-666666",
					"namespace": "default",
					"serviceName": "nginx-test",
					"containerName": "nginx-test",
					"clusterRegion": 1
				},
				"invokeResult": {
					"returnCode": 0,
					"returnMsg": "ok"
				}
			}],
			"totalCount": 1
	}
}

```
