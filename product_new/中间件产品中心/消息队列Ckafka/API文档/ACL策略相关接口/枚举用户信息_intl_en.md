>!This is a legacy API which has been hidden and will no longer be updated. We recommend using the new [CKafka API 3.0](https://intl.cloud.tencent.com/document/product/597/36407) which is standardized and faster.
>

> This feature is currently in beta. If you want to try this feature in the console, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to be allowlisted.

## 1. API Description
This API (ListUser) is used to enumerate the information of all users.

API domain name: `ckafka.api.qcloud.com`

## 2. Input Parameters
The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/product/406/5883).

| Parameter Name | Required | Type | Description |
| --- | --- | --- | --- |
| instanceId | Yes | String | Instance ID |
| searchWord| No | String | (Filter) Filter by username. Fuzzy search is supported |
| offset| No | String | Offset. Default value is 0 if left empty |
| limit| No | String | Number of results to be returned. Default value is 10 if left empty. Maximum value is 20 |

## 3. Output Parameters

| Parameter Name | Type | Description |
| --- | --- | --- |
|users|Array| List of users |
|userId|Int| User ID |
|name|String| Username |
|adminFlag|Int| Flag indicates whether the user is an admin |
|ctime|String| Creation time |
|mtime|String| Last modified time |

## 4. Samples

Input:

```
 https://domain/v2/index.php?Action=ListUser
  &instanceId=ckafka-tadfqa0
  &<Common Request Parameters>
```

Output:

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "users": [
            {
                "userId": 14,
                "name": "tesst2342",
                "ctime": "2018-04-12 20:08:33",
                "mtime": "2018-04-12 20:41:34"
            },
            {
                "userId": 15,
                "name": "tesst2f342",
                "ctime": "2018-04-12 20:08:36",
                "mtime": "2018-04-12 20:08:36"
            },
            {
                "userId": 16,
                "name": "tesst2fsd342",
                "ctime": "2018-04-12 20:08:39",
                "mtime": "2018-04-12 20:08:39"
            }
        ],
        "totalCount": 3
    }
}
```
