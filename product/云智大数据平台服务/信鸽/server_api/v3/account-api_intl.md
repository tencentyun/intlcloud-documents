## Account API v3

### Glossary
| Name | Field | Description |
| -------------- | ------- | ---------------------------------------- |
| Account | account | It refers to the user's app login account. One login account can be bound to multiple device tokens. The character length of an account must be greater than 1 byte. |
| Device | token | It refers to the user's device ID. One device can be bound to multiple accounts. The character length of a token must be between 1 and 64 bytes. |
| Account type | account_type | It is used to identify the account type. *For specific type value, see the table. |

*  <a href="https://intl.cloud.tencent.com/document/product/1024/30741">Account Type Value Table</a> 

### Account API Overview

- Account API is a general term for all account APIs
- It is mainly divided into account operation APIs and account query APIs as follows:
  - Bind token to an account
  - Bind token to an account in an overriding manner
  - Unbind token from an account
  - Unbind token from all accounts
  - Unbind account from all tokens 
  - Batch query the token relationships bound to accounts
  - Batch query the account relationships bound to tokens
  - Batch query the tokens bound to accounts
  - Batch query the accounts bound to tokens
  

  

### Account API Request Description


#### Account Binding and Unbinding (Batch Operation)
##### API Description 
 ```text
 POST https://openapi.xg.qq.com/v3/device/account/batchoperate
 ```

Async API. The API is only responsible for task delivery. Currently, it does not support real-time operations.


##### Parameter Description
| Parameter name | Type | Required | Description |
| -------------- | ------- | ---- | ---------------------------------------- |
| operator_type  | int     | Yes    |   Operation type <br>1: Bind token to an account<br>2: Bind token to an account in an overriding manner <br>3: Unbind token from multiple accounts <br>4: Unbind token from all accounts <br>5: Unbind account from all tokens |
| platform       | string  | Yes | Client platform type <br>1) android: Android <br>2) ios: Apple |
| account_list     | jsonArrary   | No | The collection of account IDs, which is valid when operator_type=5, and each element is required, including account and account_type fields. <br>Example: <br>[{"account":"926@126.com","account_type":2},{"account":"1527000000","account_type":1}]|
| token_list       | jsonArrary   | No | The collection of device IDs, which is valid when operator_type=4 and required |
| token_accounts | jsonArrary   | No | It is valid when operator_type=1, 2, or 3 and must be called each time. Up to 20 tokens are allowed, and each token_account consists of 1 token and 1 account_list. Below is a specific example: <br>[{"token":"token1","account_list":[{"account":"926@126.com","account_type":2},{"account":"1527000000","account_type":1}]},<br>{"token":"token2","account_list":[{"account":"926@163.com","account_type":2},{"account":"1527000001","account_type":1}]}] |
| op_type        | string  | No    | API operator type: qq, rtx, email, other |
| op_id          | string  |  No | API operator type: API operator id (qq\rtx\email) |

##### Response Parameter Description
| Parameter name | Type | Description |
| -------------- | ------- | ---------------------------------------- |
| ret_code       | int  | Return code |
| err_msg | String | Error message |
| result       | JsonArrary    | Result of operation for each element, for example: ["ok","token_not_exists"] |




Account API Samples 

- Bind token to an account

  ```json
{
"operator_type":1,
"platform":"android",
"token_accounts":
[{"token":"token1","account_list":[{"account":"926@126.com","account_type":2},{"account":"1527000000","account_type":1}]},
{"token":"token2","account_list":[{"account":"926@163.com","account_type":2},
{"account":"1527000001","account_type":1}]}]
}
  ```
- Bind token to an account in an overriding manner 

```json
{
"operator_type":2,
"platform":"android",
"token_accounts":
[{"token":"token1","account_list":[{"account":"926@126.com","account_type":2},{"account":"1527000000","account_type":1}]},
{"token":"token2","account_list":[{"account":"926@163.com","account_type":2},{"account":"1527000001","account_type":1}]}]
}
```
- Unbind token from an account

```json
{
"operator_type":3,
"platform":"android",
"token_accounts":
[{"token":"token1","account_list":[{"account":"926@126.com","account_type":2},{"account":"1527000000","account_type":1}]},
{"token":"token2","account_list":[{"account":"926@163.com","account_type":2},{"account":"1527000001","account_type":1}]}]
}
```
- Unbind token from all accounts

```json

{
"operator_type":4,"platform":"android","token_list":["token1","token2","token3"]
}
```
- Unbinding account from all tokens 

```json
{
"operator_type":5,"platform":"android","account_list":[{"account":"926@126.com","account_type":2},
{"account":"1527000000","account_type":1}]
}
```
#### Account-device Binding Query (Batch Operation)
##### API Description 
 ```text
 POST https://openapi.xg.qq.com/v3/device/account/query
 ```
The API feeds back in real time.

##### Parameter Description
| Parameter name | Type | Required | Description |
| -------------- | ------- | ---- | ---------------------------------------- |
| operator_type  | int     | Yes | Operation type <br>1: Batch query the corresponding token according to account <br>2: Query account according to token |
| platform       | string  | Yes | Client platform type <br>1) android: Android <br>2) ios: Apple |
| account_list     | jsonArrary   | No | The account list to be queried, which is valid when operator_type = 1 and required. Each element consists of a pair of account and account_type. Below is a specific example: <br>[{"account":"account1","account_type":1 },<br>{"account":"account2","account_type":2}]|
| token_list       | jsonArrary   | No | The token list to be queried, which is valid when operator_type = 2 and required.  |
| op_type        | string  | No    | API operator type: qq, rtx, email, other |
| op_id          | string  |  No | API operator type: API operator id (qq\rtx\email) |
##### Response Parameter Description
| Parameter name | Type | Description |
| -------------- | ------- | ---------------------------------------- |
| ret_code       | int  | Return code |
| err_msg | String | Error message |
| account_tokens       | JsonArrary    | Array of mappings from account to token, for example: :<br>[{"account":"account1","account_type":1,"token_list":["token1","token2"]}{"account":"account2","account_type":2,"token_list":["token2","token3"]}]             |
| token_accounts      | JsonArrary     | Array of mappings from token to account, for example: <br>:[{"token":"token1","account_list":[{"account":"926@126.com","account_type":2},{"account":"1527000000","account_type":1}]},<br>{"token":"token2","account_list":[{"account":"926@163.com","account_type":2},{"account":"1527000001","account_type":1}]}]  
#### Sample 

- Batch query the token relationships bound to accounts

  ```json
{
"operator_type":1,
"platform":"android",
"account_list":
[{"account":"account1","account_type":1},{"account":"account2","account_type":2}]
}
  ```
- Batch query the accounts bound to tokens 
```json
{
"operator_type":2,
"platform":"android",
"token_list":["token1","token2"]
} 
```

##### Return Field Sample
- Batch query the tokens bound to accounts

```json
{
"ret_code":0,
"err_msg":"ok",
"account_tokens":
[{"account":"account1","account_type":1,"token_list":["token1","token2"]},
{"account":"account2","account_type":2,"token_list":["token2","token3"]}]
}
```
- Batch query the accounts bound to tokens

```json
{
"ret_code":0,
"err_msg":"ok",
"token_accounts":
[{"token":"token1","account_list":[{"account":"926@126.com","account_type":2},{"account":"1527000000","account_type":1}]},
{"token":"token2","account_list":[{"account":"926@163.com","account_type":2},{"account":"1527000001","account_type":1}]}]
}
```


