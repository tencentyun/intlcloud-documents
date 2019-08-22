## 1. API Description
This API (GetAutoDelStrategy) gets the auto deletion policy when the number of repository tags exceeds the upper limit.
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
| totalCount | Number of policies | Int |
| strategyInfo | List of policy details | Object Array |

"strategyInfo" is composed as follows:

| Parameter Name | Description | Type |
|---------|---------|------|
| username | User name of the image repository | String |
| reponame | Repository name | String |
| type | Policy type <br>keep\_last\_days: keep last how many days data. <br>keep\_last\_nums: keep how many the most recent data points. | String | Yes |
| value | Policy value | Int |
| valid | Whether the policy is valid. 1: Valid; 0: Invalid | Int |
| creation_time | Time of the policy was created | String |

## 4. Samples
Input

```
  https://domain/v2/index.php?Action=GetAutoDelStrategy
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
        "strategyInfo": [
            {
                "username": "100001066666",
                "repo_name": "test/kube_test",
                "type": "keep_last_nums",
                "value": 10,
                "valid": 1,
                "creation_time": "2018-03-07T16:53:23+08:00"
            }
        ],
        "totalCount": 1
    }
}

```
