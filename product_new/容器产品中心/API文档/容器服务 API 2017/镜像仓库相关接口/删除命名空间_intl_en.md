## API Description
This API (DeleteUserNamespace) deletes the specified namespace.
API domain name:

````
ccr.api.qcloud.com
````

## Input Parameters
The following parameters are action-specific. For common parameters required for all API requests, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter Name | Description | Type | Required |
|---------|---------|---------|---------|
| namespace | Namespace name | String | No |


## Output Parameters

| Parameter Name | Description | Type |
|---------|---------|---------|
| code | Common error code. 0: Successful; other values: Failed. | Int |
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |
| message | Description of the Module error related to this API | String |


## Samples
### Input

```
  https://domain/v2/index.php?Action=DeleteUserNamespace
  &namespace=mynamespace
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