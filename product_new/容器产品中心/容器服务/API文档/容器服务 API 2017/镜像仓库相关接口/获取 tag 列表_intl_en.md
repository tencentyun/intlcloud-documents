## 1. API Description
This API (GetTagList) gets the image tag list.
API domain name: `ccr.api.qcloud.com`

## 2. Input Parameters
The list below contains only the API request parameters. For the complete common parameter list, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter Name | Description | Type | Required |
|---------|---------|---------|---------|
| reponame | Repository name | String | Yes |
| offset | Offset. Default is 0. | Uint | No |
| limit | Maximum number of returned results. Defaults is 20, and maximum is 100. | Uint | No |
| tag | Tag name used for search | String | No |


## 3. Output Parameters

| Parameter Name | Description | Type |
|---------|---------|---------|
| code | Common error code. 0: Successful; other values: Failed. | Int |
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |
| message | Description of the Module error related to this API | String |
| reponame | Repository name | String |
| server | Domain name of an image repository | String |
| tagCount | Number of tags | Int |
| tagInfo | Tag list. Results are sorted in descending order by pushTime | Object Array |

"tag" is composed as follows:

| Parameter Name | Description | Type |
|---------|---------|---------|
| repo_name | The name of the repository of the corresponding tag | String |
| tagName | Tag name | String |
| tagId | Tag ID | String |
| imageId | Image ID | String |
| size | Image size | String |
| creationTime | Creation time | String |
| updateTime | Update time | String |
| author | Image creator | String |
| architecture | CPU architecture | String |
| dockerVersion | Docker client tag |String |
| os | Operating system | String |
| pushTime | Push time | String |
| sizeByte | Image size (in bytes) | Int |
## 4. Samples
Input

```
  https://domain/v2/index.php?Action=GetTagList
  &reponame=test/kubetest  
  &offset=0
  &limit=20
  &tag=nginx_v1
  &other common parameters
```
Output

```
{
    "code": 0,
    "message": "", 
    "codeDesc": "Success",
    "data": {
	    "reponame": "test/kubetest",
	    "server": "ccr.ccs.tencentyun.com",
	    "tagCount": 1,
	    "tagInfo": [
	      {
	        "repo_name": "kubetest",
	        "tagName": "nginx_v1",
	        "tagId": "sha256:5fbb3629fba1c7c875015c9cb4c27f1d9e8e92d2f027f09b6eda35ff952323a1",
	        "imageId": "sha256:146c8220814be5f07a03b0b0b1e352ce42278684266d95670bf3e11225441b70",
	        "size": "59 MB",
	        "creationTime": "2017-09-12 15:30:23 +0800 CST",
	        "updateTime": "2017-10-25 16:33:51 +0800 CST",
	        "author": "",
	        "architecture": "amd64",
	        "dockerVersion": "1.12.5",
	        "os": "linux",
	        "pushTime": "2017-09-12 15:33:39 +0800 CST",
	        "sizeByte": 59229024
	      }
	    ]
	}
}

```
