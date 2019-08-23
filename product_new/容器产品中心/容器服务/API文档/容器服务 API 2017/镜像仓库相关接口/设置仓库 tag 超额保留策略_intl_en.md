## 1. API Description
This API (SetAutoDelStrategy) sets the auto deletion policy when the number of repository tags exceeds the upper limit. Tags are automatically deleted when the quota limit is reached.
API domain name: `ccr.api.qcloud.com`

## 2. Input Parameters
The following parameters are action-specific. For common parameters required for all API requests, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter Name | Description | Type | Required | 
|---------|---------|---------|---------
| reponame | Repository name | String | Yes |
| type | Policy type <br>keep\_last\_days: keep last how many days data. <br>keep\_last\_nums: keep how many the most recent data points. | String | Yes |
| val | Policy value | Int | Yes |


## 3. Output Parameters
 
| Parameter Name | Description | Type | 
|---------|---------|---------|
| code | Common error code. 0: Successful; other values: Failed. | Int | 
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |
| message | Description of the Module error related to this API | String |

## 4. Samples
Input

```
  https://domain/v2/index.php?Action=SetAutoDelStrategy
  &reponame=test/kube_test
  &type=keep_last_nums
  &val=10 
  &other common parameters
```
Output

```
{
    "code": 0,
    "message": "", 
    "codeDesc": "Success"
}

```
