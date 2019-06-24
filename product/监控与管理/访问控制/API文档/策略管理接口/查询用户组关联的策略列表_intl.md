## API Description

This API (ListAttachedGroupPolicies) is used to query the list of policies associated with a user group.

Request domain name:

```
cam.api.qcloud.com 
```

## Input Parameters

The following request parameter list only provides the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/6976).

| Parameter Name | Type | Required | Description |
| -------- | ---- | ---- | --------------------------- |
| groupId | int | Yes | User group ID |
| page | int | No | Page number, which starts from 1. It defaults to 1. |
| rp | int | No | Page size. It defaults to 20. |

## Output Parameters

For more information, see [ListPolicies](https://intl.cloud.tencent.com/document/product/598/15426) API description.

## Example

### Input

```
https://cam.api.qcloud.com/v2/index.php
?groupId=34444
&page=1
&rp=20
&SignatureMethod=HmacSHA256
&Action=ListAttachedGroupPolicies
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=44835
&Timestamp=1523262775
&RequestClient=SDK_PHP_1.1&
Signature=vBfc7JZiDSZZysKesDoywMN3ca80pgZmWVdiQ4QXJJg%3D
```

### Output

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "totalNum": 1,
        "list": [
            {
                "policyId": 1,
                "policyName": "AdministratorAccess",
                "addTime": "2018-04-09 16:31:19",
                "createMode": 2
            }
        ]
    }
}
```

## Error Codes

For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/598/13884).

