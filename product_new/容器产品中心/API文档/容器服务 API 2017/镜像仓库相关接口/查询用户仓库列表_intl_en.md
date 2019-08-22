## 1. API Description
This API (SearchUserRepository) searches a user's repository list.
API domain name: `ccr.api.qcloud.com`

## 2. Input Parameters
The following parameters are action-specific. For common parameters required for all API requests, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter Name | Description | Type | Required | 
|---------|---------|---------|---------
| offset | Offset. Default is 0. | Uint | No |
| limit | Maximum number of returned results. Defaults is 20, and maximum is 100. | Uint | No |
| reponame | Name of the repository to be queried. All repositories will be queried if no value is assigned. | String | No |
| public | Filter condition. 1: public; 0: private. Query all if this parameter is not specified. | String | No |
| namespace | Namespace | String | No |

## 3. Output Parameters
 
| Parameter Name | Description | Type | 
|---------|---------|---------|
| code | Common error code. 0: Successful; other values: Failed. | Int | 
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |
| message | Description of the Module error related to this API | String |
| totalCount | Number of query results | String |
| privilegeFiltered | false: Return all results; true: Not return all results | Bool |
| repoInfo | Repository information | Object Array |

"repoInfo" is composed as follows:

| Parameter Name | Description | Type | 
|---------|---------|---------|
| reponame | Repository name | String |
| repotype | Repository type <br>QCLOUD HUB: Tencent Cloud repository <br>DOCKER HUB: DockerHub image | String |
| tagCount | Number of tags | Int |
| public | Whether the repository is public. 1: Public; 0: Private | Int |
| isUserFavor | Whether the user has added this repository to Favorites. true: Yes; false: No | Bool |
| isQcloudOfficial | Whether the repository is Tencent Cloud official repository. true: Yes; false: No| Bool |
| favorCount | The number of times a repository is added to Favorites by all users | Int |
| pullCount | Number of times the repository was downloaded | Int |
| description | Description | String |
| creationTime | Creation time | String |
| updateTime | Update time | String |

## 4. Samples
Input

```
  https://domain/v2/index.php?Action=SearchUserRepository
  &offset=0
  &limit=20
  &reponame=test/kubetest
  &public=1
  &namespace=test
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
