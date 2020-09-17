
## API Description
**Request method**: POST.

The API request address corresponds to the service access point one by one; therefore, please select the request address corresponding to your application service access point.

Service access point in Guangzhou:
```shell
https://api.tpns.tencent.com/v3/statistics/get_push_record
```
Service access point in Hong Kong (China):
```shell
https://api.tpns.hk.tencent.com/v3/statistics/get_push_record
```
Service access point in Singapore:
```shell
https://api.tpns.sgp.tencent.com/v3/statistics/get_push_record
```
Service access point in Shanghai:
```shell
https://api.tpns.sh.tencent.com/v3/device/account/query
```

**Feature**: this API is used to query the binding relationships between accounts and tokens.



## Parameter Description
#### Request parameters
| Parameter Name | Type | Required | Description |
| -------------- | ------- | ---- | ---------------------------------------- |
| operator_type | Integer | Yes | Operation type: <li>Batch queries the corresponding token according to account<li>Queries the account according to token |
| account_list | Array | No | The account list to be queried, which is valid and required if `operator_type` is 1, with each element containing one set of accounts. Below is an example: `[{"account":"account1"},{"account":"account2"}]` |
| token_list | Array | No | The token list to be queried, which is valid and required if `operator_type` is 2.|

#### Response parameters

| Parameter Name | Type | Description |
| -------------- | ------- | ---------------------------------------- |
| retCode | Integer | Return code |
| errMsg | String | Error message|
| account_tokens | Array |Array of mappings from account to token, for example:<br>`[{"account":"account1","token_list":["token1","token2"]}{"account":"account2","token_list":["token2","token3"]}`] |
| token_accounts | Array |Array of mappings from token to account, for example:<br>`[{"token":"token1","account_list":[{"account":"926@126.com"},{"account":"1527000000",}]},`<br/>`{"token":"token2","account_list":[{"account":"926@163.com"},{"account":"1527000001"}]}]` |


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

#### Sample return
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


