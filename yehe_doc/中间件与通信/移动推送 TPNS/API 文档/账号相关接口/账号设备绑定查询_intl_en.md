
## API Description
**Request method**: POST

```plaintext
Service URL/v3/device/account/query
```
API service URLs correspond to service access points one to one. Please select the [service URL](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.

**Feature**: this API is used to query the binding relationships between accounts and tokens.



## Parameters
#### Request parameters
| Parameter | Type | Required | Description |
| -------------- | ------- | ---- | ---------------------------------------- |
| operator_type | Integer | Yes | Operation type:<li>`1`: Batch query tokens by account<li>`2`: Query accounts by token |
| account_list | Array | No | Account list. This parameter is valid and required when `operator_type` is `1`. Each element of the list contains one set of accounts. Example: `[{"account":"account1"},{"account":"account2"}]` |
| token_list | Array | No | Token list. This parameter is valid and required when `operator_type` is `2`. |

#### Response parameters

| Parameter | Type | Description |
| -------------- | ------- | ---------------------------------------- |
| retCode | Integer | Error code. For more information, please see [Server-Side Error Codes](https://intl.cloud.tencent.com/document/product/1024/33763).  |
| errMsg | String | Error message|
| account_tokens | Array | Array of mappings from accounts to tokens. Example:<br>`[{"account":"account1","token_list":["token1","token2"]}{"account":"account2","token_list":["token2","token3"]}`] |
| token_accounts | Array | Array of mappings from tokens to accounts. Example:<br>`[{"token":"token1","account_list":[{"account":"926@126.com"},{"account":"1527000000",}]},`<br/>`{"token":"token2","account_list":[{"account":"926@163.com"},{"account":"1527000001"}]}]` |


## Samples
#### Sample request

- Batch query the relationships of tokens bound to accounts
```json
{
    "operator_type": 1,
    "account_list": [
        {
            "account": "account1"
        },
        {
            "account": "account2"
        }
    ]
}
```
- Batch query the relationships of accounts bound to tokens
```json
{
    "operator_type": 2,
    "token_list": [
        "token1",
        "token2"
    ]
}
```

#### Sample response
- Batch query the tokens bound to accounts
```json
{
    "retCode": 0,
    "errMsg": "ok",
    "result": [
        "0",
        "0"
    ],
    "account_tokens": [
        {
            "account": "account1",
            "token_list": [
                "token1",
                "token2"
            ]
        },
        {
            "account": "account2",
            "token_list": [
                "token2",
                "token3"
            ]
        }
    ]
}
```
- Batch query the accounts bound to tokens
```json
{
    "retCode": 0,
    "errMsg": "ok",
    "result": [
        "0",
        "0"
    ],
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


