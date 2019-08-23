## API Description
This API (GetFavor) gets the list of repositories added to Favorites.
API domain name:

````
ccr.api.qcloud.com
````

## Input Parameters
The following parameters are action-specific. For common parameters required for all API requests, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter Name | Description | Type | Required |
|---------|---------|---------|---------|
| offset | Query offset. The default value is 0 | Uint | No |
| limit | Query quantity. The default value is 20 | Uint | No |

## Output Parameters

| Parameter Name | Description | Type |
|---------|---------|---------|
| code | Common error code. 0: Successful; other values: Failed. | Int |
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |
| message | Description of the Module error related to this API | String |
| totalCount | Number of query results | String |
| repoInfo | Repository information | Object Array |

"repoInfo" is composed as follows:

| Parameter Name | Description | Type |
|---------|---------|---------|
| reponame | Repository name | String |
| repotype | Repository type <br>QCLOUD HUB: Tencent Cloud repository <br>DOCKER HUB: DockerHub image | String |
| tagCount | Number of tags | Int |
| public | Whether the repository is public. 1: Yes; 0: No | Int |
| isQcloudOfficial | Whether the repository is Tencent Cloud official repository. true: Yes; false: No | Bool |
| favorCount | The number of times a repository is added to Favorites by all users | Int |


## Samples
### Input

```
  https://domain/v2/index.php?Action=GetFavor
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
			"repoInfo": [{
				"reponame": "library/wordpress",
				"repotype": "QCLOUD HUB",
				"favorCount": 62,
				"public": 1,
				"isQcloudOfficial": false,
				"tagCount": 18
			}],
			"totalCount": 1
		}
}

```