

## API Description
**Request method**: POST.

The API request address corresponds to the service access point one by one; therefore, please select the request address corresponding to your application service access point.

Service access point in Guangzhou:
```shell
https://api.tpns.tencent.com/v3/device/account/batchoperate
```
Service access point in Hong Kong (China):
```shell
https://api.tpns.hk.tencent.com/v3/device/account/batchoperate
```
Service access point in Singapore:
```shell
https://api.tpns.sgp.tencent.com/v3/device/account/batchoperate
```
Service access point in Shanghai:
```shell
https://api.tpns.sh.tencent.com/v3/device/account/batchoperate
```

**Feature**: this is an async API that is only responsible for task issuance, with real-time operation currently unsupported.




## Parameter Description
#### Request parameters

| Parameter Name | Type | Required | Description |
| -------------- | ------- | ---- | ---------------------------------------- |
| operator_type | Integer | Yes | Operation type. Value range: [1,5] as detailed below: <li>1: bind token to an account. </li><li>2: bind token to an account in an overwriting manner. </li><li>3: unbind token from multiple accounts. </li><li>4: unbind token from all accounts. </li><li>5: unbind account from all tokens.</li> |
| platform | String | Yes | Client platform type <li>Android: Android </li><li>iOS: iOS </li>|
| account_list | Array | No | The collection of account IDs, which is valid if `operator_type` is 5, with each element being required, including account and account_type fields.<br> For example:<br>`[{"account":"926@126.com"},{"account":"1527000000"}]`|
| token_list | Array | No | The collection of device IDs, which is valid if `operator_type` is 4 and is required|
| token_accounts | Array | No | It is valid if `operator_type` is 1, 2, or 3 and must be called each time. Up to 20 tokens are allowed, and each `token_account` consists of 1 token and 1 `account_list`. Below is an example:<br>`[{"token":"token1","account_list":[{"account":"926@126.com"},{"account":"1527000000"}],`<br>`{"token":"token2","account_list":[{"account":"926@163.com",{"account":"1527000001"}]}]` |


#### Response parameters

| Parameter Name | Type | Description |
| -------------- | ------- | ---------------------------------------- |
| ret_code | Integer | Return code |
| err_msg | String | Error message |
| result | Array | Operation status code corresponding to each token or account ["0","1008006"] |


## Samples
#### Sample request

- Binds token to an account
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
- Binds token to an account in an overwriting manner
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
- Unbinds token from all accounts
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
- Unbinds account from all tokens
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



#### Sample return

Binds token to an account
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

