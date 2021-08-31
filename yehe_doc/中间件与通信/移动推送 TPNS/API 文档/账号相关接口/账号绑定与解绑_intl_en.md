## API Description
**Request method**: POST

```plaintext
Service URL/v3/device/account/batchoperate
```
API service URLs correspond to service access points one to one. Please select the [service URL](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.

**Feature**: this is an async API that is only responsible for task issuance, with real-time operation currently unsupported.


## Fields
#### Request fields

| Field | Type | Required | Description |
| -------------- | ------- | ---- | ---------------------------------------- |
| operator_type | Integer | Yes | Operation type. Value range: [1,5] as detailed below: <li>1: bind a token to one more account. </li><li>2: bind a token to another account in an overriding manner. </li><li>3: unbind a token from multiple accounts. </li><li>4: unbind a token from all accounts. </li><li>5: unbind an account from all tokens.</li> |
| account_list | Array | No | List of account IDs. This field is valid and required when `operator_type` is `5`. Each element contains the `account` and `account_type` fields.<br> Example:<br>`[{"account":"926@126.com"},{"account":"1527000000"}]`|
| token_list | Array | No | List of device IDs. This field is valid and required when `operator_type` is `4`.|
| token_accounts | Array | No | This field is valid and required when `operator_type` is `1`, `2`, or `3`. Up to 20 tokens can be set in each call. Each `token_account` consists of 1 token and 1 `account_list`. Example:<br>`[{"token":"token1","account_list":[{"account":"926@126.com"},{"account":"1527000000"}],`<br>`{"token":"token2","account_list":[{"account":"926@163.com",{"account":"1527000001"}]}]` |

>? As the `token append account` API was seldom used and confusing to developers, it has been disused since October 26, 2020. If you have used it before, it will be replaced by the `Token clearAndAppendAccount` API.
>


#### Response fields

| Field | Type | Description |
| -------------- | ------- | ---------------------------------------- |
| ret_code | Integer | Error code. For more information, please see [Server-Side Error Codes](https://intl.cloud.tencent.com/document/product/1024/33763).|
| err_msg | String | Error message. |
| result | Array | Operation status code corresponding to each token or account ["0","1008006"]. |


## Samples
#### Sample request

- Bind a token to one more account
```json
{
    "operator_type": 1,
    "token_accounts": [
        {
            "token": "token1",
            "account_list": [
                {
                    "account": "926@126.com"
                },
                {
                    "account": "1527000000"
                }
            ]
        },
        {
            "token": "token2",
            "account_list": [
                {
                    "account": "926@163.com"
                },
                {
                    "account": "1527000001"
                }
            ]
        }
    ]
}
```
- Bind a token to another account in an overriding manner
```json
{
    "operator_type": 2,
    "token_accounts": [
        {
            "token": "token1",
            "account_list": [
                {
                    "account": "926@126.com"
                },
                {
                    "account": "1527000000"
                }
            ]
        },
        {
            "token": "token2",
            "account_list": [
                {
                    "account": "926@163.com"
                },
                {
                    "account": "1527000001"
                }
            ]
        }
    ]
}
```
- Unbind a token from an account
```json
{
    "operator_type": 3,
    "token_accounts": [
        {
            "token": "token1",
            "account_list": [
                {
                    "account": "926@126.com"
                },
                {
                    "account": "1527000000"
                }
            ]
        },
        {
            "token": "token2",
            "account_list": [
                {
                    "account": "926@163.com"
                },
                {
                    "account": "1527000001"
                }
            ]
        }
    ]
}
```
- Unbind a token from all accounts
```json
{
    "operator_type": 4,
    "token_list": [
        "token1",
        "token2",
        "token3"
    ]
}
```
- Unbind an account from all tokens
```json
{
    "operator_type": 5,
    "account_list": [
        {
            "account": "926@126.com"
        },
        {
            "account": "1527000000"
        }
    ]
}
```



#### Sample response

Bind a token to one more account
``` json
{
    "result": [
        "ok",
        "ok"
    ],
    "ret_code": 0,
    "err_msg": "ok"
}
```

