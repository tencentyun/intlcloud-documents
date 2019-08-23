## API Description
This API (GetRepositoryList) queries the list of TencentHub public repositories, including all Tencent Cloud official repositories and public repositories provided by users.
API domain name:

````
ccr.api.qcloud.com
````

## Input Parameters
The following parameters are action-specific. For common parameters required for all API requests, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter Name | Description | Type | Required |
|---------|---------|---------|---------|
| offset | Offset. Default is 0. | Uint | No |
| limit | Maximum number of returned results. Defaults is 20, and maximum is 100. | Uint | No |
| reponame | Name of the repository to be queried. All repositories will be queried if no value is assigned. | String | No |
| orderby | Sort-by field. If this parameter is left blank, the  repository will be sorted randomly. <br>official: Sort by official image status <br>pullCount: Sort by number of downloads | String | No |
| Order | Ascending or descending order. The default value is desc, but you can also choose asc | String | No |

## Output Parameters

| Parameter Name | Description | Type |
|---------|---------|---------|
| code | Common error code. 0: Successful; other values: Failed. | Int |
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |
| message | Description of the Module error related to this API | String |
| repoInfo | Repository information | Object Array |

"repoInfo" is composed as follows:

| Parameter Name | Description | Type |
|---------|---------|---------|
| reponame | Repository name | String |
| repotype | Repository type <br>QCLOUD HUB: Tencent Cloud repository <br>DOCKER HUB: DockerHub image | String |
| tagCount | Number of tags | Int |
| public | Whether the repository is public. 1: Public; 0: Private | Int |
| isUserFavor | Whether the user has added this repository to Favorites. true: Yes; false: No | Bool |
| isQcloudOfficial | Whether the repository is Tencent Cloud official repository. true: Yes; false: No | Bool |
| favorCount | The number of times a repository is added to Favorites by all users | Int |
| pullCount | Number of times the repository was downloaded | Int |
| description | Description | String |
| creationTime | Creation time | String |
| updateTime | Update time | String |

## Samples
### Input

```
  https://domain/v2/index.php?Action=TencentHub
  &offset=0
  &limit=20
  &other common parameters
```
### Output

```
{
    "code": 0,
    "message": "", 
    "codeDesc": "Success",
    "data": {
		"totalCount": 1,
	    "privilegeFiltered": false,
	    "repoInfo": [
	      {
	        "reponame": "test/kubetest",
	        "repotype": "QCLOUD HUB",
	        "tagCount": 2,
	        "public": 0,
	        "isUserFavor": false,
	        "isQcloudOfficial": false,
	        "favorCount": 0,
	        "pullCount": 5137,
	        "description": "",
	        "creationTime": "2017-09-12 13:02:58",
	        "updateTime": "2018-02-28 14:26:06"
	      }
	   ]
	}
}

```
