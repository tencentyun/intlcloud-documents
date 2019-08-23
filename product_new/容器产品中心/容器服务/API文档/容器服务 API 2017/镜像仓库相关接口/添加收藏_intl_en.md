## API Description
This API (AddFavor) adds the specified repository to Favorites.
API domain name:

````
ccr.api.qcloud.com
````

## Input Parameters
The following parameters are action-specific. For common parameters required for all API requests, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter Name | Description | Type | Required |
|---------|---------|---------|---------|
| reponame | Repository name | String | Yes |
| repotype   | Type of the repository added to Favorites <br>QCLOUD HUB: Tencent Cloud repository <br>DOCKER HUB: Docker Hub image | String | Yes |

## Output Parameters

| Parameter Name | Description | Type |
|---------|---------|---------|
| code | Common error code. 0: Successful; other values: Failed. | Int |
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |
| message | Description of the Module error related to this API | String |

## Samples
### Input

```
  https://domain/v2/index.php?Action=AddFavor
  &reponame=test/kube_test
  &repotype=QCLOUD HUB
  &other common parameters
```
### Output

```
{
    "code": 0,
    "message": "", 
    "codeDesc": "Success"
}

```