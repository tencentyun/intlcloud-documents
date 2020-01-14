

## API Description
**Request method**: POST.
```shell
https://api.tpns.tencent.com/v3/device/account/batchoperate
```
**Feature**: This is an async API that is only responsible for task issuance, with real-time operation currently unsupported.




## Parameter Descriptions
#### Request Parameters

| Parameter name | Type | Required | Description |
| -------------- | ------- | ---- | ---------------------------------------- |
| operator_type | int | Yes | Operation type<br><li>Bind token to an account<li>Bind token to an account in an overriding manner<li>Unbind token from multiple accounts<li>Unbind token from all accounts <li>Unbind account from all tokens |
| platform | string | Yes | Client platform type<li>Android: Android<br><li>iOS: Apple |
| account_list | jsonArrary | No | The collection of account IDs, which is valid when operator_type = 5, with each element being required, including account and account_type fields.<br> For example:<br>`[{"account":"926@126.com"},{"account":"1527000000"}]`|
| token_list | jsonArrary | No | The collection of device IDs, which is valid when operator_type = 4 and is required|
| token_accounts | jsonArrary | No | It is valid when operator_type = 1, 2, or 3 and must be called each time. Up to 20 tokens are allowed, and each token_account consists of 1 token and 1 account_list. Below is a specific example:<br>`[{"token":"token1","account_list":[{"account":"926@126.com"},{"account":"1527000000"}],`<br>`{"token":"token2","account_list":[{"account":"926@163.com",{"account":"1527000001"}]}]` |


#### Response Parameters
| Parameter name | Type | Description |
| -------------- | ------- | ---------------------------------------- |
| ret_code       | int  | Return code |
| err_msg | String | Error message |
| result | JsonArrary | Operation status code corresponding to each token or account["0","1008006"] |


## Example
#### Request Example

- Bind token to an account
```json
{
    "operator_type": 1,
    "platform": "android",
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
- Bind token to an account in an overriding manner
```json
{
    "operator_type": 2,
    "platform": "android",
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
- Unbind token from an account
```json
{
    "operator_type": 3,
    "platform": "android",
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
- Unbind token from all accounts
```json
{
    "operator_type": 4,
    "platform": "android",
    "token_list": [
        "token1",
        "token2",
        "token3"
    ]
}
```
- Unbind account from all tokens
```json
{
    "operator_type": 5,
    "platform": "android",
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



#### Return Example

- Bind token to an account
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

