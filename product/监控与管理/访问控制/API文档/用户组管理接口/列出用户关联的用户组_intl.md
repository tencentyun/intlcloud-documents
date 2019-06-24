## API Description

This API (ListGroupsForUser) is used to get the list of the user groups associated with a user.

Request domain name:

```
cam.api.qcloud.com
```

## Input Parameters

The following request parameter list only provides the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/6976).

| Parameter Name | Type | Required | Description |
| -------- | ---- | -------- | ------------------------------------- |
| page | int | No | Page number. From 1 to 200. The default is 1. |
| rp | int | No | Number of items on each page. Greater than 0 and less than or equal to 200. The default is 20. |
| uid | int | Yes | User id |

## Output Parameters

| Parameter Name | Type | Description |
| --------- | ----- | ------------------------------------------------------------ |
| totalNum | int | The total number of user groups a user joins |
| groupInfo | array | Array of user groups, where each member has the following fields: groupId (user group ID), groupName (user group name), and remark (user group description). |

## Example

### Input

```
https://cam.api.qcloud.com/v2/index.php
?rp=10
&page=1
&uid=1133398
&SignatureMethod=HmacSHA256
&Action=ListGroupsForUser
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=23509
&Timestamp=1512716160
&RequestClient=SDK_PHP_1.1
&Signature=PsukZTcNW5Ev2%2FY%2F6QBBpu1DntyI4VMFu6PywZQQ5Ww%3D
```

### Output

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "groupInfo": [
            {
                "groupId": 28791,
                "groupName": "testgrname",
                "remark": "tee123"
            }
        ],
        "totalNum": "1"
    }
}
```

## Error Codes

For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/598/13884).

