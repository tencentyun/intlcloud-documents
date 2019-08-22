## API Description
This API (GetNamespaceInfo) queries the specified namespace.
API domain name:

````
ccr.api.qcloud.com
````

## Input Parameters
The following parameters are action-specific. For common parameters required for all API requests, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter Name | Description | Type | Required |
|---------|---------|---------|---------|
| namespace | Fuzzy search by namespace name is supported | String | No |
| offset | Query offset. The default value is 0 | Uint | No |
| limit | Query quantity. The default value is 20 | Uint | No |

## Output Parameters

| Parameter Name | Description | Type |
|---------|---------|---------|
| code | Common error code. 0: Successful; other values: Failed. | Int |
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |
| message | Description of the Module error related to this API | String |
| namespaceCount | Number of query results | String |
| namespaceInfo | Namespace information | Object Array |

"namespaceInfo" is composed as follows:

| Parameter Name | Description | Type |
|---------|---------|---------|
| namespace | Namespace | String |
| creationTime | Creation time | String |
| repoCount | Number of repositories under the namespace | Int |

## Samples
### Input

```
  https://domain/v2/index.php?Action=GetNamespaceInfo
  &limit=20
  &offset=0
  &other common parameters
```
### Output

```
{
	"code": 0,
	"message": "", 
	"codeDesc": "Success",
	"data": {
		"namespaceCount": 1,
		"namespaceInfo": [{
			"namespace": "mynamespace",
			"creationTime": "2018-07-25 15:07:12",
			"repoCount": 2
		}]
	}
}
```
