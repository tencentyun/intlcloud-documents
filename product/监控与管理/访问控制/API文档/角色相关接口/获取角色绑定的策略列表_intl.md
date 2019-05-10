## API Description

This API (ListAttachedRolePolicies) is used to obtain a list of policies associated with a role.
Request domain name:

```
cam.api.qcloud.com
```

## Input Parameters 

The following request parameter list only provides the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/6976).

| Parameter Name | Type | Required | Description |
| ---------- | ------ | ---- | ------------------------------------------------------------ |
| roleId | String | No | Role ID used to specify a role. Either roleId or roleName can be used as the input parameter. |
| roleName | String | No | Role name used to specify a role. Either roleId or roleName can be used as the input parameter. |
| page | int | No | Page number, which starts from 1. It defaults to 1. |
| rp | int | No | Page size. It defaults to 20. |
| policyType | String | No | Available values: "User", which means to query custom policies only, and "QCS", which means to query preset policies only. If not specified, all associated policies are queried. |

## Output Parameters 

| Parameter Name | Type | Description |
| -------- | ----- | ------------------------------------------------------------ |
| totalNum | int | Total number of policies |
| list | array | Policy array, of which each member contains the following fields:<li>policyId: Policy ID <li>policyName: Policy name<li>addTime: Policy creation time<li>description: Policy description<li>createMode: 1 indicates a policy created according to business permissions, while other values indicate you can view policy syntax and update a policy through the policy syntax. |

## Example 
### Input
```
https://cam.api.qcloud.com/v2/index.php
?roleName=testRole
&page=1
&rp=20
&SignatureMethod=HmacSHA256
&Action=ListAttachedRolePolicies
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=33994
&Timestamp=1508492653
&RequestClient=SDK_PHP_1.1
&Signature=YQflvL9ZCPDfTJNum84oXRQex6iKKTNi2fwgLUh2qZE%3D
```

### Output

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "totalNum": 3,
        "list": [
            {
                "policyId": 524497,
                "policyName": "testpppName323",
                "addTime": "2017-10-20 17:26:16",
                "policyType": "User",
                "createMode": 2
            },
            {
                "policyId": 296232,
                "policyName": "QcloudCCSInnerFullAccess",
                "addTime": "2017-10-20 17:11:19",
                "policyType": "QCS",
                "createMode": 2
            },
            {
                "policyId": 219851,
                "policyName": "QcloudCLBReadOnlyAccess",
                "addTime": "2017-09-04 16:40:15",
                "policyType": "QCS",
                "createMode": 2
            }
        ]
    }
}
```

## Error Codes
For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/598/13884).

