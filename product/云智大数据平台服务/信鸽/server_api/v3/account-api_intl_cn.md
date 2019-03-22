## Account API v3

###名词解释
| 名称         | 英文字段     | 说明                                     |
| -------------- | ------- | ---------------------------------------- |
| 账户       | account  |指用户的app登录账号，一个登录账号可以绑定到多个token设备 , account 字符长度大于1 个字节              |
| 设备       | token    | 指用户的设备ID，一个设备可以被多个账号绑定 。Token字符长度不超过64 个字节，不小于1 个字节|
| 账户类型       | account_type    |账号类型用来标识account类型，*类型具体取值表|

*  <a href="https://xg.qq.com/docs/server_api/v3/push_api_v3.html#%E8%B4%A6%E5%8F%B7%E7%B1%BB%E5%9E%8B">账号类型取值表</a> 

### Account API 概述

- Account API 是所有Account接口的统称
- 主要分为账号操作接口以及账号查询接口，具体的接口如下：
  - Token 追加设置 Account
  - Token 覆盖绑定 Account
  - Token 删除绑定 Account
  - Token 删除所有绑定 Account
  - Account 删除所有绑定 Token 
  - 批量查询Account绑定的token关系
  - 批量查询Token 绑定的Account关系
  - 批量查询account 绑定的Token
  - 批量查询Token绑定的Account
  

  ​

### Account API 请求说明


####  账号绑定与解绑（批量操作）
#####接口说明 
 ```text
 POST https://openapi.xg.qq.com/v3/device/account/batchoperate
 ```

异步接口。接口只负责任务下发，当前不支持实时操作。


#####参数说明
| 参数名            | 类型      | 是否必需 | 参数说明                                     |
| -------------- | ------- | ---- | ---------------------------------------- |
| operator_type  | int     | 是    |   操作类型<br>1：token 追加设置account<br>2：token覆盖设置account<br> 3  : token删除绑定的多个account<br>4：token 删除绑定的所有account<br>5：account 删除绑定的所有token |
| platform       | string  | 是    | 客户端平台类型<br>1）android：安卓 <br>2）ios：苹果               |
| account_list     | jsonArrary   | 否    | 账号标识集合，当operator_type=5 时有效，且必填每个元素包含account，以及account_type 字段。 <br> 示例:<br>[{"account":"926@126.com","account_type":2},{"account":"1527000000","account_type":1}]|
| token_list       | jsonArrary   | 否    | 设备标识集合, operator_type=4 时有效，且必填|
| token_accounts | jsonArrary   | 否    | 当operator_type=1、2 、3 时有效且必须每次调用最多允许设置20个token每个token_account 由1个token 和1个account_list 组成。 具体示例如下：<br>[{"token":"token1","account_list":[{"account":"926@126.com","account_type":2},{"account":"1527000000","account_type":1}]},<br>{"token":"token2","account_list":[{"account":"926@163.com","account_type":2},{"account":"1527000001","account_type":1}]}] |
| op_type        | string  | 否    | 接口操作人员类型：qq、rtx、email、other              |
| op_id          | string  | 否    | 接口操作人员类型：接口操作人员id（ qq\rtx\email）         |

#####响应参数说明
| 参数名            | 类型       | 参数说明                                     |
| -------------- | ------- | ---------------------------------------- |
| ret_code       | int  | 返回码               |
| err_msg       | String    | 错误信息|
| result       | JsonArrary    |对于每个元素的操作结果 示例 ：["ok","token_not_exists"]
        



Account API 实际例子 

- Token 追加设置 Account

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
- Token 覆盖绑定 Account 

```json
{
"operator_type":2,
"platform":"android",
"token_accounts":
[{"token":"token1","account_list":[{"account":"926@126.com","account_type":2},{"account":"1527000000","account_type":1}]},
{"token":"token2","account_list":[{"account":"926@163.com","account_type":2},{"account":"1527000001","account_type":1}]}]
}
```
- Token 删除绑定 Account

```json
{
"operator_type":3,
"platform":"android",
"token_accounts":
[{"token":"token1","account_list":[{"account":"926@126.com","account_type":2},{"account":"1527000000","account_type":1}]},
{"token":"token2","account_list":[{"account":"926@163.com","account_type":2},{"account":"1527000001","account_type":1}]}]
}
```
- Token 删除所有绑定 Account

```json

{
"operator_type":4,"platform":"android","token_list":["token1","token2","token3"]
}
```
- Account 删除所有绑定Token 

```json
{
"operator_type":5,"platform":"android","account_list":[{"account":"926@126.com","account_type":2},
{"account":"1527000000","account_type":1}]
}
```
####  账号-设备绑定查询（批量操作）
#####接口说明 
 ```text
 POST https://openapi.xg.qq.com/v3/device/account/query
 ```
接口实时反馈

#####参数说明
| 参数名            | 类型      | 是否必需 | 参数说明                                     |
| -------------- | ------- | ---- | ---------------------------------------- |
| operator_type  | int     | 是    |   操作类型<br>1：根据account 批量查询对应token<br>2：根据 token查询account |
| platform       | string  | 是    | 客户端平台类型<br>1）android：安卓 <br>2）ios：苹果               |
| account_list     | jsonArrary   | 否    | 当operator_type = 1 时有效且必填，待查询account列表每个元素含一组account 、account_type。 具体示例如下：<br>[{"account":"account1","account_type":1 },<br>{"account":"account2","account_type":2}]|
| token_list       | jsonArrary   | 否    | 当operator_type = 2 时有效且必填待查询token 的列表|
| op_type        | string  | 否    | 接口操作人员类型：qq、rtx、email、other              |
| op_id          | string  | 否    | 接口操作人员类型：接口操作人员id（ qq\rtx\email）         |
#####响应参数说明
| 参数名            | 类型       | 参数说明                                     |
| -------------- | ------- | ---------------------------------------- |
| ret_code       | int  | 返回码               |
| err_msg       | String    | 错误信息|
| account_tokens       | JsonArrary    |account 到token 的映射关系数组 示例:<br>[{"account":"account1","account_type":1,"token_list":["token1","token2"]}{"account":"account2","account_type":2,"token_list":["token2","token3"]}]             |
| token_accounts      | JsonArrary     | token 到account 的映射关系数组 示例:<br>:[{"token":"token1","account_list":[{"account":"926@126.com","account_type":2},{"account":"1527000000","account_type":1}]},<br>{"token":"token2","account_list":[{"account":"926@163.com","account_type":2},{"account":"1527000001","account_type":1}]}]  
####示例 

- 批量查询Account绑定的Token关系

  ```json
{
"operator_type":1,
"platform":"android",
"account_list":
[{"account":"account1","account_type":1},{"account":"account2","account_type":2}]
}
  ```
- 批量查询Token 绑定的ccount关系 
```json
{
"operator_type":2,
"platform":"android",
"token_list":["token1","token2"]
} 
```

#####返回字段示例
- 批量查询Account 绑定的Token

```json
{
"ret_code":0,
"err_msg":"ok",
"account_tokens":
[{"account":"account1","account_type":1,"token_list":["token1","token2"]},
{"account":"account2","account_type":2,"token_list":["token2","token3"]}]
}
```
- 批量查询Token绑定的Account

```json
{
"ret_code":0,
"err_msg":"ok",
"token_accounts":
[{"token":"token1","account_list":[{"account":"926@126.com","account_type":2},{"account":"1527000000","account_type":1}]},
{"token":"token2","account_list":[{"account":"926@163.com","account_type":2},{"account":"1527000001","account_type":1}]}]
}
```


