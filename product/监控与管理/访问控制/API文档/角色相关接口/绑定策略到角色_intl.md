## API Description
This API (AttachRolePolicy) is used to associate a policy with a role.
Request domain name: cam.api.qcloud.com

## Input Parameters
The following request parameter list only provides the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/6976).

| Parameter Name | Required | Type | Description |
| ------------ | ------------ | ------------ | ------------ |
| policyId | No | Int | Policy ID. Either policyId or policyName can be used as the input parameter. |
| policyName | No | String | Policy name. Either policyId or policyName can be used as the input parameter. |
| roleId | No | String | Role ID used to specify a role. Either roleId or roleName can be used as the input parameter. |
| roleName | No | String | Role name used to specify a role. Either roleId or roleName can be used as the input parameter. |

## Output Parameters

| Parameter Name | Type |Description |
| ------------ | ------------ | ------------ |
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href='https://intl.cloud.tencent.com/document/product/377/8946' title='Common Error Codes'>Common Error Codes</a> on the Error Codes page. |
| message | String | Module error message description depending on API. |
| codeDesc | String | Error description |

## Example
Input
```
https://cam.api.qcloud.com/v2/index.php?Action=AttachRolePolicy&policyId=296232
&roleId=4611686018427397919&<Common request parameters>
```

Output
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": []
}

````

