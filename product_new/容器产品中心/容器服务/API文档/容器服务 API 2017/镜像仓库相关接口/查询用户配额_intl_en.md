## 1. API Description
This API (GetLimit) gets a user's quota.
API domain name: `ccr.api.qcloud.com`

## 2. Input Parameters
No parameter is provided for this API. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

## 3. Output Parameters
 
| Parameter Name | Description | Type | 
|---------|---------|---------|
| code | Common error code. 0: Successful; other values: Failed. | Int | 
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |
| message | Description of the Module error related to this API | String |
| limitInfo | Quota information | Object Array |

"limitInfo" is composed as follows:

| Parameter Name | Description | Type | 
|---------|---------|---------|
| username | User name of an image repository | String |
| type | Quota type <br>namespace: Namespace <br>repo: Repository <br>tag: Image tag <br>triggers: Trigger | String |
| value | Quota value | Int |

## 4. Samples
Input

```
  https://domain/v2/index.php?Action=GetLimit
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
        "limitInfo": [
            {
                "username": "100001066666",
                "type": "namespace",
                "value": 10
            },
            {
                "username": "100001066666",
                "type": "repo",
                "value": 100
            },
            {
                "username": "100001066666",
                "type": "tag",
                "value": 100
            },
            {
                "username": "100001066666",
                "type": "triggers",
                "value": 10
            }
        ]
    }
}

```