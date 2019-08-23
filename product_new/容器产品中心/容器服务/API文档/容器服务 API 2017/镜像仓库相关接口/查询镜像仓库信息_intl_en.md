## 1. API Description
This API (GetRepositoryInfo) gets the information of the specified repository.
API domain name: `ccr.api.qcloud.com`

## 2. Input Parameters
The following parameters are action-specific. For common parameters required for all API requests, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter Name | Description | Type | Required |
|---------|---------|---------|---------|
| reponame | Repository name | String | Yes |


## 3. Output Parameters

| Parameter Name | Description | Type |
|---------|---------|---------|
| code | Common error code. 0: Successful; other values: Failed. | Int |
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |
| message | Description of the Module error related to this API | String |
| creationTime | Time when the repository is created | String |
| description | Repository description | String |
| favorCount | The number of times a repository is added to Favorites | String |
| isQcloudOfficial | Whether the repository is Tencent Cloud official repository. true: Yes; false: No| Bool |
| isUserFavor | Whether the use has added the repository to Favorites list. true: Yes; false: No | Bool |
| public | Whether it is a public repository. 1: Public; 0: Private | Uint |
| pullCount | Number of times the repository was pulled | Uint |
| reponame | Repository name | String |
| repotype | Repository type <br>QCLOUD HUB: Tencent Cloud repository <br>DOCKER HUB: DockerHub image | String |

## 4. Samples
Input

```
  https://domain/v2/index.php?Action=GetRepositoryInfo
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
        "creationTime": "2017-12-28 11:00:10",
        "description": "",
        "favorCount": 0,
        "isQcloudOfficial": false,
        "isUserFavor": false,
        "public": 0,
        "pullCount": 0,
        "reponame": "test/kube_test",
        "repotype": "QCLOUD HUB"        
    }
}

```