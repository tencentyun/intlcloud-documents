## API Description

This API (BatchDeleteFavor) removes one or more repositories from Favorites in batches. 

API domain name:
```
ccr.api.qcloud.com
```

## Input Parameters

The following parameters are action-specific. For common parameters required for all API requests, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter name | Description | Type | Required |
| -------- | ---------------- | ------------ | ---- |
| favors | Array of the favorite repositories | Object Array | Yes |

## Output Parameters

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| code | Common error code. 0: Successful; other values: Failed. | Int |
| message | Module error message description depending on API | String |
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |



## Samples

### Input

```
  https://domain/v2/index.php?Action=BatchDeleteFavor
  &favors.0.reponame="xxx"
  &favors.0.repotype="DOCKER HUB"
  &favors.0.regionId=1
  &favors.1.reponame="qcloud/yyy"
  &favors.1.repotype="QCLOUD HUB"
  &favors.1.regionId=1
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
