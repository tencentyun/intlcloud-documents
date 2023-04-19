## API Calling Description
**Request method**: POST.

```plaintext
Service URL/v3/device/account/batchoperate
```
The API service address corresponds to the service access point one by one; therefore, please select the service address corresponding to your application [service access point](https://www.tencentcloud.com/document/product/1024/38517).

**Feature**: this is an async API that is only responsible for task issuance, with real-time operation currently unsupported.


## Parameter description
#### Request parameters

| Parameter | Type | Required | Description |
| -------------- | ------- | ---- | ---------------------------------------- |
| operator_type | Integer | Yes | Operation type. Value range: [1, 5] <li>(Disused) `1`: Bind a token to one more account. </li><li>`2`: Bind a token to another account in an overriding manner. </li><li>`3`: Unbind a token from multiple accounts. </li><li>`4`: Unbind a token from all accounts. </li><li>`5`: Unbind an account from all tokens.</li> |
| account_list | Array | No | List of account IDs. This field is valid and required when `operator_type` is `5`. Each element contains the `account` and `account_type` (for type setting) fields.<br> Example:<br>`[{"account":"926@126.com"},{"account":"1527000000"},{"account":"2849249569","account_type":9}]`|
| token_list | Array | No | List of device IDs. This field is valid and required when `operator_type` is `4`.|
| token_accounts | Array | No | This field is valid and required when `operator_type` is `1`, `2`, or `3`. Up to 20 tokens can be set in each call. Each `token_account` consists of 1 token and 1 `account_list`. Example:<br>`[{"token":"token1","account_list":[{"account":"926@126.com"},{"account":"1527000000"}],`<br>`{"token":"token2","account_list":[{"account":"926@163.com",{"account":"1527000001"}]}]` |
| account_type Integer | No  | Account type, which can be selected during account binding. The default value is `0`. For valid values, see [Account Type Value Table](https://www.tencentcloud.com/document/product/1024/40598). |

>? 
>- As the `token append account` API was seldom used and confusing to developers, it had been disused since October 26, 2020. If you have used it before, it will be replaced by the `Token clearAndAppendAccount` API.
>- Only one account can be bound to an account type. If multiple accounts are bound to an account type, an account bound later will override the one bound earlier.


#### Response parameters

| Parameter | Type | Description |
| -------------- | ------- | ---------------------------------------- |
| ret_code | Integer | Error code. For more information, see [Server-Side Error Codes](https://www.tencentcloud.com/document/product/1024/33763).|
| err_msg | String | Error message. |
| result | Array | Operation status code corresponding to each token or account ["0","1008006"]. |


## Samples
#### Sample request
- (Disused) Bind a token to one more account
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
- Bind the token to another account in an overriding manner
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
- Unbind the token from all accounts
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



#### Response example

Unbind a token from an account
``` json
{
    "ret_code": 0,
    "err_msg": "NO_ERROR",
    "result": [
        "0"
    ]
}
```

